# Virtual CPU

**A hands-on computer for aspiring ethical hackers.**

Live demo: [ramji241.github.io/virtual-cpu](https://ramji241.github.io/virtual-cpu)

---

## The story

I work in finance. I'm not a computer scientist — I taught myself JavaScript on the side (shout out to [Leon Noel](https://leonnoel.com/) and 100Devs), and I have no background in security or ethical hacking.

My son developed an interest in hacking and wanted to understand what it actually involved. I enrolled him in a summer ethical hacking camp (grant-funded, so at least it only cost me gas money driving him there and back) that turned out not to be very useful. So instead I built him a curriculum myself using free online resources — PicoCTF, YouTube, community writeups.

The area I struggled with most, and knew he would too, was assembly language and boolean logic. Most resources either gloss over it or assume you already have the mental model. I couldn't find anything that let you *feel* how a CPU actually works — how bits flow through an ALU, how a jump instruction reads flags, how C source maps to the instructions that actually run.

So I built this.

I'm sharing it to get feedback from the community on its technical accuracy, and to find out whether something like this could be genuinely useful to aspiring hackers who are starting from zero.

---

## What this is

Virtual CPU is an interactive browser app that teaches how a computer works from the ground up — from binary arithmetic through to a running assembly program with a C source monitor. No install, no account, no frameworks. One HTML file.

---

## What you can do

### ALU workbench
Work through binary arithmetic the way a real CPU does it — bit by bit. Ten operations: ADD, SUB, AND, OR, XOR, NOT, SHL, SHR, EQ, GT. Guided examples walk you through the carry flag, signed vs unsigned interpretation, and bitwise operations. Free practice mode lets you set your own inputs.

### Registers, Flags, Memory
Inspect the CPU's working state at any time. See how values move between the four registers (R0–R3), the flags register (Zero, Carry, Bit 7), and RAM. Click any memory slot to inspect its value in decimal, binary, and hex.

### Control unit
Step through a randomly generated assembly program instruction by instruction. The program is shown in both assembly and C side by side — the C monitor highlights the current line as each instruction executes, making the compiler-to-assembly relationship concrete.

When the program completes, try the **hack challenge**: modify an instruction and predict the new output. Six difficulty levels, each requiring a different kind of reasoning:

| Level | Challenge |
|-------|-----------|
| 1 | Change one ALU operation, predict the output |
| 2 | Flip a jump condition, trace the new execution path |
| 3 | Swap operand registers, trace the new data flow |
| 4 | Change a seed value, trace propagation through the program |
| 5 | Make two simultaneous changes, predict the combined effect |
| 6 | Given a target output, find the single change that produces it |

Higher levels unlock as you build a streak of correct answers without hints.

---

## Progression system

- Correct answer without reveal → XP + streak bonus
- Correct answer after reveal → streak resets, no XP (reveal is for learning, not grinding)
- Wrong answer → streak resets
- Each level unlocks when you hit a streak threshold at the previous level

Save your progress as a JSON file and load it back any time. Multiple users supported in the same save file.

---

## Why C in the monitor?

Assembly is what the CPU actually executes. C is a higher-level language that a compiler translates into those assembly instructions. Showing both at once makes the relationship concrete: the type declarations in C (`int` vs `unsigned int`) are what give meaning to the carry flag — the CPU itself never decides signed vs unsigned, the program does.

The assembly used here is a simplified teaching version, not tied to any real architecture. The concepts — registers, flags, jumps, memory — are universal across x86, ARM, and everything else you'll encounter in real CTF work.

---

## Status

`v0.1-beta` — actively in development. Feedback very welcome, especially from people who actually know what they're doing in this space (I don't).

Known limitations:
- **Desktop/tablet only** — not optimised for mobile. Works best on a screen at least 768px wide. Mobile support is on the roadmap if there is interest.
- The assembly instruction set is simplified and does not map to any real CPU
- The C source shown in the monitor is illustrative, not compilable
- Save/load uses a downloaded JSON file — no server, no accounts

---

## Feedback

Open an issue or start a discussion. Particularly interested in:
- Whether the simplified instruction set and C mapping are accurate enough to be useful, or whether they teach bad habits
- Whether the difficulty curve across the six hack challenge levels feels right
- Gaps in the explanations that were confusing or misleading
- What concepts would be most valuable to add next, from the perspective of someone who actually does CTF work

---

## Built with

- Vanilla HTML, CSS, JavaScript — no frameworks, no build step, single self-contained file. CSS and JS are intentionally inline so the app can be downloaded and run locally without a web server.
- [Claude](https://claude.ai) (Anthropic) for development assistance
- [PicoCTF](https://picoctf.org/) as the inspiration and target curriculum
