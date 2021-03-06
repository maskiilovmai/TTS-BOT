[![discord](https://img.shields.io/discord/730998659008823296.svg?label=&logo=discord&logoColor=ffffff&color=7389D8&labelColor=6A7EC2)](https://kutt.it/GrenadeGaming)
[![ci-build-status](https://img.shields.io/github/workflow/status/moonstar-x/discord-tts-bot/CI?logo=github)](https://github.com/maskiilovmai/TTS-BOT)
[![open-issues-count](https://img.shields.io/github/issues-raw/moonstar-x/discord-tts-bot?logo=github)](https://github.com/maskiilovmai/TTS-BOT)
[![docker-image-size](https://img.shields.io/docker/image-size/moonstarx/discord-tts-bot?logo=docker)](https://hub.docker.com/repository/docker/moonstarx/discord-tts-bot)
[![docker-pulls](https://img.shields.io/docker/pulls/moonstarx/discord-tts-bot?logo=docker)](https://hub.docker.com/repository/docker/moonstarx/discord-tts-bot)

# Discord TTS Bot

This is a simple TTS Bot that uses the Google Translate TTS API. With this bot you can send Text-to-Speech messages in multiple languages using Google Translate or other TTS engines.

## Requirements

To self-host this bot you'll need the following:

* [git](https://git-scm.com/)
* [node.js](https://nodejs.org/en/) (Version 12.0.0 or higher)
* ffmpeg

**ffmpeg** should be installed by default on Linux and MacOS, in case it isn't, install it with your package manager. For Windows users, head over to [ffmpeg's official website](https://www.ffmpeg.org/download.html#build-windows) to download the binary which will need to be added to your **\$PATH**. If you don't know how to add folders to your **\$PATH**, check out this [guide](https://www.architectryan.com/2018/03/17/add-to-the-path-on-windows-10/).

## Installation

In order to self-host this bot, first you'll need to clone this repository.

```text
git clone https://github.com/maskiilovmai/TTS-BOT.git
```

Install the dependencies with:

```text
npm ci --only=prod
```

Or, if you want to also install the `devDependencies`:

```text
npm install
```

After you have [configured](#configuration) the bot, you can run it with:

```text
npm start
```

## Configuration

Inside the `config` folder, rename the file *settings.json.example* to *settings.json* and edit the file with your own Discord Token and other settings. If you don't have a discord token yet, you can see a guide on how to create it [here](https://github.com/moonstar-x/discord-downtime-notifier/wiki).

Your file should look like this.

```json
{
  "token": "YOUR_DISCORD_TOKEN",
  "prefix": "$",
  "owner_id": "123123123",
  "owner_reporting": false,
  "presence_refresh_interval": 600000,
  "disconnect_timeout": 300000
}
```

You may also configure these options with environment variables. The settings set with the environment variables will take higher precedence than the ones in the config JSON file.

This table contains all the configuration settings you may specify with both environment variables and the JSON config file.

| Environment Variable              | JSON Property               | Required                    | Type               | Description                                                                                                                   |
|-----------------------------------|-----------------------------|-----------------------------|--------------------|-------------------------------------------------------------------------------------------------------------------------------|
| DISCORD_TOKEN                     | `token`                     | Yes.                        | `string`           | The bot's token.                                                                                                              |
| DISCORD_PREFIX                    | `prefix`                    | No. (Defaults to: `$`)      | `string`           | The bot's prefix.                                                                                                             |
| DISCORD_OWNER_ID                  | `owner_id`                  | No. (Defaults to: `null`)   | `string` or `null` | The ID of the bot's owner.                                                                                                    |
| DISCORD_OWNER_REPORTING           | `owner_reporting`           | No. (Defaults to: `false`)  | `boolean`          | Whether the bot should send error reports to the owner via DM when a command errors.                                          |
| DISCORD_PRESENCE_REFRESH_INTERVAL | `presence_refresh_interval` | No. (Defaults to: `900000`) | `number` or `null` | The time interval in ms in which the bot updates its presence. If set to `null` the presence auto update will be disabled.    |
| DISCORD_DISCONNECT_TIMEOUT        | `disconnect_timeout`        | No. (Defaults to: `300000`) | `number` or `null` | The time it takes the bot to leave a voice channel when inactive. If set to `null` the bot will not disconnect on inactivity. |

## Running on Docker

You can start a container with the bot's image by running:

```text
docker run -it -e DISCORD_TOKEN="YOUR DISCORD TOKEN" moonstarx/discord-tts-bot:latest
```

Check [configuration](#configuration) to see which environment variables you can use.

The following volumes can be used:

* `opt/app/config`: The config folder for the bot, here you can use the `settings.json` file to configure the bot if you don't want to use environment variables.

## Deploying to Heroku

To deploy to Heroku, you can click on the image below and login to your account.

Template by [moonstar-x](https://github.com/moonstar-x):

[![Deploy](https://www.herokucdn.com/deploy/button.svg)](https://heroku.com/deploy?template=https://github.com/moonstar-x/discord-tts-bot)

Template by [Maskiilov Mai](https://github.com/maskiilovmai):

[![Deploy](https://www.herokucdn.com/deploy/button.svg)](https://heroku.com/deploy?template=https://github.com/maskiilovmai/TTS-BOT)

You can now go back to your app's *Overview*, make sure you disable the *web* dyno and enable the *bot* dyno. Your bot should now be up and running. Remember you can always check your bot's console if you access the *View Logs* in the *More* dropdown menu.

## Usage

Here's a list of all the commands for the bot:

| Command                 | Alias      | Description                                                                                          |
|-------------------------|------------|------------------------------------------------------------------------------------------------------|
| $say \<message\>        | $s, $tts   | Send a TTS message in your voice channel.                                                            |
| $aeiou \<message\>      | $moonbase  | Send an aeiou (similar to Moonbase Alpha) TTS message in your voice channel.                         |
| $stop                   | $leave     | Stop the TTS bot and leave the channel.                                                              |
| $lang \<lang_code\>     |            | Change the TTS language.                                                                             |
| $langs                  |            | Display a list of the supported languages.                                                           |
| $speed \<slow\|normal\> |            | Change the TTS spoken speed (must be either **normal** for normal speed or **slow** for slow speed). |
| $help                   | $h         | Display a help message with all the available commands.                                              |

> Up until now, these settings are saved in memory, which means if the bot crashes/restarts, all of these settings will go back to default (`Language: Vietnamese, Speed: normal`).

## Language Support

Here's a list of all the supported languages:

| Language Code | Language Name |
|---------------|---------------|
| af            | Afrikaans     |
| hy            | Armenian      |
| id            | Indonesian    |
| bn            | Bengali       |
| ca            | Catalan       |
| cs            | Czech         |
| da            | Danish        |
| de            | German        |
| en            | English       |
| es            | Spanish       |
| fil           | Filipino      |
| fr            | French        |
| hr            | Croatian      |
| is            | Icelandic     |
| it            | Italian       |
| jv            | Javanese      |
| km            | Khmer         |
| lv            | Latvian       |
| hu            | Hungarian     |
| ml            | Malayalam     |
| mr            | Marathi       |
| nl            | Dutch         |
| ne            | Nepali        |
| nb            | Norwegian     |
| pl            | Polish        |
| pt            | Portuguese    |
| ro            | Romanian      |
| si            | Sinhala       |
| sk            | Slovak        |
| su            | Sundanese     |
| sw            | Swahili       |
| fi            | Finnish       |
| sv            | Swedish       |
| ta            | Tamil         |
| te            | Telugu        |
| vi            | Vietnamese    |
| tr            | Turkish       |
| el            | Greek         |
| ru            | Russian       |
| sr            | Serbian       |
| uk            | Ukranian      |
| ar            | Arabic        |
| hi            | Hindi         |
| th            | Thai          |
| ko            | Korean        |
| cmn           | Chinese       |
| ja            | Japanese      |

## Screenshot

Help Pannel:

<div align="center"><img src="/src/screenshot/help.png"></div>

Languages Support:

<div align="center"><img src="/src/screenshot/lang1.png"></div><div align="center"><img src="/src/screenshot/lang2.png"></div>

## Add this bot to your server

You can add Takagi bot (created by [Maskiilov Mai](https://github.com/maskiilovmai)) to your server by clicking the image below:

[![Invite this bot to your server](https://raw.githubusercontent.com/maskiilovmai/images/main/Ichigyou.jpg)](https://discord.com/api/oauth2/authorize?client_id=902168707277656064&permissions=8&scope=bot)

## Author
This source code by [moonstar-x/discord-tts-bot](https://github.com/moonstar-x/discord-tts-bot).
This bot was made by [Maskiilov Mai](https://github.com/maskiilovmai).
