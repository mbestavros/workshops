# Linux Command Line for Everyone!

Welcome to Red Hat's Linux Command Line workshop for TechTogether 2020! The main goal of this workshop is to get you acquainted with the Unix-based terminal. Command line tools are used everywhere -- not just in academia, but in the professional software world, too. And don't just take it from us: ask developers from any software company and they'll likely tell you they use the Unix terminal all the time. It may look intimidating, and it can be a bit hard to learn, but it's well worth the time investment. It will pay dividends well into your future.

This workshop is an extension and revision of the [BUILDS command line workshop](https://github.com/BUILDS-/builds-workshops/tree/master/command_line) that I substantially contributed to, along with former president Sean Smith.

Let's get started by opening up your terminal.
- If you're on Windows, this will be "Ubuntu" if you've already set up the Windows Subsystem for Linux. (If you haven't done so, you can check out the guide in the `windows-subsystem-linux` directory [here](./windows-subsystem-linux/README.md).)
	- An additional note: for the purposes of this workshop, you can assume that Linux instructions also apply to WSL, unless noted otherwise.
- If you're on Mac, this will be your "Terminal" app (probably under "Utilities").
- If you're on Linux, this will also be called "Terminal".

There's one quick command you'll need to run to get the materials you'll need for the workshop:

```bash
git clone https://github.com/mbestavros/workshops.git
```

This will put the materials for this repository on your local computer. We'll be using them later.

One final note: you'll be seeing a lot of commands in this workshop, some of them kind of long. You can choose to type them in manually or copy-paste them; if you choose the latter, you'll need to be aware that pasting in terminals uses a different keyboard shortcut than normal Ctrl+V sometimes. On Linux and Windows, you can paste into shells using Ctrl+Shift+V. Apple apparently doesn't change the shortcut, so that's nice.

## What is a terminal?
A terminal, or command line, is a text-based interface for your computer. Instead of a mouse interacting with graphical elements on screen controlling what your computer does, a terminal accepts text-based commands line-by-line. You type in what you want to do (a command), press Enter, and the computer will do it. Most modern Unix-based systems will have a common set of commands available to accomplish most common actions you'd want to do on a computer; in fact, it's entirely possible to run these machines without ever using a GUI.

Because it tends to be a lot easier to develop things when you don't need to design UI along with it, a lot of widely-used developer tools run through the command line exclusively, and understanding how to use one will allow you to use these tools yourself.

For now, we'll start with the basics.

## Navigation and File Editing
Just like your graphical file explorer, you can use the command line to navigate your filesystem. It's probably one of the most common things you'll do with the terminal, so it's a great place to start.

When you open up your terminal anew, you'll be placed in your "home" directory. It's where all your user's files are stored (like your Documents, Downloads, etc). By default, it's a little hard to tell this. Why don't we have a look around?

Type `ls`, then press Enter. You'll see a list of all the files and folders in your home directory, including the `workshops` directory that we cloned as part of setup.

	$ ls
	workshops

Hooray! You've just learned your first command. `ls` is shorthand for "list" (your files), and it does exactly that -- it lists all the files in your current directory. Keep that in your back pocket -- you'll probably want to use it a lot.

### Folder Structure
Linux machines all have file paths that start from root or `/`. But where are we relative to that? Time to learn a new command!

If you type in `pwd`, you'll see the current working directory. (**p**rint **w**orking **d**irectory)

	$ pwd
	/home/username

Like mentioned above, we're currently in our "home" directory. This can vary a bit across systems. On Mac, it's `/Users/[Username]`, where `[Username]` is your username. On Linux, it's usually `/home/[username]`.

Since the home directory is accessed quite frequently, it's shortened to `~`. From now on, we'll refer to folders as directores and we'll call your home directory `/home/username`. 

### Navigation
Now, let's learn a new command: `cd`. This moves between directory (it's shorthand for **c**hange **d**irectory). Let's try it out:

	$ cd ~

That will navigate to your home directory. You can now type:

	$ pwd
	/home/username

to see the directory you're currently in. Nothing has changed from before, since we were in the home directory to begin with.

Now, let's change directories for real. Go into the `workshops` directory using `cd workshops`. Now, if you type `pwd`, you'll see that our directory has changed:

	$ pwd
	/home/username/workshops
	
Cool! Let's navigate one directory deeper, into the `command-line` directory. This is the subdirectory of the repo you're currently reading this on! Let's explore what else we have in this directory using `ls`:

	$ cd command-line
	$ ls
	materials
	windows-subsystem-linux
	README.md

We've been navigating deeper into the directory structure. What if we want to go back up? Turns out the command is pretty simple. Using `cd ..` will take you to the parent directory. (We'll explain more about this in a bit.)

	$ pwd
	/home/username/workshops/command-line
	$ cd ..
	$ pwd
	/home/username/workshops
	
We can also use a relative file path to get where we want. It looked like there was a `projects/` subdirectory under the `command-line` directory -- let's go there directly:

	$ cd command-line/materials
	$ pwd
	/home/username/workshops/command-line/materials
	$ ls
	redhat-techtogether.txt

Hey, look! There's a text file. Hmm... what does it say? How can I view it?

	$ cat redhat-techtogether.txt

We just used a new command, `cat`. It simply prints the contents of a file. 

Let's rename that file. To do this, we can use the `mv` (move) command:

	$ mv redhat-techtogether.txt renamed.txt

You can think about this as though you're moving a file to a new file in the same directory with a new name.

Now, if you `ls`, you'll see the newly-renamed file:

	$ ls
	renamed.txt

Nice! We've learned a lot so let's recap.

#### ls
List the files and directories in a your current working directory.

	$ ls
	renamed.txt

#### pwd
List the current working directory

	$ pwd
	/home/username/workshops/command-line/materials

#### cd
Move into different folders, or move up a directory

	$ cd ..
	$ cd materials

#### cat
Print out the contents of a file.

	$ cat renamed.txt

#### mv
Rename or move a file

	$ mv renamed.txt renamedagain.txt

### Hidden Files

Some files in UNIX-based systems are hidden. Hidden files start with a `.`; you can see them by using `ls -a`. The `-a` is what's called a flag. It's used to denote special options for a command. First, let's make sure we're in the `materials` directory.

	$ pwd
	/home/username/workshops/command-line/materials
	$ ls -a
	.                           .betyoudidntseethisfile.txt
	..                          renamedagain.txt

Wow! We have three secret files. You'll notice there are two secret files that are just `.` and `..` -- those files are actually directories!

The `.` directory is the current directory. If you type:

	$ pwd
	/home/username/workshops/command-line/materials
	$ cd .
	$ pwd
	/home/username/workshops/command-line/materials

You'll notice you didn't go anywhere! This is because you changed directories into the current directory.

The next directory, `..`, is used to denote one directory up. Let's test it out:

	$ cd ..
	$ pwd
	/home/username/workshops/command-line

We've moved one directory up! This is the same command we used before: we were essentially navigating into the universal "up" directory that is a part of all UNIX directories. 

Now let's address the elephant in the room, `.betyoudidntseethisfile.txt`. Let's `cat` it out.

	$ cd materials
	$ cat .betyoudidntseethisfile.txt

Wow! It's so easy to hide files in Unix based systems.

You should now be pretty comfortable with navigating around your filesystem using UNIX commands. Chances are a lot of your interaction with the command line will be using these commands. Now, we'll move on to some more advanced topics, starting with how to edit files with a text editor.

## Editing Files Using a Command Line Text Editor

Okay, how about actually working with files instead of just navigating around and looking at them? This is where we start learning how to use Vim, a command line text editor.

Let's open up `renamedagain.txt`:

	$ vim renamedagain.txt
	
By default, Vim only looks at the file, and will not let you make changes yet. You can move the cursor around using the arrow keys. When you're ready to start editing, press `i` (for Insert) to start changing text. 

When you're done, you'll need to save and exit. This can be done by pressing the escape key, which takes you back to the default view mode. To give a command, we use the colon key, and then type a command. To exit Vim and save the file you're working on, type ``:wq!` (short for "**w**rite and **q**uit". The exclamation mark is to ignore any warnings.)

You can use the `cat` command to see your edited file.

Vim is extremely powerful, and many people swear by it. I find it most useful to make small edits to things when I'm already in the command line; if I'm doing something more substantive, I'll use my code editor (I prefer VS Code).

### SSH and SCP

Now, let's learn about two very useful tools: ``ssh`` and ``scp``. ``ssh`` (short for "secure shell") is basically remote login: it allows a UNIX-based machine to connect to another UNIX-based machine and issue commands remotely. If you're a BU student, this is how you interact with the CSA servers here at BU. In fact, let's try logging in using ``ssh`` right now:

	$ ssh [your_bu_username]@csa2.bu.edu

(If you're not a BU student, you'll just need to substitute the server address for some other machine you can SSH into. We unfortunately don't have one to demonstrate.)
	
This will begin the process of remotely logging you into the CSA2 lab machine. Assuming you've already set an account up, you'll just need to enter your BU credentials and you're all set to go. (Don't worry if your password doesn't show up in the terminal window; that's intended behavior).

You'll be presented with your CSA home directory. This is a UNIX system, so all the commands you've learned up to here still work! Explore around a little bit. When you're ready to go back to your local machine, just type ``exit``. The command history will clear, but you should still be in the same directory you started ``ssh`` from.

Now, let's learn how to move a file from our local machine to ``csa2`` using ``scp`` (short for secure copy). This is especially useful if you have, for example, a homework file that you need to submit using ``gsubmit``.

We have our text file `renamedagain.txt` in our current directory. Let's move it to the home directory on ``csa2`` with this command:

	$ scp renamedagain.txt [your_bu_username]@csa2.bu.edu:~

Just like with SSH, you'll be prompted for your login info. Once entered, it should copy up. Now, if we log in to ``csa2`` using ``ssh``, we should see your file right there!

You can customize the remote directory you send the file to by changing the file path after the colon. Note, however, that the path must exist *before* you send the file up.

### Symlinks

Exit out of CSA if you haven't already, and go back to your home directory. Symlinks (short for "symbolic links") are essentially links to another file or directory on your file system. They act like whatever they point to.

Symlinks are very handy for WSL users. Because of the way the Linux subsystem is implemented, Windows does not have direct access to the Linux filesystem. This means that any files we create in the Linux filesystem can only be used within Linux--however, any Windows files can be accessed by everyone. Thus, it is most useful to simply use Linux to interact with Windows files. Unfortunately, the file path for the Windows filesystem is convoluted, and tedious to use all the time. The solution is simple: create a symlink within your Linux home directory that links to your Windows home directory. Boom, you have direct access to all your Windows files.

To create the symlink we want (on Windows), we use ``ln -s``:

	$ ln -s [source file or directory] [symlink name]

The Windows filesystem is mounted in Linux, so our C drive is stored at `/mnt/c`. Beyond that, it's just the path from within Windows.
So, to create a symlink to my user directory in Windows, I would do this:

	$ ln -s /mnt/c/Users/[windows-username] windows-home
	
This creates a symlink called `windows-home` that links to my Windows user directory. If I navigate inside, I get my Windows home directory! This process can be repeated for any directory you want.

## Customizing your Command Line

Now we get into the really fun stuff: dotfiles. These are configuration files that dictate how your terminal works, and you can customize them deeply. Plus, it'll give us an opportunity to exercise the skills we've been working on!

First, we'll need to navigate back to our home directory. Remember how to do that? Good.

Next, we're going to be editing our dotfile with `vim`. On Linux and Mac, you'll want to edit `.bash_profile`:

	$ vim .bash_profile

On WSL, you'll need to edit `.bashrc`:

	$ vim .bashrc

Scroll down to the bottom of the file using your arrow keys. We're going to be appending a few nice quality-of-life touches to our shells.

Start editing by pressing `i`. You should see `INSERT` on the bottom of your `vim` window.

Create a new line with enter. Then, type in the following line:

```bash
echo "Welcome to the Linux terminal!"
```

This will give you a welcome message when you open up your terminal! It uses the `echo` command (which just "echoes" back whatever you give it as input). Change it to your heart's content!

As for more functional tweaks, my favorites are these two (enter them on new lines):

```bash
function cd() { builtin cd "$@" && ls; }
```

This makes it such that when you change directories with `cd`, it also lists the files in the new directory. I found myself using `ls` so often after using `cd` that I figured I'd combine them. It's probably one of my favorite small shell tweaks.

If you like, you can do the same thing with `clear` (which we haven't covered yet, but it just clears the console of output) on a new line:

```bash
alias clear="clear && ls"
```

When you've added what you want to your dotfile, you'll need to save and exit. As a reminder, in `vim`, you can do this by pressing Escape to exit Insert mode, then typing `:wq!` and hitting Enter.

Now that your dotfile is done, you'll need to refresh your shell to see the changes. Mac and Linux people can do this with `source ~/.bash_profile`. WSL people will need to exit and restart their shell.

Your shell is now customized! You should see your welcome message when you open up your shell, and if you used any of the advanced `ls` commands, they should work when you use `cd` or `clear`.

If there are any other commands you'd like to run on shell start, you can dump them in your dotfiles. You can do some neat stuff with it.
	
## Package Managers: apt

On Windows and Ubuntu Linux (but not on Mac), you should by default have the ``apt`` package manager installed. This can be used to get command-line utilities. We'll get a few fun ones and then demonstrate how they work.

	$ sudo apt install lolcat
	$ sudo apt install python-pip
	$ sudo apt install cowsay

You can get pretty much any command-line utility using apt.

## Install lolcat and fortune (for Mac users)

On Mac, you need the Ruby gem installer to install lolcat. To install gem:

	wget https://rubygems.org/rubygems/rubygems-2.4.8.zip
	unzip rubygems-2.4.8.zip
	cd rubygems-2.4.8
	sudo ruby setup.rb

Then you can install lolcat (Windows/Linux users already did this):

	gem install lolcat

And colorize text super easily:

	echo "I'm full of colors" | lolcat

## Install fortune

You'll need pip, to install pip go here: https://pip.pypa.io/en/stable/installing/

Then you can just do (on Windows too):

	pip install fortune

## Install cowsay

Install the following (already done on Windows):

	install.packages("devtools")
	devtools::install_github("sckott/cowsay")

## Alternatively, use Homebrew for MacOS

Install brew:

	$ /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
	
And install lolcat, cowsay, and fortune with brew:

	$ brew install lolcat
	$ brew install cowsay
	$ brew install fortune

## Putting it all together

Type the following for interesting quotes:

	$ echo fortune | cowsay | lolcat

If you're feeling _really_ wild, put that command as your welcome message in your dotfile. Then, you'll get a fortune every time you open your terminal!

And that's a wrap! Hopefully you found this workshop helpful. Practice and tinker in your spare time! You can do lots of cool stuff with the command line.

If you're a BU student, I've left in an `ssh-keygen` guide below to make logging into CSA even easier. It's from prior versions of the workshop, and I won't be covering it live.

## Login to CSA without a password

To setup login to csa without entering a password. I'm going to give the concise version of :https://www.digitalocean.com/community/tutorials/how-to-set-up-ssh-keys--2

	ssh-keygen -t rsa

You'll be prompted for:

	Enter file in which to save the key (/home/demo/.ssh/id_rsa):

Press enter

	Enter passphrase (empty for no passphrase):

Again press enter for no passphrase. Then copy the key over like so (you'll need to add your username instead of [YOUR_USERNAME]:

	cat ~/.ssh/id_rsa.pub | ssh [YOUR_USERNAME]@csa2.bu.edu "mkdir -p ~/.ssh && cat >>  ~/.ssh/authorized_keys"

Enter your password (for the last time) and you'll see something like this:

	The authenticity of host '12.34.56.78 (12.34.56.78)' can't be established.
	RSA key fingerprint is b1:2d:33:67:ce:35:4d:5f:f3:a8:cd:c0:c4:48:86:12.
	Are you sure you want to continue connecting (yes/no)? yes
	Warning: Permanently added '12.34.56.78' (RSA) to the list of known hosts.
	user@12.34.56.78's password: 
	Now try logging into the machine, with "ssh 'user@12.34.56.78'", and check in:

	  ~/.ssh/authorized_keys

	  to make sure we haven't added extra keys that you weren't expecting.

Enter yes when prompted.

Try and login to your csa account.

	ssh [YOUR_USERNAME]@csa2.bu.edu

You shouldn't be prompted for a username.