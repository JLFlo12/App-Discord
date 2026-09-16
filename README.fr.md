<div align="center">

# 🤖 Flo_exe

**Bot Discord tout-en-un : modération, informations sur le serveur et système d'économie**

[🇬🇧 English](README.md) · 🇫🇷 Français

![discord.js](https://img.shields.io/badge/discord.js-v13-5865F2?logo=discorddotjs&logoColor=white)
![Node.js](https://img.shields.io/badge/Node.js-16.x-5FA04E?logo=nodedotjs&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?logo=javascript&logoColor=black)
![SQLite](https://img.shields.io/badge/quick.db-SQLite-003B57?logo=sqlite&logoColor=white)
![Licence : MIT](https://img.shields.io/badge/Licence-MIT-yellow.svg)

</div>

---

## Présentation

**Flo_exe** est un bot Discord personnel écrit en JavaScript avec **discord.js v13**. Il propose une quarantaine de commandes slash, réparties en trois catégories (général, modération et économie), ainsi que des commandes à préfixe. Il génère aussi des cartes en image pour le profil des utilisateurs et pour le bot lui-même.

> [!NOTE]
> C'est un projet plus ancien. discord.js v13 n'est plus maintenu, donc certaines commandes peuvent demander des ajustements pour fonctionner avec les versions récentes de l'API Discord (une migration vers discord.js v14 est conseillée).

## Fonctionnalités

- 🛡️ **Modération** : bannissement, expulsion, mute, timeout, suppression de messages en masse, verrouillage et masquage de salons, mode lent, gestion des rôles
- ℹ️ **Informations** : serveur, membres, salons, emojis, rôles, avatar et bannière des utilisateurs
- 💰 **Économie** : porte-monnaie et banque, récompenses quotidiennes et hebdomadaires, dépôts, retraits, virements, classement, bio
- 🖼️ **Cartes en image** : carte de profil (avatar, bio, solde) et carte du bot, générées avec `canvas-constructor`
- 💤 **Mode AFK** : le statut AFK est retiré automatiquement dès que l'utilisateur envoie un message
- 🚫 **Anti-bot** : expulse automatiquement les bots qui rejoignent le serveur (activable par le propriétaire du serveur)
- ⛔ **Liste noire** : empêche certains utilisateurs d'utiliser une partie des commandes du bot
- ⚙️ **Préfixe personnalisable** par serveur (par défaut : `!`)

## Commandes

Tapez `/help` dans Discord pour afficher toutes les commandes slash.

<details>
<summary><b>ℹ️ Général (13)</b></summary>

| Commande | Description |
| --- | --- |
| `/help` | Liste toutes les commandes |
| `/ping` | Latence de l'API, latence des messages et temps de fonctionnement |
| `/bot` | Carte d'informations du bot |
| `/server` | Informations sur le serveur |
| `/members` | Nombre de membres (humains / bots) |
| `/channels` | Liste des salons par type (texte, vocal, catégorie) |
| `/channel-info` | Informations sur un salon |
| `/emojis` | Liste des emojis du serveur |
| `/user` | Informations sur un utilisateur (dates d'arrivée, ID…) |
| `/avatar` | Affiche l'avatar d'un utilisateur |
| `/banner` | Affiche la bannière d'un utilisateur |
| `/profile` | Carte de profil d'un utilisateur (image) |
| `/afk` | Vous passe en AFK, avec une raison facultative |

</details>

<details>
<summary><b>🛡️ Modération (17)</b></summary>

| Commande | Description |
| --- | --- |
| `/ban` · `/unban` | Bannit ou débannit un utilisateur |
| `/kick` | Expulse un utilisateur du serveur |
| `/mute` · `/unmute` | Empêche un membre d'envoyer des messages, ou le lui permet à nouveau |
| `/timeout` · `/untimeout` | Applique ou retire un timeout Discord |
| `/clear` | Supprime plusieurs messages d'un coup |
| `/lock` · `/unlock` | Verrouille ou déverrouille un salon textuel |
| `/hide` · `/show` | Masque ou affiche un salon |
| `/slow_mode` · `/slow_mode_remove` | Active ou désactive le mode lent |
| `/role` | Donne un rôle à un utilisateur ou le lui retire |
| `/roleinfo` | Informations sur un rôle |

</details>

<details>
<summary><b>💰 Économie (11)</b></summary>

| Commande | Description |
| --- | --- |
| `/balance` | Affiche le solde du porte-monnaie et de la banque |
| `/bankpro` | Affiche le profil bancaire d'un utilisateur |
| `/daily` | Récupère la récompense quotidienne |
| `/weekly` | Récupère la récompense hebdomadaire |
| `/deposit` | Dépose de l'argent du porte-monnaie à la banque |
| `/withdraw` | Retire de l'argent de la banque vers le porte-monnaie |
| `/transfer` | Envoie de l'argent à un autre utilisateur |
| `/leaderboard` | Classement des membres les plus riches |
| `/setbio` | Définit la bio affichée sur votre profil |
| `/addmoney` | Ajoute de l'argent à un utilisateur (propriétaire du bot uniquement) |
| `/removemoney` | Retire de l'argent à un utilisateur (administrateurs) |

</details>

<details>
<summary><b>⌨️ Commandes à préfixe uniquement</b></summary>

Ces commandes utilisent le préfixe du serveur (`!` par défaut). Certaines reprennent des commandes slash.

| Commande | Permission | Description |
| --- | --- | --- |
| `!setprefix <préfixe>` | Administrateur | Change le préfixe du bot sur le serveur |
| `!antibots on` · `!antibots off` | Propriétaire du serveur | Active ou désactive la protection anti-bot |
| `!blacklist @user` · `!unblacklist @user` | Administrateur | Ajoute un utilisateur à la liste noire ou l'en retire |
| `!roles @user` | Administrateur | Liste les rôles d'un membre |
| `!tax <montant>` | — | Calcule une taxe de 5,3 % sur un montant |
| `!top` | — | Classement des porte-monnaie |
| `!pbank [@user]` | — | Profil bancaire |

</details>

## Installation

### Prérequis

- [Node.js](https://nodejs.org/) **16.x** (exigé par discord.js v13)
- Les outils de compilation des modules natifs (`canvas`, `better-sqlite3`) :
  - Windows : Visual Studio Build Tools (*Développement Desktop en C++*) et Python
  - Linux : `build-essential`, `libcairo2-dev`, `libpango1.0-dev`, `libjpeg-dev`, `libgif-dev`
- Une application Discord créée sur le [Developer Portal](https://discord.com/developers/applications)

### 1. Créer le bot sur Discord

1. Sur le Developer Portal, créez une application, ouvrez l'onglet **Bot** et copiez le **token**.
2. Dans **Privileged Gateway Intents**, activez **Presence Intent**, **Server Members Intent** et **Message Content Intent**.
3. Invitez le bot avec les scopes `bot` et `applications.commands` (OAuth2 → URL Generator) et les permissions nécessaires (par ex. *Administrateur* pour les tests).

### 2. Installer et configurer

```bash
git clone https://github.com/JLFlo12/App-Discord.git
cd App-Discord/Flo_exe
npm install
```

Créez un fichier `.env` dans `Flo_exe/` :

```env
token=VOTRE_TOKEN_DE_BOT
```

> [!IMPORTANT]
> - Le nom de la variable est `token`, en **minuscules**.
> - Ne committez jamais le fichier `.env` : toute personne qui a le token contrôle le bot.
> - `/addmoney` est réservé à un ID de propriétaire écrit en dur dans `SlashCommands/economy/addmoney.js`. Remplacez-le par votre propre ID Discord.

### 3. Lancer le bot

```bash
node index.js
```

Au démarrage, le bot :

- enregistre les commandes slash de façon globale (`[ / Commands ]: Pushed` dans la console) ;
- lance un petit serveur web **Express** sur le port **3000**, qui répond « Hello World ». Un service de monitoring peut l'appeler régulièrement pour garder le bot éveillé sur des hébergeurs comme Replit.

## Structure du projet

```
Flo_exe/
├── index.js               # Point d'entrée : client, commandes à préfixe, anti-bot, serveur Express
├── handlers/
│   └── index.js           # Charge et enregistre les commandes slash, gère les interactions et l'AFK
├── SlashCommands/
│   ├── general/           # Commandes d'information
│   ├── mod/               # Commandes de modération
│   └── economy/           # Commandes d'économie
├── utils/
│   └── afk.js             # Liste AFK en mémoire
├── All_Files/
│   ├── functions.js       # Fonctions utilitaires
│   ├── prefix.json        # Inutilisé (les préfixes sont stockés dans quick.db)
│   ├── antibots.json      # État de l'anti-bot par serveur
│   ├── profilee.png       # Fond de la carte de profil
│   └── bot.png            # Fond de la carte du bot
├── json.sqlite            # Base quick.db (préfixes, soldes, bios, liste noire…)
├── replit.nix             # Configuration Replit (Node.js 16)
└── package.json
```

## Licence

Ce projet est distribué sous [licence MIT](LICENSE).
