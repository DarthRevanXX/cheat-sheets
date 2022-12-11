- `echo` - print
- `ls` - list all folder
- `cd` - move into directory
- `pwd` - print directory path you are in
- `mkdir` - create a folder
- `mkdfir -p` - create a directory tree
- `rm -r` - delete directory with content inside
- `cp -r` - cory directory with everything inside( cp -r my_dir /tpm/my_dir1)

## Commands - Files

- `touch` - create a file (touch test.txt)
- `cat` - read the file 
- `cat > new_file.txt` - add contents to file
- `cp new_file.txt copy_file.txt` - copy file
- `mv new_file.txt sample_file.txt` - move(rename file)
- `rm new_file.txt` - remove deleta file

User Accounts

- `whoami` - tell which user are you now
- `id` - tell users id and group id and groupd to which you belong
- `su` - switch to another user
Example: `ssh aparna@192.168.1.2`
- sudo ls /root - granted sudo permissions

Download Files

- curl http://www.some-site.com/some-file.txt -o
- wget http://www.some-site.com/some-file.txt -o some-file.txt
- `ls /etc/*release*` or `cat /etc/*release*` - check os version