# MakeCode Arcade API Reference

Quick reference for MakeCode Arcade APIs used by the converter.

## Sprites

### Creating Sprites
```typescript
// Basic sprite creation
let sprite = sprites.create(img`
    . . . . . . . .
    . . f f f f . .
    . f 5 5 5 5 f .
    . f 5 5 5 5 f .
    . . f f f f . .
`, SpriteKind.Player)

// Sprite kinds
enum SpriteKind {
    Player = 0,
    Enemy = 1,
    Projectile = 2,
    Food = 3
}
```

### Sprite Properties
```typescript
sprite.x = 80
sprite.y = 60
sprite.setPosition(x, y)
sprite.setVelocity(vx, vy)
sprite.setFlag(SpriteFlag.GhostThroughWalls, true)
sprite.z = 1  // draw order
sprite.alpha = 255  // opacity
```

### Sprite Destruction
```typescript
sprite.destroy()
sprite.destroy(effects.splatter, 500)
```

## Controller

### Movement
```typescript
controller.moveSprite(sprite)
controller.moveSprite(sprite, 100, 100)  // with speed

controller.left.moveSprite(sprite)
controller.A.moveSprite(sprite)
```

### Button Events
```typescript
controller.onButtonPressed(ControllerButton.A, function () {
    // pressed once
})

controller.onButtonHeld(ControllerButton.A, function () {
    // held continuously
})

controller.onButtonReleased(ControllerButton.A, function () {
    // released
})
```

## Game Loop

### Update Functions
```typescript
// Runs every frame (~60fps)
game.onUpdate(function () {
    // game logic
})

// Runs at interval
game.onUpdateInterval(1000, function () {
    // runs every second
})
```

### Game State
```typescript
game.over()
game.over(true)  // win
game.reset()
info.setScore(0)
info.setLife(3)
info.highScore()
```

## Collision

### Overlap Detection
```typescript
sprites.onOverlap(SpriteKind.Player, SpriteKind.Enemy, function (player, enemy) {
    player.destroy()
    game.over(false)
})

sprites.onOverlap(SpriteKind.Projectile, SpriteKind.Enemy, function (proj, enemy) {
    enemy.destroy(effects.fire, 200)
    proj.destroy()
})
```

### Tile Collisions
```typescript
scene.onHitTile(SpriteKind.Player, 1, function (sprite) {
    // hit wall tile (id 1)
})
```

## Tilemap

### Loading Maps
```typescript
// Visual editor tilemap
tiles.loadMap(tilemap`level1`)

// Programmatic
let myMap = tilemap.createMap(
    [img`...`, img`...`],
    [TileKind.Wall, TileKind.Grass],
    TileScale.Sixteen
)
```

### Tile Properties
```typescript
scene.setTile(1, img`...`)  // wall
scene.setTile(2, img`...`, TileKind.Grass)  // grass (walkable)
scene.setTile(4, img`...`, false)  // not solid

scene.setBackgroundColor(7)  // color index
```

## Audio

### Playing Melodies
```typescript
music.playMelody("C5-G5-E5-G5-C5-G5-E5-C5", 120)
music.playMelody(music.builtInPlayable(music.beat(BeatFraction.Whole)), music.PlayLoopMode.Looping)
```

### Sound Effects
```typescript
sounds.jump.play()
sounds.explosion.play()
sounds.powerUp.play()

// Custom
let mySound = sounds.mySound.play()
mySound.play()
```

### Music
```typescript
music.play(music.melodyPlayable(music.baDing), music.PlayLoopMode.Looping)
music.setTempo(120)
music.setVolume(128)
```

## Effects

```typescript
// Built-in effects
effects.starDissolve
effects.confetti
effects.smiles
effects.fire
effects.bubbles
effects.splatter
effects.dissolve

// Applying
enemy.destroy(effects.fire, 500)
player.startEffect(effects.confetti, 1000)
```

## Math & Helpers

```typescript
// Math
Math.abs(-5)           // 5
Math.min(1, 2)         // 1
Math.max(1, 2)          // 2
Math.random()           // 0-1
Math.randint(1, 10)      // 1-10

// Colors (0-15)
let c = 5  // red-ish

// Position
sprite.left
sprite.right
sprite.top
sprite.bottom
sprite.centerX
sprite.centerY
```

## Scene/Camera

```typescript
scene.cameraFollowSprite(playerSprite)
scene.centerCameraAt(80, 60)
let camX = scene.cameraProperty(CameraProperty.X)
let camY = scene.cameraProperty(CameraProperty.Y)
```

## Animation

```typescript
// Frame animation
playerSprite.setAnimation("walk", ["img1", "img2", "img3"], 500)

// Simple flip
sprite.setFlip(true, false)
```

## Enum Quick Reference

```typescript
// SpriteKind
Player, Enemy, Projectile, Food

// ControllerButton  
A, B, Left, Right, Up, Down

// ControllerDirection
Left, Right, Up, Down

// TileKind
Wall, Grass, Water, Ice, Hole

// BeatFraction
Whole, Half, Quarter, Eighth, Sixteenth

// PlayLoopMode
Once, Forever, Looping

// SpriteFlag
GhostThroughWalls, ShowPhysics, AutoDestroy, StayInScreen
```
