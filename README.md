# Forest Maze

A real-time co-op game for two players on one phone, inspired by Magic Maze. See the spec for the rules.

- Everything lives in `index.html` (no framework, no build step, no server).
- Play: host the file over HTTPS (the Screen Wake Lock API needs it), or just open it locally.
- Logic tests: open the page and run `FM.runTests()` in the browser console.
- Tunable numbers: the `CONFIG` object at the top of the script.
- Tile library: the `tile(...)` calls in the script (ASCII rows, doors, walls, logs).
