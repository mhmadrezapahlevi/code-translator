# Code Translator

A two-way translator for **plain text**, **Morse code**, and **ASCII** (decimal, hexadecimal, binary, octal). Type on one side and the other side updates instantly. Everything runs in the browser from a single HTML file, with no build step, no dependencies, and no server.

The interface mixes a Victorian telegraph office with a cyber terminal: a live **paper tape** shows your message as dots and dashes, and you can play it back as sound or have the text read aloud.

## Features

- **Translate in any direction.** Text, Morse, and ASCII are all both inputs and outputs, so you can go straight from Morse to binary, or from hex back to plain text.
- **Live conversion.** The result updates as you type.
- **Swap button.** Reverse the direction and move the output into the input in one click.
- **Paper tape preview.** The current message is drawn as a punched tape of dots and dashes.
- **Play Morse.** Hear the message as beeps while the matching marks light up on the tape. Click again to stop.
- **Speak text.** Read the decoded plain text aloud with the browser's speech engine, in an English or Indonesian voice.
- **Forgiving input.** Unknown characters are marked with `?` and a warning explains what was not recognized.
- **Copy button, example button, and a built-in Morse table.**
- **Light and dark themes.** Follows the system setting. Animations are turned off when reduced motion is requested.
- **Responsive.** Works on desktop and mobile screens.

## Supported formats

| Format | Example for `Hello World` |
| --- | --- |
| Plain text | `Hello World` |
| Morse code | `.... . .-.. .-.. --- / .-- --- .-. .-.. -..` |
| ASCII Decimal | `72 101 108 108 111 32 87 111 114 108 100` |
| ASCII Hexadecimal | `48 65 6C 6C 6F 20 57 6F 72 6C 64` |
| ASCII Binary | `01001000 01100101 01101100 01101100 01101111 ...` |
| ASCII Octal | `110 145 154 154 157 40 127 157 162 154 144` |

### Input rules

- **Morse:** use `.` and `-`. A space separates letters and `/` separates words. The symbols `·` and `–` are also accepted when decoding.
- **ASCII:** separate characters with spaces, commas, or new lines. Hexadecimal may include a `0x` prefix. Binary without spaces is accepted when its length is a multiple of 8.
- **Morse coverage:** letters A to Z, digits 0 to 9, and common punctuation (`. , ? ' ! / ( ) & : ; = + - _ " $ @`).

## Usage

### Run locally

Download `code-translator.html` and open it in a browser. That is all.

If you prefer to serve it over HTTP:

```bash
python3 -m http.server 8000
# then open http://localhost:8000/code-translator.html
```

### Deploy with GitHub Pages

1. Rename `code-translator.html` to `index.html`.
2. Push it to your repository.
3. In **Settings → Pages**, choose the branch and the root folder.

## Project structure

```
.
├── code-translator.html   # the whole app: markup, styles, and scripts
└── README.md
```

## How it works

- **Conversion pipeline.** Input is first decoded into plain text, then encoded into the target format. This is why any format can be translated to any other.
- **Morse audio.** Played with the Web Audio API using a 640 Hz tone. A dot lasts 0.09 s, a dash lasts three dots, and the gaps follow standard Morse timing.
- **Speech.** Uses the Web Speech API (`speechSynthesis`).
- **Paper tape.** Built from the Morse form of the current text, redrawn on every change.

## Browser notes

- Audio and speech need a modern browser. If speech is not supported, the **Speak text** button is disabled automatically.
- Available voices depend on your browser and operating system. If no Indonesian voice is installed, the browser falls back to the closest default voice.
- Fonts (IM Fell English and Share Tech Mono) load from Google Fonts. Offline, the app works the same and uses system fonts instead.

## Limitations

- Morse has no standard representation for lowercase letters, accents, or emoji. Text is uppercased before encoding, and unsupported characters are marked with `?`.
- ASCII covers codes 0 to 127. Characters above that are still converted to their code point, but a warning is shown.

## Credits

Designed and built by **MRPvi_**.
