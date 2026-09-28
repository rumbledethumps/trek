# Super Star Trek

Super Star Trek, the 1978 BASIC game by Mike Mayfield and Bob Leedom, on
the [Picocomputer 6502](https://picocomputer.github.io) in
[BASIC](https://github.com/picocomputer/msbasic).

<!-- rp6502
preset: basic
target: trek
title: Super Star Trek
footer: Type a command, then press Enter. XXX resigns.
-->
[Play it in your browser](https://rumbledethumps.github.io/trek/trek/).

The game is two programs. `src/instructions.bas` prints the instructions
and ends with `RUN "ROM:GAME.BAS"`, which loads and runs `src/game.bas`.
Answer `N` to skip the instructions, and type `XXX` to resign.

## Building and running

The `basic` preset needs no compiler. It packages BASIC with both
programs into one ROM, `build/basic/trek.rp6502`, and BASIC starts the
instructions by itself. The first configure downloads the emulator and
`basic.rp6502` into `tools/`.

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

The comment above the play link names the preset and the target, and
`.github/workflows/web.yml` publishes the player to GitHub Pages on each
push to `main`. See [RP6502-WEB](https://picocomputer.github.io/web.html).
