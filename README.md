# linux_notes
notes for linux
Navigation to file: 

cd - Change directory.

pwd - present working directory.

ls - list the content of the directory.

ls -l : it lists all item in the directory alphabetically 

ls -ltr: it lists all item in the dictionary according to date and time.
stat filename -> it gives details of file.


Absolute path- cd /var/log/ file name/ 

relative path - cd /var ---> cd log 



creating files : 

touch : touch file\_1 --> it creates file\_1.txt file also can create multiple files 

touch file1 file2 file3 ( it creates 3 files at a time)

cp - (cp <existing file name> <target (newly file/ existing file)>) creating file method

vi - it enable the editor on and creates the file. vi filename (hit enter)

editer will be enabled,for exiting write :wq! and hit enter



creating dictionaries: 

mkdir : mkdir <directory name> 





**copying directories**: 



cp -R <source folder> <destination folder>



**find files and directories:** 

find [path/to/directory] [search parameter like -name, -size]

eg: 
find /bin/ -name filename
find -name filename  -> no path means find in current directory.
find -iname filename  -> it ignores case sensitive.
find -mmin [time]  -> mmin - modified minute
find -mmin 5 
find -mtime 2 # 24 hour period
find -size 1GB
find -name "*.txt" -size 1MB --> it satisfies and condition
find -perm 664 -> find files with permission 664.
find -perm -664 -> find files with atleast permission 664 (minimum 664).

**to find** 


Wildcards: 

these help to easy the tasks like create files , remove files, and many more.
* is used for multiple characters 
? is used for single character ( ls -l ?ABC-* )
{} is used for range of character {1..9} , {A..J}


types of Linux file:

add notes here later.

soft link or hard link ( add notes what , why, how) 
first go to tmp file in home and type below command: 
ln -S  --> to create soft link
ln file path  --> it creates hard link

to check the status of it's creation command (ls -l)
so you can see the linked file will be visible in blue colour.

to check the i node type command ls -ltri  : it represent the inode of the file/ directory.


chapter 4 (Linux fundamentals)

File permissions for file and directories: 

chmod ( this command is used to change the file permission of file or directory)

permission is given for u- user , g - group, o- other
type of permission: rwx (read , write and executable)

chmod a +/-rwx  {filename}
chmod u+r {filename} 
chmod o - x {filename}

above command helps to add or remove the permissions to user, group or others/ public.



numerical method of file permission:

Numeric	Symbolic	Permission
0	---	none
1	--x	execute only
2	-w-	write only
3	-wx	write and execute
4	r--	read only
5	r-x	read and execute
6	rw-	read and write
7	rwx	read, write, and execute

chmod u+s filename execute file as fileowner
chmod g+s filename execute file as group owner
chmod +t filename -> this file can delete by only file owner

chmod 444 {filename}


file ownership :

there are two types of owner of file or dictionary.
user and group 

command to change the file ownership:
chown changes the ownership of file and dictionary.
chgrp changes the group ownership of the file or dictionary.

to change the ownership you need to login as root so that you can change the user to root.
to do that 
su - or sudo su -
enter password -> go to that file path -> then type command 

chown root {filename}
chgrp root {filename}

type -> exit (to logout)
# how to create user and add user to group.
sudo useradd -m -G mygroup newuser
-m creates a home directory for the user.
-G assigns the user to the specified group.

# how to create group

 groupadd devteam

# add user to group

sudo usermod -aG devteam john




Access control list (ACL): 
list of commands to set up ACL

to add permission to user:
setfacl -m u:user: rwx /path/to/file

to add permission to group:
setfacl -m g:groupname:rwx rwx /path/to/file

to allow file or dictionaries to inherit ACL entries from the dictionary it is within 
setfacl -dm "entry" /path/to/file

to remove a specific entry:
setfacl -x u:user /path/to/file

to remove all entries:
setfacl -b u:user /path/to/file

.

# Help command

whatis {write a command for which you need info}
command --help
man command

# adding text to file or redirects:

3 ways to add text to file:
vi
Redirect command output > or >>
echo > or >>


#eg
echo "my name is shrikant" > shrikant.txt
ls -l ( to check the data)
echo "i work in bosch" >> shrikant.txt (double arrows will be used to add the second line to the same file.)

standard output to a file 

echo "file content text" | tee {filename}



# input and output redirectories 

important for daily task.

# standard output to a file:

ls -l | tee {filename}  (it gives the command output inside the file)

echo "some text" | tee {filename}   (this command used to add text into file)
echo " next text" | tee -a {filename}   (this command is used to append the next line to that file)

wc -c {file name}   ( used to count bytes of file)

ls -l | tee {file name}
ls -l | tee {file name} {filename 2} {file name 3} ( this can be used to copy command ls -l output to multiple files)

# pipes:

a pipe is used by the shell to connect the output of and the input of another command.

command 1 [argument] | command 2 [argument]
ls -ltr | more ( to see all file page by page )  ll is like ls -ltr

ls -ltr | tail -1 (gives last line for it)

# executing multiple commands using ;

; can be used to execute the multiple commands in a single line.

mkdir file1; cd file1; touch textfile.txt 

(it creates a directory named file1 then it enters into that directory and then creates a file into it)
if any of those command fail it execute the rest command. 


# text processors

cut
awk
grep and egrep
sort
uniq
wc (word count) 

cut : 
cut command used to cut a part of line and print the result to standard output. it can be used to cut the parts of line by delimiter; byte position and character. 

awk:
awk is utility / language designed for data extraction. Most of the time it is used to extract the fields from a file or from a output. 

consider we have a file and it contains name and sirmname in it and if we want name alone then following command we need to use
awk '{print $1}' filename 
awk '{print $2}' filename  - gives second column (sirname)


# grep:

grep --version or grep --help
grep keyword filename
 eg:
grep -c rakhe filename  -> it gives the no of hits for the keyword search
grep -i rakhe filename  -> it gives the results of keyword match without case sensitive.
grep -n rekhe filename  -> it gives at which line no that match is available.
grep -v rakhe filename  -> it gives other results than matching cases.
grep keyword files | awk '{print $1} filename  -> it gives keywords and prints the perticular column.

egrep -i "keyword1|Keyword2" filename  -> it gives results for two keywords.

# sort / unique command: 

sort --version or sort --help

sort filename  -> it sorts the file content in the file.
sort -r filename  -> it sorts the file content in reverse order.
sort -k2 filename  -> it sorts the file content in second column.
ls -l | sort k9 -> sorts all directories and files and sort last column.

uniq:

uniq filename - 
sort filename | uniq -> first it sorts and removes duplicates. ( always first sort and apply uniq)
sort filename | uniq -c -> first it sorts and removes duplicates and gives the count. 
sort filename | uniq -d -> sow only repeated line. 

# compare files (diff - line by line, cmp - byte by byte)

diff filename1 filename2 ( enter 3 characters in filename1, enter some characters in filename2 ) 
cmp filename1 filename 2 (gives the difference in bytes)(ompare command)


# WC (word count)
The wc command in Linux stands for word count and is used to count lines, words, characters, and bytes in a file. When used with the -l option, the command specifically counts the number of lines in the specified file.

Syntax

wc -l some_file
Copy
Example Usage

If you have a file named example.txt containing:

Line 1
Line 2
Line 3
Copy
Running the command:

wc -l example.txt
Copy
Will output:

3 example.txt

# compress and uncompressed (tar, gzip, gunzip):

tar - command compresses but does not reduce the size of the file

tar cvf vboxuser.tar folder_name --> it zip you the whole big file but will not compress / reduce file size
gzip - > it reduces size / compresses the file.tar file  -> gzip vboxuser.tar
gzip -d vboxuser.tar.gz  -> this is command to uncompress the file 
gzip -d or gunzip -> both commands are same.
rm -rf /any directory name ( this is used to remove the directory)

# truncatefile size (truncate): 
the linux truncate command is often used to shrink or extend the size of a file to the specified size
truncate command actually not used to compress but rather if we apply this command on a file having size 50 kb and we keep size 40 kb it will cut down some lines available in the file and when we cat the same file we will get to see some line we lost due to truncating it.
truncate -s 10 filename 

# combining and splitting files :
multiple files can be combined into one 
one file can be split into multiple files
 cat file1 file2 file3 > file4
 split file4

split file.txt into 300 lines per file and output to file1 file2 and file3

add contry names in a file (10 contry names)
split -l 2 contries.txt sep  -> hit enter it will create 5 files each containing 2 names. 

cat file1 file2 file3 > combined_file_name -> it combines files into one 

# linux vs windows commands :

# module 5 : System Administration -

# linux file editor (vi, vim): 

A text editor is a program which enables you to create and manipulate data in a linux file.
vi
vim
Most common keys in vi:
i - to insert  Esc - escape from any mode
r - replace -go to the letter which u want to replace type r and type letter you want to type and similar way you can go for next in command mode.
d - delete
:q! - quit without saving 
:wq! quit and save.
in command mode type u it will bring you back deleted line.
x -remove space / work as backspace 
o - type it to add new line and also get into insert mode.
if you have file and too much text in it and you wanted to find one line like lesson then in command mode type " /word that you want to search"

# Difference between vi and vim :
vim has added features more than vi 
Vim has autocompletion of command, spell check, comparison, merging, unicode, vimdiff
regular expressions, scripting language, plugins ,
GUI, folding syntax, highlighting 
 for study -www.openvim.com  ,  www.vimgenius.com , vim-adventures.com (games) 


# sed command: 

it is used for:
replace a string in a file with new string
find and delete a line
remove empty line
remove first line or n lines in a file
to replace tabs with spaces
show defined lines from a file
substitue within vi editor
and much more..
 

 sed 's/kenny/lenny/g' filename    s: substitute, g global( if you want change everywhere in file) here kenny will be replaced with lenny
 above command does not make chages in previous file so you need to 
 sed -i 's/kenny/lenny/g' filename  -> now it will make the changes permanantly 

 sed -i 's/kenny/ /g' filename -> it removes that word kenny and make it blank.
 sed -i 's/kenny/d' filename  -> it deletes all the lines which contains kenny
 sed '<line_number> s/word/replacement/g' input_file
 sed ‘1s/Bash/Shell/g’ file0.txt -> it replaces the bash in first line 
 sed '1s/Bash/Shell/2' file0.txt -> 2 denotes occurance 2 in first line.
 create empty lines in a file and now you want to delete delete empty lines in that
 sed -i '/^$/d' filename   -> ^ it denotes anything it starts $ anything it ends thus it deletes all empty lines. 
 sed -i '1,2d' filename it deletes 1st and 2nd line of file.
 if you wanted delete the tab space then use below command
 sed -i 's/\t/ /g' filename
 if you wanted to see only few lines in file -> sed -n 12,18p filename 
 if you want to see data except 12 to 18 line -> sed sed 12,18d filename
 replace the one word in all places except 8th line -> sed '8! s /ram/sham/' filename

 # User account manager:

 commands:
 useradd
 groupadd
 userdel
 groupdel 
 usermod

 Files: 
 /etc/passwd
 /etc/group
 /etc/shadow

 example -
 useradd -g superheros -s /bin/bash -c "user description" -m -d /home/spiderman spiderman  (-g : option to add a group, -s: show environment, -c : to define user description, -m -d : to show home directory and user)

 to create user or group get into root with su - 
 useradd spiderman
 id spiderman - > to check / vlidate 
also can be checked in the home directory.

groupadd superheros -> it adds group
cat /etc/group -> it shows that names of groups it created 
userdel -r spiderman -> it deletes the user 

groupadd nonew
cat /etc/group
groupdel nonew -> it deletes the created group
cat /etc/group -> to verfy it deleted.

usermod -G spiderman,superheros spiderman -> it adds siderman to superheros group
grep spiderman /etc/group -> to check 
if you do ls -l you will see the group is still spiderman as it's main group is that one only just it is a part of superheros too.
to change that group
chgrp -R superheros spiderman  (-R is used to cascade this info to every folder of spiderman)
ls -ltr -now you can see the grp has changed

cat /etc/passwd ->the created user got added in it.
cat /etc/group -> to see the groups and users part of it.
cat /etc shadow -> to see the password encrypted

useradd -G superheros -s /bin/bash -c "ironman character" -m -d /home ironman ironman
id ironman -> to validate 
cat /etc/passwd

To set password:
passwd ironman -> enter password 

# enable password aging: 

The chage command -per user
eg :
chage [-m mindays] [-M maxdays] [-d lastdays] [-I inactive] [-E expieredate] [-W wanrdays] user

File = /etc/login.def

PASS_MAX_DAYS  99999
PASS_MIN_DAYS 0
PASS_MIN_LEN  5
PASS_WARN_AGE 7

LOGIN AS ROOT

more /etc/login.defs 

Please create a user named "bububutt"
id babu 
grep babu /etc/shadow 

chage -m 5 -M 90 -W 10 -I3 babubutt 
grep babubutt /etc/shadow  -> it will show you all the options we entered through the command.

chage -l username -> prints all the information for the user password.

# Switch Users and sudo Access:

su - username
sudo command 
visudo 

file:
/etc/sudoers 

ifconfig -> used to find out ip of user 
copy the ip and put it in the putty and put Vboxuser and password in the console
check whoami
su - spiderman
enter password
whoami
exit -> to logout user
su -    ( now you are root)

now you are vboxuser 

sudo dmidecode -> it will give you error
fdisk -l -> gives disk space info but will give an error

visudo 

vboxuser all=(all) 
usermod -aG wheel vboxuser 
grep wheel /etc/group -> to varify the changes.

su - vboxuser 
whoami
sudo dmidecode -> it will ask for password now 
sudo fdisk 

# Monitor Users :

who 
last 
w 
finger 
id

hostname 
who - how many terminal with how many users.
login as spiderman user and then try who command it will show u the users currently working / logged in. it is used to know who are logged in at very high load.

last -> it gives data who logged in from day 1
last | more 

login as root and run -> yum install finger -y

id -> it gives own information 
id {username}

# talking to users (users, wall, write):

users
wall
write

# Special permission with setuid, setgid and sticky bit:

to assign special permission at the user level:
chmod u+s xyz.sh

to assign special permission at group level:
chmod g+s xyz.sh

To remove special permission at the user or group level:
chmod u-s xyz.sh
chmod g-s xyz.sh

to find all executable in linux with setuid and setgid permissions
find / -perm /6000 -type f

main content: sticky bits are used when you dont want to delete any file at any cost by anyone by mistakenly.
chmod -t directory

# linux account authentication:

# difference betn active directory, LDAP, IDM, WinBIND, OpenLDAP etc

active directory = microsoft 

All of these — Active Directory, LDAP, OpenLDAP, Winbind, and IdM (FreeIPA) — are related to identity management and authentication.

They help manage:

Who can log in (users)

What they can do (permissions, groups, policies)

Where they can log in (computers, servers, domains)

But each one plays a different role in that process.


# system utility command (date, hostname,uptime,uname, which,cal, bc)

date – Displays or sets the current system date and time.

hostname – Shows or sets the system’s host name.

uptime – Displays how long the system has been running and the system load averages.

uname – Prints system information like OS name, kernel version, and hardware details.

which – Shows the full path of a command’s executable file.

cal – Displays a calendar for the current month or a specified month/year.

bc – A command-line calculator for performing mathematical calculations.

# processes, jobs and scheduling:

systemctl command:  in windows we can double click and open any application but in linux systemctl is used. 
systemctl is used to control and manage systemd services and system states (start, stop, enable, disable, check status, reboot, etc.).

systemctl start | stop | status servicename.service  (firewall)

systemctl enable servicename.service 
systemctl restart | reload servicename.service 
systemctl list-units --all 


# ps command
 The ps command in Linux (short for “process status”) is a utility used to view information about running processes on a system.

 When you run ps, it shows details like:

PID (Process ID)

User running the process

CPU and memory usage

TTY (terminal controlling the process)

Start time

Command that started the process

Common use cases
Monitoring, troubleshooting, scripting, performance tuning

ps -e or ps -A	Show all processes on the system
ps -f	Show full format listing (includes PPID, time, etc.)
ps -u <user>	Show processes for a specific user
ps -x	Show processes not attached to a terminal (e.g. daemons)
ps -aux	Show all processes in BSD style (commonly used form)
ps -ef	Show all processes in full-format (System V style)
ps -p <PID>	Show details for a specific process ID
ps --sort=-%mem	Sort by memory usage (descending)
ps --sort=-%cpu	Sort by CPU usage (descending)

# top command:
The top command in Linux/Unix is a real-time process monitoring tool. Unlike ps (which gives a snapshot), top continuously updates the list of running processes and system resource usage.

When you run top, you’ll see:

System summary (top section):

Uptime, number of users, load average

CPU usage (user, system, idle, etc.)

Memory usage (total, used, free, buffers, cache, swap)

Process list (bottom section):

PID → Process ID

USER → Owner of the process

PR / NI → Priority and nice value

VIRT / RES / SHR → Virtual, resident, and shared memory

%CPU / %MEM → CPU and memory usage percentage

TIME+ → Total CPU time consumed

COMMAND → The command that started the process

⚡ Common Usage
Run top → Starts the monitor.

Press q → Quit.

Press k → Kill a process (you’ll be asked for PID).

Press r → Renice (change priority).

Press M → Sort by memory usage.

Press P → Sort by CPU usage.

Press 1 → Show CPU usage per core.

top - gives live process status ( if you type c it will show you absolute path)
top -u vboxuser/root  ->  shows tasks / processes own by user

# kill command :

The kill command in Linux/Unix is used to terminate processes by sending them signals. Despite its name, it doesn’t only “kill” processes — it can send different signals to control them.

kill -[options] <PID> 
PID = Process ID (you can find it using ps, top, or pgrep).

kill is a process control command used to send a signal to one or more processes.

By default, it sends the TERM (terminate) signal, which politely asks the process to stop.

If the process refuses to stop, you can send a KILL signal, which forces it to stop immediately.

Use Case	Description	Example
🧹 Stop unresponsive processes	When an app hangs or freezes	kill -9 5678
🔄 Restart services	Stop and start daemons or background services	kill -HUP $(pidof nginx)
⚙️ Automate system tasks	Scripts use kill to control background jobs	In scripts: kill -TERM $PID
👮 System administration	Manage runaway or high-resource processes	`ps aux
💤 Pause or resume jobs	Temporarily stop or resume background jobs	kill -STOP <PID> / kill -CONT <PID>

kill -l -> to get a list of all signal names or signal number 
Commonly Used Signals
Signal	Name	Description
1	SIGHUP	Hang up — reload configuration or restart process
2	SIGINT	Interrupt — same as pressing Ctrl + C
9	SIGKILL	Force kill — immediately stops the process (cannot be ignored)
15	SIGTERM	Terminate gracefully — allows cleanup before stopping (default)
18	SIGCONT	Continue a stopped process
19	SIGSTOP	Stop (pause) a running process temporarily

killall -> kill allprocess or all child process
pkill -> kill by process name

# process signals in linux:

SIGINT (signals interrupt) -> kill -SIGINT PID
SITERM (signals terminate) -> it allow to save the data and kill it gracefully -  kill -SIGTERM PID
SIGKILL 9signals kill - forcefully kill process - kill -SIGKILL PID
SIGSTOP 9pause running process
SIGCONT (resume stopped process)
SIGSEGV (sinals segmentation fault) access invalid memory location.

Real time signals :

types :
SIGRTMIN
SIGRTMAX
intermediate signals bet these two

SIGRTMIN -
marks begining of signal range - signal starts from this range

SIGRTMAX - 
highest numbers in this range - marks end of signal range

intermediate signal
used for custom processes 

to practice above commands - open vim command in another terminal and execute all above commands
when u use SIGTERM it allow to save before it terminate
so after it use ls -al and then access that file again with vim -r filename

# crontab command :

crontab command is used to scedule the specific task that you run on daily basis.
crontab (cron table) is used to create, edit, install, uninstall, and list the cron jobs for a specific user.
Cron jobs allow you to run scripts or commands automatically at given times: hourly, daily, weekly, monthly, or at custom intervals.

It is used in:

Linux/Unix systems for automation
Servers (backup scripts, cleanup tasks, monitoring scripts)
DevOps / SysAdmin tasks
Scheduling repeated tasks, such as:
Log rotation
Database backups
Running scripts at timed intervals
Monitoring system resources
Updating data files automatically

Command	Description
crontab -e	Edit the current user's cron jobs
crontab -l	List current user's cron jobs
crontab -r	Remove all cron jobs for current user
crontab -u username -e	Edit cron jobs for another user (requires root)
crontab -u username -l	List cron jobs for another user
crontab -i -r	Remove cron jobs with confirmation prompt

* * * * * command
│ │ │ │ └── Day of week (0–7)
│ │ │ └──── Month (1–12)
│ │ └────── Day of month (1–31)
│ └──────── Hour (0–23)
└────────── Minute (0–59)

# at command:

The at command in Linux/Unix is used to schedule a one-time task to run at a specific time in the future. Unlike cron, which is for recurring jobs, at is perfect for tasks you want to run just once.

at TIME
Then type the command(s) you want executed, and press Ctrl+D to save and exit.

at 10:30 PM  - command

atq to see the list of at executed
echo "backup.sh" | at 9am tomorrow

# additional cronjobs (hourly, daily, weekly, monthly):

Additional cron jobs simply mean adding more scheduled tasks to the existing cron system. You do this by editing your crontab file (crontab -e) or system-wide cron directories (like /etc/cron.d/, /etc/cron.daily/, /etc/cron.weekly/). You use additional cron jobs when you need recurring automation beyond what a single crontab entry covers. Compared to at, which is for one-time jobs, additional cron jobs are for multiple recurring tasks that need to run at different times or frequencies

Let’s say you want to run a log cleanup script weekly.
sudo nano /etc/cron.weekly/clean_logs

add the commands in the file clean_logs

#!/bin/bash
#Simple log cleanup
rm -f /var/log/myapp/*.log
echo "Logs cleaned on $(date)" >> /var/log/cleanup.log

make the script executable :
sudo chmod +x /etc/cron.weekly/clean_logs

Verify:
Cron will automatically run this script once a week (usually Sunday at midnight, depending on your distro).
You can check logs in /var/log/syslog or /var/log/cron to confirm execution.

# When to Use This Instead of crontab or at
Use system cron directories when:
You want simple recurring jobs (daily, weekly, monthly) without writing cron expressions.
You prefer modular management (each script is separate, not all jobs in one crontab file).
System administrators want to keep jobs organized by frequency.

Use crontab when:
You need custom schedules (e.g., every 10 minutes, every Tuesday at 3 PM).

Use at when:
You need a one-time job (e.g., run a script tomorrow at 5 PM).

# Process management (bg, fg, nice):

bg/fg → When you want to multitask in the same terminal.
nice/renice → When you want to control CPU usage and prevent one process from slowing down the system.

By default, it runs in the foreground (you can’t use the terminal until it finishes).
You can send it to the background so you can keep using the terminal.
You can also adjust its priority so the system decides how much CPU time it gets.

ctrl z - it stops the process

fg %job_id
bg %job_id


nohup process 
Prevents the process from stopping when the terminal session closes
Redirects output if needed
Is commonly used for running long-running scripts, servers, or background tasks

nohup sleep 70 /filepath 2>&1 &
jobs - command give u the bg jobs running currently


Priority Control
nice
Sets the priority of a process when starting it.
Priority values range from -20 (highest priority) to 19 (lowest priority).
Default is 0.


nice -n [value] command
nice -n 10 ./heavy_script.sh

# system monitoring (df, dmseg, iostat 1,netstat, free, top) : 

top - 

# log monitoring (/var/log):

mostly used logs : (google it and uderstand it)
boot
chronyd
cron
maillog
secure
message
httpd

# system maintenance commands (shutdown, init, reboot, halt):

shutdown [OPTION] [TIME] [MESSAGE]
shutdown -h +10 "System will shut down in 10 minutes"
shutdown -h now - it shutdown now 
shutdown -h now - it re strarts the system 

you should be root
to reboot:
shutdown -r now
reboot

to halt:
Stops all processes and halts the CPU.
Doesn’t always power off the machine (depends on hardware and init system).
halt

for init:
Changes the system’s runlevel (system state).
Runlevels (traditional SysV init):
0 → Halt (shutdown)
1 → Single-user mode
3 → Multi-user mode (text-based)
5 → Multi-user mode with GUI
6 → Reboot

init 0   # shutdown
init 6   # reboot


# changing system Hostname (hostnamectl): 

sudo su
cat /etc/hostname
hostnamectl set-hostname indiahost1
cat /etc/hostname
hostname - it will give new hostname but command line will still hold old hostname for this you need to reboot the machine so apply command
init 6  -it will reboot

# finding system information( uname, dmidecode):

cat /etc/redhat-release
uname -a
dmidecode

# System architecture (arch):to know our system is 32 bit or 64 bit 

arch
uname -a

# SOS report : ()

it collect amd package diagnostic and support data.
duso su 
sosreport 

# terminal control keys:


Ctrl+C	Interrupt	Stops the current foreground process (sends SIGINT).
Ctrl+Z	Suspend	Pauses the current process and puts it into background (sends SIGTSTP).
Ctrl+D	End of Input	Signals end-of-file (EOF) to the terminal; often logs you out of a shell.
Ctrl+S	Stop Output	Pauses terminal output (flow control).
Ctrl+Q	Resume Output	Resumes terminal output after Ctrl+S.
Ctrl+\\	Quit	Kills the current process (sends SIGQUIT), often with a core dump.
Ctrl+L	Clear Screen	Clears the terminal display (like clear command).
Ctrl+H	Backspace	Deletes the character before the cursor.
Ctrl+U	Kill Line	Deletes everything typed on the current line.
Ctrl+W	Delete Word	Deletes the word before the cursor.
Ctrl+R	Reverse Search	Search through command history interactively.
Ctrl+A	Beginning of Line	Moves cursor to start of the line.
Ctrl+E	End of Line	Moves cursor to end of the line.
Ctrl+K	Kill to End	Deletes everything from cursor to end of line.
Ctrl+Y	Yank	Pastes (yanks) the last killed text.

# terminal commands (clear, exit, script):

The script command in Linux/Unix is a handy utility that records everything you type and see in the terminal into a file. It’s often used for logging sessions, creating tutorials, or saving troubleshooting steps.

script filename 

 - after this whatever you work will be recorded in the same folder where you executed this command. once the required recoding is done type exit

 exit  - to stop the recording.

 # recover root password: 

 if you wanted to change the root password you need to know the previous root password and if we  do not know it we need to implement below steps:
 restart computer - reboot
 edit grub
 change password
 reboot

 # environment variables: 

 printevn or evn


 # screen commands: 


 # TMUX 
 
# module 6 - Shell Scripting 

# types of shell 


# module 7 ( Networking , services and system updates):

# network files and commands (ping, ifup, ifdown, netstat, tcpdump): 

# NIC information (ethtool):

# NIC or port bonding 
