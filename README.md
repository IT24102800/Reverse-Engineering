# The Ghost's Game - CTF Challenge

## Overview

**Difficulty:** Hard  
**Theme:** Reverse Engineering & Client-Side Analysis  
**Domains:** Reverse Engineering, Web Security, Programming / Scripting  

This CTF challenge simulates a real-world reverse engineering investigation where participants must analyze a trojanized browser-based game to recover a hidden flag embedded by a rival attacker known as "SilentPlayer."

## Challenge Summary

Participants receive a single HTML file containing a browser-based puzzle-platformer game called **Ghost Runner**. The game has been trojanized by a rival studio's operative, who embedded a "dead man's switch" - a hidden flag that only reveals itself when a specific runtime condition is met. Participants must analyze the client-side JavaScript, identify the win condition, and extract the flag using browser Developer Tools.

### Scenario

PulseForge Studios, an indie game development company, was on the verge of releasing their flagship game, **Ghost Runner**. A week before launch, their build server was breached by a rival company, Helix Interactive. The attacker, known only as **"SilentPlayer"**, replaced the final build with a modified version.

The game plays normally on the surface, but **SilentPlayer** embedded a hidden flag inside the JavaScript. The flag only appears when a specific runtime condition is met - one that cannot be achieved by normal gameplay.

PulseForge's legal team has hired you, a freelance reverse engineer, to analyze the game, find the hidden flag, and prove the tampering. The evidence is in the code. The ghost left traces.

### Starting Point

- **File:** `ghost_runner.html`
- **Source:** [Ghost Runner](https://it24102800.github.io/Reverse-Engineering/ghost_runner.html)

## Learning Objectives

1. Apply client-side reverse engineering techniques to analyze JavaScript game logic
2. Identify hardcoded values and winning conditions in obfuscated code
3. Use browser Developer Tools to inspect runtime state and modify variables
4. Trigger functions manually to bypass game restrictions
5. Chain multiple analysis steps from source reading to runtime exploitation

## Required Tools

| Tool | Purpose |
|------|---------|
| Web Browser | Load and play the game |
| DevTools (F12) | Inspect JavaScript, Console tab for runtime manipulation |
| Text Editor (optional) | Analyze source code offline |

### Installation

No installation required. Open the game in any modern web browser.

## Solution Path

### Phase 1: Reconnaissance

| Step | Command/Action | Purpose | Finding |
|------|----------------|---------|---------|
| 1 | Play through Levels 1-4 | Attempt normal completion | Level 4 is significantly harder |
| 2 | Look for shortcuts | Try to bypass gameplay | No obvious shortcuts found |
| 3 | Conclusion | Playing takes too long | Investigate code instead |

### Phase 2: Source Analysis

| Step | Command/Action | Purpose | Finding |
|------|----------------|---------|---------|
| 1 | View Page Source (Ctrl+U) | Access raw HTML/JS | Obfuscated JavaScript present |
| 2 | Search for "flag" | Locate flag references | No direct match |
| 3 | Search for "win" | Locate win logic | Found `_0xwin()` function |
| 4 | Analyze `_0xwin()` | Understand win condition | Checks `level > 4` and `keysCollected === 3` |
| 5 | Analyze `_0x4a2b` | Find flag parts | Flag components located |
| 6 | Locate flag parts | Assemble flag | Flag pieces identified |

### Phase 3: Runtime Exploitation

| Step | Command/Action | Purpose | Finding |
|------|----------------|---------|---------|
| 1 | Open Console tab (F12) | Access JS runtime | Console ready |
| 2 | Type `level = 5` | Set level variable | Level set to 5 |
| 3 | Type `keysCollected = 3` | Set keys variable | Keys set to 3 |
| 4 | Type `checkWin()` | Trigger win check | Flag revealed in console/alert |

### Phase 4: Submission

| Step | Command/Action | Purpose | Finding |
|------|----------------|---------|---------|
| 1 | Read the flag | Extract flag from output | `IE3132{gh0st_pl4ys_t0_w1n}` |

## Flag

```
IE3132{gh0st_pl4ys_t0_w1n}
```

## Hints

<details>
<summary><b>Hint 1</b></summary>
"The game seems beatable, but maybe you don't need to play it at all. Open your browser's Developer Tools (F12) and explore JavaScript."
</details>

<details>
<summary><b>Hint 2</b></summary>
"There's a function in the code called `_0xwin()`. Find it. What two variables does it check?"
</details>

<details>
<summary><b>Hint 3</b></summary>
"The win condition requires `level > 4` and `keysCollected === 3`. Can you set these values from the Console tab?"
</details>

<details>
<summary><b>Hint 4</b></summary>
"Try typing `level = 5` and `keysCollected = 3` in the Console, then call `checkWin()`. What happens?"
</details>

## Red Herrings

| Red Herring | Why It's a Trap | What Participants Might Try |
|-------------|-----------------|----------------------------|
| `particles` array | Visual background effect | Thinking it encodes data |
| `ghost.speed` values | Gameplay tuning only | Setting ghost speed to 0 and playing |
| `bgImage.src` | Just a background image | Trying to read stego from PNG |
| `TOTAL_LEVELS = 4` | Level count, not flag length | Trying to set to other numbers |

## Hidden Artifacts

| Artifact | Location | Value |
|----------|----------|-------|
| Win function | JavaScript source | `_0xwin()` |
| Flag parts | JavaScript source | `_0x4a2b` |
| Win condition | `_0xwin()` function | `level > 4 && keysCollected === 3` |
| Flag | Runtime output | `IE3132{gh0st_pl4ys_t0_w1n}` |

## Stage Specification

| Field | Information |
|-------|-------------|
| Stage ID | CTF-RE |
| Title | The Ghost's Game |
| Domain | Reverse Engineering, Client-Side Analysis, JavaScript Forensics |
| Difficulty | Hard |
| Difficulty Justification | Multi-step chain: gameplay → source analysis → variable manipulation → function invocation. Requires understanding of JavaScript runtime, DevTools usage, and logical reasoning. The win condition is non-obvious and hidden behind obfuscated names. |
| Scenario | PulseForge Studios' game Ghost Runner was trojanized by a rival attacker, SilentPlayer. A hidden flag is embedded in the JavaScript. Recover it to prove tampering. |
| Learning Objective | Apply client-side reverse engineering to identify and manipulate a JavaScript game's win condition, extracting hidden data via runtime inspection. |
| Environment | Single HTML file (`ghost_runner.html`) + `background.png`, hosted statically on GitHub |
| Player Task | Analyze the game's source, find the win condition, and either (a) complete Level 4 legitimately or (b) force the win via DevTools Console |
| Tools Required | Web browser, DevTools (F12), Text Editor (optional) |
| Flag Format | `IE3132{gh0st_pl4ys_t0_w1n}` |

## Author Notes

This challenge is designed to simulate a realistic reverse engineering scenario. Participants are expected to:

- Apply client-side reverse engineering techniques to analyze JavaScript game logic
- Identify hardcoded values and winning conditions in obfuscated code
- Use browser Developer Tools to inspect runtime state and modify variables
- Trigger functions manually to bypass game restrictions
- Chain multiple analysis steps from source reading to runtime exploitation

The trail is intentionally multi-layered and requires patience and attention to detail to complete successfully.

---

*Happy investigating, and remember: the evidence is in the code. The ghost left traces.*
