# Pygame Example in Solar

This example demonstrates how to use **pygame** with the **Solar programming language** to create a simple game loop with player movement, enemies, collision detection, and scoring.

---

## Importing pygame

First, import the pygame package:

```text
contain pygame
```

---

## Full Example Code

```text
contain pygame

pg init
pg window game 800 600 "Test Game - Made with Solar v1.0.2-beta"
pg fps game 60

# player
let px = 380
let py = 520
let ps = 6

# enemy
let ex = randint(0, 760)
let ey = 0
let es = 5

# local scoring
let score = 0

pg loop game
  pg poll game
  pg quitif game

  # input
  pg key game K_LEFT into left
  pg key game K_RIGHT into right

  # movement
  let px = clamp(px + (right - left) * ps, 0, 760)

  # enemy fall
  let ey = ey + es

  # if enemy passes screen, reset enemy and score++
  if ey > 600 then let ey = 0
  if ey == 0 then let ex = randint(0, 760)
  if ey == 0 then let score = score + 1

  # collision
  if abs(px - ex) < 40 and abs(py - ey) < 40 then pg stop game

  # draw
  pg clear game 20 20 25
  pg rect game px py 40 40 80 200 255
  pg rect game ex ey 40 40 255 90 90

  pg text game ("score: " + str(score)) 10 10 28 255 255 255

  pg flip game
  pg tick game 60
pg end
```

---

## What This Example Shows

- Importing **pygame** in Solar
- Creating a window and game loop
- Keyboard input handling
- Player and enemy movement
- Collision detection
- Basic scoring system
- Rendering shapes and text

---

Made for **Solar v1.0.2**
