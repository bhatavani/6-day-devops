Day 2 – Basic Linux Commands

The second day of our DevOps Skill Lab training focused on gaining practical experience with essential Linux commands. As Linux is the most widely used operating system in the DevOps and cloud computing domains, mastering these commands is crucial for managing servers and environments effectively. We were introduced to a wide range of commands covering different areas such as file and directory handling, process management, user management, system monitoring, networking, and more. These commands were demonstrated with live examples, allowing us to perform hands-on activities in a Linux environment.

1. Directory & File Management
These commands are used to navigate the file system and perform operations on files and directories.

  >pwd – Displays the present working directory.

  >ls – Lists files and directories.

  >ls -l – Shows detailed listing including permissions, owner, etc.

  >ls -a – Lists all files including hidden ones.

  >cd <directory> – Changes to the specified directory.

  >cd .. – Moves one directory up.

  >mkdir <folder> – Creates a new directory.

  >rmdir <folder> – Deletes an empty directory.

  >touch <file> – Creates an empty file.

  >rm <file> – Deletes a file.

  >rm -r <folder> – Recursively deletes a folder and its contents.

  >mv <src> <dest> – Moves or renames files and directories.

  >cp <src> <dest> – Copies files or directories.



2. File Viewing & Editing
These commands allow users to view or modify file contents using command-line tools or editors.

  >cat <file> – Displays file content.

  >more <file> / less <file> – Views file content one page at a time.

  >head -n 10 <file> – Shows the first 10 lines of a file.

  >tail -n 10 <file> – Shows the last 10 lines of a file.

  >nano <file> – Opens the file in the nano text editor.

  >vi <file> – Opens the file in the vi editor.

  >echo "text" > file – Writes text to a file (overwrites existing content).

  >echo "text" >> file – Appends text to an existing file.



3. File Permissions & Ownership
  >Used for setting access rights and ownership to control file accessibility.

  >chmod +x <file> – Makes a file executable.

  >chmod 755 <file> – Sets read/write/execute permissions.

  >chown user:user <file> – Changes the file's ownership.

  >ls -l – Displays file permissions in long listing format.

4. System Information & Monitoring
These commands are used to fetch system-related information and monitor performance.

  >clear – Clears the terminal screen.

  >history – Shows the list of previously executed commands.

  >whoami – Prints the currently logged-in user.

  >uname -a – Displays detailed system information.

  >uptime – Shows how long the system has been running.

  >top – Displays real-time system processes.

  >htop – Interactive version of top (if installed).

  >free -h – Shows memory usage in a human-readable format.

  >df -h – Displays disk space usage.


5. Searching & Filtering
These commands assist in locating files or filtering content within files.

  >grep "pattern" <file> – Searches for matching text in a file.

  >find . -name "*.yml" – Searches for files matching a pattern.

  >wc -l <file> – Counts the number of lines in a file.

  >sort <file> – Sorts the contents of a file.

  >cut -d ":" -f 1 <file> – Extracts specific columns from a file.


6. Networking & Internet
  >These commands help in managing network connections and fetching data from the internet.

  >ping google.com – Checks network connectivity.

  >curl <url> – Fetches content from a specified URL.

  >wget <url> – Downloads files from a URL.

  >ifconfig / ip a – Displays network interface information.

  >netstat -tulpn – Lists open ports and services.


7. Process Management
Used for listing and controlling running processes.

  >ps aux – Lists all running processes.

  >kill <PID> – Terminates a process by its process ID.

  >kill -9 <PID> – Forcefully terminates a process.

  >bg / fg – Sends processes to background or foreground.



8. Package Management (Debian/Ubuntu)
These commands manage software packages using the APT package manager.

  >sudo apt update – Updates the package list.

  >sudo apt upgrade – Installs the latest version of installed packages.

  >sudo apt install <package> – Installs a new package.

  >sudo apt remove <package> – Removes an installed package.


9. User Management
These are used to manage user accounts and switch between users.

  >adduser <username> – Adds a new user to the system.

  >passwd <username> – Sets or changes the user's password.

  >who – Displays currently logged-in users.

  >su - <user> – Switches to a different user account.


Outcomes:
By the end of this session, we acquired hands-on experience with a wide range of Linux commands. These covered file system navigation, user management, system monitoring, file editing, process handling, and networking—forming a strong foundation for future tasks involving tools like Docker, Kubernetes, and CI/CD pipelines.
