# Linux Basics
Linux is an open-source, Unix-like operating system kernel that powers a wide range of devices, from servers and desktops to smartphones and embedded systems. Known for its stability, security, and flexibility, it's widely used by developers, enterprises, and enthusiasts around the world.
<p></p>

## Linux Command Line

### 1. The Shell
What is the shell? The shell is basically a program that takes your commands from the keyboard and sends them to the operating system to perform. If you’ve ever used a GUI, you’ve probably seen programs such as "Terminal" or "Console"; these are just programs that launch a shell for you.<br>
Here's a basic shell command to print `Hello World` in Linux<br>

```
echo Hello World
```
### 2. Print Working Directory

Everything in Linux is a file.<br>
The first directory in the filesystem is aptly named the root directory. The root directory has many folders and files, which can store more folders and files, etc. Here is an example of what the directory tree looks like:<br>

```
/
|-- bin
|   |-- file1
|   |-- file2
|-- etc
|   |-- file3
|   `-- directory1
|       |-- file4
|       `-- file5
|-- home
|-- var
```

The location of these files and directories are referred to as paths. If you had a folder named home with a folder inside of it named pete and another folder in that folder called Movies, that path would look like this: /home/pete/Movies.<br>
To print this file directory, use the command:

```
pwd
```

### 3. cd (Change Directory)
There are two different types of paths in linux system. These are:

- Absolute Path: This is the path from the root directory. Root is commonly shown as `/`
- Relative Path: This is the path where you are currently in the file system.

To change the directory, simply use,

```
cd /home/pete/Pictures
```
and to go to a file in `Pictures` named `Hawaii`, use:

```
cd Hawaii
``` 

There are several shortcuts in Linux for navigation. These are:

```
cd .        // . (current directory): This is the directory you are currently in.
cd ..       // .. (previous directory): Takes you to the directory above your current one.
cd ~        // ~ (home directory): This directory defaults to your “home directory,” such as /home/pete.
cd -        // - (previous directory): This will take you to the previous directory you were just at.
```

## 4. ls (List Directories)
