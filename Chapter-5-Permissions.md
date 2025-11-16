# Permissions
When you run:

```bash
ls -la
```

you see rows like this:

```
-rw-r--r--  1  alice  staff   4096  Nov 14 10:20  file.txt
```

The **first user** and **second user** after the permissions mean:

---

# ✅ **1. First name → Owner (User)**

This is the **user** who owns the file.

Example:

```
alice
```

This means user **alice** created or owns the file.

---

# ✅ **2. Second name → Group**

This is the **group** that the file belongs to.

Example:

```
staff
```

This means the file belongs to the **staff** group.

---

# 📌 **So the order is:**

```
permissions | links | owner (user) | group | size | date | filename
```

Example:

```
drwxr-xr-x  2 root   root   4096 Nov 14 10:20  folder
```

* `root` → the **user** who owns the file
* `root` → the **group** that owns the file

Another example:

```
-rw-r--r--  1 arun   sudo   1024 Nov 14 12:00 test.txt
```

* `arun` → file owner (user)
* `sudo` → group that owns the file

---

# Why does this matter?

Because Linux permissions apply separately to:

* **u** (user/owner)
* **g** (group)
* **o** (others)

So the group matters for users who are part of that group.

---

If you want, I can also explain:

* How file permissions work (`rwxr-xr--`)
* How chmod, chown, chgrp work
* How user–group permission priority works

To switch to a different user in Linux, you use the **`su`** or **`sudo`** commands.

Here are the ways:

---

# ✅ **1. Switch to another user (requires their password)**

```bash
su username
```

Example:

```bash
su arun
```

You will be asked for **arun’s password**.

---

# ✅ **2. Switch to another user with a full login shell**

This loads the user's `.bashrc`, environment, PATH, home directory, etc.:

```bash
su - username
```

This is the preferred way.

---

# 🔐 **3. Switch to another user using sudo (requires *your* sudo password)**

If your user has sudo privileges:

```bash
sudo su - username
```

This does **not** ask for the other user’s password — only your own sudo password.

Useful when switching to **root**:

```bash
sudo su -
```

---

# 🔥 **4. Execute a single command as another user**

```bash
sudo -u username command
```

Example:

```bash
sudo -u postgres psql
```

---

# 🧾 **5. Check which user you currently are**

```bash
whoami
```

---

If you want, I can explain:

* The difference between `su` and `sudo`
* Why `su` sometimes fails even with the right password
* How to prevent users from switching to root

Here’s exactly what is happening in your screenshot:

---

# ✅ **1. `su - bob` tries to switch to user *bob* with a full login shell**

When you use:

```bash
su - bob
```

the `-` (login shell) tells Linux:

* load bob’s environment vars
* switch to bob’s home directory → `/home/bob`

---

# ❌ **2. Error: “cannot change directory to /home/bob: No such file or directory”**

```
su: warning: cannot change directory to /home/bob: No such file or directory
```

This means:

👉 **The user `bob` exists**
👉 **But `/home/bob` DOES NOT exist**

This happens if the user was created using:

```bash
sudo useradd bob
```

(without `-m`, so no home directory was created)

---

# ❌ **3. Then you typed `ls` and got “Permission denied”**

```
ls: cannot open directory '.': Permission denied
```

This is because:

* Since `/home/bob` did not exist, `su` left you in your previous directory (probably your original user's home).
* But now you are **bob**, and bob **does not have permission** to read that directory.

So `ls` fails because bob cannot access the current working directory.

---

# 📌 **What’s happening in simple words**

You switched to a user **who has no home directory** and ended up in a directory bob cannot access.

---

# ✅ **How to fix it**

### **Option 1 — Create home directory for bob**

```bash
sudo mkdir /home/bob
sudo chown bob:bob /home/bob
sudo chmod 755 /home/bob
```

Or delete and re-create the user properly:

### **Option 2 — Recreate bob with a home directory**

```bash
sudo userdel -r bob
sudo useradd -m bob
sudo passwd bob
```

---

# 🎯 After fixing, test again

```bash
su - bob
```

You should now be inside `/home/bob` and `ls` will work.

---

If you want, I can also help you:

* create a user with sudo privileges
* understand file permissions and home directory ownership
* diagnose other user-switching issues


# `ls -l` again
- `drwxr-xr-x 5 root root 4096 Dec 5 10:47 charsets`
- First character: File Type
- Rest of the section: Permissions of file for owner, groups, and users, respectively.
- Number of links.
- Owner of the file
- The size of the file in bytes
- When the file was created or last modified
- The name of the file
- The first character tells you the file type, where d stands for a directory
and a dash (–) indicates a file. These are the two most common file types.
The next section defines the permissions on the file. There are three sets
of three characters, made of some combination of read (r), write (w), and
execute (x), in that order. The first set represents the permissions of the
owner; the second, those of the group; and the last, those of all other users.

- Regardless of which set of three letters you’re looking at, for files, if
you see an r first, that user or group of users has permission to open and
read that file or directory. A w as the middle letter means they can write to
(modify) the file, and an x at the end means they can execute (or run) the
file or access the directory. If any r, w, or x is replaced with a dash (-), then
the respective permission hasn’t been given. Note that users can have permission
to execute only either binaries or scripts.

# Change permissions with decimal notation
| **Binary** | **Octal** | **rwx**|
| --- | --- | --- |
| 000 | 0 | --- |
| 001 | 1 | --x |
| 010 | 2 | -w- |
| 011 | 3 | -wx |
| 100 | 4 | r-- |
| 101 | 5 | r-w |
| 110 | 6 | rw- |
| 111 | 7 | rwx |

- Only read (r--) corresponds to 4, write (-w-) and execute (--x) corresponds to 2 and 1 respectively. When all permissions are on, the octal equivalent is 7 (4 + 2 + 1).
- So, if we wanted to represent all permissions for the owner, group, and
all users, we could write it as follows: 7 7 7
- `chmod 774 hashcat.hcstat` gives the owner all permissions, the group all permissions, and others (users) only the read permission.

# Changing permissions with UGO (user, group, others)
- Enter the chmod command and then the users
you want to change permissions for, providing u for user, g for group, or o for
others, followed by one of three operators:
- `-` Removes a permission
- `+` Adds a permission
- `=` Sets a permission
- `chmod u-w hashcat.hcstat2` says to remove (-) the write (w) permission for hashcat.hcstat for the user (u).
- `chmod u+x, o+x hashcat.hcstat2` says to add the execute permission for the user aswell as the others for the file hashcat.hcstat2.

# Giving Root Execute Permission on a new tool
