# How we tested the skill

A skill is only useful if it changes what Claude actually does. So we tested it like code: we watched an agent work without it first, then wrote the skill to fix what went wrong.

## Round 1: no skill (baseline)

A fresh agent planned "Bruno's Dinosaurs" from scratch. The plan was sensible, but it didn't match the family, and it missed the hard lessons:

- It chose a different stack: Vitest, Playwright, and a GitHub Actions deploy.
- It made code and pages cache-first, so installed iPads would keep running old versions.
- It missed iPad Safari's need for byte-range responses before it plays audio from the offline cache.
- It missed speech cutting off mid-sentence, fast double taps, timers firing after a kid leaves a screen, and sound questions asked while sounds are turned off.
- It added features nobody asked for, like backup codes and recorded voice-overs.

## Round 2: with the skill

Same scenario, with the skill loaded. The agent:

- Kept the zero-dependency stack and the GitHub Pages setup.
- Kept every pitfall fix from the templates.
- Asked before publishing.

Its list of gaps exposed a real bug in both live games. They share one web address, and each one deleted the other's offline copy. The template now fixes this, and a test guards the fix.

## Round 3: a new topic

A third agent planned a bugs-and-insects game. That surfaced smaller gaps, which we closed:

- The templates now include data and screens, not just the engine.
- The skill says which hardcoded numbers in the tests to rewrite.
- It explains topics where only some subjects make sounds.
- It sets the first cache version and the naming rule for new games.

## Checking the templates

The template files run against a copy of Bruno's Zoo. All 74 tests pass, including the new cache-prefix test.

## When you change the skill

Run the same kind of test again. Give a fresh agent a new topic, with the skill loaded, and ask it to plan the game and list anything unclear. Fix what it finds, then test once more.
