<div align="center">

# 🤖 Flo_exe

**All-in-one Discord bot: moderation, server info and an economy system**

🇬🇧 English · [🇫🇷 Français](README.fr.md)

![discord.js](https://img.shields.io/badge/discord.js-v13-5865F2?logo=discorddotjs&logoColor=white)
![Node.js](https://img.shields.io/badge/Node.js-16.x-5FA04E?logo=nodedotjs&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?logo=javascript&logoColor=black)
![SQLite](https://img.shields.io/badge/quick.db-SQLite-003B57?logo=sqlite&logoColor=white)
![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)

</div>

---

## About

**Flo_exe** is a personal Discord bot written in JavaScript with **discord.js v13**. It includes about forty slash commands, split into three categories (general, moderation and economy), plus prefix-based commands. It also generates image cards for user profiles and for the bot itself.

> [!NOTE]
> This is an older project. discord.js v13 is no longer maintained, so some commands may need updating to work with recent versions of the Discord API (migrating to discord.js v14 is recommended).

## Features

- 🛡️ **Moderation**: ban, kick, mute, timeout, bulk message deletion, channel lock/hide, slow mode, role management
- ℹ️ **Information**: server, members, channels, emojis, roles, user avatar and banner
- 💰 **Economy**: wallet and bank, daily/weekly rewards, deposits, withdrawals, transfers, leaderboard, bio
- 🖼️ **Image cards**: profile card (avatar, bio, balance) and bot card, generated with `canvas-constructor`
- 💤 **AFK mode**: the AFK status is removed automatically when the user sends a message
- 🚫 **Anti-bot**: automatically kicks bots that join the server (server owner can turn it on or off)
- ⛔ **Blacklist**: stops certain users from using some of the bot's commands
- ⚙️ **Custom prefix** per server (default: `!`)

## Commands

Type `/help` in Discord to see every slash command.

<details>
<summary><b>ℹ️ General (13)</b></summary>

| Command | Description |
| --- | --- |
| `/help` | Lists all commands |
| `/ping` | API latency, message latency and uptime |
| `/bot` | Bot information card |
| `/server` | Server information |
| `/members` | Member count (humans / bots) |
| `/channels` | Lists channels by type (text, voice, category) |
| `/channel-info` | Information about a channel |
| `/emojis` | Lists the server's emojis |
| `/user` | Information about a user (join dates, ID…) |
| `/avatar` | Shows a user's avatar |
| `/banner` | Shows a user's banner |
| `/profile` | User profile card (image) |
| `/afk` | Sets you as AFK, with an optional reason |

</details>

<details>
<summary><b>🛡️ Moderation (17)</b></summary>

| Command | Description |
| --- | --- |
| `/ban` · `/unban` | Bans or unbans a user |
| `/kick` | Kicks a user from the server |
| `/mute` · `/unmute` | Stops a member from sending messages, or lets them again |
| `/timeout` · `/untimeout` | Applies or removes a Discord timeout |
| `/clear` | Deletes several messages at once |
| `/lock` · `/unlock` | Locks or unlocks a text channel |
| `/hide` · `/show` | Hides or shows a channel |
| `/slow_mode` · `/slow_mode_remove` | Enables or disables slow mode |
| `/role` | Gives a role to a user or removes it |
| `/roleinfo` | Information about a role |

</details>

<details>
<summary><b>💰 Economy (11)</b></summary>

| Command | Description |
| --- | --- |
| `/balance` | Shows your wallet and bank balance |
| `/bankpro` | Shows a user's bank profile |
| `/daily` | Claims the daily reward |
| `/weekly` | Claims the weekly reward |
| `/deposit` | Moves money from your wallet to the bank |
| `/withdraw` | Moves money from the bank to your wallet |
| `/transfer` | Sends money to another user |
| `/leaderboard` | Richest members |
| `/setbio` | Sets the bio shown on your profile |
| `/addmoney` | Adds money to a user (bot owner only) |
| `/removemoney` | Removes money from a user (admins) |

</details>

<details>
<summary><b>⌨️ Prefix-only commands</b></summary>

These commands use the server prefix (`!` by default). Some of them repeat slash commands.

| Command | Permission | Description |
| --- | --- | --- |
| `!setprefix <prefix>` | Administrator | Changes the bot's prefix on the server |
| `!antibots on` · `!antibots off` | Server owner | Turns anti-bot protection on or off |
| `!blacklist @user` · `!unblacklist @user` | Administrator | Adds a user to the blacklist or removes them |
| `!roles @user` | Administrator | Lists a member's roles |
| `!tax <amount>` | — | Calculates a 5.3% tax on an amount |
| `!top` | — | Wallet leaderboard |
| `!pbank [@user]` | — | Bank profile |

</details>

## Getting started

### Prerequisites

- [Node.js](https://nodejs.org/) **16.x** (required by discord.js v13)
- Build tools for native modules (`canvas`, `better-sqlite3`):
  - Windows: Visual Studio Build Tools (*Desktop development with C++*) and Python
  - Linux: `build-essential`, `libcairo2-dev`, `libpango1.0-dev`, `libjpeg-dev`, `libgif-dev`
- A Discord application created in the [Developer Portal](https://discord.com/developers/applications)

### 1. Create the bot on Discord

1. In the Developer Portal, create an application, then open the **Bot** tab and copy the **token**.
2. Under **Privileged Gateway Intents**, turn on **Presence Intent**, **Server Members Intent** and **Message Content Intent**.
3. Invite the bot with the `bot` and `applications.commands` scopes (OAuth2 → URL Generator) and the permissions it needs (e.g. *Administrator* for testing).

### 2. Install and configure

```bash
git clone https://github.com/JLFlo12/App-Discord.git
cd App-Discord/Flo_exe
npm install
```

Create a `.env` file in `Flo_exe/`:

```env
token=YOUR_BOT_TOKEN
```

> [!IMPORTANT]
> - The variable name is `token`, in **lowercase**.
> - Never commit the `.env` file: anyone with the token controls the bot.
> - `/addmoney` is limited to one owner ID hard-coded in `SlashCommands/economy/addmoney.js`. Replace it with your own Discord ID.

### 3. Start the bot

```bash
node index.js
```

At startup, the bot:

- registers the slash commands globally (`[ / Commands ]: Pushed` in the console);
- starts a small **Express** web server on port **3000**, which replies "Hello World". An uptime service can ping it to keep the bot awake on hosts such as Replit.

## Project structure

```
Flo_exe/
├── index.js               # Entry point: client, prefix commands, anti-bot, Express server
├── handlers/
│   └── index.js           # Loads and registers slash commands, handles interactions and AFK
├── SlashCommands/
│   ├── general/           # Information commands
│   ├── mod/               # Moderation commands
│   └── economy/           # Economy commands
├── utils/
│   └── afk.js             # In-memory AFK list
├── All_Files/
│   ├── functions.js       # Helper functions
│   ├── prefix.json        # Unused (prefixes are stored in quick.db)
│   ├── antibots.json      # Anti-bot status per server
│   ├── profilee.png       # Profile card background
│   └── bot.png            # Bot card background
├── json.sqlite            # quick.db database (prefixes, balances, bios, blacklist…)
├── replit.nix             # Replit configuration (Node.js 16)
└── package.json
```

## License

This project is released under the [MIT License](LICENSE).
