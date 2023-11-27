---
author: Erwin de Keijzer
date: MMMM dd, YYYY
paging: "%d / %d"
---

# Using the CLI for fun and profit

## Or, how to shave your yak



About me:
- Erwin de Keijzer
- DevOps Engineer @ Fullstaq
- Yak Shaver @ home
  - Janky project profesional
- CLI aficionado

[comment]: # (change font size, float tmux, vif wezterm, edit/save for live reload)
[comment]: # (everything you see should get explained)

---

# terminal emulator

It's 2023, you can do better than the built in terminal

- kitty
- alacritty
- wezterm
- warp
- tabby

## modern features

- hyperlink support
- cat images
- ligatures
- gpu rendering catting big ass files is really fast)
- scriptability


[comment]: # (tell we are using wezterm, cat an image on the CLI)

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

[comment]: # (update chezmoi config on 1 host, gitui commit/push, chezmoi update on other host)

---


# terminal multiplexer

- screen
- tmux
- tab-rs

----

# ideeen

- slides (this presentation)
- dotfiles / chezmoi / devpod
- tmux / screen / zellij / tab-rs
- zsh / fish / nushell / powershell
  - oh my zsh
  - znap
  - zsh-autosuggestions
  - zsh-syntax-highlighting
  - ctrl-keybindings
- find / ag / fd
- fzf / skim
- ls / exa / eza / lsd
- bat
- git / tig / gitui / 
- top / htop / btop
- atuin
- vim / neovim / lunarvim / nvchad / helix
- direnv / $KUBECONF / k9s
- putting it all together
  - cd (fd | fzf) zellij
