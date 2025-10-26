## pemacs

Tiny Emacs-flavored TTY editor in pure PHP — single file, no deps. ✨

This is a minimal, for-fun clone of some Emacs editing vibes written in PHP. It runs directly in your terminal, renders with ANSI escapes, and aims to be surprisingly usable despite its size. It was vibe-coded in a few hours while doing other stuff — so please don’t take it too seriously. 😄

### Highlights
- **Single-file**: just `pemacs` — easy to read, hack, and run.
- **Pure PHP**: no extensions required (optional `pcntl` for nicer signal handling).
- **TTY-native**: uses raw mode, alternate screen buffer, and ANSI rendering.
- **Syntax color**: simple highlighter for PHP, JS, and HTML (tags/attrs), numbers, strings, comments.
- **Status bar**: file name, modified flag, and cursor position.
- **Incremental search**: Emacs-style `I-Search` with live updates.
- **Selections and kill ring-ish**: set mark, kill region, yank.
- **Window splits**: basic horizontal split (2 panes) with quick toggle.
- **Smart indent**: tab-based indentation, block-aware newline.
- **Bracket jumps**: jump to matching bracket forward/backward.
- **Mini-prompts**: inline prompts for search, goto line, and find-file.

### Requirements
- **PHP 7.4+**
- **Linux TTY** (works best on a real terminal; tmux/screen generally fine)
- `stty` and `tput` available on PATH
- Optional: `pcntl` for signal handling (clean restores on Ctrl+C, etc.)

### Install
```bash
git clone https://github.com/mikeitnow/pemacs.git
cd pemacs
chmod +x pemacs
```

### Run
```bash
./pemacs [optional-file]
# or
php pemacs [optional-file]
```

If you pass a path that doesn’t exist, pemacs will create the file on save. It enters the terminal’s alternate screen and restores your TTY on exit. If your terminal looks weird after a crash, run `reset`.

### Keybindings ⌨️

#### Files
| Key | Action |
| --- | --- |
| `C-x C-f` | Find file (with a tiny picker; Tab completes; arrows navigate) |
| `C-x C-s` | Save file |
| `C-x C-c` | Quit (asks if buffer is modified) |

#### Windows (horizontal split)
| Key | Action |
| --- | --- |
| `C-x 2` | Split window |
| `C-x o` | Other window |
| `C-x 1` | Make current window the only one |
| `C-x 0` | Close current window |

#### Navigation
| Key | Action |
| --- | --- |
| Arrows | Move cursor |
| `Home` / `End` | Line start/end |
| `PgUp` / `PgDn` | Scroll by window height |
| `C-a` / `C-e` | Beginning/End of line |
| `M-b` / `M-f` | Move by word backward/forward |
| `C-PgUp` / `C-PgDn` | Jump to previous/next blank-block |
| `C-Up` / `C-Down` | Same as above (terminal dependent) |
| `C-l` | Recenter view around cursor |
| `M-g` | Goto line |
| `M-C-b` / `M-C-f` | Jump to matching bracket backward/forward |

#### Editing
| Key | Action |
| --- | --- |
| printable chars | Insert |
| `Enter` | New line with smart indent (brace-aware) |
| `Tab` | Indent current line or selected region |
| `Backspace` / `Del` | Delete backward/forward |
| `C-SPC` | Toggle mark (start/stop selection) |
| `C-w` | Kill region (copy + delete) |
| `C-y` | Yank (paste) |
| `M-d` / `M-Backspace` | Kill word forward/backward |
| `C-x u` | Undo (simple snapshot-based) |
| `ESC ESC ESC` | Cancel selection (like Emacs) |

#### Search
| Key | Action |
| --- | --- |
| `C-s` | Incremental search; type to refine |
| `C-s` (again) | Next match |
| `Enter` / `ESC` | Finish search |
| `C-g` | Abort and jump back to origin |

Notes:
- Mark + region are shown with reverse video.
- Tabs are visualized as single spaces for rendering, but indentation uses real tabs.
- Clipboard is internal to pemacs (no system clipboard integration).

### Find File mini-picker 📁
- Inline list opens above the status bar.
- Type to filter; `Tab` to complete; `Enter` to open.
- `Up/Down` to select, `Right` to enter directory, `Left` to go up.
- `~` is expanded to `$HOME`. Relative inputs are resolved against current directory.

### Syntax colors 🎨 (rough, fast, readable)
- Comments: dim gray; Strings: bright red; Keywords: magenta; Functions: bright blue; Variables: yellowish; Numbers: blue.
- HTML tags and attributes are colored distinctly.

### Caveats & Tips ⚠️
- Linux TTY focused; other environments may vary. If the screen stays in alt buffer after a crash, run `reset`.
- Single buffer shared across splits (no multiple files at once yet).
- Minimal undo (snapshot-based) and no redo.
- This is a toy editor — expect rough edges. PRs welcome! 🙌

### Why PHP? 🐘
Because it’s fun to push languages into weird corners. Also: ubiquitous, instant startup, and perfect for a single-file TTY toy.

### License
GPL-3.0 — see `LICENSE`.

### Credits
Inspired by GNU Emacs and the countless tiny editors that came before. ❤
