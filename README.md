# dotfiles

## Quickly Get Set Up with These Dotfiles

```sh
# I would consider these packages essential or very nice to have. The GTK
# version of Vim is to get +clipboard support, you'd still run terminal Vim.
sudo apt-get update && sudo apt-get install -y \
  git \
  gitk \
  python3-pip \
  python3-venv \
  python3-tk \
  curl \
  exuberant-ctags \
  ack-grep

# https://vimawesome.com/plugin/vim-autoformat
python3 -m pip install pynvim

# Clone down this dotfiles repo to your home directory. Feel free to place
# this anywhere you want, but remember where you've cloned things to.
git clone git@github.com:Malkiz/dotfiles-1.git ~/dotfiles

# Create symlinks to various dotfiles. If you didn't clone it to ~/dotfiles
# then adjust the symlink source (left side) to where you cloned it.
#
# NOTE: The last one is WSL 1 / 2 specific. No need to do this on native Linux.
ln -s ~/dotfiles/.bashrc ~/.bashrc \
  && ln -s ~/dotfiles/.bash_profile ~/.bash_profile \
  && ln -s ~/dotfiles/.gitconfig ~/.gitconfig \
  && ln -s ~/dotfiles/.vimrc-example ~/.vimrc \
  && sudo ln -s ~/dotfiles/etc/wsl.conf /etc/wsl.conf

# Create your own personal ~/.gitconfig.user file. After copying the file,
# you should edit it to have your name and email address so git can use it.
cp ~/dotfiles/.gitconfig.user ~/.gitconfig.user

# Install FZF (fuzzy finder on the terminal and used by a Vim plugin).
sudo add-apt-repository ppa:x4121/ripgrep
sudo apt-get update
sudo apt-get install ripgrep
git clone --depth 1 https://github.com/junegunn/fzf.git ~/.fzf && ~/.fzf/install

# vim-plug
curl -fLo ~/.vim/autoload/plug.vim --create-dirs \
    https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim

# nvm
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.3/install.sh | bash
```

Optionally confirm that a few things work after closing and re-opening your
terminal:

```sh
# Sanity check to see if you can run some of the tools we installed.
node --version

# Check to make sure git is configured with your name, email and custom settings.
git config --list
```

#### Using WSL 1 or WSL 2?

In addition to the Linux side of things, there's a few config files that I have
in various directories of this dotfiles repo. These have long Windows paths.

It would be expected that you copy those over to your system while replacing
"Nick" with your Windows user name if you want to use those things, such as my
Microsoft Terminal `settings.json` file and others. Some of the paths may
also contain unique IDs too, so adjust them as needed on your end.

Some of these configs expect that you have certain programs or tools installed
on Windows. The [tools I use blog
post](https://nickjanetakis.com/blog/the-tools-i-use) has a complete list of
those tools so you can pick the ones you want to install.

Pay very close attention to the `c/Users/Nick/.wslconfig` file because it has
values in there that you will very likely need to change before using it.
[This commit
message](https://github.com/nickjj/dotfiles/commit/d0f1fc2622204b809cf7fcbb1a82d45b451064c4)
goes into the details.

Also, you should reboot to activate your `/etc/wsl.conf` file (symlinked
earlier). That will be necessary if you want to access your mounted drives at
`/c` or `/d` instead of `/mnt/c` or `/mnt/d`.
