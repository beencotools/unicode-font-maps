# unicode-font-maps

Plain JSON character maps for the Unicode "fancy font" styles: bold, italic, script, fraktur, double-struck, sans-serif, monospace, fullwidth, circled, small caps, upside-down and more.

These are the maps behind **[The Font Generator](https://thefontgenerator.com)**, a free copy-and-paste font tool that also shows which styles survive the paste in Instagram, Discord and TikTok.

## Use

```js
const maps = require("./unicode-font-maps.json");
const style = (text, name) => [...text].map(c => maps[name][c] ?? c).join("");

style("Hello", "bold");   // 𝐇𝐞𝐥𝐥𝐨
style("Hello", "script"); // ℋℯ𝓁𝓁ℴ
```

## The gotchas these maps already handle

- **Missing letters.** Unicode reserved some letters in the Mathematical Alphanumeric Symbols block because they already existed elsewhere. Italic `h` is `ℎ` (U+210E), and script `B`, `E`, `F`, `H`, `I`, `L`, `M`, `R` and `e`, `g`, `o` come from the Letterlike Symbols block. A naive "add an offset" converter outputs empty boxes for these. These maps don't.
- **Character limits.** Most of these characters are outside the Basic Multilingual Plane: 4 bytes in UTF-8 and 2 UTF-16 code units. A 30-character bio in bold can count as 60 against a limit.
- **Accessibility.** Screen readers often read these characters one by one ("mathematical bold capital H…") or skip them. Don't style anything a person needs to understand.

Compatibility notes per style and per app are kept up to date at [thefontgenerator.com](https://thefontgenerator.com).

## License

MIT. Attribution to [The Font Generator](https://thefontgenerator.com) is appreciated.
