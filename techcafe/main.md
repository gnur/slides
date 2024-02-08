---
author: Erwin
date: MMMM dd, YYYY
paging: "%d / %d"
theme: ./theme.json
---

# Using the CLI for fun and profit

## Or, how to shave your yak

About me:

- Erwin de Keijzer
- DevOps Engineer @ Fullstaq
- Yak Shaver @ home
  - Janky project professional
- CLI aficionado

[comment]: # "change font size, float tmux, vif wezterm, edit/save for live reload"
[comment]: # "everything you see should get explained"
[comment]: # "I learned that I should not intro myself, let's remove it"

---

# living the CLI life

## Why though?

- keyboard focused (but mouse is supported!)
- very portable
  - ssh
  - devpod
  - devcontainer
- looks cool

---

# heul veul projecten

## we vliegen er door heen, voel je vrij om direct vragen te stellen

---

# deze frikkin presentatie

## dit update live

[slides](https://github.com/maaslalani/slides)

---

## Code execution

```go
package main

import "fmt"

func main() {
  fmt.Println("Hellow KCD Utrecht!")
}
```

### output:

---

# terminal emulator

It's 2024, you can do better than the built in terminal

- kitty
- iterm2
- alacritty
- wezterm
- warp
- tabby

## modern features

- hyperlink support
- cat images
- mouse support
- ligatures
- gpu rendering catting big ass files is really fast
- scriptability

---

# managing dotfiles

## goals

- same experience on all hosts
- some way for host / architecture / os specific stuff
- optionally, secure way to use secrets

---

## github.com/twpayne/chezmoi

```
~~~figlet
chezmoi
~~~
```

```bash
$ chezmoi init git@github.com:gnur/dotfiles.git
...
```

## live demo!

[comment]: # "update chezmoi config on 1 host, gitui commit/push, chezmoi update on other host"

---

# terminal multiplexer

- screen
- tmux
- tab-rs
- zellij
- byobu
- terminal emulator itself
- wezterm

[comment]: # "I'm using tmux here, I've added some stuff, show resizing panes with mouse, floating window"

---

# shell

Bash is just so, bash.

- zsh
- fish
- nushell
- powershell

## configuration

- oh my zsh
- znap
- zsh-syntax-highlighting
- zsh-autosuggestions
- ctrl-keybindings
- starship / oh my posh

[comment]: # "If you're new to this, please start with fish and zellij, I think it's the lowest effort to get some very big improvements"
[comment]: # "ctrl keybindings, ctrl-a, ctrl-e, ctrl-u, ctrl-p, ctrl-n, ctrl-j"

---

# finding and selecting stuff

`find` and `grep` are fine, but it's 2024, let's modernize

- [fd](https://github.com/sharkdp/fd)
- ack
- ag
- rg
- fzf
- skim

## examples

`fd` (just recursively lists everything, really fast)

`rg -i setupr` (grep recursive and case insensitive for "setupr", really fast)

`$EDITOR $(fd -t file | fzf)` (fuzzy search all files in (sub)dir and open the selected one with your editor)

`alt-c` (fuzzy search all dirs and cd into it, with the fzf zsh plugin)

---

# listing files and contents

`ls` and `cat` have been around forever, but there is more

- [lsd](https://github.com/lsd-rs/lsd) (drop in replacement for ls with modern powers)
- [eza](https://github.com/eza-community/eza) (modern alternative for ls, formerly exa)
- [bat](https://github.com/sharkdp/bat) (improved cat / less)

---

# putting this all together

Combining this we can get this monstrosity:

```bash
func ctrl-space() {
  RG_PREFIX="rg --hidden --iglob '!google-cloud-sdk' --iglob '!flutter' --column --line-number --no-heading --color=always --smart-case "
  RG_SUFFIX="~/prive ~/code/src/github.com/gnur ~/bin ~/Documents ~/.config"
  FD_PREFIX="fd --type d --hidden"
  FD_SUFFIX="$HOME"
  VIF_CMD="fd --type f --hidden . '$HOME'"
  INITIAL_QUERY="${*:-}"
  f=$(echo -n '' | fzf --ansi --query "$INITIAL_QUERY" \
    --bind "change:reload:sleep 0.1; $RG_PREFIX {q} $RG_SUFFIX || true" \
    --bind "start:reload($FD_PREFIX {q} $FD_SUFFIX)+unbind(ctrl-d,change)" \
    --bind "ctrl-f:unbind(ctrl-f)+change-prompt(2. edit> )+enable-search+reload($VIF_CMD)+transform-query('')+change-preview(exa --long --classify --icons --no-user --no-permissions {})" \
    --bind "ctrl-r:unbind(ctrl-r)+change-prompt(3. ripgrep> )+disable-search+reload($RG_PREFIX {q} $RG_SUFFIX || true)+rebind(change,ctrl-f)+transform-query('')+change-preview(bat --color=always {1} --highlight-line {2})" \
    --color "hl:-1:underline,hl+:-1:underline:reverse" \
    --prompt '1. cd > ' \
    --delimiter : \
    --header '╱ CTRL-R (ripgrep mode) ╱ CTRL-F (edit mode) ╱ CTRL-D (dir mode) /' \
    --preview 'exa --long --classify --icons --no-user --no-permissions {}' \
    --preview-window 'up,60%,border-bottom,+{2}+3/3,~3' )
}
```

---

# putting it all together #2

- ctrl-space in your shell for quickly:
  - cd-ing into a directory
  - ctrl-f to switch to quickly editing files
  - ctrl-r to switch to searching for substrings and editing the files that contain them

## LIVE DEMO

---

# watch your process

You've probably used `top` before

- but have you used `htop` ?
- or `btop` ?

## LIVE DEMO

[comment]: # "in btop, click some stuff"

---

# git

For the people that like to use git but dislike using `git`.

- ghq (easy way to checkout git repositories in ordered directories)
- gitui
- tig
- lazygit

## LIVE DEMO

[comment]: # "Just show gitui"

---

# history

This is one is so great, it gets its own page

```
~~~figlet
atuin
~~~
```

- replaces your shell history with an sqlite database
- allows fuzzy searching your history
- stores additional context for each command (exit code, run duration, date)

[comment]: # "do a ctrl-r, search for reborn vending machine, see that it downloaded"

---

# editors

Time for some controversy.

## THE BEST EDITOR EVER

```
~~~figlet
neovim
~~~
```

[comment]: # "maybe not, just trolling"

---

# editors

There has been a lot of progress in this field:

- (neo)vim has progressed so much
  - lunarvim
  - nvchad
  - lazyvim
  - astrovim
- kakoune
- helix
- emacs

## common ground

- lsp
- treesitter

[comment]: # "also mention how you need extra config & plugins to make nvim work"
[comment]: # "edit a setuprouter file, show gd, <space>k"

---

```
~~~figlet
k9s
~~~
```

[comment]: # "open k9s, show pod logs, describe deployment"

---

# summary

- slides (this presentation)
- dotfiles / chezmoi / devpod
- tmux / screen / zellij / tab-rs
- zsh / fish / nushell / powershell
  - oh my zsh
  - znap
  - zsh-autosuggestions
  - zsh-syntax-highlighting
  - ctrl-keybindings
- find / ag / fd / rg
- fzf / skim
- ls / exa / eza / lsd
- bat
- git / tig / gitui
- top / htop / btop
- atuin
- vim / neovim / lunarvim / nvchad / helix
  - lsp
  - treesitter
- direnv / $KUBECONF / k9s
- putting it all together
  - cd (fd | fzf) zellij
