# Download Zotero
1. Go to the [Zotero download page](https://www.zotero.org/download/)
2. open a terminal
3. Run the following commands:
```bash
mkdir -p ~/zotero
tar -xjf zotero.tar.bz2 -C ~/zotero --strip-components=1
```
4. run Zotero with the following command:
```bash
cd ~/zotero
./zotero
```

5. To create a desktop shortcut, create a file named `zotero.desktop` in `~/.local/share/applications` with the following content:
```bash
nano ~/.local/share/applications/zotero.desktop
```
```bash
[Desktop Entry]
Encoding=UTF-8
Name=Zotero
Exec=/home/chuang/zotero/zotero
Icon=/home/chuang/zotero/chrome/icons/default/default48.png
Type=Application
Categories=Office;
Comment=Manage your research with Zotero
Terminal=false
```
6. Make the file executable:
```bash
chmod +x ~/.local/share/applications/zotero.desktop
```

