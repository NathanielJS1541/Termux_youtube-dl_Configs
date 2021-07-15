# Installation and Configuration
## Install Termux and Requirements
It is **important** that these are both installed from the **same** appstore, whether that is F-Droid or Google play. You will need the following:
- Termux
  - Google Play:	https://play.google.com/store/apps/details?id=com.termux
  - F-Droid:		https://f-droid.org/en/packages/com.termux/
- Termux:API
  - Google Play:	https://play.google.com/store/apps/details?id=com.termux.api
  - F-Droid:		https://f-droid.org/en/packages/com.termux.api/

## Make Sure Termux and its Packages are up to date
- Open Termux
- Type in `pkg upgrade` (You may have to type `y` and hit enter for this)

## Setup Termux for the First Time
- Install Termux:API with `pkg install termux-api`
- Set up file access with `termux-setup-storage`

## Install [Python](https://www.python.org/), [NodeJS and nmp](https://nodejs.org/en/), and [ffmpeg](https://ffmpeg.org/)
- Type `pkg install python nodejs ffmpeg`

## Install and Configure [youtube-dl](https://github.com/ytdl-org/youtube-dl)
- First make sure pip is up to date with `pip install -U pip`
- Type `pip install youtube-dl`
- Check if the directories we need already exist with `ls -al`. We need one called `.config` **(The dot is important!)** and `bin`.
  - If `bin` doesn't exist, type in `mkdir bin`.
  - If `.config` doesn't exist, type in `mkdir -p .config/youtube-dl`. **Remeber the dot!**
- To edit the config file, `nano .config/youtube-dl/config`
  - If it's already got stuff in, just `CTRL + X` to exit nano and then type `rm .config/youtube-dl/config`. Then run the nano command again.
  - If this throws an error because the folder doesn't exist, type `mkdir .config/youtube-dl` and try the previous command again.
  - If there's stuff in the file already, just delete it.
- In a note app or similar, open the config I have provided. Copy the contents and paste it into the termux window.
- Once you have added the content to the file, press `CTRL + X` and press `y` to save.
- Now edit the termux-url-opener with `nano bin/termux-url-opener`.
  - As before, if there is stuff here already just delete it by exiting out, then typing `rm bin/termux-url-opener` and running the nano command
    again.
- Open the termux-url-opener that I provided in another app. Copy the entire contents and paste into the termux window as before.
- Again, press `CTRL + X` and press `y` to save.

## Install [spotify-dl](https://github.com/SwapnilSoni1999/spotify-dl)
- Type `npm install -g spotify-dl`

## Install and Configure [instaloader](https://github.com/instaloader/instaloader)
- Type `pip install instaloader`
- To create the configuration file for instaloader, from the home directory type `nano bin/instaloader_args.txt`
- As with the youtube-dl config, copy the contents of the `instaloader_args.txt` file from this repo and paste them into Termux.
- If you don't plan on saving posts from private accounts, you're done here. Just press `CTRL + X` to exit and then `y` to save. However if
  you would like to save posts from private accounts, follow the next steps.
- Create a new line at the top of the file and type in `--login=` and then your instagram username. Beware of downloading enormous amounts of posts if
  logged in, though. It is likely to get your account suspended if it is deemed "supicious".
  - If you encounter login errors, please follow the **Login Error** section of the [Instaloader Troubleshooting Guide](https://instaloader.github.io/troubleshooting.html)
- If you do not want to login interactively, you *can* add a new line with `--password=`, but that doesn't mean you should as this is horrible security practice.
- Finally, of course, you can save and exit with `CTRL + X`, and then `y`.

# Usage
- From any app that supports sharing, simply click share, and click on *Termux* in the app list. A popup should appear showing the download
  progress. Once it is finished, just make sure it hasn't screamed any errors at you and press any key to close the window.
  - For Spotify, however, the process is slightly more convoluted. Spotify puts a load of junk in front of the actual URL, which causes Termux
    to not recognise it. The easiest way I have found to get round this is to copy it into a text editor, select **only the link**, and then press
	share again to get only the link to be shared to Termux. Since that is pretty tedious for a song-by-song basis, I'd recommend only using the
	spotify downloader for albums and public playlists.
  - Another note about the spotify-dl program is it depends on depreciated packages. A.k.a it is jank as hell, if it throws an error just share the
    exact same link to it again and it should sort itself out. It doesn't seem to handle unstable internet connections well.
- Since we set a default *template* with our `.config/youtube-dl/config`, you can also just copy any link from a browser etc. and type into Termux
  `youtube-dl [URL]`, and it should try and download the video. You can also override template options by specifying them in the command, such as
  overriding the format options with `-f "bestvideo[height<=1080][fps<=60]+bestaudio/best"` to download in the highest quality up to 1080p 60fps.
  Just be warned that some website extractors handle template arguments such as `%(title)s` very strangeley, which is why I have custom written
  output templates for the most common websites I use. If your youtube-dl keeps telling you that you have already downloaded a video, it may be that
  the *title* it is extracting may be something random like a username which causes every video by that user to try and write to the same file. That
  is why I try and include the `%(id)s` argument in the default case to avoid this.
- If you start getting errors from youtube-dl about the extractor being broken... blah blah blah, the website probably updated it's API. Go to the
  next section about updating youtube-dl.

# Updating the Programs
## Updating Termux Packages
- No matter which program you are having problems with, it is wise to do this first. Simply type `pkg upgrade` and then `y`.

## Using Pip to Upgrade youtube-dl
- You can check if any pip packages need updating by typing `pip list -o`. You can then update each of these packages with `pip install -U [PACKAGE]`.
  - If pip is on the list, you should first do `pip install -U pip`
  - In the case of youtube-dl, this would be `pip install -U youtube-dl`.
  - In the case this is instaloader, type `pip install -U instaloader`

## Using npm to Update spotify-dl
- To update packages installed with npm, simply run `npm update -g`