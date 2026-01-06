---
layout: default
title: Solar v1.0.3
nav_order: 103
---

# Solar v1.0.3

Solar v1.0.3 is a major release focused on making Solar feel like a real language: user-defined functions, block control-flow, real expressions, and a first “pure Solar” Pygame layer for games.

## Highlights

### solar_def: Solar functions

## YOU CANT MAKE FUNCTIONS WITH ARGS YET!! I WILL ADD IT IN 1.0.4!!
Define functions in Solar (no Python passthrough needed) and call them like normal Solar commands.

Example:

```solar
solar_def no_args:
     print "test func without args"
end

no_args
```

Notes:
- Functions are registered automatically into `funcs["name"]`.
- `return <expr>` is supported.

### Block syntax: if / elif / else / while / for

Solar now supports block statements terminated by `end`.

```solar
let score = 7

if score >= 10:
    print "great"
elif score >= 5:
    print "ok"
else:
    print "rip"
end
```

Loops:

```solar
let x = 0
while x < 5:
    print x
    let x = x + 1
end

for i in 0..3:
    print "i=" i
end
```

### Real expressions

Expressions now support:
- Arithmetic: `+ - * / %`
- Comparisons: `== != < <= > >=`
- Boolean: `and or not`
- Parentheses
- Indexing: `arr[0]`
- Function calls in expressions: `foo(1, 2)` (calls `funcs["foo"]`)

### UI (customtkinter)

Solar UI syntax remains available and works with customtkinter widgets:

- `ui window`, `ui title`, `ui size`
- `ui bg`, `ui fg`
- `ui label`, `ui entry`, `ui checkbox`, `ui slider`, `ui button`
- `ui text`, `ui set`, `ui get ... into ...`, `ui run`

### contain imports

`contain <module>` inserts a Python import into the compiled program.

```solar
contain pygame
contain pygame as pg
```

## Pygame: Solar-only game loop (beta)

Solar v1.0.3 introduces a small Pygame DSL under `pg` so you can write a working loop in Solar syntax.

Supported commands:
- `pg init`
- `pg window <w> <h> title "text"`
- `pg fps <n>`
- `pg rect <name> x y w h color r g b`
- `pg var <name> <value>`
- `pg loop:` ... `end`
- `pg event quit ->` ... `end`
- `pg key held <KEY> ->` ... `end`
- `pg clear r g b`
- `pg draw <rectname>`
- `pg move <rectname> dx dy`
- `pg flip`
- `pg exit`

### Example game (Solar syntax)

A tiny “move the box” game using only Solar:

```solar
contain pygame

pg init
pg window 800 600 title "Solar v1.0.3 - Pygame demo"
pg fps 60

pg rect player 50 50 40 40 color 255 80 80
pg var vx 0
pg var vy 0

pg loop:
    pg event quit ->
        pg exit
    end

    # reset velocity each frame
    pg set vx 0
    pg set vy 0

    pg key held A ->
        pg set vx -5
    end
    pg key held D ->
        pg set vx 5
    end
    pg key held W ->
        pg set vy -5
    end
    pg key held S ->
        pg set vy 5
    end

    pg move player vx vy

    pg clear 20 20 25
    pg draw player
    pg flip
end
```

## Notes / Limitations

- The Pygame DSL is intentionally small. It is meant as a foundation for more Solar-native game features in future versions.
- Python passthrough is still supported (raw Python lines are kept in-order), but v1.0.3 reduces the need for it.
