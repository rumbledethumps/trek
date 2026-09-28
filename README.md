# Super Star Trek

Super Star Trek, the 1978 BASIC game by Mike Mayfield and Bob Leedom, on
the [Picocomputer 6502](https://picocomputer.github.io) in
[Microsoft BASIC](https://github.com/picocomputer/msbasic).

[Play it in your browser](https://rumbledethumps.github.io/trek/).

The game is two programs. `src/trek_instructions.bas` prints the
instructions and ends with `RUN ":TREK_GAME.BAS"`, which loads and runs
`src/trek_game.bas`. Answer `N` to skip the instructions, and type `XXX`
to resign.

## Running it

Both programs are installed on the null drive, where BASIC reads each one
as `:name`, in any case. `-c1` keeps the keyboard in capitals, because the
game takes commands only in capitals, and the last argument is the program
BASIC loads and runs first.

```bash
$ rp6502-emu --install src/trek_game.bas --install src/trek_instructions.bas \
    basic.rp6502 -- -c1 :TREK_INSTRUCTIONS.BAS
```

`basic.rp6502` is on the
[Microsoft BASIC releases page](https://github.com/picocomputer/msbasic/releases/latest).
A Picocomputer installs only ROMs, so the pair runs only in the emulator.

## Web player

`index.html` plays the game in a browser. In its `CONFIG`, `rom` is
`basic.rp6502`, `install` lists the two programs, and `args` holds the
arguments above. GitHub Actions publishes it to GitHub Pages on each push
to `main`, with `.github/workflows/pages.yml`. See
[RP6502-WEB](https://picocomputer.github.io/web.html).
