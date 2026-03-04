# JS to Arcade Converter

[![GitHub Pages](https://img.shields.io/badge/Deployed-GitHub_Pages-brightgreen)](https://github.com/features/pages)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Made for MakeCode Arcade](https://img.shields.io/badge/Made%20for-MakeCode_Arcade-0078D4)](https://arcade.makecode.com/)

Convert JavaScript HTML games to MakeCode Arcade TypeScript - 100% browser-based.

## What It Does

**JS to Arcade Converter** transforms traditional JavaScript/HTML games into [MakeCode Arcade](https://arcade.makecode.com/) projects:

- Converts JavaScript/HTML games to MakeCode Arcade TypeScript
- Handles ZIP file uploads of full projects
- Auto-converts images to MakeCode `img`\` pixel art format using the 16-color MakeCode palette
- Auto-converts audio to `music.playMelody()` strings via frequency analysis
- Outputs tabbed code: `main.ts`, `images.ts`, `audio.ts`, and a TODOs list
- 100% browser-based - no server needed, all processing happens locally

## How To Use

### Quick Start

1. **Go to the Live Site**: https://your-username.github.io/js-to-arcade-converter
2. **Upload your .zip file** OR paste JavaScript code directly
3. **Click CONVERT**
4. **Copy the output tabs** into MakeCode Arcade's JavaScript editor:
   - `main.ts` - Game logic
   - `images.ts` - Sprite definitions
   - `audio.ts` - Melody functions

### Manual Asset Setup

For images:
- Use [pxt-arcade-asset-tool](https://riknoll.github.io/pxt-arcade-asset-tool/) to manually edit or create sprites

For audio:
- Use [Audio-to-MakeCode-Arcade](https://github.com/TycoonCoder/Audio-to-MakeCode-Arcade) for more precise conversion

### Tips for Best Results

- Keep sprites small (16x16, 32x32) - MakeCode screen is only 160x120px
- Simplify game logic before converting
- Remove all browser APIs (document, window, localStorage) manually
- Review the TODOs list for items requiring manual work

## Limitations

- Complex game engines may need significant manual cleanup
- Browser-only APIs must be manually removed
- Large sprites may need manual pixel art redrawing
- Audio conversion is approximate (frequency-based, not note-perfect)
- MakeCode Arcade screen is 160x120px max
- Not all JavaScript features map 1:1 to MakeCode APIs

## Credits

- [MakeCode Arcade](https://arcade.makecode.com/) by Microsoft
- [pxt-arcade-asset-tool](https://riknoll.github.io/pxt-arcade-asset-tool/) by riknoll
- [Audio-to-MakeCode-Arcade](https://github.com/TycoonCoder/Audio-to-MakeCode-Arcade) by TycoonCoder
- [JSZip](https://stuk.github.io/jszip/) library for ZIP handling

## Contributing

Contributions are welcome! This is a single-file application - all logic is in `index.html`.

### How to Contribute

1. Fork the repository
2. Make your changes to `index.html`
3. Submit a Pull Request

### Adding New Conversion Patterns

The converter uses a pattern-based approach. To add new conversions:

1. Find the `detectPatterns()` function in index.html
2. Add your new pattern to the patterns array
3. Add对应的代码生成逻辑

## License

MIT License - See LICENSE file for details.

---

Made with ❤️ for the MakeCode Arcade community
