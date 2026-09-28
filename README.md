# Super Star Trek

Super Star Trek, the 1978 BASIC game by Mike Mayfield and Bob Leedom, on
the [Picocomputer 6502](https://picocomputer.github.io) in
[BASIC](https://github.com/picocomputer/msbasic).

<!-- rp6502
preset: basic
publish: trek.zip
frames: 300
-->
[![Play Super Star Trek](https://rumbledethumps.github.io/trek/trek/screenshot.png)](https://rumbledethumps.github.io/trek/trek/)

[Play it in your browser](https://rumbledethumps.github.io/trek/trek/).

The game is two programs. `src/instructions.bas` prints the instructions
and ends with `RUN "ROM:GAME.BAS"`, which loads and runs `src/game.bas`.
Answer `N` to skip the instructions, and type `XXX` to resign.

## Building and running

The `basic` preset packages BASIC with both programs into one ROM,
`build/basic/trek.rp6502`, and BASIC starts the instructions by itself.
The configure fetches BASIC release `build-96e229e`, which
`CMakeLists.txt` names, because `tests/play.txt` is written for the
galaxy that this release sets up with `--seed 1`. To move to another
release, name it there and check the test. The first configure also
downloads the emulator into `tools/`.

```bash
$ cmake --preset basic
$ cmake --build --preset basic
$ tools/rp6502-emu build/basic/trek.rp6502
```

In VS Code, choose the `basic` preset and press F5. On a Picocomputer,
`INSTALL trek.rp6502`, then type `TREK`.

## Testing

`tests/play.txt` is an emulator script that reads the instructions, tries
every command, fights a Klingon, resigns, and plays a second game, which
runs the setup again after the `CLEAR` on line 260 of `src/game.bas`. It
runs with `--seed 1`, which fixes the galaxy that the script is written
for.

```bash
$ ctest --preset basic
```

## Web player

`rp6502_web()` in `CMakeLists.txt` packages the ROM with `web/index.html`
into `build/basic/web/trek.zip`; in VS Code, "RP6502 (Web)" plays it in a
browser. The comment above the play link names the zip, and
`.github/workflows/web.yml` publishes it to GitHub Pages on each push to
`main`. See [RP6502-WEB](https://picocomputer.github.io/web.html).
