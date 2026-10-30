> [!WARNING]
> This repository has been archived. [More information](https://t.me/craveio_aosp/137)

[![forthebadge](https://forthebadge.com/images/badges/powered-by-electricity.svg)](https://forthebadge.com) [![forthebadge](https://forthebadge.com/images/badges/you-didnt-ask-for-this.svg)](https://forthebadge.com) [![forthebadge](https://forthebadge.com/images/badges/gluten-free.svg)](https://forthebadge.com) [![forthebadge](https://forthebadge.com/images/badges/works-on-my-machine.svg)](https://forthebadge.com)
# BuildDroid
An opensource tool to build Android ROMs on Crave. If you have better name for this script, let me know!

> [!WARNING]  
> Forking this repository is not recommended as its content frequently changes; instead, please refer to the instructions below. You don't need to fork it.

## How to start<br>
Connect to `crave devspace`, create your project (`crave clone list` and `crave clone create "my_first_build" --projectID XX`) and run `crave ssh`.<br>
Create an empty file with name `config.ini`, then put `#!/bin/bash` at start of the file. (`nano config.ini`) After that, add some variables.<br>
Example `config.ini` file can be found [here](https://github.com/wojtekojtek/builddroid/blob/main/examples/config.ini)<br>
When you'll be ready, simply run `exit` and:<br>
`crave run --no-patch -- "curl https://raw.githubusercontent.com/wojtekojtek/builddroid/refs/heads/main/builddroid.sh | bash"`<br>
If you ran all commands correctly, you should see "Waiting for build id:XXXXX to start...". You can close your terminal now. Check results on [crave](https://foss.crave.io).<br>

## Variables
There are 30 variables, only 3 are required to build custom ROM.

### Required variables
- `codename` - your device's codename<br>
- `lunch` - type of android build: user, userdebug or eng<br>
- `manifest` - link to your manifest with trees, fill this or `trees`<br>
- `trees` - all your device-related repositories, fill this or `manifest`<br>

### Signing
- `sign` - set to true or false<br>
- `keys` - directory with keys<br>

### Uploading
- `server` - SourceForge, BashUpload, PixelDrain. Only these are supported.<br>
- `sfproject` - project name if you're using SourceForge<br>
- `sfdir` - directory to upload to, if you're using SourceForge<br>
- `sfuser` - SourceForge username<br>
- `ssh` - auth file name if you're using SourceForge, read more [here](https://sourceforge.net/p/forge/documentation/SSH%20Keys/#key-generation-openssh). don't use passphrase!<br>

### OTA
For now, only GitHub is supported.<br>
- `ota` - set to true or false<br>
- `githubota` -  repo with OTA jsons, in format: "username/repo"<br>
- `url` - url to raw json OTA file<br>
- `jsonversion` - version of the rom<br>
- `jsonromtype` - type of build<br>
- `downloadurl` - custom url to download, leave empty if you're using `server`<br>
- `gitemail` - public github email<br>
- `gituser` - github username<br>
- `gitbranch` - ota repo branch, leave "main" if you aren't using different branch<br>

### Status
- `telegram` - send info to telegram, set to true or false<br>
- `chat_id` - telegram chat id<br>
- `private_chat_id` - to send BashUpload download link (because the file can be downloaded only once). you can use `chat_id`<br>
- `console` - if true, will show messages printed by this script<br>
- `quiet` -  if true, hide repo tool, github, and other's output, **it doesn't hide script output and build logs**<br>
- `user_id` - your telegram user ID, allows you to kill build task through telegram (`/kill`)

### Secrets
- `githubtoken` - for uploading ota jsons<br>
- `telegramtoken` - required if you want to send info about building to telegram<br>
- `pixeldraintoken` - if you are uploading to pixeldrain, fill this too!<br>

### Unsupported ROMs (only for crave)
- `unsupported` - put repo init command here to sync unsupported by crave rom<br>

### Build settings
- `cleanbuild` - set to true only if you got permission and you need to<br>
