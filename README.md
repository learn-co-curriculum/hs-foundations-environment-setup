---
tags: setup, environment, bash, kids
languages: ruby
---

## Environment Setup
###This is for students using Mac computers
Let's go ahead and get your environment setup. Don't worry too much about the how's and why's of all of this. No one sets up a programming environment all the time, so a lot of people are confused about this anyway. Our goal is to get you up and running as fast as possible!

##1. Set Up a Github Account
[Github](http:s//github.com) is a powerful site for version control and storing your code on a server. You all need to create free accounts in order to complete the lab work for this course. Go to Github, and fill out the form to create a username and click signup. You will need to then check your email to verify your new account by clicking a link in an email.

##2. Let's set up our `.bash_profile`. 

We'll spend a lot more time in termindal today, but it's helpful if your .bash_profile looks just like the instructor's. We're going to open terminal and enter the following commands:
`cd ~`
`ls -a` - this command should bring up a list of all the files on your computer, including secret hidden files that begin with a `.`. We're looking for a file called `.bash_profile`. 
If it's there go aheah and enter `open .bash_profile`. 
It it's not there, enter `touch .bash_profile` follow by `open .bash_profile`
We're going to use the standard [Flatiron School Bash Profile](https://github.com/flatiron-school/dotfiles/blob/master/bash_profile) for ours. Copy and paste the contents of this page into your `.bash_profile` and save it. If you open a new tab (press command T), you'll see a brand new prompt!

##3. Download Homebrew 
Homebrew(http://brew.sh/.). is an awesome package manager, and makes downloading lots of software really easy. Download Homebrew by entering 
```
ruby -e "$(curl -fsSL https://raw.github.com/Homebrew/homebrew/go/install)"
```
Once downloading is complete, you'll want to enter `brew doctor` to make sure you don't have any conflicts.

##4. Let's make sure we have the correct and most updated version of Git.
To see what your current version is, enter `git version`
To update our version, we enter `brew install git`
Once the download is complete, you'll want to open a new terminal tab, and reenter `git version` to compare and see if we have a new version number.

##5. Installing RVM
RVM stands for Ruby Version Manager. Programming languages, just like software, has newer and older versions. RVM allows you to have multiple versions of ruby installed on your computer that you can easily switch back and forth between. 

```
\curl -L https://get.rvm.io | bash -s stable --ruby=2.1.0
```

This command will install the latest version as ruby, as well as the newest stable version, which here is 2.1.0.

Now, we want to make 2.1.0 our default version. Enter `rvm use 2.1.0 --default`. If you open a new tab and then type `ruby -v`, you should see 2.1.0

If you have issues with Homebrew, You can try reinstalling it with this command:
```
\curl -L https://gist.github.com/mxcl/1173223/raw/a833ba44e7be8428d877e58640720ff43c59dbad/uninstall_homebrew.sh | bash
```

##6. Git Tab Autocompletion
This is a super handy shortcut, we'll explain how this works more in depth, but git can autocomplete words for you. 
```
brew install bash-completion
```

###7. Set Up a .gitconfig File

a .gitconfig file is a file that automatically logs you in to git through terminal. This will be incredibly helpful later on. 

* Make sure you're in the correct place before we create this file: `cd ~`.

* Enter `touch .gitconfig` then `open .gitconfig` 

* Copy and paste the [Flatiron School Gitconfig](https://github.com/flatiron-school/dotfiles/blob/master/hs-gitconfig) into this file

* You're going to need to replace some values with your own information from Github including:

  * the email address that you used to register for github, where you see `<GITHUB EMAIL ADDRESS>`. You'll be replacing the whole thing, you don't want any of the < > angle brackets around the things you replace.

  * Your github username and API token. This is how you find and generate API tokens on github.com:

    * On https://github.com/settings/applications, next to "Personal access tokens" you should see a button for "Generate new token". Click on it. 
    * Under "Token description" enter 'flatiron-school', then click the green "Generate token" button. 
    * Once the screen refreshes you'll see a token (a series of randomly generated letters and numbers). Copy that and paste it into your .gitconfig file, replacing `<API token>`. (It's in a couple of places.) 

* Now scroll all the way to the top of the file and replace the text <YOUR_HOME_DIRECTORY> with the name of your computer user. You can type `pwd` in terminal to see your computer username and figure out what you need to type in.

* Finally, you don't want any of the < > angle brackets around the things you replaced, like your email, username, or tokens, so make sure you replaced everything properly.

##8. Set Up a Gitignore
A .gitignore file basically tells Github to not keep track of certain files.

* Make sure you are in the home directory. You should see this `~` in your command line. 

* Enter `touch .gitignore` then `open .gitignore`

* Copy and paste [Flatiron School's Gitignore](https://github.com/flatiron-school/dotfiles/blob/master/gitignore).


##9. Set Up a Sublime Sym Link
This means that instead of typing `open` to open files, you can type `subl` and it will open that file in Sublime Text. Programmers love shortcuts and this one is super helpful.
```
ln -s "/Applications/Sublime Text 2.app/Contents/SharedSupport/bin/subl" /usr/local/bin
```

##11. RVM and Sublime Together
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

## Congrats! 

Phew! That was a lot of work, but now you are all set to use git and github.





