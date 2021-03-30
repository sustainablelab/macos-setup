My setup for working on MacOS.

## Table of Contents

- [Terminal](README.md#terminal)
- [Git](README.md#git)
- [Brew](README.md#brew)
- [Vim](README.md#vim)
- [Safari](README.md#vim)

# Lastpass

- Install Lastpass
- sign in

Lastpass is a little broken on the mac. Works well enough.

- access the vault search using Shit+Cmd+L
    - this opens a little search bar
    - the first time it works as intended: click on a search
      result and pick what you want (e.g., copy password)
    - after that, the search results still show up, but there is
      nothing to pick (e.g., no copy password option)
    - so I end up having to open the full vault and do the stuff
      there
- there is no Safari extension icon
    - Lastpass sits in the Dock
    - clicking it opens a bright white vault
    - so, when it works, Shift+Cmd+L provides the browser
      extension behavior I’m used to

# Terminal

Shockingly, there is no keyboard shortcut to open a terminal.

## Make it easy to open Terminal

- click **launchpad**:
    - icon is in dock
    - looks like a `3x3` grid of color tiles
- find Terminal
    - open it
    - right-click on terminal icon in Dock
    - select Options - Keep in Dock
    - select Options - Open at Login

## Make the Terminal font bigger

- open a **Terminal** window
- open **Terminal Preferences**:
    - press `Cmd+,`
- click **Profiles**
    - change font size
        - default is 11
        - I like 16
- change colors of things:
    - drag one of the ANSI colors up to the thing
    - default is text and bold text are "Bright White"
    - I like:
        - text "Normal White"
        - bold text "Normal Yellow"

## Terminal shortcuts

- `Ctrl+Cmd+F`
    - toggles fullscreen

# Git

Try to use git:

```shell
% git —version
```

If there's an error about ``xcrun`` you need to install/update
the Xcode tools:

```shell
% xcode-select --install
```

Git should work now.
```shell
% git --version
git version 2.24.3 (Apple Git-128)
```

Configure user name and email. You can skip this if you're just
cloning repositories, but you'll need the config setup if you
create a repository or commit changes to a repository.

```shell
% git config --global user.name "John Doe"
% git config --global user.email johndoe@example.com
% git config --global core.editor vim
% git config --global core.autocrlf input
```

The `core.autocrlf input` turns CRLF into LF. This is in case Git
encounters a Windows file with CRLF instead of LF. This happens
if a Windows user edits repository files but did not set their
`.gitconfig` with `core.autocrlf true`. That settings converts
the Windows user's CRLF to LF.

See crlf details here:

https://git-scm.com/book/en/v2/Customizing-Git-Git-Configuration

# Brew

Brew is the package manager. I use Brew to install Vim.

## Set brew permissions

Run `brew doctor` to see what's up:

```shell
% brew doctor
Please note that these warnings are just used to help the Homebrew maintainers
with debugging if you file an issue. If everything you use Homebrew for is
working fine: please don't worry or file an issue; just ignore this. Thanks!

Warning: The following directories are not writable by your user:
/usr/local/etc/bash_completion.d
/usr/local/share/aclocal
/usr/local/share/doc
/usr/local/share/info
/usr/local/share/man
/usr/local/share/man/man1
/usr/local/var/homebrew/locks

You should change the ownership of these directories to your user.
  sudo chown -R $(whoami) /usr/local/etc/bash_completion.d /usr/local/share/aclocal /usr/local/share/doc /usr/local/share/info /usr/local/share/man /usr/local/share/man/man1 /usr/local/var/homebrew/locks

And make sure that your user has write permission.
  chmod u+w /usr/local/etc/bash_completion.d /usr/local/share/aclocal /usr/local/share/doc /usr/local/share/info /usr/local/share/man /usr/local/share/man/man1 /usr/local/var/homebrew/lock
```

Do what is says. Run brew doctor again.

```shell
% brew doctor
Your system is ready to brew.
```

# Vim

```shell
brew install vim
```

Launching Vim it should basically work but the default
Vim configuration on Mac is ugly: missing line numbers and syntax
highlighting, looks very unfriendly.

My Vim configuration takes only a minute to setup.

All of my Vim configuration is in one GitHub repository. Three
git commands (one command to clone and two commands to clone the
submodules), and Vim works exactly the way I'm used to.

## Use my vimrc

Clone private repo `vim-dotvim` in the home directory and use the
name `.vim` instead of the default repo name `vim-dotvim`

```shell
git clone https://github.com/sustainablelab/vim-dotvim.git ~/.vim
```

If you run Vim now, it will be mostly functional, but will report
errors about missing submodules because my `.vimrc` uses git
submodules for Vim plugins and for some Vimscripts I wrote.

Clone the submodules:

```shell
cd ~/.vim
git submodule init
git submodule update
```

Now Vim should launch without reporting any missing submodule
errors.

Why is the repository named `vim-dotvim`? I could not name the
repository .vim, so this was my workaround -- i.e., I do not have
a repository named `vim-dotvim` on my computer, the repository
clone is in the `.vim` folder, and that folder is created when I
run this `git clone` command.

# Safari

- Add extensions for dark mode, and keyboard shortcuts.
- Enable opening local files in Safari.

## Enable local files

- Safari - Preferences - Advanced
- check box "Show Develop menu in menu bar"
- Now there's a "Develop" menu
- Click "Develop"
- check "Disable Local File Restrictions"

## Put file path in the URL bar

Prefix the path with `file:///`, for example:

```
file:///Users/sustainablelab/macos-setup/README.md
```

Unfortunately, I haven't found a Safari extension for viewing
Markdown.
