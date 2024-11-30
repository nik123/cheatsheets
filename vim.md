# Vim

Other cheat sheets:
- https://devhints.io/vim

# Text objects

- `g_` - like `$` but without newline character.
- `0` - begining of the line
- `^` - first word in the line

# Folding

- `zM` - close all
- `zR` - open all
- `za` - toggle
- `zo`/`zc` - open/close non-recursively 

# Commands

- `dt<character>` - delete til character, e.g. `dtc` - delete til next 'c' occurence.
- `:setlocal ff=unix` - replace Windows line endings with Linux line endings.

## Navigation

- `c-u`, `c-d`. half-page up, half-page down.
- `{`, `}` - next empty line, previous empty line.

# Misc.

- Ctrl + r - redo
- i - insert before cursor
- a - insert after cursor
- `>`, `<` (in visual mode) - shift line rightwards or leftwards.
- `"+y` - copy to system clipboard(neovim).
- Copy text from registr to vim command line: enter command mode, press `:`, press `ctrl+r`, press `"`.

# Search

Search text selected in visual mode:
1. Select text
2. Yank
3. `q/p` - for details about 'q' see vim help on command-line window.
