# ⚡ TensorForge

**A LeetCode-style practice lab for PyTorch, NumPy, Python and Matplotlib.**
2,049 problems · 681 concepts · every one graded by real automated tests · an AI coach powered
by your own Groq key · ships as a single executable you double-click.

---

## Screens

| Library | Task / Practice |
|---|---|
| ![Library](https://github.com/user-attachments/assets/70bdf375-bbbf-41ed-96ae-132e30738442) | ![Task](https://github.com/user-attachments/assets/1cf8210a-fecb-4527-bc98-42cdf7abc495) |

---

## What you get

**Library**
One row per *concept*, not per file: `Broadcast add #1 / #2 / #3` collapse into a single row with
a `Variants` column showing `2/3`. Topic chips with solved counters, full-text search,
Status (unsolved · solved · partial · attempted · starred) and Difficulty filters, and **Shuffle**
when you don't want the same corner of the syllabus every day.

**Practice — three panes, all resizable**

| Pane | What it does |
|---|---|
| **Problem navigator** | the filtered problem list with live status dots, topic/difficulty segments, "unsolved only", and **Pick for me** (random problem under your current filters) |
| **Description** | prompt, required signature, worked example, graded hints, and what the hidden checks look for — tabs: `Description · AI Coach · Solution · Notes` |
| **Editor** | line-numbered Python editor, variant switcher, reset, **Run**, **Submit**, and a `Testcase / Test result` pane with per-check verdicts, stdout and rendered Matplotlib figures |

Drag the splitters to re-balance the panes (the layout is remembered); collapse a pane with `⟨`
and bring it back from the **Panes** row in the left rail; `⇄` swaps description and editor.

**AI coach** — replaces the "Theory" tab that showed you the answer

* **Hint n** — three escalating hints, aware of the code you have written
* **Review my code** — reads your failing checks and explains the bug
* **Explain solution** — walks through the reference solution
* **Chat** — streaming Q&A about shapes, broadcasting, gradients, why your loss is NaN…

**Progress** — segmented ring, current *and* best streak, recent activity, per-concept status,
notes and stars on every problem, JSON export.

---

## The problem bank

| Track | Problems | Concepts | Easy / Medium / Hard | Covers |
|---|---:|---:|---|---|
| 🔥 **PyTorch** | 846 | 282 | 162 / 510 / 174 | tensors & broadcasting, autograd, `nn` modules, losses, optimizers & schedulers, metrics, attention, data pipelines, internals |
| 🔢 **NumPy** | 675 | 225 | 144 / 459 / 72 | creation, indexing, broadcasting, reductions, linear algebra, statistics, sorting, random |
| 🐍 **Python** | 321 | 105 | 99 / 207 / 15 | core language, data structures, classes, generators, decorators, algorithms (two-sum → LRU cache → Roman numerals) |
| 📊 **Matplotlib** | 207 | 69 | all easy | lines, scatter, bars, hist, subplots, styles, legends, ticks, 3-D, images, violin/box |

Each problem ships with:

* a **starter snippet** with the exact required signature,
* a **worked example** (input → expected output),
* **hidden tests** — randomised cases plus edge cases; for plots, property checks on the actual
  artists (colours, labels, limits, ticks, legend location, bar heights…), not pixels,
* **3 graded hints**, plus an AI version that reads your code,
* a **reference solution** you can reveal or have explained.

### Why 2,049 problems but 681 rows?

Most concepts were generated in three variants (`#1`, `#2`, `#3`) with different shapes and edge
cases. The library groups them into one row; the variant picker in the editor header moves between
them, and a concept only counts as *solved* when all of its variants pass.

---

## How the checking works

* `runner.py` executes your submission in a **separate process**, then runs each check against it.
* A warm worker is kept alive between runs, so a `▶ Run` answers in milliseconds instead of
  re-importing torch on every click.
* Infinite loops are cut off by a wall-clock timeout; a crashed worker is detected and replaced.
* stdout and Matplotlib figures are captured and shown in the **Test result** tab.
* Plot problems are graded by inspecting artists, so students can style freely while the required
  structure is still enforced.

---

## Quick start

### A. Windows, one file to double-click *(recommended)*

1. Double-click **`build_windows.bat`**.
   It finds a Python 3.9+ (or installs 3.12 by itself via winget / a silent python.org install),
   creates `.venv`, installs Flask/NumPy/Matplotlib/PyTorch (~250 MB, CPU build), then freezes
   everything into **`dist\TensorForge.exe`**. First run: 10–20 minutes, ~3 GB free disk.
2. Double-click **`dist\TensorForge.exe`**. Your browser opens `http://127.0.0.1:8765`.

No Python on the PC? That's handled — the script detects the Microsoft Store stub and installs a
real interpreter. Re-running the build while TensorForge is open is also fine: the script closes a
running copy first, and `build_exe.py` retries, renames or relocates the old exe instead of dying
with `WinError 5`.

### B. Run it without building an exe

Double-click **`run_from_source.bat`**. Same dependency install, but it starts the app directly and
skips the 5–10 minute freeze. Ideal while you're still poking at things.

### C. Build on GitHub's machines (no Python locally)

Push the project to a repo, then **Actions → “Build TensorForge.exe” → Run workflow** and download
the `TensorForge-windows` artifact. The workflow is in `.github/workflows/build-windows.yml`.

### D. macOS / Linux

```bash
python -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt
pip install torch --index-url https://download.pytorch.org/whl/cpu   # avoids the CUDA download
python app.py                       # http://127.0.0.1:8765
python build_exe.py                 # or: dist/TensorForge
```

---

## Setting up the AI coach

1. Get a free key at **[console.groq.com/keys](https://console.groq.com/keys)**.
2. In the app: **Settings** (bottom-left) → paste the key → **Test connection** → **Save**.

The key is stored locally in `tensorforge.db` and survives restarts; you can replace or remove it
from the same screen at any time. Defaults:

| Setting | Default |
|---|---|
| Base URL | `https://api.groq.com/openai/v1` |
| Model | `qwen/qwen3.8-27b` |
| Temperature | `0.6` |
| Max tokens | `1200` |

Any OpenAI-compatible endpoint works (Groq, OpenRouter, vLLM, Ollama, LM Studio…) — change **Base
URL** and **Model**. Everything else runs on your machine; the only network traffic is to the
endpoint you configure. **Without a key the app still works**: the built-in hints, tests and
reference solutions don't need the AI.

---

## Keyboard shortcuts

| Key | Action |
|---|---|
| `Ctrl` + `Enter` | Run the tests |
| `Tab` / `Shift` + `Tab` | Indent / unindent (or indent the selection) |
| `Enter` | keep the current indentation, extra indent after `:` |
| `Ctrl` + `/` | toggle `#` comment on the line |
| `/` | jump to search (library) |
| `Esc` | back to the library, or close a dialog |
| `Enter` in chat | send · `Shift` + `Enter` for a newline |

**Run** and **Submit** both execute the full hidden suite; the verdict, progress, streak and
variant counters update either way. Code autosaves 0.8 s after you stop typing.

---

## Your data

| OS | Path |
|---|---|
| Windows | `%APPDATA%\TensorForge\` |
| macOS | `~/Library/Application Support/TensorForge/` |
| Linux | `~/.local/share/tensorforge/` |

* `tensorforge.db` — settings (API key), progress, notes, bookmarks
* `tensorforge.log` — startup log, useful if the app ever fails to appear

Set `TENSORFORGE_HOME=/some/dir` to override (handy for a USB-stick install).
**Settings → Export progress** downloads a JSON snapshot; **Reset progress** clears it.

---

## Command-line flags

```
--port 8765        port for the local server
--host 127.0.0.1   bind address (use 0.0.0.0 to reach it from another device)
--no-browser       don't open a browser tab automatically
```

Starting a second copy while one is already running no longer crashes: it detects the existing
instance and opens it. If the port belongs to something else you get
`Port 8765 is used by another program. Try: --port 8766`.

---

## Building

```bat
build_windows.bat                      :: zero-click: venv + deps + PyInstaller
python build_exe.py --clean            :: manual, current OS
python build_exe.py --onedir           :: folder build — starts much faster, no temp unpack
```

Output is a single file (~175 MB Windows, ~240 MB Linux with the CPU torch wheel). One-file builds
unpack their runtime into `%TEMP%` on every launch, so the first window takes 10–30 s; `--onedir`
avoids that at the cost of a folder instead of one file.

`tensorforge.spec` handles the awkward parts: it bundles the problem bank and the HTML, ships
torch's Python sources (some problems use `inspect.getsource`), adds `ctypes.util`/`ctypes.wintypes`
(used by `torch._dynamo`), bundles the MSVC runtime DLLs, and monkeypatches PyInstaller's binary
probe so it doesn't try to import torch's optional CUDA/ROCm libraries.

---

## Project layout

```
app.py                 Flask app: bank loader, SQLite progress, AI proxy, settings, export
runner.py              isolated test worker (warm process, JSON protocol)
templates/index.html   the entire UI — one file, inline CSS/JS, no CDN or web fonts
bank/*.json            2,049 problems: prompt, starter, reference solution, generated checks
tools/                 problem generators (dsl.py, specs_*.py) + validate.py
build_bank.py          regenerates bank/ from the specs
tensorforge.spec       PyInstaller spec (one-file, splash, icon, torch hooks)
hooks/hook-torch.py    curated torch hook: ships the .py sources, drops dynamo/inductor extras
build_exe.py           build helper (--clean, --onedir, locked-exe recovery)
build_windows.bat      one-click Windows build (auto-installs Python if needed)
run_from_source.bat    run without freezing
docs/                  screenshots used by this README
```

---

## HTTP API

The UI is just a client of these routes — handy if you want to script anything.

| Method | Route | Purpose |
|---|---|---|
| GET | `/api/home` | counts, streak, recent activity, AI status |
| GET | `/api/problems?topic=&difficulty=&status=&q=&shuffle=1` | library rows (concepts + variants) |
| GET | `/api/problem/<id>` | prompt, starter, hints, checks, variants, saved code/notes |
| GET | `/api/random?topic=&difficulty=&unsolved=1` | a random problem for **Pick for me** |
| POST | `/api/run` | `{id, code}` → verdict, per-check results, figures, stdout |
| POST | `/api/save` · `/api/note` | autosave code · notes and stars |
| GET/POST | `/api/settings` · `/api/settings/test` | API key, model, connection test |
| POST | `/api/hint` · `/api/review` · `/api/explain` | AI hint levels, code review, walkthrough |
| POST | `/api/chat` | streaming (SSE) tutor chat |
| GET | `/api/export` | JSON progress export |

---

## Troubleshooting

| Symptom | Fix |
|---|---|
| Windows SmartScreen warning | "More info" → "Run anyway" — the exe is unsigned |
| `PermissionError: [WinError 5] Access is denied: …\dist\TensorForge.exe` | TensorForge was still running (Windows locks a running exe). The builder now kills it, retries the delete, renames the old file, or builds to `dist-build\` and swaps. Close the app / pause antivirus and re-run. |
| `The process cannot access the file … being used by another process` | Same cause. `build_windows.bat` now kills a stray `TensorForge.exe` before it starts. |
| Port already in use | `TensorForge.exe --port 8766` |
| AI says "No API key" | Settings → paste key → **Test connection**. Built-in hints work without it. |
| AI returns 401 | The key is invalid or revoked — paste a fresh one in Settings. |
| First launch takes 20–30 s | One-file builds unpack once per launch; later runs are cached by the OS (`--onedir` avoids it) |
| Antivirus quarantines the exe | Common for unsigned PyInstaller binaries — whitelist it, or build locally |
| `VCRUNTIME140.dll` missing | The exe bundles it; if antivirus stripped it, install the [VC++ 2015-2022 redistributable](https://aka.ms/vs/17/release/vc_redist.x64.exe) |
| Build fails on memory | The freeze peaks around 1.5 GB RAM — close other programs and retry |

---

## Notes and limitations

* TensorForge is a **local web app**: the executable starts a server on `127.0.0.1:8765` and opens
  your browser. There is no Electron window, and nothing is uploaded anywhere.
* The AI features need a working key and an internet connection; the graded tests never do.
* Optimizer/scheduler problems inspect state (`param.data`, `param_groups`, `lr`) rather than pixel
  output, and plot problems inspect artists — both are deterministic, unlike image diffing.
* The problem bank was generated and validated programmatically, so a handful of prompts read a
  little mechanical — every one of them is still graded by executable checks.
