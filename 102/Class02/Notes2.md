# **201**

# **Notes 2**

# *Linux 1*

## **Everything is a File**

Ok, the first thing we need to appreciate with linux is that under the hood, everything is actually a file. A text file is a file, a directory is a file, your keyboard is a file (one that the system reads from only), your monitor is a file (one that the system writes to only) etc. To begin with, this won't affect what we do too much but keep it in mind as it helps with understanding the behaviour of Linux as we manage files and directories.

## **Linux is an Extensionless System**

This one can sometimes be hard to get your head around but as you work through the sections it will start to make more sense. A file extension is normally a set of 2 - 4 characters after a full stop at the end of a file, which denotes what type of file it is. The following are common extensions:

1.) **file.exe - an executable file, or program.**

2.) **file.txt - a plain text file.**

3.) **file.png, file.gif, file.jpg - an image.**

In other systems such as Windows the extension is important and the system uses it to determine what type of file it is. Under Linux the system actually ignores the extension and looks inside the file to determine what type of file it is. So for instance I could have a file myself.png which is a picture of me. I could rename the file to myself.txt or just myself and Linux would still happily treat the file as an image file. As such it can sometimes be hard to know for certain what type of file a particular file is. Luckily there is a command called file which we can use to find this out.

## **Linux is Case Sensitive**

This is very important and a common source of problems for people new to Linux. Other systems such as Windows are case insensitive when it comes to referring to files. Linux is not like this. As such it is possible to have two or more files and directories with the same name but letters of different case.

1.) **user@bash:** ls Documents

2.) FILE1.txt File1.txt file1.TXT

3.)...

4.) **user@bash:** file Documents/file1.txt

5.) Documents/file1.txt: ERROR: cannot open 'file1.txt' (No such file or directory)
Linux sees these all as distinct and separate files.

Also be aware of case sensitivity when dealing with command line options. For instance with the command ls there are two options s and S both of which do different things. A common mistake is to see an option which is upper case but enter it as lower case and wonder why the output doesn't match your expectation.

## **Spaces in names**

Spaces in file and directory names are perfectly valid but we need to be a little careful with them. As you would remember, a space on the command line is how we seperate items. They are how we know what is the program name and can identify each command line argument. If we wanted to move into a directory called Holiday Photos for example the following would not work.

1.) **user@bash:** ls Documents

2.) FILE1.txt File1.txt file1.TXT Holiday Photos

3.) ...

4.) **user@bash:** cd Holiday Photos

5.) bash: cd: Holiday: No such file or directory

What happens is that Holiday Photos is seen as two command line arguments. cd moves into whichever directory is specified by the first command line argument only. To get around this we need to identify to the terminal that we wish Holiday Photos to be seen as a single command line argument. There are two ways to go about this, either way is just as valid.

## **Quotes**

The first approach involves using quotes around the entire item. You may use either single or double quotes (later on we will see that there is a subtle difference between the two but for now that difference is not a problem). Anything inside quotes is considered a single item.

1.) **user@bash:** cd 'Holiday Photos'

2.) **user@bash:** pwd

3.) /home/ryan/Documents/Holiday Photos

## **Escape Characters**

Another method is to use what is called an escape character, which is a backslash ( \ ). What the backslash does is escape (or nullify) the special meaning of the next character.

1.) **user@bash:** cd Holiday\ Photos

2.) **user@bash:** pwd

3.) /home/ryan/Documents/Holiday Photos

In the above example the space between Holiday and Photos would normally have a special meaning which is to separate them as distinct command line arguments. Because we placed a backslash in front of it, that special meaning was removed.


**Tab Completion:** If you use it before encountering the space in the directory name then the terminal will automatically escape any spaces in the name for you.

## **Hidden Files and Directories**

Linux actually has a very simple and elegant mechanism for specifying that a file or directory is hidden. If the file or directory's name begins with a . (full stop) then it is considered to be hidden. You don't even need a special command or action to make a file hidden. Files and directories may be hidden for a variety of reasons. Configuration files for a particular user (which are normally stored in their home directory) are hidden for instance so that they don't get in the way of the user doing their everyday tasks.

To make a file or directory hidden all you need to do is create the file or directory with it's name beginning with a . or rename it to be as such. Likewise you may rename a hidden file to remove the . and it will become unhidden. The command ls which we have seen in the previous section will not list hidden files and directories by default. We may modify it by including the command line option -a so that it does show hidden files and directories.

1.) **user@bash:** ls Documents

2.) FILE1.txt File1.txt file1.TXT

3.) ...

4.) **user@bash:** ls -a Documents

5.) . .. FILE1.txt File1.txt file1.TXT .hidden .file.txt

6.) ...

In the above example you will see that when we listed all items in our current directory the first two items were . and .. 

# **Summary**

## **file**

obtain information about what type of file a file or directory is.

## **ls -a**

List the contents of a directory, including hidden files.

# **Important Concepts**

**Everything is a file under Linux**
Even directories.

**Linux is an extensionless system**
Files can have any extension they like or none at all.

**Linux is case sensitive**
Beware of silly typos.



# *Linux 2*

**pwd**

 which stands for Print Working Directory. (You'll find that a lot of commands in linux are named as an abbreviation of a word or words describing them. This makes it easier to remember them.) The command does just that. It tells you what your current or present working directory is.

1.) **user@bash:** pwd

2.) /home/ryan

3.) **user@bash:**

It's one thing to know where we are. Next we'll want to know what is there. The command for this task is **ls**. It's short for **list**. Let's give it a go.

1.) **user@bash:** ls

2.) bin Documents public_html

3.) **user@bash:**

1.) **Line 1 -** We ran ls in it's most basic form. It listed the contents of our current directory.

2.) **Line 4 -** We ran ls with a single command line option ( -l ) which indicates we are going to do a long listing. A long listing has the following:

- First character indicates whether it is a normal file ( - ) or directory ( d )

- Next 9 characters are permissions for the file or directory (we'll learn more about them in section 6).

- The next field is the number of blocks (don't worry too much about this).

- The next field is the owner of the file or directory (ryan in this case).

- The next field is the group the file or directory belongs to (users in this case).

- Following this is the file size.

- Next up is the file modification time.

- Finally we have the actual name of the file or directory.

3.) **Line 10 -** We ran ls with a command line argument ( /etc ). When we do this it tells ls not to list our current directory but instead to list that directories contents.

4.) **Line 13 -** We ran ls with both a command line option and argument. As such it did a long listing of the directory /etc.

5.) Lines 12 and 18 just indicate that I have cut out some of the commands normal output for brevities sake. When you run the commands you will see a longer listing of files and directories.


## **Paths**

In the previous commands we started touching on something called a path. I would like to go into more detail on them now as they are important in being proficient with Linux. Whenever we refer to either a file or directory on the command line, we are in fact referring to a path. ie. A path is a means to get to a particular file or directory on the system.

## **Absolute and Relative Paths**

There are 2 types of paths we can use, **absolute** and **relative**. Whenever we refer to a file or directory we are using one of these paths. Whenever we refer to a file or directory, we can, in fact, use either type of path (either way, the system will still be directed to the same location).

To begin with, we have to understand that the file system under linux is a hierarchical structure. At the very top of the structure is what's called the **root** directory. It is denoted by a single slash ( / ). It has subdirectories, they have subdirectories and so on. Files may reside in any of these directories.

Absolute paths specify a location (file or directory) in relation to the root directory. You can identify them easily as they always begin with a forward slash ( / )

Relative paths specify a location (file or directory) in relation to where we currently are in the system. They will not begin with a slash.

Here's an example to illustrate:

1.) **user@bash:** pwd

2.) /home/ryan

3.) **user@bash:** 

4.) **user@bash:** ls Documents

5.) file1.txt file2.txt file3.txt

6.) ...

7.) **user@bash:** ls /home/ryan/Documents

8.) file1.txt file2.txt file3.txt

9.) ...

10.) **user@bash:**

- **Line 1 -** We ran pwd just to verify where we currently are.

- **Line 4 -** We ran ls providing it with a relative path. Documents is a directory in our current location. This command could produce different results depending on where we are. If we had another user on the system, bob, and we ran the command when in their home directory then we would list the contents of their Documents directory instead.

- **Line 7 -** We ran ls providing it with an absolute path. This command will provide the same output regardless of our current location when we run it.

## **More on Paths**

You'll find that a lot of stuff in Linux can be achieved in several different ways. Paths are no different. Here are some more building blocks you may use to help build your paths.

- **~ (tilde) -** This is a shortcut for your home directory. eg, if your home directory is /home/ryan then you could refer to the directory Documents with the path /home/ryan/Documents or ~/Documents

- **. (dot) -** This is a reference to your current directory. eg in the example above we referred to Documents on line 4 with a relative path. It could also be written as ./Documents (Normally this extra bit is not required but in later sections we will see where it comes in handy).

- **.. (dotdot)-** This is a reference to the parent directory. You can use this several times in a path to keep going up the hierarchy. eg if you were in the path /home/ryan you could run the command ls ../../ and this would do a listing of the root directory.


In order to move around in the system we use a command called cd which stands for change directory. It works as follows:

**cd [location]**

If you run the command cd without any arguments then it will always take you back to your home directory.

## **Tab Completion**

Typing out these paths can become tedious. If you're like me, you're also prone to making typos. The command line has a nice little mechanism to help us in this respect. It's called Tab Completion.

When you start typing a path (anywhere on the command line, you're not just limited to certain commands) you may hit the Tab key on your keyboard at any time which will invoke an auto complete action. If nothing happens then that means there are several possibilities. If you hit Tab again it will show you those possibilities. You may then continue typing and hit Tab again and it will again try to auto complete for you.

It's kinda hard to demonstrate here so it's probably best if you try it yourself. If you start typing cd /h**Tab**/< beginning of your username > **Tab** you'll get a feel for how it works.

# **Summary**


**pwd**

Print Working Directory - ie. Where are we currently.

**ls**

List the contents of a directory.

**cd**

Change Directories - ie. move to another directory.

# **Important Concepts**

**Relative path**

A file or directory location relative to where we currently are in the file system.

**Absolute path**

A file or directory location in relation to the root of the file system.


# *Linux 3*

Linux has a graphical user interface and it works pretty much like the GUI's on other systems that you are familiar with such as Windows and OSX.

A command line, or terminal, is a text based interface to the system. You are able to enter commands by typing them on the keyboard and feedback will be given to you similarly as text.

The command line typically presents you with a prompt. As you type, it will be displayed after the prompt. Most of the time you will be issuing commands. Here is an example:

1.) **user@bash:** ls -l /home/ryan

2.) total 3

3.) drwxr-xr-x  2 ryan users 4096 Mar 23 13:34 bin

4.) drwxr-xr-x 18 ryan users 4096 Feb 17 09:12 Documents

5.) drwxr-xr-x  2 ryan users 4096 May 05 17:25 public_html

6.) **user@bash:**

- **Line 1** presents us with a prompt ( user@bash ). After that we entered a command ( ls ). Typically a command is always the first thing you type. After that we have what are referred to as command line arguments ( -l /home/ryan ). Important to note, these are separated by spaces (there must be a space between the command and the first command line argument also). The first command line argument ( -l ) is also referred to as an option. Options are typically used to modify the behaviour of the command. Options are usually listed before other arguments and typically start with a dash ( - ).

- **Lines 2 - 5** are output from running the command. Most commands produce output and it will be listed straight under the issuing of the command. Other commands just perform their task and don't display any information unless there was an error.

- **Line 6** presents us with a prompt again. After the command has run and the terminal is ready for you to enter another command the prompt will be displayed. If no prompt is displayed then the command may still be running (you will learn later how to deal with this).

- Your terminal probably won't have line numbers on it. I have just included them here to make it easier to refer to different parts of the material.


## **Opening A Terminal**

- If you're on a Mac then you'll find the program Terminal under Applications -> Utilities. An easy way to get to it is the key combination 'command + space' which will bring up Spotlight, then start typing Terminal and it will soon show up.

- If on Linux then you will probably find it in Applications -> System or Applications -> Utilities. Alternatively you may be able to 'right-click' on the desktop and there may be an option 'Open in terminal'.

- If you are on Windows and intend to remotely log into another machine then you will need an SSH client. A rather good one is Putty (free) .

## **Bash**

Within a terminal you have what is known as a shell. This is a part of the operating system that defines how the terminal will behave and looks after running (or executing) commands for you. There are various shells available but the most common one is called bash which stands for Bourne again shell. This tutorial will assume you are using bash as your shell.

If you would like to know which shell you are using you may use a command called echo to display a system variable stating your current shell. echo is a command which is used to display messages.

1.) **user@bash:** echo $SHELL

2.) /bin/bash

3.) **user@bash:** 

As long as it prints something to the screen that ends in bash then all is good.

# **Shortcut**

When you enter commands, they are actually stored in a history. You can traverse this history using the up and down arrow keys. So don't bother re-typing out commands you have previously entered, you can usually just hit the up arrow a few times. You can also edit these commands using the left and right arrow keys to move the cursor where you want.