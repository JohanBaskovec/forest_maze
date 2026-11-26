# Forest Maze

A real-time co-op game for two players on one phone, inspired by Magic Maze. See the spec for the rules.

- Everything lives in `index.html` (no framework, no build step, no server).
- Play: host the file over HTTPS (the Screen Wake Lock API needs it), or just open it locally.
- Logic tests: open the page and run `FM.runTests()` in the browser console (about 15 s).
- Tunable numbers: the `CONFIG` object at the top of the script.

## How the map works

- Tiles are generated when a doorway is explored (`genTile`), each a random width and height from 3 to 7, fitted into the free space behind the doorway. The deck only says what each tile must contain (food, exit, timer square, tower), so the same seed and the same exploring give the same map.
- The map is always winnable (checked by the tests and by AI self-play): every tile is connected inside without flyer gates, a doorway stays open while tiles remain in the deck, each food square, exit and tower is reachable, and the exits only unlock once every exit has been found (so no animal leaves while exploring still needs its colour).

## Random action sets

Each game deals exactly 2 of the 4 directions to each player, and shares the other actions (Explore, Climb, Burrow, and Destroy with hunting towers) at random, each held by exactly one player, each player getting at least one.

## Optional extras (setup screen)

- **Flyer gates** (Off / Few / Some / Many): fence gaps only the bird and squirrel can cross. Shortcuts only, never the sole route.
- **Exits** (Shared / One each): with "One each" every animal leaves through its own exit, after all four have been found.
- **Hunting towers** (Off / 1 / 2 / 3): the monkey must stand on each tower and use Destroy. Nobody can leave until all are gone.

## AI partner

Choose "AI partner" in setup. You are Player 1; tap Pass to hand the phone to the AI (Player 2). It plays up to 6 moves with its action set, passes back, and pings the animal it would move next. It reads your pings (a ping on an animal or a doorway steers it). Planner: `aiChoose`. `FM.selfPlay({seed, difficulty, timeMs, gates, exits, towers})` plays both sides with the AI against a simulated clock, which is how winnability was checked across thousands of generated maps.
