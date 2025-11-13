# All commands used so far

## Chapter 1 and 2

- `aircrack-ng --help`
- `nmap -h`
- `locate aircrack-ng`
- `whereis aircrack-ng` to look for binary files
- `which aircrack-ng`
- `find / -type f -name apache2`
- `find / -type f -name apache2.\*`
- `cat > hacking` to enter interactive mode. `Ctrl+D` to exit and save.
- `cat >> hacking` to append.
- `ps aux | grep apache2`. `ps` stands for processes. `|` is piping, it is used to pass output of one command as input to another.
- `head`, `tail`, `more` and `less`.
- `nl` is used for numbering lines.
- `cat /usr/share/metasploit-framework/data/wordlists`. This is a directory of multiple wordlists that can be used to brute force passwords in various password-protected devices using Metasploit, the most popular pentesting and hacking framework.
- `cat password.lst`
- `cat password.lst | grep 123`

- `sed 's/old/new/' file.txt` to replace first occurance per line.
- `sed 's/old/new/g' file.txt` to replace all occurances in line.

- `sed -i 's/old/new/g' file.txt` to edit the file in-place.

- `sed '5d' file.txt` delete line no. 5
- `sed '10,20d' file.txt` to delete lines 10 to 20

- `sed -n '3p' file.txt` to print only line 3

- `sed -n '5,10p' file.txt` prints line 5 to 10

- `sed '1i This goes at the top' file.txt` to insert before line 1

- `sed '1a This goes after line 1' file.txt` to append after line 1

- Find and replace in pipeline: `echo "Hello World" | sed 's/World/Kali/'
`
