Install software from non-OS repos
----
# Visual Studio Code
Download the Microsoft GPG key, and convert it from OpenPGP ASCII armor format to GnuPG format, move it into the apt trusted keys directory, then add the VS Code repository.
```
curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg
mv microsoft.gpg /etc/apt/trusted.gpg.d/microsoft.gpg
echo "deb [arch=amd64] https://packages.microsoft.com/repos/vscode stable main" > /etc/apt/sources.list.d/vscode.list
 
# Update and install Visual Studio Code 
apt update && apt install code
```

# Node.js
```
curl -sL https://deb.nodesource.com/setup_8.x | sudo -E bash -
sudo apt install -y nodejs
```

# Laverna
Download Laverna and unzip to ~/Apps/Laverna. Then add the following file in /usr/share/applications

```
[Desktop Entry]
Name=Laverna
Comment=Record information on InfoSec study
Keywords=onenote;evernote;notes;laverna;keepnote;
Exec=/home/rafael/Apps/Laverna/laverna
Icon=/home/rafael/Dropbox/Computers/Linux/icons/laverna.png
Terminal=false
Type=Application
StartupNotify=true
OnlyShowIn=GNOME;Unity;
Categories=GNOME;GTK;System;Core;
MimeType=inode/directory;application/x-gnome-saved-search;
```