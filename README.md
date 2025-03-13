# Creating, Modifying, and Removing Files and Folders Linux

> Aisha Shaban

<aside>
This tutorial guide will walk you through basic Linux file management operations using command line.

</aside>



# Linux Overview

The **file system** controls how data is stored and retrieved in a computer. All files and folders in a Linux system are part of a bigger tree-like structure rooted at /. Files and folders are added to the file system by appending them to this tree structure, and deleted by removing them. **All file names are case sensitive**. When working with files and directories on the command line, special characters, like space and brackets, have to be **escaped** using a backslash.

---

Here are a few helpful navigation commands to help you explore the Linux file system:

You can check out the contents of the current directory using the **ls** command.

```bash
1 ls
```

You can view more details about the files, like ownership and permissions, by adding the flag **-l** to the **ls** command.

```bash
1 ls -l
```

You can see hidden files in the current directory by passing flag **-a** to the **ls** command.

```bash
1 ls -a
```

You can find out where you are in relation to the rest of the file system using the **pwd** command.

```bash
1 pwd
```

You can navigate to different directories using the **cd** command.

```bash
1 cd /path/to/other/directory
```

You can check out the contents of a file using the **cat** command.

```bash
1 cat /path/to/file/file_name
```

For large input files, the less command allows movement within the files. The syntax is similar to that of the **cat** command, but you can move.

Reading large file using **less**

```bash
1 less /path/to/file/file_name
```

The command will provide you with a scrollable view of the content within the file, up to the end of the file content. Scroll down using **Enter**, and exit the view by pressing **q**.

---


# **Create directories (folders)**

Directories (folders) in Linux are created using the **mkdir** command. The command takes the directory name as the argument.

```bash
1 mkdir directory_name
```

Multiple directories can be supplied as arguments, and **mkdir** will create all of them.

```bash
1 mkdir dir1 dir2 dir3
```

### Parameters

**mkdir** can take three options:

- **p**: allow mkdir to create parent directories if they don't exist
- **m**: (mode) used to set permissions of directories during creation
- **v**: run command in verbose mode

In this Linux virtual machine, directory **/home/user/Desktop** contains a file called **colors**. We'll open the file, and for every line listed in it, we'll create a new folder with that name in the directory **/home/user/Documents**.

1. Change into the working directory.

```bash
1 cd /home/user/Documents
```

1. Show the contents of the file **colors** within the **Desktop** directory.

```bash
1 cat /home/user/Desktop/colors
```

Output:

```bash
red
blue
green
yellow
magenta
```

1. Create the directories

```bash
1 mkdir red blue green yellow magenta
2 ls
```

Output:

```bash
**Hidden  blue  green  magenta  red  yellow**
```

# Removing Empty Directories

To remove empty directories, use the **rmdir** command. The name of the directory to be removed is passed as an argument.

```bash
1 rmdir dir_name
```

<aside>
💡

Multiple directory names can be passed as arguments, and **rmdir** will remove all of them.

</aside>

```bash
1 rmdir dir1 dir2 dir3 dir4
```

<aside>
💡

**Head's up:** **rmdir** only removes empty directories. To remove a non-empty directory, the command **rm** is used.

</aside>

**rmdir** takes only one option, which tells it to remove parent directories if they're also empty.

- **p**: remove parent directories, if they're also empty

# Creating files

By default, the **touch** command is used to change the modification and access times of a file. If the file doesn't exist, the **touch** command is used to create a file with default permissions.

In the current directory, we can create an empty file called **empty_file**:

```bash
1 touch empty_file
```

### Options

The **touch** command can take the **-c** option to prevent a new file from being created.

- **c**: do not create file if the file doesn't exist

# **Copying, moving and deleting files and directories (folders)**

The **cp** command is used to make a copy of one or more directories or files. The command takes **at least** one source name and one target name. If the target is a file, then the source must also be a file. A copy of the source will be made with the new name supplied in target. If the target name isn't specified, a copy of source will be made in the target directory under the same name. If a file with the target name already exists in the target directory, it will be replaced. If the target is an existing directory, then all sources (one or more) will be copied into the target directory. If the target is a directory that doesn't exist, then the source must also be a directory. A copy of the directory and its contents will be made in target under the same name.

## Example 1:

Copy the file **source_file** in the directory **/home/user/** to the directory **duplicates** as **target_file**

```bash
1 cp /home/user/source_file /home/user/duplicates/target_file
```

The **duplicates** directory now contains a copy of the original file.

**mv**

The move command is used to move one or more files or directories into a different location, or rename them to a new name. You're required to pass at least one source and target file names or directories. The **mv** command follows the rules for existing or non-existing directories or files, as does **cp**.

## Example 2:

Move the file **source_file** in **/home/user/** to the directory **moved_files** and give it the name **target_file**.

```bash
1 mv /home/user/source_file /home/user/moved_files/target_file
```

The original directory doesn't contain the file now. It's been moved to the new directory **moved_files**.

**rm**

The **rm** command is used to remove one or more files. You need to supply **at least** one argument to remove.

## Example 3:

We can remove the duplicate file we created in the directory **duplicates** using **rm**:

```bash
1 rm /home/user/duplicates/target_file
```

Let's see how to copy, move, and rename files by going through a few examples.

In the directory **/home/user/Pictures**, we'll take all the hidden files and move them into the directory **/home/user/Documents/Hidden**.

1. Change into the Pictures directory

```bash
1 cd /home/user/Pictures
```

1. Show the directory contents, including hidden files

```bash
1 ls -a
```

**HOW THIS APPEARS IN SHELL:**

```bash
1 student@ca721599e80e:~$ cd /home/user/Pictures
2 student@ca721599e80e:/home/user/Pictures$ ls -a
3 .  ..  .apple  .banana  .broccoli  .milk  chocolate  egg
```

1. Move the hidden files into the target directory

```bash
1 mv .apple .banana .broccoli .milk /home/user/Documents/Hidden
```

In the directory **/home/user/Movies**, there's a folder called **Europe Pictures**. We'll move this folder into the correct directory for pictures: **/home/user/Pictures***.* Note the use of the backslash **\** to escape the space between "Europe" and "Pictures" in the directory name, **Europe Pictures**.

```bash
1 mv /home/user/Movies/Europe\ Pictures /home/user/Pictures
```

You can also use a **dot** (**.**) to copy or move files to the current directory. In the directory **/home/user/Images**, we can move the file **Vacation.JPG** into the **Pictures** directory. To do that, we change into the **Pictures** directory, then add a **dot** to the **mv** command as the target.

```bash
1 cd /home/user/Pictures
2 mv /home/user/Images/Vacation.JPG .
```

**HOW THIS APPEARS IN SHELL:**

```bash
1 student@ca721599e80e:~$ cd /home/user/Pictures
2 student@ca721599e80e:/home/user/Pictures$ mv /home/user/Images/Vacation.JPG .student@ca721599e80e:/home/user/Pictures$ ls
3 'Europe Pictures'   Vacation.JPG   chocolate   egg
```

Some files in the directory **/home/user/Music** need to be cleaned up. We'll see an example of removing files and directories by removing:

- **Best_of_the_90s**
- **80s_jams**
- **Classical**
- **Rock** (folder)
1. Navigate to the Music folder.

```bash
1 cd /home/user/Music
```

1. Remove the files.

```bash
1 rm Best_of_the_90s 80s_jams Classical
```

**HOW THIS APPEARS IN SHELL:**

```bash
1 student@ca721599e80e:~$ cd /home/user/Music
2 student@ca721599e80e:/home/user/Music$ ls
3 80s_jams  Best_of_the_90s  Classical  Electronic  Rock  Smooth_jazz
4 student@ca721599e80e:/home/user/Music$ rm Best_of_the_90s 80s_jams Classical
5 student@ca721599e80e:/home/user/Music$ ls
6 Electronic  Rock  Smooth_jazz
```

1. Remove the directory

```bash
rmdir Rock
```

To remove a directory with content, the **rm** command is used instead of **rmdir**. The option **-r** tells the command to remove the directory, along with its content, recursively.

## Example 4:

```bash
1 rm -r non_empty_dir
```

# Searching in Files

**grep** is a super powerful Linux command used to search through files for the occurrence of a string of characters that matches a specified pattern. We can use the command in combination with a bunch of different options and flags for efficient searching.

### Options and flags

- **r**: search recursively
- **w**: match the whole word
- **n**: only in line number
- **e**: match pattern
- **-include** and **-exclude**: include and exclude files in the search
- **-include-dir** and **-exclude-dir**: include or exclude directories in the search

Let's take a look at the **grep** command in action. In the directory **/home/user/Downloads** of your virtual machine, a number of files exist. We'll find the files that have the word "vacation" in them, and move them to **/home/user/Documents**.

1. Find files

```bash
1 grep -rw /home/user/Downloads -e "vacation"
```

Output:

```bash
1 /home/user/Downloads/Japan:We enjoyed our vacation here.
2 /home/user/Downloads/Iceland:We had a great vacation here.
```

1. Move the directories that match into the target directory.

```bash
1 mv /home/user/Downloads/Iceland /home/user/Downloads/Japan /home/user/Documents
```

# Editing files

Lots of Linux distributions come with pre-installed text editors. The most popular ones are **vi** and **nano**, which will be included in nearly every distribution. Other text editors, like Emacs and Gedit, might also be present. In this lab, we'll modify files using the Nano editor.

You can use the **nano** command to open the nano editor and modify an existing file, or create a new one. To edit an existing file, we'll first start with opening it.

## Example 1

```bash
1 nano /path/to/existing/file
```

The command will open the file in the terminal and display the current file contents. To modify, you can edit the content in the terminal, just like a normal editor. The editor is managed using various shortcuts.

**Chromebook users: Instructions for saving a file in the nano editor**

1. **Save the file:**
    - Press **Ctrl + O** (which stands for "**Write Out**").
    - You will see a prompt "**My files**" window will open, simply close it.
    - Press **Enter** to save the changes.
2. **Close the nano editor:**
    - Press **Ctrl + X** to exit nano and perform the next command.

These shortcuts include:

- **Ctrl+O:** Save modifications to the file.
- **Ctrl+X:** Exit the program.
- **Ctrl+G:** Get help (can be used at any time while using the editor). **Ctrl+X** will exit help mode.

Alright, now let's practice how to edit files using nano.

In the current directory, create an empty file called **editor_test.txt**.

```bash
1 touch editor_test.txt
```

Open the file with the nano editor.

```bash
1 nano editor_test.txt
```

**NANO EDITOR DISPLAYS:**

```bash
1
2
3
4
5
6 ^G Get Help    ^O Write Out   ^W Where Is    ^K Cut Text    ^J Justify
7 ^X Exit        ^R Read File   ^\ Replace     ^U Uncut Text  ^T To Spell
```

Add content to the file. (In this case, we add five lines, each separated by an empty line.)

```bash
1 Knock Knock
2 
3 Who's there ?
4 
5 very long pause...
6  
7 java.
8 
9 :-)
10 
11 
12 
13 
14 
15 ^G Get Help    ^O Write Out   ^W Where Is    ^K Cut Text    ^J Justify
16 ^X Exit        ^R Read File   ^\ Replace     ^U Uncut Text  ^T To Spell
```

Save the file by hitting **Ctrl+O**.

```bash
1 Knock Knock
2 
3 Who's there ?
4 
5 very long pause...
6  
7 java.
8 
9 :-)
10 
11 
12 
13 
14 
15 
16
17 File Name to Write: editor_test.txt    
18 ^G Get Help        M-D DOS Format     M-A Append         M-B Backup File
19 ^C Cancel          M-M Mac Format     M-P Prepend        ^T To Files 
```

You'll need to confirm the file that you want to write the content to by hitting **Enter**. After this, exit the program by hitting **Ctrl+X**.

That's it! You've successfully created and modified a file.

## Conclusion

<aside>
In this lab, we've gone through the basics of creating, modifying, copying, and removing files and folders in Linux. As always, you can learn more about each of the commands we've covered by using the **man** command.

</aside>
