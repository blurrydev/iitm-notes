# Structure

## Output of `ls -l`

1. **File permissions**: The first column represents the file permissions. It consists of ten characters, divided into four sections:
    
    - The first character indicates the file type (`-` for regular files, `d` for directories, `l` for symbolic links, etc.).
		- `-` (hyphen): Indicates a regular file.
		- `d`: Represents a directory.
		- `l`: Denotes a symbolic link.
		- `c`: Indicates a character device file.
		- `b`: Represents a block device file.
		- `p`: Denotes a named pipe (FIFO).
		- `s`: Represents a socket file.
    - The next three characters (`rwx`) indicate the read, write, and execute permissions for the file owner.
    - The following three characters (`rwx`) represent the read, write, and execute permissions for the group.
    - The last three characters (`rwx`) denote the read, write, and execute permissions for other (everyone else).

- The permission characters can be one of the following:

	- `r`: Read permission. Allows viewing the contents of a file or listing the contents of a directory.
	- `w`: Write permission. Allows modifying the contents of a file or creating, deleting, and renaming files in a directory.
	- `x`: Execute permission. Allows executing a file or accessing files within a directory.
	- `-` (hyphen): Indicates the absence of a particular permission.

2. **Number of hard links**: The second column shows the number of hard links associated with the file. A hard link is an additional name for the same file.
    
3. **Owner**: The third column displays the username or user ID of the file owner.
    
4. **Group**: The fourth column shows the group name or group ID associated with the file.
    
5. **File size**: The fifth column indicates the size of the file in bytes. For directories, this value represents the size occupied by the directory's metadata.
    
6. **Modification timestamp**: The next columns represent the date and time when the file was last modified or updated.
    
7. **File/directory name**: The last column displays the name of the file or directory. 

```linux
-rw-r--r--  1 user  group  4096  Jun 1 10:30  file.txt
drwxr-xr-x  2 user  group  4096  Jun 1 10:45  directory
lrwxrwxrwx  1 user  group    15  Jun 1 11:20  link -> /path/to/file
```


### Permission Code

- Read (r): 4
- Write (w): 2
- Execute (x): 1

To calculate the permission code for a file, you add up the numeric values of the desired permissions.

# Commands

- `date`: Display date and time.
- `ps`: Lists current processes.
- `cal`: Display calendar.
	- can be clubbed with a month and year to display specific month.
	- `cal Jun 1999`
	- cannot be clubbed with only month, but can be with only year.
- `free`: Shows memory stats.
- `groups`: Groups to which the current user belongs to.
- `file` {followed by file name}: To check the type of file.
- `less`: It is used to read the contents of a file.

> `less` does not work like `cat`. `cat` prints the value on the screen whereas less enables you to read it and then provides an option to quit the reading mode once done.

> There is another command called `more` which works like `cat`.


- `chmod` is used to change the permissions of files and directories in Linux.
	- Three types of permissions: read (r), write (w), and execute (x).
	- Permissions can be assigned to three groups: owner (u), group (g), and others (o).
	- Numeric representation can be used to set permissions.
	- Numeric values: 4 for read, 2 for write, and 1 for execute.
	- To set permissions for a file:
	    - `chmod u+r file`: Add read permission for the owner.
	    - `chmod g+w file`: Add write permission for the group.
	    - `chmod o-x file`: Remove execute permission for others.
	- Symbolic representation can be used to set permissions.
	- Symbolic values: `+` adds a permission, `-` removes a permission, and `=` sets exact permissions.
	- To set permissions for a file:
	    - `chmod u=rw file`: Set read and write permissions for the owner.
	    - `chmod go-wx file`: Remove write and execute permissions for group and others.
	- Recursive permission changes can be done using the `-R` flag.

- `touch`: 
	- `touch` is used to create new files or update timestamps of existing files.
	- If the file already exists, `touch` updates the access and modification timestamps to the current time.
	- If the file doesn't exist, `touch` creates an empty file with the specified name.
	- Common usage: `touch filename` or `touch file1 file2 file3` to create or update the timestamps of one or multiple files.
	- `touch` can also be used to create multiple files at once by specifying their names as arguments.
	- Use the `-c` option to avoid creating a new file if it doesn't exist.
	- Use the `-d` option to specify a date/time for setting timestamps.
	- Use the `-r` option to copy the timestamps from an existing file.

- `cp`: 
	- `cp` is used to copy files and directories in Linux.
	- Syntax: `cp source_file destination_file`.
	- To copy a file to a directory: `cp file.txt directory/`.
	- To copy multiple files to a directory: `cp file1.txt file2.txt directory/`.
	- To recursively copy a directory and its contents: `cp -r source_directory/ destination_directory/`.
	- Use the `-i` option for interactive mode, prompting before overwriting existing files.
	- Use the `-u` option to only copy files that are newer than the destination files.
	- Example: `cp file.txt backup/` copies "file.txt" to the "backup" directory.
- `mv`: 
	-  `mv` is used to move or rename files and directories in Linux.
	- Syntax: `mv source_file destination_file`.
	- To move a file to a directory: `mv file.txt directory/`.
	- To rename a file: `mv old_name.txt new_name.txt`.
	- To move and rename a file simultaneously: `mv file.txt directory/new_name.txt`.
	- Use the `-i` option for interactive mode, prompting before overwriting existing files.
	- Example: `mv file.txt documents/` moves "file.txt" to the "documents" directory.
- `mkdir`: 
	- `mkdir` is used to create directories in Linux.
	- Syntax: `mkdir directory_name`.
	- To create multiple directories: `mkdir dir1 dir2 dir3`.
	- Use the `-p` option to create parent directories if they don't exist.
	- Example: `mkdir new_directory` creates a directory named "new_directory".
- `rm`: 
	- `rm` is used to remove files and directories in Linux.
	- Syntax: `rm file.txt` or `rm -r directory/` for recursive removal.
	- Use the `-i` option for interactive mode, prompting for confirmation before deleting each file.
	- Use the `-f` option to force removal without confirmation.
	- To remove directories and their contents recursively: `rm -r directory/`.
	- Example: `rm file.txt` removes the file named "file.txt".

- `ls`: Lists the available directories and file in the pwd.
	- `-l`: Shows the same thing but with long details. [Read More](#Output%20of%20`ls%20-l`)
	- `-a`: Shows all files and directories, even the hidden ones.
	- `-la`: Hybrid of the above two.
 
- `pwd`: Returns the Present Working Directory