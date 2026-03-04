# Conversion Guide

Pattern mapping table: JavaScript/HTML concept → MakeCode Arcade equivalent

## Game Loop

| JavaScript | MakeCode Arcade |
|------------|-----------------|
| `requestAnimationFrame(loop)` | `game.onUpdate(function () { ... })` |
| `setInterval(fn, 1000)` | `game.onUpdateInterval(1000, function () { ... })` |
| `setTimeout(fn, 1000)` | `setTimeout` not available - use `game.onUpdateInterval` |

## Sprites & Graphics

| JavaScript | MakeCode Arcade |
|------------|-----------------|
| `new Image()` | Use `img`\` template literal |
| `ctx.drawImage(img, x, y)` | `sprite = sprites.create(img\`...\`, kind)` |
| `ctx.fillRect(x, y, w, h)` | Draw directly on `img`\` template |
| `element.style.backgroundImage` | `sprites.create(img\`...\`, kind)` |
| Canvas drawing | Convert to sprite + `img\` template |

### Image Loading Pattern

```javascript
// BEFORE (JavaScript)
var playerImg = new Image();
playerImg.src = "player.png";
// Draw in game loop
ctx.drawImage(playerImg, x, y);
```

```typescript
// AFTER (MakeCode)
// Define in images.ts
const playerSprite = sprites.create(img`
    . . . . . . . .
    . . f f f f . .
    . f 5 5 5 5 f .
`, SpriteKind.Player)

// Position
playerSprite.setPosition(80, 60)
```

## Input Handling

| JavaScript | MakeCode Arcade |
|------------|-----------------|
| `document.addEventListener('keydown', fn)` | `controller.onButtonPressed(ControllerButton.A, fn)` |
| `e.key === 'ArrowUp'` | `controller.up.isPressed()` |
| `e.which === 38` | `ControllerButton.Up` |
| `window.addEventListener('keyup', fn)` | `controller.onButtonReleased(Button, fn)` |

### Keyboard Pattern

```javascript
// BEFORE
document.addEventListener('keydown', (e) => {
    if (e.key === 'ArrowUp') player.y -= 5;
    if (e.key === ' ') shoot();
});
```

```typescript
// AFTER
controller.moveSprite(playerSprite, 64, 64)
controller.A.onButtonPressed(ControllerButton.A, function () {
    // shoot projectile
})
```

## Collision Detection

| JavaScript | MakeCode Arcade |
|------------|-----------------|
| `rectIntersect(r1, r2)` | Built-in `sprites.onOverlap()` |
| `checkCollision(x, y, tile)` | `scene.onHitTile()` |
| Custom collision math | `sprites.overlaps(sprite1, sprite2)` |

### Collision Pattern

```javascript
// BEFORE
function checkCollision(player, enemy) {
    return player.x < enemy.x + enemy.width &&
           player.x + player.width > enemy.x &&
           player.y < enemy.y + enemy.height &&
           player.y + player.height > enemy.y;
}
```

```typescript
// AFTER
sprites.onOverlap(SpriteKind.Player, SpriteKind.Enemy, function (player, enemy) {
    player.destroy()
    game.over(false)
})
```

## Audio

| JavaScript | MakeCode Arcade |
|------------|-----------------|
| `new Audio('file.mp3').play()` | `sounds.file.play()` |
| `audio.play()` | `music.playMelody("C5-G5-E5", 120)` |
| `AudioContext` | Not available - use melodies |

### Audio Pattern

```javascript
// BEFORE
var shootSound = new Audio('shoot.wav');
shootSound.play();
```

```typescript
// AFTER
// In audio.ts
sounds.shoot.play()
// Or melody
music.playMelody("C5", 120)
```

## DOM Manipulation

| JavaScript | MakeCode Arcade |
|------------|-----------------|
| `document.getElementById('id')` | N/A - use sprites |
| `element.style.left = '100px'` | `sprite.x = 100` |
| `element.innerHTML = 'text'` | `game.showDialog()` |
| `element.classList.add('c')` | N/A |

**Note**: All DOM manipulation must be removed or replaced with sprite operations.

## Browser APIs

| JavaScript | MakeCode Arcade |
|------------|-----------------|
| `localStorage.setItem(k, v)` | Use `settings` namespace |
| `fetch(url)` | Not available |
| `XMLHttpRequest` | Not available |
| `console.log()` | `console.log()` works |
| `Math.random()` | `Math.random()` available |
| `Date.now()` | `control.millis()` |

## Variables & State

| JavaScript | MakeCode Arcade |
|------------|-----------------|
| `let score = 0` | `info.setScore(0)` |
| `let lives = 3` | `info.setLife(3)` |
| Global variables | Use `let` in namespace or global |

## Tilemap/Level

| JavaScript | MakeCode Arcade |
|------------|-----------------|
| 2D array of tiles | `tiles.loadMap(tilemap\`level\`)` |
| Array of barriers | `scene.setTile(1, wallImg, true)` |

### Tilemap Pattern

```javascript
// BEFORE (custom format)
const map = [
    [1,1,1,1,1],
    [1,0,0,0,1],
    [1,0,1,0,1]
];
```

```typescript
// AFTER
tiles.loadMap(tilemap`level1`)
// Or define:
scene.setTile(1, img`. . . . .`, true)  // wall
scene.setTile(0, img`. . . . .`)        // floor
```

## Game State Management

| JavaScript | MakeCode Arcade |
|------------|-----------------|
| `if (gameOver)` | `game.over(win)` |
| `requestAnimationFrame` | `game.onUpdate()` |

## Effects

| JavaScript | MakeCode Arcade |
|------------|-----------------|
| CSS animations | `effects.blink`, `effects.fade` |
| Canvas effects | Built-in effects |

```typescript
// Effects
enemy.destroy(effects.fire, 500)
player.startEffect(effects.confetti)
```

## Common Conversions Summary

| Original Code | Converted Code |
|--------------|----------------|
| `ctx.fillRect(0,0,160,120)` | Background + tilemap |
| `player.style.left = x + 'px'` | `sprite.x = x` |
| `if (keyIsDown(37))` | `controller.left.isPressed()` |
| `Math.floor(Math.random()*10)` | `Math.randint(0,9)` |
| `setInterval(spawn, 1000)` | `game.onUpdateInterval(1000, spawn)` |
| `alert('Game Over')` | `game.over(false)` |

## Quick Fixes

### Variable Declaration
```javascript
// Add types where needed
let score: number = 0
let player: Sprite = null
```

### Semicolons
```typescript
// Add missing semicolons
sprite.setPosition(80, 60);
```

### Function Syntax
```javascript
// Arrow functions need conversion
// Before: () => { ... }
// After: function () { ... }
```

### Enum Values
```typescript
// MakeCode enums
SpriteKind.Player
ControllerButton.A
TileKind.Wall
```

## Testing Checklist

- [ ] Game loop runs without errors
- [ ] Sprites render correctly
- [ ] Controller input works
- [ ] Collisions detected properly
- [ ] Score/lives display works
- [ ] Game over triggers correctly
- [ ] Tilemap loads if used
- [ ] Audio plays if applicable
