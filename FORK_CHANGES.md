# This fork's changes compared to main STK

I could forget something.

## Major features

* Possibility to have a proper Grand Prix server: doesn't become private after the start, players can use different karts in different races, players can join or leave, added custom scoring, in-game (short) and in-lobby (longer) standings.
* Possibility to play a Gnu Elimination.
* Soccer tournament mode: the first mode to have players colored in 3 colors, enforces rules of soccer tournament provided in config file. The number of matches, their duration, team colors, allowed arenas, tournament teams, special labels can be changed. Referees have multiple commands to control the game flow.
* Possibility to have a table of records for racing servers and notify a player if he has beaten a record.
* Possibility to record ghost replays on a server if the player agrees.
* Angry owner mode: with password available only to owner, the owner can become invulnerable to kicks and kick (or temporarily ban) annoying players even being not a crowned player. There are also some other functions like forbidding to start the game.
* Possibility to force players to have certain number of certain addons (karts, tracks, battle arenas and/or soccer fields) to enter the server.
* Possibility to send messages only to certain players.
* /teamchat: a command that makes messages to be received only by teammates in team-based gamemodes. Unlike built-in button (that appeared much later), works also in the lobby.
* Auto spectating mode (/spectate) slightly differs from the main STK and is actively used in servers on which not all players are intended to play.
* Possibility to make a server where only the crowned player can play.

## Minor features

* Possibility to provide information to players using /help command without making server description long.
* Possibility to force players to have certain tracks/arenas to enter the server.
* Possibility to enable (or disable) only a fixed subset of tracks/arenas on the server.
* Possibility to have a server with fixed lap count (up to 255) and/or fixed number of goals/duration of soccer game.
* Possibility to forbid certain difficulties and/or modes on a configurable server.
* Possibility to create chat-only server.
* Possibility to disable kicks on a server with crowned player.
* Possibility for players to send a message to the server owner (works like a report in the database), and for the server owner to send one-time messages to certain players.
* Possibility to store the facts of one player kicking another in a database with reports.
* Possibility to have "unfair teams" in team-based gamemodes (like 1 vs 7).
* Possibility to predefine the first several tracks played on the server.
* Possibility to allow a predefined list of players to enter anything as a password for a private server.
* Possibility to not show mobile icons near players' names.
* Possibility to get rid of own goals and replace most of them with normal goals using the principle "the scorer is the one who touched last from the scoring team".
* max-moveable-objects is changed to 30 to allow tracks like bowling to work.
* Servers try to reset to initial mode and difficulty when all players are gone (doesn't work if players quit mid-race for now).

## Commands

Standard STK server commands work in the same way, with the exception of `/spectate`, which toggles your autospectate state on and off, and the game does *not* start if all players want to spectate.

* `/standings [gp|gnu]` - a command to show the standings of an ongoing Grand Prix or Gnu elimination. One can specify which standings to show in the (rare) case when there are both.
* `/gnu [kart_id]` - starts a Gnu elimination with Gnu kart (or another kart if specified).
* `/nognu` - stops a Gnu elimination.
* `/record (track_id) (time-trial|normal) (normal|reverse) (laps)` - finds the best time in the database corresponding to the specified race settings.
* `/replay (0|1)` - tells the server to record or to not record a ghost replay.
* `/to [player] [...] [player]` - forces the server to send your messages only to specified players. A lock emoji is displayed in case the message is not sent to everyone.
* `/public` - erases `/to` limitations.
* `/teamchat` - forces the server to send your messages only to your teammates in soccer and CTF modes. Note that there is an official GUI alternative, but it works only in-game. `/teamchat` also works in lobby, but doesn't work with splitscreen multiplayer. You can use any combination of two teamchats at any moment.
* `/start` - has the same effect as pressing the green ready button.
* `/config (parameters)` - set the server difficulty and/or mode to a specified value. It is equivalent to choosing from a GUI menu.
* `/commands` - lists some of available commands.
* `/tell (info)` - sends a report to a server.
* `/version` - displays the version. It is set manually in the code for now, and server owners can change it at their own decision. If you change the version, we recommend to make sure the version is informative enough to compare different servers.
* `/register (info)` - allows to register for an event, the information is stored as a report in a specified table in a database.


## Soccer tournament referee commands
* `/role (player) (role_id)`, `/role (player) (role_id)` - sets a role to a player, where `role_id` is one of characters in `RrBbJjSs`.
* `/game [number [duration]]` - starts the next (or specified) game with the default (or specified) duration (in minutes or goals, depending on the tournament format).
* `/stop` - stops the goal count during the game.
* `/go | /resume | /continue` - resumes the goal count of game.
* `/lobby` - stops the game fully, forcing all players to move to the lobby.
* `/init (red_goals) (blue_goals)` - sets the initial goal count of the game to a specific value (during the game). Players will see it at the bottom of the screen.

Referees can also use all server admin commands and crowned player commands (`/kick`, etc.).

## Server admin commands

* `/power (password)` - switches the admin to invulnerable mode, in which no one can kick the admin, but the admin can kick anyone regardless of who is the crowned player (if any), and invoke additional commands.
* `/admin (command)` - can only be invoked in invulnerable mode.
* `/admin start (0|1)` - allows or forbids to start the game. Can be useful for scheduled events, or to prevent players from starting too fast.
* `/kickban [player]`, `/ban [player]` - temporarily bans a player (it is reset upon server restart). The first version also kicks the player from the server, and thus can be used only when that player is on the server.
* `/unban [player]` - removes temporary ban from a player. Note that database-stored bans are not affected by `/ban`, `/kickban`, and `/unban` commands.

Invulnerable mode also allows invoking server owner commands.
