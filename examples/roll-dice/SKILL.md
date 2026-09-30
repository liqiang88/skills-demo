---
name: roll-dice
description: >-
  Rolls dice by generating random numbers via terminal commands. Use when the
  user asks to roll dice, 掷骰子, pick a random number in a dice range, or wants
  a demo of randomness from the shell.
disable-model-invocation: true
---

# Roll Dice

## Instructions

When this skill is invoked:

1. Parse the request:
   - Default: one 6-sided die (`1d6`) → integer in `1..6`
   - `NdM` (e.g. `2d6`, `1d20`): roll `N` dice with `M` faces each; each face is `1..M`
   - If only a face count is given (e.g. "d20"), treat as `1d20`
2. Generate randomness **only** by running a terminal command. Do not invent numbers yourself.
3. Prefer this cross-platform command (replace `MIN` / `MAX` with inclusive bounds):

```bash
python -c "import random; print(random.randint(MIN, MAX))"
```

On Windows PowerShell, this is also fine for a single roll:

```powershell
Get-Random -Minimum MIN -Maximum (MAX + 1)
```

4. For `NdM`, run the command once per die (or one Python one-liner that prints all rolls), then sum if the user asked for a total.
5. Reply briefly with the rolls (and total when `N > 1` or the user asked for it). No extra commentary unless asked.

## Examples

**User:** 掷骰子  

```bash
python -c "import random; print(random.randint(1, 6))"
```

**Agent:** 🎲 4

**User:** roll 2d6  

```bash
python -c "import random; print(*(random.randint(1, 6) for _ in range(2)))"
```

**Agent:** 🎲 3 + 5 = 8

**User:** d20  

```bash
python -c "import random; print(random.randint(1, 20))"
```

**Agent:** 🎲 17
