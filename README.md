# Forest Maze

A real-time co-op game for two players on one phone, inspired by Magic Maze. See the spec for the rules.

- Everything lives in `index.html` (no framework, no build step, no server).
- Play: host the file over HTTPS (the Screen Wake Lock API needs it), or just open it locally.
- Logic tests: open the page and run `FM.runTests()` in the browser console.
- Tunable numbers: the `CONFIG` object at the top of the script.
- Tiles: by default generated per game from the seed (`genTile`). The 20 hand-made tiles (`tile(...)` calls) stay available as the "Premade" option.
- AI partner: choose "AI partner" on the setup screen. You are Player 1; tap Pass to hand the phone to the AI (Player 2). It plays up to 6 moves with its action set, passes back, and pings the animal it would move next. It reads your pings (a ping on an animal or a doorway steers it). Planner: `aiChoose` in the script. `FM.selfPlay({seed, difficulty, tiles, timeMs})` plays both sides with the AI against a simulated clock, for tuning.
