# Troubleshooting

*Please read carefully warning messages during installation !!*

## General Issues

* If something goes wrong, please run **[`$ dotfiles update`](../bin/dotfiles)** (or [install.py](../install.py)) to make everything up-to-date.
    * Please carefully READ the error/warning message printed by the installation script.
    * If you have your own `~/.zshrc`, `~/.vimrc`, `~/.vim`, etc., that are NOT symbolic links,
      they will not be overwritten by default.
      In such cases you should delete these files *manually*.

## Display Issues

### Weird Icons in Vim/Statusline
**Q**: I see some weird icons like `⍰` in (neo)vim or in the [statusline](https://github.com/powerline/powerline#vim-statusline).
- **A**: Use [Nerd fonts](https://github.com/ryanoasis/nerd-fonts) v3. If you haven't upgrade to Nerd fonts [**v3.1.1** or higher](https://github.com/ryanoasis/nerd-fonts/releases/tag/v3.1.1), upgrade to v3 due to the new (breaking) Material Design Icons codepoints.
  - Note: `JetBrainsMono Nerd Font Mono` ~~`JetBrainsMono NFM`~~ (nerd-fonts [v3.1.0 is buggy](https://github.com/ryanoasis/nerd-fonts/issues/1434))
- Mac users can install via: `brew install --cask font-*-nerd-font`.
  - (Minimal fonts only `brew install --cask font-jetbrains-mono-nerd-font`)
- To upgrade existing installations, try `brew reinstall --cask $(brew list | grep nerd-font)`.

### Color Issues
**Q**: Does vim color look weird (e.g. only black-and-white)?
- Check whether your terminal emulator supports [24-bit color](https://github.com/wookayin/dotfiles/pull/9). Use iTerm2, wezterm, or kitty; NOT built-in Terminal.
- Latest Mosh (1.4.0+) support 24-bit colors, so try upgrading mosh if you are using it.
- Try `:set notermguicolors` to temporarily disable 24-bit colors.

### Tmux Issues
**Q**: Does tmux look weird?
- Make sure that tmux version is [2.3](../etc/ubuntu-setup.sh) or higher.
- Run `$ dotfiles install tmux` to install `tmux` into `$HOME/.local/bin`, if you do not have sudo.

## Neovim Issues

### Treesitter Errors
* If neovim + treesitter emits an error like `query: invalid node type`, run `:TSUpdate` (and wait for installation is done).
  * See [nvim-treesitter#3092](https://github.com/nvim-treesitter/nvim-treesitter/issues/3092) for more details.

### GLIBC Version Issues
* If neovim cannot run due to `version 'GLIBC_2.29' not found` errors (on Ubuntu 18.04 or earlier),
  you should upgrade your Ubuntu distribution to 20.04+ in order to run nvim 0.8.x or higher.
  If you use [appimage](https://github.com/neovim/neovim/releases/tag/stable) binary of neovim,
  this will work in Ubuntu 18.04; install neovim through `dotfiles install neovim` or `NEOVIM_VERSION=0.9.4 dotfiles install neovim`.

### Startup Errors
* If [**neovim**](https://github.com/neovim/neovim) emits any startup errors (e.g. `no module named neovim`):
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

## Getting Help

If you are still lost, or you've found a bug, please feel free to contact me or raise an issue --- I will happy to assist.