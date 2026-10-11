# How the Bruno games work

This page explains the pattern behind every game in the family, and why it looks the way it does. Read it when you want to change a default or understand a choice.

## The loop kids play

1. **Explore.** Kids tap each subject in a zone. They hear its sound, see its name, and Bruno tells them a fun fact out loud.
2. **Quiz.** Once they've met everyone in a zone, a short quiz opens: "Who makes this sound?", "Find the lion!", or a true-or-false fact from Bruno.
3. **Reward.** First-try answers earn stars and stickers. Stars unlock the next zone.

Six first-try answers earn three stars, four or five earn two, and anything else earns one. Zone *n* opens at 2 × *n* total stars, so a kid who earns two stars everywhere can open every zone.

## Why these choices

| Choice | Why |
|---|---|
| Plain HTML, CSS, and JavaScript with no build step | Nothing to install or upgrade. Any change is live the moment you save |
| `node --test`, no test libraries | Zero dependencies to keep current. Tests run in about a tenth of a second |
| GitHub Pages from `main` | Free hosting, no deploy pipeline to maintain |
| Installable, offline-first | Kids play in cars, on planes, and in places with weak Wi-Fi |
| Bundled 3D art instead of device emoji | Emoji look different on every device, and flag emoji show up as letters on Windows |
| Real recorded sounds, openly licensed | Kids learn what animals really sound like, and every creator gets credit |
| Bruno speaks everything important | Kids aged 6–10 read at very different levels |
| Pure quiz and progress logic | The rules are fully tested without a browser |

## How the code fits together

- **`main.js`** owns the current screen and hands each screen a small context: state, translations, audio, and navigation.
- **Screens** draw themselves from that context and keep no state of their own.
- **`quiz.js` and `progress.js`** are pure functions. They never touch the page or storage, so tests can pass in a seeded random number generator (RNG) and a fake storage object.
- **`audio.js`** wraps sound clips, speech, and chimes. Every call is safe: if something fails, the game keeps going.
- **`sw.js`** is the service worker—the piece that saves the game for offline play. Pictures and sounds load from the saved copy first. Code loads from the network first, so updates arrive on the next online launch.

## One web address, many games

Every game lives under `mariotristan.github.io`, so they all share one browser storage area. Each game needs its own storage key and its own cache name prefix. Otherwise, opening one game can erase another game's progress or offline copy. The template service worker only cleans up caches that start with its own prefix, and a test checks that.
