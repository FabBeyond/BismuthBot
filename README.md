# Bismuth

Bismuth is an open-source, 100% free, general purpose discord bot just like MEE6, Dyno, etc.

Its currently still in very early alpha but the website can be found at https://bismuth.fabbeyond.dev
Please not that inviting doesnt even work at all right now but it will be fixed soon.

## Requirements

- Python 3.10+
- PostgreSQL
- A Discord application with a bot ([Developer Portal](https://discord.com/developers/applications))

## Discord setup

1. Create an application in the Developer Portal and add a bot.
2. Under **Bot**, turn on **Server Members Intent**.
3. Copy the bot token.
4. Invite the bot to a test server: **OAuth2 → URL Generator**, tick the scopes `bot` and `applications.commands`, tick **Manage Roles**, then open the generated URL.

## Database setup

Create a database and a user:

```sql
CREATE USER bismuth WITH PASSWORD 'yourpassword';
CREATE DATABASE bismuth OWNER bismuth;

You don't need to create any tables. The bot runs the migrations in `db/migrations/` when it starts.

## Running locally

```bash
git clone https://github.com/FabBeyond/BismuthBot.git
cd BismuthBot

python -m venv .venv
source .venv/bin/activate        # Windows: .venv\Scripts\activate
pip install -r requirements.txt
```

Create a `.env` file in the project root:

```env
DISCORD_TOKEN=your-bot-token
DATABASE_URL=postgresql://bismuth:yourpassword@localhost:5432/bismuth
```

Start the bot:

```bash
python bot.py
```

Start it from the project root, because the bot loads `cogs/` and `db/migrations/` by relative path.

When everything works, the log shows each cog being loaded, followed by `Ready as <bot name>`.

## Troubleshooting

| Error | Fix |
|---|---|
| `PrivilegedIntentsRequired` | Turn on **Server Members Intent** in the Developer Portal |
| `Connection refused` / `password authentication failed` | Check that PostgreSQL is running and `DATABASE_URL` is correct |
| `KeyError: 'DISCORD_TOKEN'` | `.env` is missing, or you started the bot from a different folder |

## Related projects

- [Bismuth API](https://github.com/FabBeyond/BismuthApi): backend for the dashboard
- [Bismuth Website](https://github.com/FabBeyond/BismuthWebsite): the dashboard frontend
