---
tags: setup, environment, bash, kids
languages: ruby
---

## Environment Setup for Students Using Mac Computers
Let's go ahead and get your environment setup. Don't worry too much about the how's and why's of all of this. No one sets up a programming environment all the time, so a lot of people are confused about this anyway. Our goal is to get you up and running as fast as possible!

##1. Set Up a Github Account
[Github](http:s//github.com) is a powerful site for version control and storing your code on a server. You all need to create free accounts in order to complete the lab work for this course. Go to Github, and fill out the form to create a username and click signup. You will need to then check your email to verify your new account by clicking a link in an email.

##2. Let's set up our `.bash_profile`.

###Set Up Your Bash Profile

We'll spend a lot more time in terminal today, but it's helpful if your `.bash_profile` looks just like mine. We're going to open terminal and enter the following commands:

`cd ~`

`ls -lah`

This command should bring up a list of all the files on your computer, including secret hidden files that begin with a `.`. We're looking for a file called `.bash_profile`. 
If it's there go ahead and enter `open .bash_profile`. 
It it's not there, enter `touch .bash_profile` followed by `open .bash_profile`.

We're going to use the standard for ours. Copy and paste this code below into your `.bash_profile` and save it. 

```bash
# Configuring Our Prompt
# ======================

  # if you install git via homebrew, or install the bash autocompletion via homebrew, you get __git_ps1 which you can use in the PS1
  # to display the git branch.  it's supposedly a bit faster and cleaner than manually parsing through sed. i dont' know if you care 
  # enough to change it

  # This function is called in your prompt to output your active git branch.
  function parse_git_branch {
    git branch --no-color 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/ (\1)/'
  }

  # This function builds your prompt. It is called below
  function prompt {
    # Define some local colors
    local         RED="\[\033[0;31m\]" # This syntax is some weird bash color thing I never
    local   LIGHT_RED="\[\033[1;31m\]" # really understood
    local        CHAR="♥"
    # ♥ ☆ - Keeping some cool ASCII Characters for reference

    # Here is where we actually export the PS1 Variable which stores the text for your prompt
    export PS1="\[\e]2;\u@\h\a[\[\e[37;44;1m\]\t\[\e[0m\]]$RED\$(parse_git_branch) \[\e[32m\]\W\[\e[0m\]\n\[\e[0;31m\]$CHAR \[\e[0m\]"
      PS2='> '
      PS4='+ '
    }

  # Finally call the function and our prompt is all pretty
  prompt

  # For more prompt coolness, check out Halloween Bash:
  # http://xta.github.io/HalloweenBash/

  # If you break your prompt, just delete the last thing you did.
  # And that's why it's good to keep your dotfiles in git too.

# Environment Variables
# =====================
  # Library Paths
  # These variables tell your shell where they can find certain
  # required libraries so other programs can reliably call the variable name
  # instead of a hardcoded path.

    # NODE_PATH
    # Node Path from Homebrew I believe
    export NODE_PATH="/usr/local/lib/node_modules:$NODE_PATH"

    # Those NODE & Python Paths won't break anything even if you
    # don't have NODE or Python installed. Eventually you will and
    # then you don't have to update your bash_profile

  # Configurations

    # GIT_MERGE_AUTO_EDIT
    # This variable configures git to not require a message when you merge.
    export GIT_MERGE_AUTOEDIT='no'

    # Editors
    # Tells your shell that when a program requires various editors, use sublime.
    # The -w flag tells your shell to wait until sublime exits
    export VISUAL="subl -w"
    export SVN_EDITOR="subl -w"
    export GIT_EDITOR="subl -w"
    export EDITOR="subl -w"

  # Paths

    # The USR_PATHS variable will just store all relevant /usr paths for easier usage
    # Each path is seperate via a : and we always use absolute paths.

    # A bit about the /usr directory
    # The /usr directory is a convention from linux that creates a common place to put
    # files and executables that the entire system needs access too. It tries to be user
    # independent, so whichever user is logged in should have permissions to the /usr directory.
    # We call that /usr/local. Within /usr/local, there is a bin directory for actually
    # storing the binaries (programs) that our system would want.
    # Also, Homebrew adopts this convetion so things installed via Homebrew
    # get symlinked into /usr/local
    export USR_PATHS="/usr/local:/usr/local/bin:/usr/local/sbin:/usr/bin"

    # Hint: You can interpolate a variable into a string by using the $VARIABLE notation as below.

    # We build our final PATH by combining the variables defined above
    # along with any previous values in the PATH variable.

    # Our PATH variable is special and very important. Whenever we type a command into our shell,
    # it will try to find that command within a directory that is defined in our PATH.
    # Read http://blog.seldomatt.com/blog/2012/10/08/bash-and-the-one-true-path/ for more on that.
    export PATH="$USR_PATHS:$PATH"

    # If you go into your shell and type: $PATH you will see the output of your current path.
    # For example, mine is:
    # /Users/avi/.rvm/gems/ruby-1.9.3-p392/bin:/Users/avi/.rvm/gems/ruby-1.9.3-p392@global/bin:/Users/avi/.rvm/rubies/ruby-1.9.3-p392/bin:/Users/avi/.rvm/bin:/usr/local:/usr/local/bin:/usr/local/sbin:/usr/bin:/usr/local/mysql/bin:/usr/local/share/python:/bin:/usr/sbin:/sbin:

# Helpful Functions
# =====================

# A function to CD into the desktop from anywhere
# so you just type desktop.
# HINT: It uses the built in USER variable to know your OS X username

# USE: desktop
#      desktop subfolder
function desktop {
  cd /Users/$USER/Desktop/$@
}

# A function to easily grep for a matching process
# USE: psg postgres
function psg {
  FIRST=`echo $1 | sed -e 's/^\(.\).*/\1/'`
  REST=`echo $1 | sed -e 's/^.\(.*\)/\1/'`
  ps aux | grep "[$FIRST]$REST"
}

# A function to extract correctly any archive based on extension
# USE: extract imazip.zip
#      extract imatar.tar
function extract () {
    if [ -f $1 ] ; then
        case $1 in
            *.tar.bz2)  tar xjf $1      ;;
            *.tar.gz)   tar xzf $1      ;;
            *.bz2)      bunzip2 $1      ;;
            *.rar)      rar x $1        ;;
            *.gz)       gunzip $1       ;;
            *.tar)      tar xf $1       ;;
            *.tbz2)     tar xjf $1      ;;
            *.tgz)      tar xzf $1      ;;
            *.zip)      unzip $1        ;;
            *.Z)        uncompress $1   ;;
            *)          echo "'$1' cannot be extracted via extract()" ;;
        esac
    else
        echo "'$1' is not a valid file"
    fi
}

# Aliases
# =====================
  # LS
  alias l='ls -lah'

  # Git
  alias gst="git status"
  alias gl="git pull"
  alias gp="git push"
  alias gd="git diff | mate"
  alias gc="git commit -v"
  alias gca="git commit -v -a"
  alias gb="git branch"
  alias gba="git branch -a"
  alias gcam="git commit -am"
  alias gbb="git branch -b"


# Case-Insensitive Auto Completion
  bind "set completion-ignore-case on" 

# Final Configurations and Plugins
# =====================
  # Git Bash Completion
  # Will activate bash git completion if installed
  # via homebrew
  if [ -f `brew --prefix`/etc/bash_completion ]; then
    . `brew --prefix`/etc/bash_completion
  fi

  # RVM
  # Mandatory loading of RVM into the shell
  # This must be the last line of your bash_profile always
  [[ -s "/Users/$USER/.rvm/scripts/rvm" ]] && source "/Users/$USER/.rvm/scripts/rvm"  # This loads RVM into a shell session.
```

##3. Download Homebrew 
[Homebrew](http://brew.sh/.). is an awesome package manager, and makes downloading lots of software really easy. Download Homebrew by entering 
```
  ruby -e "$(curl -fsSL https://raw.github.com/Homebrew/homebrew/go/install)"
```

Once downloading is complete, you'll want to enter `brew doctor` to make sure you don't have any conflicts.

##4. Let's make sure we have the correct and most updated version of Git.
To see what your current version is, enter `git version`
To update our version, we enter `brew install git`

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

a `.gitconfig` file is a file that automatically logs you in to git through terminal. This will be incredibly helpful later on. 

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





