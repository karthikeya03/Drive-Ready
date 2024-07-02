# SESSION 5 : USERS

## 1. Directories:
- `/` : Top-most directory

- `/home` : Users' home directories
  - Example: `cd /home`

- `/etc` : Configuration files
  - Example: `cd /etc`
  - Example: `ls -l | more` (View files)

## 2. Files in `/etc`:
- `/etc/passwd` : User information
  - Example: `vim /etc/passwd`

- `/etc/shadow` : Password requirements
  - Example: `vim /etc/shadow`

- `/etc/group` : Group information
  - Example: `vim /etc/group`

## 3. Commands:
- `date` : Display current date and time (GMT +5:30)
  - Example: `date`

- `cal` : Display calendar
  - Example: `cal`
  - Example: `cal January`

- `timedatectl` : Display date and time details
  - Example: `timedatectl`

## 4. Viewing File Content:
- `head (filename)` : Display first ten lines of a file
  - Example: `head filename`

- `tail (filename)` : Display last ten lines of a file
  - Example: `tail filename`

- `head -n 5 passwd` : Display first 5 lines of a file
  - Example: `head -n 5 passwd`

- `head -n 2 passwd` : Display first 2 lines of a file
  - Example: `head -n 2 passwd`

## 5. User Management:
- Switch to root for user management tasks (create users, set passwords):
  - `sudo su`

- `useradd` : Add a user
  - Example: `useradd username`

- `whoami` : Display current username
  - Example: `whoami`

- `su username` : Switch to another user
  - Example: `su username`

- `sudo su` then `useradd username` to create a user

- `userdel username` : Delete a user
  - Example: `userdel username`

# USER & SERVER:

## 1. Hardware:
- Memory
- Storage
- CPU

## 2. Operating System:
- Server Version

## 3. Applications to the Server:
- Web Application: APACHE, FLUTTER, REACT, NODE

## 4. User:
- Responsible for designing the website

# Types of Servers:

## 1. On-Premise Server:
- Physical Server
- Hardware:
- OS Server Version:
- Cloud Server Application:
- Cloud Server Availability:

## 2. Cloud Server:
- Virtual Server

## 3. Email Server:
- Email: 22p31a0506@acet.ac.in
- Managed by Microsoft
- Microsoft Exchange: OS server application
- Hardware:
- Email Server Version:
- Email Server Application:
- Emails Availability:

## 4. IP Server:
- Hardware:
- OS Server Version:
- IP Server Application:
- IP Availability:

## 5. LMS Server:
- Learning Management System

# PERMISSIONS:

## 1. Permission Types:
- rwx: Read, Write, Execute

## 2. Permission Structure:
- File and group created under the same name

## 3. Permissions Breakdown:
- `file | user | group | other`: Not a user and not part of the group

## 4. Examples:
- `- rwx rwx rwx`:  
  - User: read, write, execute 
  - Group: read, write, execute 
  - Others: read, write, execute
- `- rw- rw- r--`: 
  - User: read, write 
  - Group: read, write 
  - Others: read only
- `- r- rw- ---`: 
  - User: read 
  - Group: read, write 
  - Others: no permissions

# CHMOD Command:

## 1. Usage:
- Used to change the permissions of any file

## 2. Syntax:
- `chmod u:` (user)
- `g:` (group)
- `o:` (others)

## 3. Examples:
- `chmod u-w test` (Removes write permission for the user on the file 'test')
- `chmod u+w test` (Adds write permission for the user on the file 'test')
