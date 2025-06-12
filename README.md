# Dustin's Dotfiles

🏠 Personal dotfiles for \*NIX (macOS and Linux) systems.

Originally forked from [wookayin/dotfiles](https://github.com/wookayin/dotfiles) and customized for my personal workflow.

## Installation

### Manual Installation

```bash
$ git clone --recursive https://github.com/dustin-liddick/dotfiles.git ~/.dotfiles
$ cd ~/.dotfiles && python install.py
```


The installation script will clone the repository into `~/.dotfiles` and create symbolic links (e.g., `~/.vimrc`) for you.
If target files already exist (e.g. `~/.vim`, `~/.vimrc`), you will need to manually resolve the conflict (delete the old one or just ignore). See Troubleshooting below for details.

## What's Included

This dotfiles configuration provides a comprehensive development environment with:

### 🔧 Core Tools
- **Neovim**: Advanced text editor with modern features, LSP support, and extensive plugin ecosystem
- **Zsh**: Enhanced shell with Oh My Zsh, custom themes, and productivity plugins
- **Tmux**: Terminal multiplexer for session management
- **Git**: Version control with advanced aliases and delta diff viewer

### 🎨 Terminal & UI
- **Alacritty/Kitty/WezTerm**: GPU-accelerated terminal emulators
- **Nerd Fonts**: Enhanced font support with icons and symbols
- **24-bit color support**: True color terminal experience
- **Custom color schemes**: Optimized for readability and aesthetics

### 💻 Development Environment
- **LSP Integration**: Language Server Protocol support for multiple languages
- **Tree-sitter**: Advanced syntax highlighting and code understanding
- **DAP (Debug Adapter Protocol)**: Debugging support within Neovim
- **Completion**: Advanced autocompletion with nvim-cmp
- **Snippets**: Custom code snippets for faster development

### 🐍 Python Development
- **ptpython**: Enhanced Python REPL
- **Conda**: Environment management configuration
- **Code style**: PEP8 compliance with pycodestyle and pylint
- **Debugging**: pudb integration for visual debugging

### ⚡ Key Features
- **Fast fuzzy finding**: FZF integration for files, buffers, and text search
- **Git integration**: Fugitive, gitsigns, and custom git aliases
- **Project management**: Session handling and workspace organization
- **Performance optimized**: Lazy loading and efficient plugin management


## Usage

### Dotfiles Management

**To update dotfiles** (pull changes from upstream and run [`install.py`][install.py] again):

```bash
$ dotfiles update
$ dotfiles update --fast          # fast update mode: skip updating {vim,zsh} plugins
```

On Linux, you can [install some common softwares locally][linux-locals.sh] (into `$HOME/.local/bin`) *without sudo*:

```bash
$ dotfiles install neovim         # -> ~/.local/bin/nvim
$ dotfiles install ripgrep        # -> ~/.local/bin/rg
```

### Quick Start Guide

After installation, here are some key things to get you started:

#### Neovim
- Launch with `nvim` or `vim`
- `:checkhealth` - Verify installation
- `:Lazy` - Plugin manager interface
- `<leader>` key is set to space
- `<leader>ff` - Find files with Telescope
- `<leader>fg` - Live grep with Telescope

#### Zsh
- Rich completions and syntax highlighting
- `fzf` integration for history and file search
- Git status in prompt
- Custom aliases in `zsh/zsh.d/alias.zsh`

#### Tmux
- Prefix key: `Ctrl-a`
- `prefix + I` - Install plugins
- Session management and window splitting

### Personal Configuration

After installation, you'll need to set up your personal information:

1. **Git Configuration**: Copy the template and customize it:
   ```bash
   cp ~/.dotfiles/.gitconfig.secret.template ~/.gitconfig.secret
   # Edit ~/.gitconfig.secret with your name, email, and GitHub username
   ```

2. **SSH Keys**: Make sure your SSH keys are set up for GitHub:
   ```bash
   ssh-keygen -t ed25519 -C "your-email@example.com"
   # Add the public key to your GitHub account
   ```

### Customization

The dotfiles are designed to be customizable. Key areas you might want to modify:

- **Zsh aliases**: Edit `zsh/zsh.d/alias.zsh`
- **Neovim config**: Modify files in `nvim/lua/config/`
- **Terminal colors**: Adjust terminal emulator configs in `config/`
- **Git aliases**: Add custom git aliases in `git/gitconfig`


🆘 Troubleshooting
------------------

*Please read carefully warning messages during installation !!*

* If something goes wrong, please run **[`$ dotfiles update`][dotfiles-update]** (or [install.py]) to make everything up-to-date.
    * Please carefully READ the error/warning message printed by the installation script.
    * If you have your own `~/.zshrc`, `~/.vimrc`, `~/.vim`, etc., that are NOT symbolic links,
      they will not be overwritten by default.
      In such cases you should delete these files *manually*.

* Q: I see some weird icons like `⍰` in (neo)vim or in the [statusline](https://github.com/powerline/powerline#vim-statusline).
  - A: Use [Nerd fonts](https://github.com/ryanoasis/nerd-fonts) v3. If you haven't upgrade to Nerd fonts [**v3.1.1** or higher](https://github.com/ryanoasis/nerd-fonts/releases/tag/v3.1.1), upgrade to v3 due to the new (breaking) Material Design Icons codepoints.
    - Note: `JetBrainsMono Nerd Font Mono` ~~`JetBrainsMono NFM`~~ (nerd-fonts [v3.1.0 is buggy](https://github.com/ryanoasis/nerd-fonts/issues/1434))
  - Mac users can install via: `brew install --cask font-*-nerd-font`.
    - (Minimal fonts only `brew install --cask font-jetbrains-mono-nerd-font`)
  - To upgrade existing installations, try `brew reinstall --cask $(brew list | grep nerd-font)`.

* If neovim + treesitter emits an error like `query: invalid node type`, run `:TSUpdate` (and wait for installation is done).
  * See [nvim-treesitter#3092](https://github.com/nvim-treesitter/nvim-treesitter/issues/3092) for more details.

* If neovim cannot run due to `version 'GLIBC_2.29' not found` errors (on Ubuntu 18.04 or earlier),
  you should upgrade your Ubuntu distribution to 20.04+ in order to run nvim 0.8.x or higher.
  If you use [appimage](https://github.com/neovim/neovim/releases/tag/stable) binary of neovim,
  this will work in Ubuntu 18.04; install neovim through `dotfiles install neovim` or `NEOVIM_VERSION=0.9.4 dotfiles install neovim`.

* If [**neovim**][neovim] emits any startup errors (e.g. `no module named neovim`):
    * Use **latest neovim** (e.g., neovim 0.9.5).
      To install/upgrade neovim on your system, you can run `dotfiles install neovim` (linux) or `brew install neovim` (mac).
    * Try `:checkhealth`.
    * Try `:Lazy update`: some errors from vim plugin could be easily solved by updating plugins to date.
      You can do `:Lazy update` (in vim) or `$ dotfiles update` (in zsh).
    * We require python3 version not less than 3.6. See https://endoflife.date/python
    * Make sure that the [`pynvim`](https://pypi.python.org/pypi/pynvim/) pypi package is installed on *local* python 3,
      i.e. the python3 on conda, virtualenv, etc.
      This should have been automatically installed.
      If it doesn't work, check `which python3`. Use the following vim command to tell which host python is used:
          [`:echo g:python3_host_prog`](https://github.com/wookayin/dotfiles/blob/master/nvim/init.vim).
      * If you are not sure, manually running `python3 -m pip install --user pynvim` might help.

* Does vim color look weird (e.g. only black-and-white)?
  * Check whether your terminal emulator supports [24-bit color](https://github.com/wookayin/dotfiles/pull/9). Use iTerm2, wezterm, or kitty; NOT built-in Terminal.
  * Latest Mosh (1.4.0+) support 24-bit colors, so try upgrading mosh if you are using it.
  * Try `:set notermguicolors` to temporarily disable 24-bit colors.
* Does tmux look weird? Make sure that tmux version is [2.3](etc/ubuntu-setup.sh) or higher.
    * Run `$ dotfiles install tmux` to install `tmux` into `$HOME/.local/bin`, if you do not have sudo.
* If you are still lost, or you've found a bug, please feel free to contact me or raise an issue ---
  I will happy to assist.


[neovim]: https://github.com/neovim/neovim
[dotfiles-update]: bin/dotfiles
[linux-locals.sh]: etc/linux-locals.sh
[install.py]: install.py


## License

[The MIT License (MIT)](LICENSE)

Copyright (c) 2025 Dustin Liddick

Originally forked from [wookayin/dotfiles](https://github.com/wookayin/dotfiles)  
Copyright (c) 2012-2024 Jongwook Choi (@wookayin)
