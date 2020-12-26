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
### Configure multiple Git accounts on a single machine with SSH keys
#### Generating the SSH keys
```
ls -al ~/.ssh
cd ~/.ssh
ssh-keygen -t rsa -C "email@personal_mail.com -f "id_rsa_personal"
ssh-keygen -t rsa -C "email@work_mail.com" -f "id_rsa_work"
```
#### Adding the new SSH key to the corresponding Git account
1. Copy ssh rsa public key for personal account for Mac
```
pbcopy < ~/.ssh/id_rsa_personal.pub
```
or Linux
```
xclip -selection clipboard < ~/.ssh/id_rsa_personal.pub
```
2. Go to **Settings**
3. Select **SSH and GPG keys** from the menu to the left
4. Click on **New SSH key**, provide a suitable title, and paste the key in the box below
5. Click **Add key** — and you’re done!
6. Do the same for work account
#### Registering the new SSH Keys with the ssh-agent
```
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_rsa_personal
ssh-add ~/.ssh/id_rsa_work
```
#### Creating the SSH config File
Add to ~/.ssh/config
```
# Personal account, - the default config
Host github.com
   HostName github.com
   User git
   IdentityFile ~/.ssh/id_rsa_personal
   
# Work account
Host github-work.com
   HostName github.com
   User git
   IdentityFile ~/.ssh/id_rsa_work
```
#### Change gitconfig on Git project
Add to ~/.gitconfig to change **Author/Committer** in the commit message for personal/work identities
```
[includeIf "gitdir:~/workspace/*"]
    path = .gitconfig-work
[includeIf "gitdir:~/personalspace/*"]
    path = .gitconfig-personal
```
Create ~/.gitconfig-work and ~/.gitconfig-personal, add to each file
```
[user]
	name = <user name>
	email = <user email>
```
