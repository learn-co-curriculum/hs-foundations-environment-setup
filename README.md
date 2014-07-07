---
tags: setup, environment, bash, kids
languages: ruby
---

## Environment Setup

Let's go ahead and get your environment setup. Don't worry too much about the how's and why's of all of this. No one sets up a programming environment all the time, so a lot of people are confused about this anyway. Our goal is to get you up and running as fast as possible!

##1. Set Up a Github Account
[Github](http:s//github.com) is a powerful site for version control and storing your code on a server. You all need to create free accounts in order to complete the lab work for this course. Go to Github, and fill out the form to create a username and click signup. You will need to then check your email to verify your new account by clicking a link in an email.

##2. Let's set up our `.bash_profile`. 

We'll spend a lot more time in termindal today, but it's helpful if your .bash_profile looks just like mine. We're going to open terminal and enter the following commands:
`cd ~`
`ls -lah` - this command should bring up a list of all the files on your computer, including secret hidden files that begin with a `.`. We're looking for a file called `.bash_profile`. 
If it's there go aheah and enter `open .bash_profile`. 
It it's not there, enter `touch .bash_profile` follow by `open .bash_profile`
We're going to use the standard [Flatiron School Bash Profile](https://github.com/flatiron-school/dotfiles/blob/master/bash_profile) for ours. Copy and paste the contents of this page into your `.bash_profile` and save it. If you open a new tab (press command T), you'll see a brand new prompt!

##3. If you don't have XCode already downloaded, Go to the App Store and download XCode. It's a free application that we have to download before anything else. Once Xcode is installed, open it, then in the menu bar click on Xcode > preferences, then select Downloads. Download the command line tools. 

If you are using using OS 10.9(Mavericks) or above, you need to download the command line tools from Apples developer website, or if you don't have an Apple developer account, you can download the command line tools [here](http://flatiron-school.s3.amazonaws.com/software/command_line_tools_os_x_mavericks_for_xcode__late_october_2013.dmg).

To test and see if you installed command line tools correctly, type `gcc` into terminal.
If you see output like this you installed it correctly.
 ```
clang: error: no input files
```

##4. Download Homebrew 
Homebrew(http://brew.sh/.). is an awesome package manager, and makes downloading lots of software really easy. Download Homebrew by entering 
```
ruby -e "$(curl -fsSL https://raw.github.com/Homebrew/homebrew/go/install)"
```
Once downloading is complete, you'll want to enter `brew doctor` to make sure you don't have any conflicts.

##5. Let's make sure we have the correct and most updated version of Git.
To see what your current version is, enter `git version`
To update our version, we enter `brew install git`
Once the download is complete, you'll want to open a new terminal tab, and reenter `git version` to compare and see if we have a new version number.

##6. Installing RVM
RVM stands for Ruby Version Manager. Ruby, just like software, has newer and older versions. RVM allows you to have multiple versions of ruby installed on your computer that you can easily switch back and forth between. 

```
\curl -L https://get.rvm.io | bash -s stable --ruby=2.1.0
```

This command will install the latest version as ruby, as well as the newest stable version, which here is 2.1.0.

Now, we want to make 2.1.0 our default version. Enter `rvm use 2.1.0 --default`. If you open a new tab and then type `ruby -v`, you should see 2.1.0

If you get any errors installing RVM that are related to XCode of GCC, it means you'll need to uninstall XCode and start this guide all over from step 2.

If you have issues with Homebrew, You can try reinstalling it with this command:
```
\curl -L https://gist.github.com/mxcl/1173223/raw/a833ba44e7be8428d877e58640720ff43c59dbad/uninstall_homebrew.sh | bash
```

##7. Git Tab Autocompletion
This is a super handy shortcut, we'll explain how this works more in depth, but git can autocomplete words for you. 
```
brew install bash-completion
```

##8. Set Up a .gitconfig File
a `.gitconfig` file is a file that automatically logs you in to git through terminal. This will be incredibly helpful later on. Lets make sure we're in the correct place before we create this file:
`cd ~`. 

To create the file, enter `touch .gitconfig`. Then to open the file `open .gitconfig`. Once the file is open, use the [Flatiron School Gitconfig File](https://github.com/flatiron-school/dotfiles/blob/master/gitconfig).

You're going to need to replace some values with your own information from Github. You will need to enter the email address that you used to register for github email address in three different places. You will also need to enter your github username and your API token. Your API token can be found on github.com. If you click settings in the top right corner (it's an icon with a wrench and a screwdriver), it should bring up a menu on the left side. You will want to click applications in that menu. From there, next to `personal access tokens` you'll want to click `generate new token`. It will bring up a new page with instructions to enter a token description. Go ahead and enter 'flatiron-camp' and then click the green `generate token` button. Once it refreshes the screen and displays your token (a series of randomly generated letters and numbers), you'll want to copy that and paste it into your .gitconfig file. You don't want any of the `< >` angle brackets around your email, username, or tokens.

You will also need to scroll all the way to the top of the file and after `[core]`, you'll want to replace the text `<YOUR_HOME_DIRECTORY>` with the name of your computer user. You can type `pwd` in terminal to figure out what you need to type in!

##9. Set Up a Gitignore
a `.gitignore` file basically tells Github to not keep track of certain files. Please use [Flatiron School's Gitignore](https://github.com/flatiron-school/dotfiles/blob/master/gitignore)


##10. Download Sublime Text 2
Sublime Text 2 is an incredible text editor for writing code. You can download it [here](http://www.sublimetext.com/2). You want to make sure you select the OSX version. You'll want to make sure that Sublime Text 2 is in the Applications directory on your computer.

##11. Set Up a Sublime Sym Link
This means that instead of typing `open` to open files, you can type `subl` and it will open that file in Sublime Text. Programmers love shortcuts and this one is super helpful.
```
ln -s "/Applications/Sublime Text 2.app/Contents/SharedSupport/bin/subl" /usr/local/bin
```

##12. RVM and Sublime Together
To get RVM and Sublime to play nice, we need to do the following:
```
open "$HOME/Library/Application Support/Sublime Text 2/Packages/Ruby/Ruby.sublime-build"
```
Once the file is open, you'll need to paste the below into the file:
```
{
  "env":{
      "PATH":"${HOME}/.rvm/bin:${PATH}"
  },
  "cmd": ["rvm-auto-ruby", "$file"],
  "file_regex": "^(...*?):([0-9]*):?([0-9]*)",
  "selector": "source.ruby"
} 
```

##13 Set Up Github SSH Keys
An SSH key is how github can identify you without you having to enter your username and password every single time you want to push code up to the server. Github has a great online documention [here](https://help.github.com/articles/generating-ssh-keys). 

So the first thing you'll need to do is open terminal and make sure you're at your root directory. It will look like `~`. If you're not there, `cd ~` will move you to the root directory.

Then we want to look and see if we have a .ssh directory. `ls -la` will show you all the hidden files. If you don't even have a `.ssh` directory, you can make it `mkdir .ssh`

Now we need to generate the SSH key, `ssh-keygen -t rsa -C "your_email@example.com"`. You'll need to enter the same email address that you used to set up your github account between the quotation marks.

You'll get prompted to type the password to your computer twice (the letters won't actually show up when you type. Don't worry, it's just for security purposes).

Once the SSH key generation is done, you'll enter `ssh-add ~/.ssh/id_rsa`

Then `pbcopy < ~/.ssh/id_rsa.pub` which just adds your SSH key to your clipboard.

Then you'll need to go to your github account online, and in the top right corner select Account Settings (the symbol with the wrench). In the left toolbar, you'll select SSH Keys. Then you'll select `Add SSH Key`.

You'll enter a name of `Github SSH` and then paste your SSH key into the `key` field. Then you'll click the green `Add Key` button.

After that, you'll want to go back to terminal and verify that you successfull added the SSH key, `ssh -T git@github.com`. You should get back `Hi username! You've successfully authenticated, but GitHub does not provide shell access.`





