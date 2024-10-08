# ![title](https://gist.githubusercontent.com/khanhas/40999296b19662cdc1f877505c35a934/raw/fdc223e2c557b7be2e5e68e87f93cb3950c8b887/zshelf_title.svg)

<p align="center">
  <a href="https://z-lib.org">Z-Library</a> browser and downloader for <a href="https://remarkable.com/">reMarkable</a> devices
  <br>
  <br>
  <br>
  <img src="https://i.imgur.com/UbcwJ9L.png" width="300" title="Browse">
  <img src="https://i.imgur.com/CWWoQfk.png" width="300" title="Book metadata">
  <img src="https://i.imgur.com/38oxA3a.png" width="300" title="Search UI">
</p>

<p align = "center"><b>This fork is not on Toltec.</b></p>

## Installation
[Note: If you are using a reMarkable 2, you will need [rm2fb](https://github.com/ddvk/remarkable2-framebuffer). This dependency means that Zshelf is not officially supported on versions higher than 3.3.2.1666. See the full list of supported versions [here](https://github.com/ddvk/remarkable2-framebuffer/blob/master/src/shared/config.cpp)]

1. Download the latest release from the [Releases page](https://github.com/phthallo/zshelf/releases), and unzip it.
2. Edit your `config.json` file, as instructed below.
3. [Find your device IP address](https://remarkable.guide/guide/access/ssh.html#finding-your-device-password-and-ip-addresses).
4. Move the `backend` folder, `config.json` file and `zshelf` file in the release to your device to the location `/home/root/apps/` [Note: Install a launcher, such as [Remux](https://rmkit.dev/apps/remux) or [Oxide](https://oxide.eeems.codes/) to be able to open Zshelf.] You can use the following command to move all at once, replacing the IP address if required.
   ```bash
   scp -r * root@10.11.99.1:/home/root/apps
   ```
5. [SSH into your device](https://remarkable.guide/guide/access/ssh.html#connecting-via-ssh). Type the following to turn `zshelf` into an executable.
   ```bash
   chmod +x /apps/zshelf
   ``` 
6. Restart your device, then start Zshelf from your launcher.


### [IMPORTANT] Configure Domain and Cookie
As Z-Library does not allow anonymous downloads, you will need to configure your Z-library domain and session cookies to download from your reMarkable. This requires an existing account - free user accounts are limited to 10 books a day.

1. Open [https://singlelogin.re](https://singlelogin.re) in your web browser. If this link doesn't work, refer to the [masterpost of official Z-library links](https://www.reddit.com/r/zlibrary/wiki/index/access/).
3. Log in with your account.
4. In any page, open up Console (hit <kbd>F12</kbd> and switch to the Console tab), and run:
  ```js
  document.cookie
  ```
  It will return a string that contains your cookie. Copy the parts that have `remix_userkey` and `remix_userid` and ignore the rest.

6. Open `config.json`. Enter the URL you used to access Z-library as the `"domain"` value.  
7. Enter the string from above as the `"cookie"` value. 
8. Save the file.


#### Further Configuration
By default, Zshelf saves downloaded ebooks to Xochitl. You can skip this by setting `"skipXochitl"` to anything other than a null value. 

To save your ebooks to another location (I'll add customising save location in Xochitl soon), set `"additionalBookLocation"` to the path of the location where you wish to save it (the default value is `/home/root/Books`) This option is useful if you use an external ebook reader, such as [Koreader](https://github.com/koreader/koreader/), on your reMarkable.

To edit your configuration from within the reMarkable, use a terminal text editor like vim or nano. 

## Development
This section assumes the use of a Linux based system.

0. [Set up reMarkable toolchain](https://remarkable.guide/devel/toolchains.html), NodeJS and `npm`
1. Run `git clone https://github.com/phthallo/zshelf` and `cd` into it.
2. Source the toolchain to load its environment variables. You will need to do this every time you open a new terminal.
```bash
$ source /opt/codex/rm11x/3.1.15/environment-setup-cortexa7hf-neon-remarkable-linux-gnueabi
```
3. Run `qmake`
4. Run `make`
5. Run `cd backend` to move to the backend folder.
6. Run `npm install`. This will generate a `zshelf` file.

## Notes
Files saved to Xochitl will appear only after a restart. 

Files saved to Xochitl also have the following properties, meaning they will not sync if you do not have Connect.
```
"deleted": false,
"lastModified": "1",
"lastOpenedPage": 0,
"metadatamodified": false,
"modified": false,
"parent": "",
"pinned": false,
"synced": false,
"type": "DocumentType",
"version": 1,
"visibleName": fileName
```

## Credits
- [Qt-Quick-Keyboard](https://github.com/mireq/Qt-Quick-Keyboard) by mireq

