<p align="center">
  <img src="http://i.imgur.com/GMnses0.png">
</p>

dev-setup
============

Dev machine setup instructions, dotfiles/scripts, and tools. Also includes dotfiles/scripts for python data analysis, AWS, JavaScript web development, and hacker defaults for OSX. https://bit.ly/git-dotfiles

## Motivation

**Setting up a new developer machine** can be an **ad-hoc, manual, and time-consuming** process.  This repo aims to **simplify the process** with easy-to-understand **instructions** and **dotfiles/scripts** that **automate** the following:

* Customize commonly-used **developer apps**
* Customize the **terminal** and **vim**
* Setup **OS defaults** for OSX users
* Install common **Homebrew formulae** for OSX users
* Install common modules used for **Python data analysis**
* Setup the **Amazon Web Services** (AWS) and **Heroku** environments
* Setup common **data stores**
* Setup **Javascript web development**

Sections Summary:
* Section 1 contains the dotfiles/scripts to setup your system.  **TLDR version**.
* Sections 2 through 6 detail more information about what is installed in Section 1.  It also describes some intallation details if you prefer to install only specific components.

This repo builds on the awesome work from [Mathias Bynens](https://github.com/mathiasbynens) and [Nicolas Hery](https://github.com/nicolashery), listed in the [Credits](#credits).

## Section 1: Installation

* [Step 1: Update the Operating System](https://github.com/donnemartin/dev-setup#step-1-update-the-operating-system)
    * [Install Xcode Command Line Tools](https://github.com/donnemartin/dev-setup#install-xcode-command-line-tools)
    * [Optional: Install Apps](https://github.com/donnemartin/dev-setup#optional-install-apps)
* [Step 2: Run the bootstrap.sh Script](https://github.com/donnemartin/dev-setup#step-2-run-the-bootstrapsh-script)
    * [Running with Git](https://github.com/donnemartin/dev-setup#running-with-git)
    * [Running without Git](https://github.com/donnemartin/dev-setup#running-without-git)
    * [Optional: Specify PATH](https://github.com/donnemartin/dev-setup#optional-add-custom-commands)
    * [Optional: Add Custom Commands](https://github.com/donnemartin/dev-setup)
* [Step 3: Run the .osx Script](https://github.com/donnemartin/dev-setup#step-3-run-the-osx-script)
* [Step 4: Run the brew.sh Script](https://github.com/donnemartin/dev-setup#step-4-run-the-brewsh-script)
* [Step 5: Run the pydata.sh Script](https://github.com/donnemartin/dev-setup#step-5-run-the-pydatash-script)
* [Step 6: Run the aws.sh Script](https://github.com/donnemartin/dev-setup#step-6-run-the-aws.sh-script)

## Section 2: General Apps and Tools

* [Google Chrome](#google-chrome)
* [Homebrew](#homebrew)
* [Sublime Text](#sublime-text)
* [Atom](#atom)
* [Terminal Customization](#terminal-customization)
* [Git](#git)
* [Vim](#vim)
* [Python](#python)
* [Pip](#pip)
* [Virtualenv](#virtualenv)
* [Virtualenvwrapper](#virtualenvwrapper)

## Section 3: Python Data Analysis

* [Anaconda](#anaconda)
* [IPython Notebook](#ipython-notebook)
* [NumPy](#numpy)
* [Pandas](#pandas)
* [Matplotlib](#matplotlib)
* [Seaborn](#seaborn)
* [Scikit-learn](#scikit-learn)
* [SciPy](#scipy)
* [Flask](#flask)
* [Bokeh](#bokeh)

## Section 4: AWS and Heroku

* [Spark](#spark)
* [MapReduce](#mapreduce)
* [AWS CLI](#aws-cli)
* [Boto](#boto)
* [S3cmd](#s3cmd)
* [S3DistCp](#s3distcp)
* [S3-parallel-put](#s3-parallel-put)
* [Redshift](#redshift)
* [Kinesis](#kinesis)
* [Lambda](#lambda)
* [AWS Machine Learning](#aws-machine-learning)
* [Heroku](#heroku)

## Section 5: Data Stores

* [MySQL](#mysql)
* [MySQL Workbench](#mysql-workbench)
* [MongoDB](#mongodb)
* [Redis](#redis)
* [Elasticsearch](#Elasticsearch)

## Section 6: JavaScript Web Development

* [Node.js](#nodejs)
* [JSHint](#jshint)
* [Ruby and RVM](#ruby-and-rvm)
* [Less](#less)

## Section 7: Misc

* [Contributions](#contributions)
* [Credits](#credits)
* [License](#license)

## Section 1: Installation

### Step 1: Update the Operating System

First thing you need to do on any OS, is to update the system.  On a Mac run the "App Store" and select the "Updates" icon and update both the OS and installed apps.

#### Install Xcode Command Line Tools

An important dependency before many tools such as Homebrew can work is the **Command Line Tools** for **Xcode**. These include compilers like gcc that will allow you to build from source.  Git is also included.

Now, Xcode weighs something like 2GB, and you don't need it unless you're developing iPhone or Mac apps. Good news is Apple provides a way to install only the Command Line Tools, without Xcode.

If you are running **OS X 10.9 Mavericks or later**, then you can install the Xcode Command Line Tools directly from the command line with:

```bash
xcode-select --install
```

If you're running 10.8 or older, you'll need to go to [http://developer.apple.com/downloads](http://developer.apple.com/downloads), and sign in with your Apple ID (the same one you use for iTunes and app purchases). Unfortunately, you're greeted by a rather annoying questionnaire. All questions are required, so feel free to answer at random.

Once you reach the downloads page, search for "command line tools", and download the latest **Command Line Tools (OS X Mountain Lion) for Xcode**. Open the **.dmg** file once it's done downloading, and double-click on the **.mpkg** installer to launch the installation. When it's done, you can unmount the disk in Finder.

#### Optional: Install Apps

Some of the scripts tweak settings on apps such as [Google Chrome](#google-chrome) and [Sublime Text](#sublime-text).  If you use these apps, it might be useful to install them first.

### Step 2: Run the bootstrap.sh Script

The bootstrap.sh script will sync the dev-tools repo to your local machine.  This will include customizations for Vim, bash, curl, git, tab completion, aliases, a number of utility functions, etc.  Section 2 of this README describes some of the customizations.

Below you'll find two ways to run the bootstrap script, one using Git and the other using curl.

#### Running with Git

Git should have been installed from the section [Install Xcode Command Line Tools](https://github.com/donnemartin/dev-setup#install-xcode-command-line-tools).  You can clone the repository wherever you want. (I like to keep it in `~/dev/dev-setup`, with `~/dev-setup` as a symlink.) The bootstrapper script will pull in the latest version and copy the files to your home folder.

```bash
git clone https://github.com/donnemartin/dev-setup.git && cd dev-setup && source bootstrap.sh
```

To update, `cd` into your local `dev-setup` repository and then:

```bash
source bootstrap.sh
```

Alternatively, to update while avoiding the confirmation prompt:

```bash
set -- -f; source bootstrap.sh
```

#### Running without Git

To install these dotfiles without Git:

```bash
cd; curl -#L https://github.com/donnemartin/dev-setup/tarball/master | tar -xzv --strip-components 1 --exclude={README.md,bootstrap.sh,LICENSE-MIT.txt}
```

To update later on, just run that command again.

#### Optional: Specify PATH

If `~/.path` exists, it will be sourced along with the other files, before any feature testing (such as [detecting which version of `ls` is being used](https://github.com/donnemartin/dev-setup/blob/aff769fd75225d8f2e481185a71d5e05b76002dc/.aliases#L21-26)) takes place.

Here’s an example `~/.path` file that adds `/usr/local/bin` to the `$PATH`:

```bash
export PATH="/usr/local/bin:$PATH"
```

#### Optional: Add Custom Commands

If `~/.extra` exists, it will be sourced along with the other files. You can use this to add a few custom commands without the need to fork this entire repository, or to add commands you don’t want to commit to a public repository.

My `~/.extra` looks something like this:

```bash
# Git credentials
GIT_AUTHOR_NAME="Donne Martin"
GIT_COMMITTER_NAME="$GIT_AUTHOR_NAME"
git config --global user.name "$GIT_AUTHOR_NAME"
GIT_AUTHOR_EMAIL="donne.martin@gmail.com"
GIT_COMMITTER_EMAIL="$GIT_AUTHOR_EMAIL"
git config --global user.email "$GIT_AUTHOR_EMAIL"

# Pip should only run if there is a virtualenv currently activated
export PIP_REQUIRE_VIRTUALENV=true

# Install or upgrade a global package
# Usage: gpip install –upgrade pip setuptools virtualenv
gpip(){
   PIP_REQUIRE_VIRTUALENV="" pip "$@"
}
```

You could also use `~/.extra` to override settings, functions and aliases from my dotfiles repository. It’s probably better to [fork this repository](https://github.com/donnemartin/dev-setup/fork) instead, though.

### Step 3: Run the .osx Script

When setting up a new Mac, you may want to set some sensible OS X defaults.  This script also configures common third-party apps such as Chrome and Sublime Text.  For a full listing of configuration changes, refer to the commented [source file](https://github.com/donnemartin/dev-setup/blob/master/.osx) directly.  Section 2 of this README describes some of the customizations.

I suggest you at least skim through the [.osx source file](https://github.com/donnemartin/dev-setup/blob/master/.osx) and tweak any settings based on your personal preferences.

```bash
./.osx
```

**For your terminal customization to take full effect, quit and re-start the terminal.**

### Step 4: Run the brew.sh Script

First, install [Homebrew](http://brew.sh/), a package manager that simplifies installing and updating applications or libraries.

Run the following command and follow the steps on the screen:

```bash
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

When setting up a new Mac, you may want to install some common Homebrew formulae.  For a full listing of installed formulae, refer to the commented [brew.sh source file](https://github.com/donnemartin/dev-setup/blob/master/brew.sh) directly.

```bash
./brew.sh
```

This will include the latest version of Python 2 and Python 3.

Restart your terminal.  If you run into the following error, it is because brew installed an updated bash version, but it doesn't switch it to be your default:

```bash
-bash: declare: -A: invalid option
declare: usage: declare [-afFirtx] [-p] [name[=value] ...]
-bash: complete: -D: invalid option
complete: usage: complete [-abcdefgjksuv] [-pr] [-o option] [-A action] [-G globpat] [-W wordlist] [-P prefix] [-S suffix] [-X filterpat] [-F function] [-C command] [name ...]
```

Add the newly installed shell to the list of allowed shells:

```bash
sudo bash -c 'echo /usr/local/bin/bash >> /etc/shells'
```

Change to the new shell:

```bash
chsh -s /usr/local/bin/bash
```

**For your terminal customization to take full effect, quit and re-start the terminal.**

### Step 5: Run the pydata.sh Script

If you'd like to set up a development environment to work with Python and data analysis, run the following script:

```bash
./pydata.sh
```

[Section 3: Python Data Analysis](#section-3-python-data-analysis) describes the installed packages and usage.

### Step 6: Run the aws.sh Script

If you'd like to set up a development environment to work Amazon Web Services, run the following script:

```bash
./aws.sh
```

[Section 4: AWS and Heroku](#section-4-aws-and-heroku) describes the installed packages and usage.

## Section 2: General Apps and Tools

### Google Chrome

Install your favorite browser, mine happens to be Chrome.

#### Installation

Download from [www.google.com/chrome](https://www.google.com/intl/en/chrome/browser/). Open the **.dmg** file once it's done downloading (this will mount the disk image), and drag and drop the **Google Chrome** app into the Applications folder (on the Mac, most applications are installed this way). When done, you can unmount the disk in Finder (the small "eject" icon next to the disk under **Devices**).

#### Configuration

The section [Step 3: Run the .osx Script](https://github.com/donnemartin/dev-setup#step-3-run-the-osx-script) contains Chrome configurations.

### Homebrew

Package managers make it so much easier to install and update applications (for Operating Systems) or libraries (for programming languages). The most popular one for OS X is [Homebrew](http://brew.sh/).

#### Installation

The section [Step 4: Run the brew.sh Script](https://github.com/donnemartin/dev-setup#step-4-run-the-brewsh-script) installs Homebrew and a number of useful Homebrew formulae.

#### Usage

To install a package (or **Formula** in Homebrew vocabulary) simply type:

    $ brew install <formula>

To update Homebrew's directory of formulae, run:

    $ brew update

**Note**: I've seen that command fail sometimes because of a bug. If that ever happens, run the following (when you have Git installed):

    $ cd /usr/local
    $ git fetch origin
    $ git reset --hard origin/master

To see if any of your packages need to be updated:

    $ brew outdated

To update a package:

    $ brew upgrade <formula>

Homebrew keeps older versions of packages installed, in case you want to roll back. That rarely is necessary, so you can do some cleanup to get rid of those old versions:

    $ brew cleanup

To see what you have installed (with their version numbers):

    $ brew list --versions

### Sublime Text

With the terminal, the text editor is a developer's most important tool. Everyone has their preferences, but unless you're a hardcore [Vim](http://en.wikipedia.org/wiki/Vim_(text_editor)) user, a lot of people are going to tell you that [Sublime Text](http://www.sublimetext.com/) is currently the best one out there.

#### Installation

Go ahead and [download](http://www.sublimetext.com/) it. Open the **.dmg** file, drag-and-drop in the **Applications** folder, you know the drill now. Launch the application.

**Note**: At this point I'm going to create a shortcut on the OS X Dock for both for Sublime Text. To do so, right-click on the running application and select **Options > Keep in Dock**.

Sublime Text is not free, but I think it has an unlimited "evaluation period". Anyhow, we're going to be using it so much that even the seemingly expensive $70 price tag is worth every penny. If you can afford it, I suggest you [support](http://www.sublimetext.com/buy) this awesome tool.

#### Configuration

The section [Step 3: Run the .osx Script](https://github.com/donnemartin/dev-setup#step-3-run-the-osx-script) contains Sublime Text configurations.

#### Soda Theme

The [Soda Theme](https://github.com/buymeasoda/soda-theme) is a great UI theme for Sublime Text, especially if you use a dark theme and think the side bar sticks out like a sore thumb.

##### Installation with Sublime Package Control

If you are using Will Bond's excellent [Sublime Package Control](http://wbond.net/sublime_packages/package_control), you can easily install Soda Theme via the `Package Control: Install Package` menu item. The Soda Theme package is listed as `Theme - Soda` in the packages list.

##### Installation with Git

Alternatively, if you are a git user, you can install the theme and keep up to date by cloning the repo directly into your `Packages` directory in the Sublime Text application settings area.

You can locate your Sublime Text `Packages` directory by using the menu item `Preferences -> Browse Packages...`.

While inside the `Packages` directory, clone the theme repository using the command below:

```bash
git clone https://github.com/buymeasoda/soda-theme/ "Theme - Soda"
```

##### Activating the Theme on Sublime Text 2

* Open your User Settings Preferences file `Sublime Text 2 -> Preferences -> Settings - User`
* Add (or update) your theme entry to be `"theme": "Soda Light.sublime-theme"` or `"theme": "Soda Dark.sublime-theme"`

**Example Sublime Text 2 User Settings**

    {
        "theme": "Soda Light.sublime-theme"
    }

##### Activating the Theme on Sublime Text 3

* Open your User Settings Preferences file `Sublime Text -> Preferences -> Settings - User`
* Add (or update) your theme entry to be `"theme": "Soda Light 3.sublime-theme"` or `"theme": "Soda Dark 3.sublime-theme"`

**Example Sublime Text 3 User Settings**

    {
        "theme": "Soda Light 3.sublime-theme"
    }

### Atom

[Atom](https://github.com/atom/atom) is a great open-source editor from GitHub that is rapidly gaining contributors and popularity.  Unfortunately I have found that it does not perform as well when working with very large files that you typically encounter while working with data.  As Atom matures, I'm hopeful its performance will improve.

### Terminal Customization

Since we spend so much time in the terminal, we should try to make it a more pleasant and colorful place.

#### Configuration

The sections [Step 2: Run the bootstrap.sh Script](https://github.com/donnemartin/dev-setup#step-2-run-the-bootstrapsh-script) and [Step 3: Run the .osx Script](https://github.com/donnemartin/dev-setup#step-3-run-the-osx-script) contain terminal customizations.

### Git

#### Installation

Git should have been installed when you ran through the [Install Xcode Command Line Tools](https://github.com/donnemartin/dev-setup#install-xcode-command-line-tools) section.

#### Configuration

What's a developer without [Git](http://git-scm.com/)?

    $ git --version

And `$ which git` should output `/usr/local/bin/git`.

Let's set up some basic configuration. Download the [.gitconfig](https://raw.githubusercontent.com/donnemartin/dev-setup/master/.gitconfig) file to your home directory:

    $ cd ~
    $ curl -O https://raw.githubusercontent.com/donnemartin/dev-setup/master/.gitconfig

It will add some color to the `status`, `branch`, and `diff` Git commands, as well as a couple aliases. Feel free to take a look at the contents of the file, and add to it to your liking.

Next, we'll define your Git user (should be the same name and email you use for [GitHub](https://github.com/) and [Heroku](http://www.heroku.com/)):

    $ git config --global user.name "Your Name Here"
    $ git config --global user.email "your_email@youremail.com"

They will get added to your `.gitconfig` file.

To push code to your GitHub repositories, we're going to use the recommended HTTPS method (versus SSH). So you don't have to type your username and password everytime, let's enable Git password caching as described [here](https://help.github.com/articles/set-up-git):

    $ git config --global credential.helper osxkeychain

**Note**: On a Mac, it is important to remember to add `.DS_Store` (a hidden OS X system file that's put in folders) to your `.gitignore` files. You can take a look at this repository's [.gitignore](https://github.com/donnemartin/dev-setup/blob/master/.gitignore) file for inspiration.

### Vim

Although Sublime Text will be our main editor, it is a good idea to learn some very basic usage of [Vim](http://www.vim.org/). It is a very popular text editor inside the terminal, and is usually pre-installed on any Unix system.

For example, when you run a Git commit, it will open Vim to allow you to type the commit message.

I suggest you read a tutorial on Vim. Grasping the concept of the two "modes" of the editor, **Insert** (by pressing `i`) and **Normal** (by pressing `Esc` to exit Insert mode), will be the part that feels most unnatural. After that it's just remembering a few important keys.

#### Configuration

The sections [Step 2: Run the bootstrap.sh Script](https://github.com/donnemartin/dev-setup#step-2-run-the-bootstrapsh-script) contains Vim customizations.

### Python

OS X, like Linux, ships with [Python](http://python.org/) already installed. But you don't want to mess with the system Python (some system tools rely on it, etc.), so we'll install our own version with Homebrew. It will also allow us to get the very latest version of Python 2.7 and Python 3.

#### Installation

The section [Step 4: Run the brew.sh Script](https://github.com/donnemartin/dev-setup#step-4-run-the-brewsh-script) installs the latest versions of Python 2 and Python 3.

### Pip

[Pip](https://pypi.python.org/pypi/pip) is the Python package manager.

#### Installation

The section [Step 5: Run the pydata.sh Script](https://github.com/donnemartin/dev-setup#step-5-run-the-pydata-script) installs pip.

#### Usage

Here are a couple Pip commands to get you started. To install a Python package:

    $ pip install <package>

To upgrade a package:

    $ pip install --upgrade <package>

To see what's installed:

    $ pip freeze

To uninstall a package:

    $ pip uninstall <package>

### Virtualenv

[Virtualenv](http://www.virtualenv.org/) is a tool that creates an isolated Python environment for each of your projects. For a particular project, instead of installing required packages globally, it is best to install them in an isolated folder in the project (say a folder named `venv`), that will be managed by virtualenv.

The advantage is that different projects might require different versions of packages, and it would be hard to manage that if you install packages globally. It also allows you to keep your global `/usr/local/lib/python2.7/site-packages` folder clean.

#### Installation

The section [Step 5: Run the pydata.sh Script](https://github.com/donnemartin/dev-setup#step-5-run-the-pydata-script) installs Virtualenv.

#### Usage

Let's say you have a project in a directory called `myproject`. To set up virtualenv for that project:

    $ cd myproject/
    $ virtualenv venv --distribute

If you want your virtualenv to also inherit globally installed packages (like IPython or Numpy mentioned above), use:

    $ virtualenv venv --distribute --system-site-packages

These commands create a `venv` subdirectory in your project where everything is installed. You need to **activate** it first though (in every terminal where you are working on your project):

    $ source venv/bin/activate

You should see a `(venv)` appear at the beginning of your terminal prompt indicating that you are working inside the virtualenv. Now when you install something:

    $ pip install <package>

It will get installed in the `venv` folder, and not conflict with other projects.

**Important**: Remember to add `venv` to your project's `.gitignore` file so you don't include all of that in your source code!

### Virtualenvwrapper

[Virtualenvwrapper](https://virtualenvwrapper.readthedocs.org/en/latest/) is a set of extensions that includes wrappers for creating and deleting virtual environments and otherwise managing your development workflow, making it easier to work on more than one project at a time without introducing conflicts in their dependencies.

Main features include:

* Organizes all of your virtual environments in one place.
* Wrappers for managing your virtual environments (create, delete, copy).
* Use a single command to switch between environments.
* Tab completion for commands that take a virtual environment as argument.

#### Installation

The section [Step 5: Run the pydata.sh Script](https://github.com/donnemartin/dev-setup#step-5-run-the-pydata-script) installs Virtualenvwrapper.

#### Usage

Create a new virtual environment. When you create a new environment it automatically becomes the active environment:

    $ mkvirtualenv [env name]

Remove an existing virtual environment. The environment must be deactivated (see below) before it can be removed:

    $ rmvirtualenv [env name]

Activate a virtual environment. Will also list all existing virtual environments if no argument is passed:

    $ workon [env name]

Deactivate the currently active virtual environment. Note that workonwill automatically deactivate the current environment before activating a new one:

    $ deactivate

## Section 3: Python Data Analysis

### Anaconda

Anaconda is a free distribution of the Python programming language for large-scale data processing, predictive analytics, and scientific computing that aims to simplify package management and deployment.

#### Installation

The section [Step 5: Run the pydata.sh Script](https://github.com/donnemartin/dev-setup#step-5-run-the-pydata-script) installs packages you need to run Python data applications.  Alternatively, you can install the more heavy-weight Anaconda instead.

Follow instructions to install [Anaconda](http://docs.continuum.io/anaconda/install.html) or the more lightweight [miniconda](http://conda.pydata.org/miniconda.html).

### IPython Notebook

[IPython](http://ipython.org/) is an awesome project which provides a much better Python shell than the one you get from running `$ python` in the command-line. It has many cool functions (running Unix commands from the Python shell, easy copy & paste, creating Matplotlib charts in-line, etc.) and I'll let you refer to the [documentation](http://ipython.org/ipython-doc/stable/index.html) to discover them.

IPython Notebook is a web-based interactive computational environment where you can combine code execution, text, mathematics, plots and rich media into a single document.

#### Installation

The section [Step 5: Run the pydata.sh Script](https://github.com/donnemartin/dev-setup#step-5-run-the-pydata-script) installs IPython Notebook.  If you prefer to install it separately, run:

    $ pip install "ipython[notebook]"

If you run into an issue about pyzmq, refer to the following [Stack Overflow post](http://stackoverflow.com/questions/24995438/pyzmq-missing-when-running-ipython-notebook) and run:

    $ pip uninstall ipython
    $ pip install "ipython[all]"

#### Usage

    $ ipython notebook

For an examples of IPython Notebooks used in Data Science, see the repo [data-science-ipython-notebooks](https://github.com/donnemartin/data-science-ipython-notebooks).

### NumPy

NumPy adds Python support for large, multi-dimensional arrays and matrices, along with a large library of high-level mathematical functions to operate on these arrays.

#### Installation

The section [Step 5: Run the pydata.sh Script](https://github.com/donnemartin/dev-setup#step-5-run-the-pydata-script) installs NumPy.  If you prefer to install it separately, run:

    $ pip install numpy

#### Usage

Refer to the following [Numpy IPython Notebook](https://github.com/donnemartin/data-science-ipython-notebooks#numpy).

### Pandas

Pandas is a software library written for data manipulation and analysis in Python. Offers data structures and operations for manipulating numerical tables and time series.

#### Installation

The section [Step 5: Run the pydata.sh Script](https://github.com/donnemartin/dev-setup#step-5-run-the-pydata-script) installs Pandas.  If you prefer to install it separately, run:

    $ pip install pandas

#### Usage

Refer to the following [pandas IPython Notebooks](https://github.com/donnemartin/data-science-ipython-notebooks#pandas).

### Matplotlib

Matplotlib is a Python 2D plotting library which produces publication quality figures in a variety of hardcopy formats and interactive environments across platforms.

#### Installation

The section [Step 5: Run the pydata.sh Scripts](https://github.com/donnemartin/dev-setup#step-5-run-the-pydata-script) installs matplotlib.  If you prefer to install it separately, run:

    $ pip install matplotlib

#### Usage

Refer to the following [matplotlib IPython Notebooks](https://github.com/donnemartin/data-science-ipython-notebooks#matplotlib).

### Seaborn

Seaborn is a Python visualization library based on matplotlib. It provides a high-level interface for drawing attractive statistical graphics.

#### Installation

The section [Step 5: Run the pydata.sh Scripts](https://github.com/donnemartin/dev-setup#step-5-run-the-pydata-script) installs matplotlib.  If you prefer to install it separately, run:

    $ pip install seaborn

#### Usage

Refer to the following [matplotlib with Seaborn IPython Notebooks](https://github.com/donnemartin/data-science-ipython-notebooks#matplotlib).

### Scikit-learn

Scikit-learn adds Python support for large, multi-dimensional arrays and matrices, along with a large library of high-level mathematical functions to operate on these arrays.

#### Installation

The section [Step 5: Run the pydata.sh Script](https://github.com/donnemartin/dev-setup#step-5-run-the-pydata-script) installs Scikit-learn.  If you prefer to install it separately, run:

    $ pip install scikit-learn

#### Usage

Refer to the following [scikit-learn IPython Notebooks](https://github.com/donnemartin/data-science-ipython-notebooks#scikit-learn).

### SciPy

SciPy is a collection of mathematical algorithms and convenience functions built on the Numpy extension of Python. It adds significant power to the interactive Python session by providing the user with high-level commands and classes for manipulating and visualizing data.

#### Installation

The section [Step 5: Run the pydata.sh Script](https://github.com/donnemartin/dev-setup#step-5-run-the-pydata-script) installs SciPy.  If you prefer to install it separately, run:

    $ pip install scipy

#### Usage

Refer to the following [SciPy IPython Notebooks](https://github.com/donnemartin/data-science-ipython-notebooks#statistical-inference-scipy).

### Flask

Flask is a micro web application framework written in Python.

#### Installation

The section [Step 5: Run the pydata.sh Script](https://github.com/donnemartin/dev-setup#step-5-run-the-pydata-script) installs SciPy.  If you prefer to install it separately, run:

    $ pip install Flask

#### Usage

Refer to the following [Flask IPython Notebooks](https://github.com/donnemartin/data-science-ipython-notebooks#).

### Bokeh

Bokeh is a Python interactive visualization library that targets modern web browsers for presentation. Its goal is to provide elegant, concise construction of novel graphics in the style of D3.js, but also deliver this capability with high-performance interactivity over very large or streaming datasets. Bokeh can help anyone who would like to quickly and easily create interactive plots, dashboards, and data applications.

#### Installation

The section [Step 5: Run the pydata.sh Script](https://github.com/donnemartin/dev-setup#step-5-run-the-pydata-script) installs Bokeh.  If you prefer to install it separately, run:

    $ pip install bokeh

#### Usage

Refer to the following [Bokeh IPython Notebooks](https://github.com/donnemartin/data-science-ipython-notebooks#).

## Section 4: AWS and Heroku

### Spark

Spark is an in-memory cluster computing framework, up to 100 times faster for certain applications and is well suited for machine learning algorithms.

#### Installation

The section [Step 6: Run the aws.sh Script](https://github.com/donnemartin/dev-setup#step-5-run-the-pydata-script) installs Spark.  If you prefer to install it separately, run:

    $ brew install apache-spark

#### Usage

Refer to the following [Spark IPython Notebook](https://github.com/donnemartin/data-science-ipython-notebooks#spark).

### MapReduce

Mrjob supports MapReduce jobs in Python, running them locally or on Hadoop clusters such as AWS Elastic MapReduce (EMR).

#### Installation

**Mrjob is Python 2 only.**

The section [Step 6: Run the aws.sh Script](https://github.com/donnemartin/dev-setup#step-5-run-the-pydata-script) installs mrjob.  If you prefer to install it separately, run:

    $ pip install mrjob

The aws.sh script also syncs the template ```.mrjob.conf``` file to your home folder.  Note running the aws.sh script will overwrite any existing ```~/.mrjob.conf``` file.  Update the config file with your credentials, keypair, region, and S3 bucket paths:

```
runners:
  emr:
    aws_access_key_id: YOURACCESSKEY
    aws_secret_access_key: YOURSECRETKEY
    aws_region: us-east-1
    ec2_key_pair: YOURKEYPAIR
    ec2_key_pair_file: ~/.ssh/YOURKEYPAIR.pem
    ...
    s3_scratch_uri: s3://YOURBUCKETSCRATCH
    s3_log_uri: s3://YOURBUCKETLOG
    ...
```

#### Usage

Refer to the following [mrjob IPython Notebook](https://github.com/donnemartin/data-science-ipython-notebooks#mapreduce-python).

### AWS CLI

The AWS Command Line Interface is a unified tool to manage AWS services, allowing you to control multiple AWS services from the command line and to automate them through scripts.

#### Installation

The section [Step 6: Run the aws.sh Script](https://github.com/donnemartin/dev-setup#step-5-run-the-pydata-script) installs the AWS CLI.  If you prefer to install it separately, run:

    $ pip install awscli

Run the following command to configure the AWS CLI:

    $ aws --configure

Alternatively, the aws.sh script also syncs the template ```.aws/``` folder to your home folder.  Note running the aws.sh script will overwrite any existing ```~/.aws/``` folder.  Update the config file with your credentials and location:

```
[default]
region = us-east-1
```

```
[default]
aws_access_key_id = YOURACCESSKEY
aws_secret_access_key = YOURSECRETKEY
```

**Be careful you do not accidentally check in your credentials.**  The .gitignore file is set to ignore files with credentials.

#### Usage

Refer to the following [AWS CLI IPython Notebook](https://github.com/donnemartin/data-science-ipython-notebooks#aws).

### Boto

Boto is the official AWS SDK for Python.

#### Installation

The section [Step 6: Run the aws.sh Script](https://github.com/donnemartin/dev-setup#step-5-run-the-pydata-script) installs boto.  If you prefer to install it separately, run:

    $ pip install boto

The aws.sh script also syncs the template ```.boto``` file to your home folder.  Note running the aws.sh script will overwrite any existing ```~/.boto``` file.  Update the config file with your credentials:

```
[Credentials]
aws_access_key_id = YOURACCESSKEY
aws_secret_access_key = YOURSECRETKEY
```

**Be careful you do not accidentally check in your credentials.**  The .gitignore file is set to ignore files with credentials.

#### Usage

Refer to the following [Boto IPython Notebook](https://github.com/donnemartin/data-science-ipython-notebooks#aws).

### S3cmd

S3cmd interacts with S3 through the command line.

#### Installation

**S3cmd is Python 2 only.**

The section [Step 6: Run the aws.sh Script](https://github.com/donnemartin/dev-setup#step-5-run-the-pydata-script) installs s3cmd.  If you prefer to install it separately, run:

    $ pip install s3cmd

Running the following command will prompt you to enter your AWS access and AWS secret keys. To follow security best practices, make sure you are using an IAM account as opposed to using the root account.

I also suggest enabling GPG encryption which will encrypt your data at rest, and enabling HTTPS to encrypt your data in transit. Note this might impact performance.

    $ s3cmd --configure

Alternatively, the aws.sh script also syncs the template ```.s3cfg``` file to your home folder.  Note running the aws.sh script will overwrite any existing ```~/.s3cfg``` file.  Update the config file with your credentials and location:

```
[Credentials]
aws_access_key_id = YOURACCESSKEY
aws_secret_access_key = YOURSECRETKEY
...
bucket_location = US
...
gpg_passphrase = YOURPASSPHRASE
```

**Be careful you do not accidentally check in your credentials.**  The .gitignore file is set to ignore files with credentials.

#### Usage

Refer to the following [s3cmd IPython Notebook](https://github.com/donnemartin/data-science-ipython-notebooks#aws).

### S3DistCp

S3DistCp combines smaller files and aggregates them together by taking in a pattern and target file. S3DistCp can also be used to transfer large volumes of data from S3 to your Hadoop cluster.

#### Installation

S3DistCp comes bundled with the AWS CLI.

#### Usage

Refer to the following [S3DistCp IPython Notebook](https://github.com/donnemartin/data-science-ipython-notebooks#aws).

### S3-parallel-put

S3-parallel-put uploads multiple files to S3 in parallel.

#### Installation

    $ git clone https://github.com/twpayne/s3-parallel-put.git

#### Usage

Refer to the following [s3-parallel-put IPython Notebook](https://github.com/donnemartin/data-science-ipython-notebooks#aws).

### Redshift

Redshift is a fast data warehouse built on top of technology from massive parallel processing (MPP).

#### Setup

Follow these [instructions](http://docs.aws.amazon.com/redshift/latest/gsg/rs-gsg-prereq.html).

#### Usage

Refer to the following [Redshift IPython Notebook](https://github.com/donnemartin/data-science-ipython-notebooks#aws).

### Kinesis

Kinesis streams data in real time with the ability to process thousands of data streams per second.

#### Setup

Follow these [instructions](http://docs.aws.amazon.com/kinesis/latest/dev/before-you-begin.html).

#### Usage

Refer to the following [Kinesis IPython Notebook](https://github.com/donnemartin/data-science-ipython-notebooks#aws).

### Lambda

Lambda runs code in response to events, automatically managing compute resources.

#### Setup

Follow these [instructions](http://docs.aws.amazon.com/lambda/latest/dg/setting-up.html).

#### Usage

Refer to the following [Lambda IPython Notebook](https://github.com/donnemartin/data-science-ipython-notebooks#aws).

### AWS Machine Learning

Amazon Machine Learning is a service that makes it easy for developers of all skill levels to use machine learning technology. Amazon Machine Learning provides visualization tools and wizards that guide you through the process of creating machine learning (ML) models without having to learn complex ML algorithms and technology. Once your models are ready, Amazon Machine Learning makes it easy to obtain predictions for your application using simple APIs, without having to implement custom prediction generation code, or manage any infrastructure.

#### Setup

Follow these [instructions](http://docs.aws.amazon.com/machine-learning/latest/dg/setting_up.html).

#### Usage

Refer to the following [AWS Machine Learning IPython Notebook](https://github.com/donnemartin/data-science-ipython-notebooks#aws).

### Heroku

[Heroku](http://www.heroku.com/), if you're not already familiar with it, is a [Platform-as-a-Service](http://en.wikipedia.org/wiki/Platform_as_a_service) (PaaS) that makes it really easy to deploy your apps online. There are other similar solutions out there, but Heroku was among the first and is currently the most popular. Not only does it make a developer's life easier, but I find that having Heroku deployment in mind when building an app forces you to follow modern app development [best practices](http://www.12factor.net/).

#### Installation

Assuming that you have an account (sign up if you don't), let's install the [Heroku Client](https://devcenter.heroku.com/articles/using-the-cli) for the command-line. Heroku offers a Mac OS X installer, the [Heroku Toolbelt](https://toolbelt.heroku.com/), that includes the client. But for these kind of tools, I prefer using Homebrew. It allows us to keep better track of what we have installed. Luckily for us, Homebrew includes a `heroku-toolbelt` formula:

    $ brew install heroku-toolbelt

The formula might not have the latest version of the Heroku Client, which is updated pretty often. Let's update it now:

    $ heroku update

Don't be afraid to run `heroku update` every now and then to always have the most recent version.

#### Usage

Login to your Heroku account using your email and password:

    $ heroku login

If this is a new account, and since you don't already have a public **SSH key** in your `~/.ssh` directory, it will offer to create one for you. Say yes! It will also upload the key to your Heroku account, which will allow you to deploy apps from this computer.

If it didn't offer create the SSH key for you (i.e. your Heroku account already has SSH keys associated with it), you can do so manually by running:

     $ mkdir ~/.ssh
     $ ssh-keygen -t rsa

Keep the default file name and skip the passphrase by just hitting Enter both times. Then, add the key to your Heroku account:

    $ heroku keys:add

Once the key business is done, you're ready to deploy apps! Heroku has a great [Getting Started](https://devcenter.heroku.com/articles/python) guide, so I'll let you refer to that (the one linked here is for Python, but there is one for every popular language). Heroku uses Git to push code for deployment, so make sure your app is under Git version control. A quick cheat sheet (if you've used Heroku before):

    $ cd myapp/
    $ heroku create myapp
    $ git push heroku master
    $ heroku ps
    $ heroku logs -t

The [Heroku Dev Center](https://devcenter.heroku.com/) is full of great resources, so be sure to check it out!

## Section 5: Data Stores

### MySQL

#### Installation

The section [Step 4: Run the brew.sh Script](https://github.com/donnemartin/dev-setup#step-4-run-the-brewsh-script) installs MySQL.  If you prefer to install it separately, run:

    $ brew update # Always good to do
    $ brew install mysql

As you can see in the ouput from Homebrew, before we can use MySQL we first need to set it up with:

    $ unset TMPDIR
    $ mkdir /usr/local/var
    $ mysql_install_db --verbose --user=`whoami` --basedir="$(brew --prefix mysql)" --datadir=/usr/local/var/mysql --tmpdir=/tmp

#### Usage

To start the MySQL server, use the `mysql.server` tool:

    $ mysql.server start

To stop it when you are done, run:

    $ mysql.server stop

You can see the different commands available for `mysql.server` with:

    $ mysql.server --help

To connect with the command-line client, run:

    $ mysql -uroot

(Use `exit` to quit the MySQL shell.)

**Note**: By default, the MySQL user `root` has no password. It doesn't really matter for a local development database. If you wish to change it though, you can use `$ mysqladmin -u root password 'new-password'`.

#### MySQL Workbench

In terms of a GUI client for MySQL, I'm used to the official and free [MySQL Workbench](http://www.mysql.com/products/workbench/). But feel free to use whichever you prefer.

Installation

You can find the MySQL Workbench download [here](http://www.mysql.com/downloads/workbench/). (**Note**: It will ask you to sign in, you don't need to, just click on "No thanks, just start my download!" at the bottom.)

### MongoDB

[MongoDB](http://www.mongodb.org/) is a popular [NoSQL](http://en.wikipedia.org/wiki/NoSQL) database.

#### Installation

The section Step 4: Run the brew.sh Script installs MongoDB. If you prefer to install it separately, run:

    $ brew update
    $ brew install mongo

#### Usage

In a terminal, start the MongoDB server:

    $ mongod

In another terminal, connect to the database with the Mongo shell using:

    $ mongo

I'll let you refer to MongoDB's [Getting Started](http://docs.mongodb.org/manual/tutorial/getting-started/) guide for more!

### Redis

[Redis](http://redis.io/) is a blazing fast, in-memory, key-value store, that uses the disk for persistence. It's kind of like a NoSQL database, but there are a lot of [cool things](http://oldblog.antirez.com/post/take-advantage-of-redis-adding-it-to-your-stack.html) that you can do with it that would be hard or inefficient with other database solutions. For example, it's often used as session management or caching by web apps, but it has many other uses.

#### Installation

The section Step 4: Run the brew.sh Script installs Redis. If you prefer to install it separately, run:

    $ brew update
    $ brew install redis

#### Usage

Start a local Redis server using the default configuration settings with:

    $ redis-server

For advanced usage, you can tweak the configuration file at `/usr/local/etc/redis.conf` (I suggest making a backup first), and use those settings with:

    $ redis-server /usr/local/etc/redis.conf

In another terminal, connect to the server with the Redis command-line interface using:

    $ redis-cli

I'll let you refer to Redis' [documentation](http://redis.io/documentation) or other tutorials for more information.

### Elasticsearch

As it says on the box, [Elasticsearch](http://www.elasticsearch.org/) is a "powerful open source, distributed real-time search and analytics engine". It uses an HTTP REST API, making it really easy to work with from any programming language.

You can use elasticsearch for such cool things as real-time search results, autocomplete, recommendations, machine learning, and more.

#### Installation

Elasticsearch runs on Java, so check if you have it installed by running:

```bash
java -version
```

If Java isn't installed yet, a window will appear prompting you to install it. Go ahead and click "Install".

Next, install elasticsearch with:

```bash
$ brew install elasticsearch
```

**Note**: Elasticsearch also has a `plugin` program that gets moved to your `PATH`. I find that too generic of a name, so I rename it to `elasticsearch-plugin` by running (will need to do that again if you update elasticsearch):

```bash
$ mv /usr/local/bin/plugin /usr/local/bin/elasticsearch-plugin
```

Below I will use `elasticsearch-plugin`, just replace it with `plugin` if you haven't followed this step.

As you guessed, you can add plugins to elasticsearch. A popular one is [elasticsearch-head](http://mobz.github.io/elasticsearch-head/), which gives you a web interface to the REST API. Install it with:

```bash
$ elasticsearch-plugin --install mobz/elasticsearch-head
```

### Usage

Start a local elasticsearch server with:

```bash
$ elasticsearch -f
```

(The `-f` option tells it to run in the foreground, so you can stop it with `Ctrl+C`.)

Test that the server is working correctly by running:

```bash
$ curl -XGET 'http://localhost:9200/'
```

If you installed the elasticsearch-head plugin, you can visit its interface at `http://localhost:9200/_plugin/head/`.

Elasticsearch's [documentation](http://www.elasticsearch.org/guide/) is more of a reference. To get started, I suggest reading some of the blog posts linked on this [StackOverflow answer](http://stackoverflow.com/questions/11593035/beginners-guide-to-elasticsearch/11767610#11767610).

## Section 6: Web Development

### Node.js

Install [Node.js](http://nodejs.org/) with Homebrew:

    $ brew update
    $ brew install node

The formula also installs the [npm](https://npmjs.org/) package manager. However, as suggested by the Homebrew output, we need to add `/usr/local/share/npm/bin` to our path so that npm-installed modules with executables will have them picked up.

To do so, add this line to your `~/.path` file, before the `export PATH` line:

```bash
PATH=/usr/local/share/npm/bin:$PATH
```

Open a new terminal for the `$PATH` changes to take effect.

We also need to tell npm where to find the Xcode Command Line Tools, by running:

    $ sudo xcode-select -switch /usr/bin

(If Xcode Command Line Tools were installed by Xcode, try instead:)

    $ sudo xcode-select -switch /Applications/Xcode.app/Contents/Developer

Node modules are installed locally in the `node_modules` folder of each project by default, but there are at least two that are worth installing globally. Those are [CoffeeScript](http://coffeescript.org/) and [Grunt](http://gruntjs.com/):

    $ npm install -g coffee-script
    $ npm install -g grunt-cli

#### Npm usage

To install a package:

    $ npm install <package> # Install locally
    $ npm install -g <package> # Install globally

To install a package and save it in your project's `package.json` file:

    $ npm install <package> --save

To see what's installed:

    $ npm list # Local
    $ npm list -g # Global

To find outdated packages (locally or globally):

    $ npm outdated [-g]

To upgrade all or a particular package:

    $ npm update [<package>]

To uninstall a package:

    $ npm uninstall <package>

### JSHint

JSHint is a JavaScript developer's best friend.

If the extra credit assignment to install Sublime Package Manager was completed, JSHint can be run as part of Sublime Text.

Install JSHint via npm (global install preferred)

    $ npm install -g jshint

Follow additional instructions on the [JSHint Package Manager page](https://sublime.wbond.net/packages/JSHint) or [build it manually](https://github.com/jshint/jshint).

### Ruby and RVM

Like Python, [Ruby](http://www.ruby-lang.org/) is already installed on Unix systems. But we don't want to mess around with that installation. More importantly, we want to be able to use the latest version of Ruby.

#### Installation

When installing Ruby, best practice is to use [RVM](https://rvm.io/) (Ruby Version Manager) which allows you to manage multiple versions of Ruby on the same machine. Installing RVM, as well as the latest version of Ruby, is very easy. Just run:

    $ curl -L https://get.rvm.io | bash -s stable --ruby

When it is done, both RVM and a fresh version of Ruby 2.0 are installed. The following line was also automatically added to your `.bash_profile`:

```bash
[[ -s "$HOME/.rvm/scripts/rvm" ]] && source "$HOME/.rvm/scripts/rvm" # Load RVM into a shell session *as a function*
```

I prefer to move that line to the `.extra` file, keeping my `.bash_profile` clean. I suggest you do the same.

After that, start a new terminal and run:

    $ type rvm | head -1

You should get the output `rvm is a function`.

#### Usage

The following command will show you which versions of Ruby you have installed:

    $ rvm list

The one that was just installed, Ruby 2.0, should be set as default. When managing multiple versions, you switch between them with:

    $ rvm use system # Switch back to system install (1.8)
    $ rvm use 2.0.0 --default # Switch to 2.0.0 and sets it as default

Run the following to make sure the version you want is being used (in our case, the just-installed Ruby 1.9.3):

    $ which ruby
    $ ruby --version

You can install another version with:

    $ rvm install 1.9.3

To update RVM itself, use:

    $ rvm get stable

[RubyGems](http://rubygems.org/), the Ruby package manager, was also installed:

    $ which gem

Update to its latest version with:

    $ gem update --system

To install a "gem" (Ruby package), run:

    $ gem install <gemname>

To install without generating the documentation for each gem (faster):

    $ gem install <gemname> --no-document

To see what gems you have installed:

    $ gem list

To check if any installed gems are outdated:

    $ gem outdated

To update all gems or a particular gem:

    $ gem update [<gemname>]

RubyGems keeps old versions of gems, so feel free to do come cleaning after updating:

    $ gem cleanup

I mainly use Ruby for the CSS pre-processor [Compass](http://compass-style.org/), which is built on top of [Sass](http://sass-lang.com/):

    $ gem install compass --no-document

### LESS

CSS preprocessors are becoming quite popular, the most popular processors are [LESS](http://lesscss.org/) and [SASS](http://sass-lang.com). Preprocessing is a lot like compiling code for CSS. It allows you to reuse CSS in many different ways. Let's start out with using LESS as a basic preprocessor, it's used by a lot of popular CSS frameworks like [Bootstrap](http://getbootstrap.com/).

#### Install

To install LESS you have to use NPM / Node, which you installed earlier using Homebrew. In the terminal use:

    $ npm install less --global

Note: the `--global` flag is optional but it prevents having to mess around with file paths. You can install without the flag, just know what you're doing.

You can check that it installed properly by using:

    $ lessc --version

This should output some information about the compiler:

    lessc 1.5.1 (LESS Compiler) [JavaScript]

Okay, LESS is installed and running. Great!

#### Usage

There's a lot of different ways to use LESS. Generally I use it to compile my stylesheet locally. You can do that by using this command in the terminal:

    $ lessc template.less template.css

The two options are the "input" and "output" files for the compiler. The command looks in the current directory for the LESS stylesheet, compiles it, and outputs it to the second file in the same directory. You can add in paths to keep your project files organized:

    $ lessc less/template.less css/template.css

Read more about LESS on their page here: http://lesscss.org/

## Section 7: Misc

### Contributions

Bug reports and suggestions are [welcome](https://github.com/donnemartin/dev-setup/issues)!

### Credits

This repo builds on the awesome work from the following repos:

* [dotfiles](https://github.com/mathiasbynens/dotfiles) by Mathias Bynens
* [mac-dev-setup](https://github.com/nicolashery/mac-dev-setup) by Nicolas Hery

### License

This repository contains a variety of content; some developed by Donne Martin, and some from third-parties.  The third-party content is distributed under the license provided by those parties.

The content developed by Donne Martin is distributed under the following license:

    Copyright 2015 Donne Martin

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

       http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.
