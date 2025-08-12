# useful-bash-scripts

A small collection of scripts to speed up development workflows.

## Scripts

### rr — rerun a script on save (with clear screen + timestamp)

`rr` watches a single source file and re-runs it automatically whenever you save changes. It clears the screen before each run and prints a timestamp so you can see when the last execution happened.

Supported file types:
- `.py` → runs with `python3`
- `.js` → runs with `node`

#### Requirements
- macOS or Linux
- [`entr`](https://eradman.com/entrproject/) installed
  - macOS: `brew install entr`
  - Debian/Ubuntu: `sudo apt-get install entr`
- The appropriate runtime for your file type (`python3` or `node`)

#### Installation
You can use the script in-place or put it somewhere on your `PATH`:

```bash
chmod +x rr
# Option A: symlink into a bin directory on your PATH
ln -s "$PWD/rr" /usr/local/bin/rr
# Option B: add this repo directory to your PATH in your shell config
```

#### Usage

```bash
rr <file> [args...]
```

Examples:

```bash
# Python
rr app.py
rr tools/task.py --verbose --limit 10

# Node.js
rr server.js --port 3000
```

Behavior details:
- Exits early if the file does not exist or the extension is unsupported
- Clears the terminal before each run (`entr -c`)
- Prints the current date/time, then runs your program
- Passes any extra arguments through to your program unchanged

#### Troubleshooting
- "entr: command not found" → install `entr` (see Requirements)
- "unsupported extension" → only `.py` and `.js` are supported currently
- "not found" → check the path to the file you want to watch

#### Possible enhancements
- Support more languages (e.g., `.ts`, `.rb`, `.go`)
- Allow watching multiple files or glob patterns
- Custom runner command per project

---

If you find this useful, feel free to copy/tweak to your needs or open a PR to add more tiny scripts.
