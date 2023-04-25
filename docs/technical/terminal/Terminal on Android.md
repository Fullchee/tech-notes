## Setting up git on Android

[Mobile Sync for Obsidian | Some Thoughts](https://werzum.github.io/tech/2022/02/13/Obsidian-Mobile-Sync.html)

### Termux Terminal on Android

1. Download [Termux (terminal)](https://termux.dev/en/) on F Droid
    1. not on Google Play
2. Download the [Termux:Widget | F-Droid](https://f-droid.org/en/packages/com.termux.widget/)
3. `pkg update`
	1. if it doesn't work: `termux-change-repo`
	2. select the first option
4. `pkg install git`
5. `pkg install openssh`
	1. `ssh-keygen`
	2. `cat ~/.ssh/id_rsa.pub`
	3. [add SSH key to GitHub](https://github.com/settings/ssh/new)
6. `termux-setup-storage`
	1. give termux access to the file system via `~/storage`
	2. no SD card access without root 😥
7. `cd ~/storage/downloads`
8. Install vim
	1. `pkg install vim`
9. Setup git
	1. `git config --global pull.rebase false`
	2. `git config --global user.name "Fullchee Zhang"`
	3. `git config --global user.email "fullchee@gmail.com"`
10. `git clone git@github.com:Fullchee/notes.git`
11. `git clone git@github.com:Fullchee/private-notes.git`
12. `chmod 700 -R /data/data/com.termux/files/home/.shortcuts`
13. `~/.shortcuts/sync_notes.sh`

Let git know to trust that folder


```sh
#/bin/bash
sync() {
	git add -A && git commit -m "Android" && git pull && git push;
}

cd ~/storage/downloads/notes
echo "Syncing notes"
sync

cd ~/storage/downloads/private-notes
echo "Syncing private notes"
sync
```
