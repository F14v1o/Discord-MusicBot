# Discord Music Bot

A small Discord music bot in Python. It streams audio from YouTube into a voice channel, keeps a per-server queue and leaves the channel when nobody is listening.

## Commands

| Command | What it does |
|---|---|
| `!join` | Join your current voice channel |
| `!leave` | Leave the voice channel |
| `!play <url or search>` | Play a track, or queue it if something is already playing |
| `!pause` / `!resume` | Pause or resume the current track |
| `!skip` | Skip to the next track in the queue |
| `!stop` | Stop playback and clear the queue |

## Setup

1. Install FFmpeg (`sudo apt install ffmpeg` on Debian/Ubuntu, `brew install ffmpeg` on macOS).
2. Install the Python dependencies:

   ```bash
   pip install -r requirements.txt
   ```

3. Create a bot in the [Discord Developer Portal](https://discord.com/developers/applications): add a bot user, enable the **Message Content** intent, and invite it to your server with the `bot` scope and the permissions *View Channels*, *Send Messages*, *Connect* and *Speak*.
4. Put the token into a `.env` file (never commit it):

   ```bash
   cp .env.example .env
   # edit .env and paste your token
   ```

5. Run it:

   ```bash
   python music_bot.py
   ```

## Running it 24/7

On any small Linux VM the bot runs fine inside `tmux`:

```bash
tmux new -s musicbot
python3 music_bot.py
# detach with Ctrl+B, then D; reattach with: tmux attach -t musicbot
```

For a proper setup use a systemd service instead, so the bot restarts after reboots.

## Notes

- If YouTube asks for a login on some videos, yt-dlp can use a `cookies.txt` exported from your browser. The bot picks it up automatically if the file exists; it is git-ignored.
- Audio is streamed, not stored.
