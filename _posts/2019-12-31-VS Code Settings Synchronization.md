---
layout:     post
title:      VS Code Settings Synchronization
#subtitle:   None
date:       2019-12-31
author:     Lance
header-img: img/bg.jpg
catalog: true
#tags:
---

## Key Features

- Use your GitHub account token and Gist.
- Easy to Upload and Download on one click.
- Show a summary page at the end with details about config and extensions effected.
- Auto download Latest Settings on Startup.
- Auto upload Settings on file change.
- Share the Gist with other users and let them download your settings.
- Supports GitHub Enterprise
- Support pragmas with @sync keywords: host, os and env are supported.
- GUI for changing settings / logging in

## It Syncs

All the extensions and complete User Folder that Contains

- Settings File
- Keybinding File
- Launch File
- Snippets Folder
- VSCode Extensions & Extensions Configurations
- Workspaces Folder

## Shortcuts

- Upload Key : `Shift + Alt + U`
- Download Key : `Shift + Alt + D`

## Configure Settings Sync

Settings Sync Configuration page will be opened automatically on code start and requires two things to setup:

1. **Github Token**
2. **Github GIST ID**

Github Token needs to be retrived by your Github account while Settings Sync creates GIST if you are first time user.

Following are the steps you need to perform to configure.

- Click on `Login with Github` .
- Login Github on Browser and close the browser tab once you get Success message.
- If you are using Settings Sync first time GIST will be created automatically - Configuration Completed.
- If you already have GIST, new window will be opened to allow you to select the GIST or `Skip` to create new GIST - Configurartion Completed.

![Login with GitHub](https://shanalikhan.github.io/img/login-with-github.png)

![Existing Gist](https://shanalikhan.github.io/img/existing-gist.png)

You can always **verify created gist** by going to **`https://gist.github.com` **and checking for a gist named `cloudSettings`

## Upload Your Settings

**Press `Shift + Alt + U`**

> Type “>Sync” In Command Palette into order download / upload

When downloading or uploading for the first time, the welcome page will automatically open, where you can configure the Settings Sync.

Once you select upload, after uploading the settings. You will see the Summary details with the list of each files and extensions uploaded.

## Download your Settings

**Press `Shift + Alt + D`**

> Type “>Sync” In Command Palette into order download / upload

When downloading or uploading for the first time, the welcome page will automatically open, where you can configure the Settings Sync.

Once you select download, after downloading. Settings Sync will display you Summary containing the list of each files and extension being downloaded.

New popup will be opened to allow you to restart the code to apply the settings.

## Reset Extension Settings

> Select **”> Sync : Reset Extension Settings”** in the Command Palette to reset your settings### Toggle Auto Download

Auto Download is **disabled by default**. It will sync all the setting by default when the editor starts. Please make sure you have valid github Token and Gist available to make it work properly.

Select Command **“Sync : Advance Options > Toggle Auto-Download On Startup”** command to Turn ON / OFF the auto download.

### Toggle Force Download

Force Download is **disabled by default**. By default extension wont download the latest settings if you already have latest downloaded version , but sometime when you delete some extension locally and dont upload the settings it will still show you have latest versions by date or time checks, by turning this ON it will always download the cloud settings on startup.

Please make sure you have valid github Token and Gist available to make it work properly.

Select Command **“Sync : Advance Options > Toggle Force Download”** command to Turn ON / OFF the force download.

### Toggle Auto-Upload on change

Auto-upload is **disabled by default**. When the settings are changed and saved this feature will automatic start the upload process and save the settings online.

Please make sure you have valid github Token and Gist available to make it work properly.

Select Command **“Sync : Advance Options > Toggle Auto-Upload on Setting Change”** command to Turn ON / OFF the auto-upload.

### Toggle Summary

Summary is **enabled by default** which shows all the files and extensions that are added or deleted in a single page. You may turn it off in order to make a upload and download process clean and quiet.

Select Command **“Sync : Advance Options > Toggle Summary Page On Upload / Download”** command to Turn ON / OFF the auto download.

### Create Public Gist To Share Settings

By default, it creates secret Gist so only you can see it but if you want to share your Gist with other users, you can set it to public. You can’t change the exiting Gist type from secret to public so it will reset the Gist ID so you can create new Gist with all the existing editor settings.

Select Command **“Sync : Advance Options > Share Settings with Public GIST”**

Other users can give your Gist Id to download the Gist, but they cant upload their settings on your Gist.



## Reference  
- [Visual Studio Code Settings Synchronization](http://shanalikhan.github.io/2015/12/15/Visual-Studio-Code-Sync-Settings.html)


