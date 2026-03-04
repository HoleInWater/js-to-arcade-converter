# How to Use JS to Arcade Converter

This guide provides a detailed walkthrough for converting your JavaScript games to MakeCode Arcade.

## Prerequisites

- A modern web browser (Chrome, Firefox, Edge, Safari)
- A GitHub account (for GitHub Pages deployment)
- MakeCode Arcade account (optional, for saving projects)

## Step-by-Step Guide

### Step 1: Prepare Your JavaScript Project

Before converting, clean up your code:

1. **Remove browser-specific APIs**:
   - `document.*` - Use sprites instead
   - `window.*` - Remove completely
   - `localStorage` - Use settings namespace
   - `XMLHttpRequest` / `fetch` - Remove completely

2. **Simplify game loop**:
   - Convert `requestAnimationFrame` to `game.onUpdate()`
   - Convert `setInterval` to `game.onUpdateInterval()`

3. **Prepare assets**:
   - Keep images as PNG/GIF files
   - Keep audio as MP3/WAV files
   - Organize in folders (sprites/, audio/, etc.)

### Step 2: Upload or Paste Code

**Option A: ZIP Upload**
1. Create a ZIP file of your project
2. Click "UPLOAD ZIP"
3. Select your ZIP file
4. Wait for extraction to complete

**Option B: Paste Code**
1. Copy your JavaScript code
2. Paste into the text area
3. Click "CONVERT"

### Step 3: Review Detection Summary

After conversion, you'll see:
- Total JS files processed
- Images found and converted
- Audio files found and converted  
- Browser APIs removed
- TODOs remaining
- Compatibility score

### Step 4: Copy Output Code

The converter produces 4 tabs:

1. **main.ts** - Your game logic (converted)
2. **images.ts** - Sprite definitions (auto-generated)
3. **audio.ts** - Melody functions (auto-generated)
4. **TODOs** - Items needing manual work

Click each tab and copy its contents.

### Step 5: Import into MakeCode

1. Go to https://arcade.makecode.com/#editor
2. Create a new project
3. Create three files: `main.ts`, `images.ts`, `audio.ts`
4. Paste the copied code into each file
5. Add sprite images in the editor's image gallery

### Step 6: Test and Debug

- Use the MakeCode simulator to test
- Check console for errors
- Review TODOs and fix manually
- Iterate on your original code if needed

## Common Errors and Fixes

### "Cannot find variable 'document'"
**Cause**: DOM API used in code  
**Fix**: Remove or replace with sprite operations

### "Cannot find variable 'window'"
**Cause**: Browser window object referenced  
**Fix**: Remove all window.* calls

### "Expected ;"
**Cause**: Some JS syntax not valid in TypeScript  
**Fix**: Add semicolons, fix type declarations

### Sprites not showing
**Cause**: Images not imported  
**Fix**: Add images manually in MakeCode editor

### No sound
**Cause**: Melody format incorrect  
**Fix**: Use Audio-to-MakeCode-Arcade tool for better conversion

## Tips for Best Results

1. **Start Simple**: Convert simple games first (Pong, Snake, Tetris)
2. **Clean Code**: Remove unused code before converting
3. **Small Sprites**: Keep sprites 16x16 or 32x32
4. **Limited Colors**: Use max 4-16 colors per sprite
5. **Simple Physics**: Avoid complex physics engines

## Advanced Tips

### Manual Image Conversion
If auto-conversion doesn't work well:
1. Use https://riknoll.github.io/pxt-arcade-asset-tool/
2. Draw or import your sprite
3. Export as `img`\` code
4. Paste into images.ts

### Manual Audio Conversion
For better audio results:
1. Use https://github.com/TycoonCoder/Audio-to-MakeCode-Arcade
2. Upload your MP3/WAV
3. Copy the generated melody string
4. Paste into audio.ts

### Tilemap Setup
1. In MakeCode, click "Tilemap" in the editor
2. Design your level visually
3. Or use tiles.setTilemap() with a tilemap\` literal
