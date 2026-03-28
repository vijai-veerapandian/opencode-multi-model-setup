# 01 - OpenCode Installation on Ubuntu

## Prerequisites

Ensure you have a modern terminal emulator installed. Supported on Linux:

- [Ghostty](https://ghostty.org/)
- [Kitty](https://sw.kovidgoyal.net/kitty/)
- [WezTerm](https://wezterm.org/)
- [Alacritty](https://alacritty.org/)

---

## Install OpenCode

Run the official install script:

```bash
curl -fsSL https://opencode.ai/install | bash
```

# Reload PATH for current session
```
export PATH="$HOME/.local/bin:$PATH"
```

# Make it permanent in Zsh
```
echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.zshrc
source ~/.zshrc
```

## Verify Installation
```
opencode --version
```

## Launch OpenCode
```
cd ~/your-project
opencode
```



