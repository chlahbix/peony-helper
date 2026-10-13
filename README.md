# Helper — a prefix + slash Discord bot

**Helper** is a self-contained Discord utility bot with **155 commands** across **15 categories**:

- **prefix** — everything, `!help` by default (per-server configurable with the `prefix` command, mentioning the bot also works)
- **slash** — the 7 **setup commands only**: `/verify-setup`, `/apply-setup`, `/ticket-setup`, `/selfrole-setup`, `/jail-setup`, `/welcome-setup`, `/starboard-setup`

It covers verification, staff applications, clans, tickets, self-roles, moderation, a jail system, premium features and a large set of fun/information commands.

Built with [discord.js](https://discord.js.org) v14. No database server required — everything is stored in a local JSON file.

---

## Quick start

1. **Install dependencies**

   ```powershell
   npm install
   ```

2. **Add your bot token**

   Copy `.env.example` to `.env` and fill it in (recommended):

   ```env
   DISCORD_TOKEN=your-bot-token-here
   OWNERS=your-user-id,another-user-id
   ```

   …or put the token in `config.json` → `"token"`.

3. **Run the bot**

   ```powershell
   npm start
   ```

4. **Invite the bot** — use the `invite` command (or the [Discord OAuth2 page](https://discord.com/oauth2/authorize)) with the permissions your server needs.

> **Important:** enable the **Message Content** and **Server Members** privileged intents for your bot in the Discord Developer Portal → Bot → Privileged Gateway Intents. The bot will not read prefix commands without Message Content.

---

## Configuration (`config.json`)

| Key               | Description                                                     |
| ----------------- | --------------------------------------------------------------- |
| `prefix`          | Default prefix, e.g. `"!"` (each server can override with `prefix`) |
| `token`           | Bot token (can be overridden by the `DISCORD_TOKEN` env var)    |
| `ownerIds`        | User IDs allowed to run `ownerOnly` commands                    |
| `embedColor`      | Default embed colour                                            |
| `colors`          | Per-purpose colours (success, error, warning, premium, …)       |
| `cooldownSeconds` | Default per-command cooldown                                    |
| `help.title`      | Heading of the help panel, e.g. `"◇ Peony Helper"` (empty = bot name) |
| `help.intro`      | Intro line of the help panel (empty = a generic intro)          |
| `help.banner`     | Banner image/GIF URL for the panel (empty = the bot avatar)     |
| `slash.enabled`   | Register the slash commands on startup (default `true`)         |
| `slash.global`    | Register them globally — up to an hour to appear (default `true`) |
| `slash.guilds`    | Guild IDs that get the commands registered instantly (testing)  |

---

## Commands (155)

| Category | Count | Commands |
| --- | --- | --- |
| 🛡️ **Verification** | 8 | `verify-setup` `verify` `verify-role` `verify-channel` `verify-log` `verify-info` `verify-disable` `verifypass` |
| 📋 **Apply** | 4 | `apply-setup` `apply` `apply-role` `apply-review` |
| ⚔️ **Clans** | 19 | `clan-create` `clan-info` `clan-invite` `clan-invites` `clan-join` `clan-leave` `clan-kick` `clan-promote` `clan-demote` `clan-members` `clan-leaderboard` `clan-points` `clan-addpoints` `clan-setleader` `clan-rename` `clan-icon` `clan-search` `clan-reset` `clan-claim` |
| 💎 **Premium** | 18 | `premium-activate` `premium-generate` `premium-revoke` `premium-info` `premium-status` `premium-list` `premium-perks` `welcome-setup` `welcome-disable` `autorole` `embed` `giveaway` `giveaway-reroll` `starboard-setup` `tag` `tag-create` `tag-delete` `reactionrole` |
| 🔍 **Checker** | 7 | `voice-check` `voice-list` `server-check` `user-check` `invite-check` `channel-check` `role-check` |
| 🛠️ **Admin Tools** | 9 | `slowmode` `lock` `unlock` `hide` `unhide` `moveall` `nuke` `announce` `lockdown` |
| 🎖️ **Roles** | 4 | `addrole` `removerole` `roles` `role-color` |
| 🔊 **Voice** | 4 | `join` `disconnect` `move` `vlock` |
| 🎫 **Ticket Setup** | 5 | `ticket-setup` `ticket-log` `ticket-limit` `ticket-close` `ticket-disable` |
| 🧩 **Selfrole Setup** | 6 | `selfrole-setup` `selfrole-add` `selfrole-remove` `selfrole-list` `selfrole-info` `selfrole-delete` |
| ℹ️ **Information** | 12 | `serverinfo` `userinfo` `membercount` `avatar` `banner` `roleinfo` `channelinfo` `botinfo` `uptime` `ping` `invite` `boosts` |
| 🧰 **General Tools** | 5 | `help` `prefix` `afk` `remind` `calc` |
| 🎮 **Fun Tools** | 26 | `8ball` `coinflip` `dice` `choose` `rate` `ship` `pp` `joke` `fact` `quote` `wouldyourather` `truth` `dare` `slot` `emojify` `mock` `reverse` `vaporwave` `say` `hug` `slap` `kiss` `pat` `poke` `wave` `highfive` |
| 🛡 **Moderation** | 16 | `ban` `unban` `kick` `mute` `unmute` `timeout` `untimeout` `warn` `warns` `warninfo` `clearwarns` `purge` `nick` `massban` `softban` `modlogs` |
| 🔒 **Jail** | 12 | `jail-setup` `jail-disable` `jail` `unjail` `unjail-all` `jail-list` `jail-info` `jail-role` `jail-channel` `jail-log` `jail-time` `jail-history` |

**`!help`** posts a modern **component-v2 panel**: heading, intro text, the prefix/category/command stats line, a banner gallery and a **category select menu** — picking a category expands its full command list inside the same panel. The panel's branding (title, intro, banner) lives in `config.json` → `help`.

**`!help <category>`** opens the panel with that category already expanded, and **`!help <command>`** shows the detailed embed (usage, aliases, permissions, cooldown, premium).

---

## Slash commands (setup only)

Slash is intentionally limited to the **7 setup commands**, so admins get proper pickers (role, channel, drop-downs) where it matters most. Everything else is prefix-only.

| Slash command | What it configures |
| --- | --- |
| `/verify-setup` | verification panel |
| `/apply-setup` | staff application panel |
| `/ticket-setup` | ticket panel |
| `/selfrole-setup` | self-role panel |
| `/jail-setup` | jail system |
| `/welcome-setup` | welcome message (premium) |
| `/starboard-setup` | starboard (premium) |

- **Typed options are generated automatically** from each command's `usage` string: `<@user>` → user picker, `<@role>` → role picker, `[#channel]` → channel picker, `<1-100>` → integer with min/max, `<approve|deny>` and `[on|off]` → dropdowns, everything else free text.
- **One source of truth**: the slash adapter converts the resolved options back into the exact `(message, args)` pair every command's `execute` expects, so all checks (owner, premium, permissions, cooldown) are enforced centrally in `src/utils/commandChecks.js`.
- **Prefix equivalents still work** — `/verify-setup` and `!verify-setup` run the very same command object.

**Registration** happens automatically on startup:

- **Global** (default): visible in every server, but Discord can take up to an hour to propagate.
- **Instant**: add server IDs to `config.json` → `"slash": { "guilds": ["123…"] }` or set `SLASH_GUILDS=123…` in `.env` — useful while testing.

---

## Project structure

```
helper/
├── index.js                  # Entry point: client, intents, login, safety nets
├── config.json               # Prefix, colours, owners, cooldowns, help branding, slash settings
├── .env                      # Token (copy from .env.example)
├── package.json              # Scripts + dependencies
├── scripts/
│   ├── validate.js           # Syntax + structure + per-category command counts
│   └── smoke.js              # Executes every command against mocked Discord objects
├── data/
│   └── database.json         # Auto-created at runtime (guild settings, clans, jails, …)
└── src/
    ├── categories.js         # Category display metadata (emoji, name, description)
    ├── commands/             # One file per category — each exports an array of commands
    │   ├── verification.js   ├── apply.js      ├── clans.js      ├── premium.js
    │   ├── checker.js        ├── admin.js      ├── roles.js      ├── voice.js
    │   ├── ticket.js         ├── selfrole.js   ├── information.js├── general.js
    │   ├── fun.js            ├── moderation.js └── jail.js
    ├── events/
    │   ├── ready.js               # Presence, scheduler start-up, slash registration
    │   ├── messageCreate.js       # Prefix parsing, permissions, cooldowns, AFK
    │   ├── interactionCreate.js   # Slash commands + dispatches buttons/selects/modals
    │   ├── guildMemberAdd.js      # Welcome message + autorole (premium)
    │   └── messageReactionAdd.js  # Starboard + reaction roles (premium)
    ├── handlers/
    │   ├── commandHandler.js      # Loads src/commands/* (single object or array)
    │   ├── slashHandler.js        # Registers + handles /commands (shared gate)
    │   └── eventHandler.js        # Loads src/events/*
    └── utils/
        ├── database.js        # JSON store with dot-paths (debounced writes, safe flush)
        ├── embed.js           # Coloured embed builders
        ├── helpers.js         # Args parsing, durations, resolvers, prefix, usage errors
        ├── commandChecks.js   # Shared owner/premium/permission/cooldown gate
        ├── permissions.js     # Permission + hierarchy checks
        ├── premium.js         # Premium status, keys, grant/revoke
        ├── scheduler.js       # Persistent delayed jobs (reminders, giveaways, jail time)
        ├── slashDefinitions.js# Builds /commands + typed options from usage strings
        ├── slashAdapter.js    # Turns a slash interaction into (message, args)
        └── interactions.js    # Registry for button/select handlers
```

### Adding a command

Create or edit a file in `src/commands/` (the file name becomes the category) and append an object:

```js
module.exports = [
  {
    name: 'ping',
    aliases: ['latency'],
    description: 'Show the bot latency.',
    usage: '',                       // '' when the command takes no arguments
    permissions: ['ManageGuild'],    // optional - checked automatically
    botPermissions: ['EmbedLinks'],  // optional - checked automatically
    premium: false,                  // optional - requires active premium
    cooldown: 5,                     // seconds
    async execute(message, args, client) {
      return message.reply({ embeds: [/* embeds.info(...) */] });
    },
  },
];
```

Permissions, ownership, premium status and cooldowns are enforced centrally by `src/utils/commandChecks.js` (used by both `src/events/messageCreate.js` and `src/handlers/slashHandler.js`), so `execute` can focus on the command itself.

The `usage` string does double duty: it documents the command for `help` AND generates the typed slash options automatically — `<@user>` becomes a user picker, `<#channel>` a channel picker, `[reason]` an optional text field, and so on. Every command is reachable by prefix; a command named `…-setup` is additionally exposed as a top-level slash command for free.

---

## Notable features

- **Prefix + setup slash** — everything runs as `!command`; the 7 setup commands are also top-level slash (`/verify-setup`) with typed pickers, running the identical command object with the same checks and cooldowns.
- **Help panel** — `help` renders a component-v2 panel (heading, intro, banner, category select menu) that expands the chosen category in place; branding is configurable in `config.json` → `help`.
- **Verification** — panel button or `verify` command, staff `verifypass`, log channel.
- **Applications** — `apply-setup [#review-channel] [@manager-role]` posts a panel listing five staff positions (**Staff Team**, **Event Hoster**, **Designer**, **Partnership**, **Developer**), each with its own button. A button opens a modal form for that position (name, age, relevant experience, motivation, daily availability). Submissions are posted to the application log channel as an embed (avatar, applicant ID, position, age, availability, relative submit time, the experience/motivation answers as blockquotes) with **Accept / Refuse** buttons; the manager role is shown in the message and the "Attention Managers" field with `allowedMentions: { parse: [] }`, so the mention displays but never notifies anyone. On approval the position's role is granted if one is linked with `apply-role <position> <@role>`. Staff can also use `apply-review <approve|deny> <@user>`.
- **Clans** — invites, ranks, points, leaderboards, daily `clan-claim`.
- **Tickets** — panel button creates a private channel with staff access, `ticket-close` logs and deletes it, per-user limits.
- **Self-roles** — select-menu panel built with `selfrole-add`.
- **Jail** — strips & later restores roles, hides every channel, optional auto-release via `jail-time` (survives restarts).
- **Premium** — key system (`premium-generate` / `premium-activate`) unlocking welcome/autorole, custom embeds, giveaways, starboard, tags and reaction roles.
- **Scheduler** — reminders, giveaway endings and jail releases are stored on disk and re-armed after a restart.
- **Data** — everything lives in `data/database.json`; edits are debounced and flushed on shutdown.

---

## Scripts

```powershell
npm run check   # syntax + structure + exact command counts (155) + slash definitions
npm run smoke   # runs every command against mocked Discord objects (direct + setup-slash pipeline)
npm test        # both of the above
npm run dev     # start with auto-reload on file changes
```

---

## Notes

- **Slash registration** — global commands can take up to an hour to appear after the first start; use `slash.guilds` (or `SLASH_GUILDS`) for instant per-server registration while testing.
- **Voice** — `join` connects the bot to your channel using `@discordjs/voice` (with `libsodium-wrappers`); audio playback is not included.
- **Permissions** — the bot needs the permissions each command declares; the `help <command>` view lists them.
- **Safety** — hierarchy checks (`perms.canModerate` / `canManageRole`) prevent moderating members or roles above the invoker or the bot.
- **Owner commands** — `premium-generate`, `premium-revoke`, `premium-list` are limited to `ownerIds`.
