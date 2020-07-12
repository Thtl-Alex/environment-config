## Environment Configuration
### Requirements
- Alacritty version >= 0.5.0
### Create hard links for config files
```
ln ${HOME_DIR}/environment-config/.tmux.conf ~/.tmux.conf
ln ${HOME_DIR}/environment-config/alacritty.yml ~/.config/alacritty/alacritty.yml
```
### Use Alacritty as default terminal (Ctrl + Alt + T)
```
gsettings set org.gnome.desktop.default-applications.terminal exec 'alacritty'
```
### Tmux
|Usage|Command|
|-|-|
|Create a new tmux session|```tmux new -s <session-name>```|
|Delete all tmux sessions |```tmux kill-server```|
|Open an existed tmux session|```tmux attach -t <session-name>```|
|Rename a tmux session|```tmux rename-session -t <old-name> <new-name>```|