# 🧠 Second Brain: One-Page Cheat Sheet

**What it is:** a notebook of plain folders and text files that an AI (Claude) keeps organized for you.
**You** add things and ask questions. **The AI** files, summarizes, links and tidies.

---

## 🗂️ The folders

| Folder / file | What it's for | Who changes it |
|---|---|---|
| `raw/` | Drop box for links, articles and notes | You add. **Nobody edits.** |
| `pages/` | Clean, linked notes | AI |
| `wiki/index.md` | Table of contents | AI |
| `wiki/log.md` | Diary of what happened and when | AI |
| `wiki/processed.md` | Checklist of what's already been filed | AI |
| `outputs/` | Finished reports and briefings | AI |
| `CLAUDE.md` | Rulebook the AI follows (sits one folder up) | You and the AI |

> ⚠️ **One change from the original prompt:** keep the AI's notes in `pages/`, **not** inside `raw/`.
> Otherwise the AI may re-file its own notes over and over.

---

## 💬 The 4 things you'll say

| Say this | What happens |
|---|---|
| **"add this"** + a link, file or text | Saved to `raw/`, turned into notes, then added to the table of contents, diary and checklist |
| **"what do I know about ___?"** | Answer built from your notes, with sources |
| **"save that"** | That answer becomes a new note |
| **"save this session"** | Key points from this chat are saved into the notebook |

Bonus: **"dream sequence"** runs the tidy-up right away.

---

## 🌙 The weekly tidy-up (Dream Sequence)
- Files anything new in `raw/`
- Fixes notes that disagree with each other
- Merges duplicates
- Links up notes that nothing points to
- Lists gaps worth filling

---

## 💻 Setting it up on your computer
1. Install **Claude Code** or the **Claude desktop app**.
2. Make a folder, for example `my-brain/`, and open it in Claude.
3. Paste the Second Brain prompt, with the fix above, then reply **"go"**.
4. *(Recommended)* Turn on **git** (version history) so you can undo mistakes.
5. *(Optional)* Open the folder in **Obsidian** to browse your notes and their links.
6. *(Optional)* Install the **Obsidian Web Clipper** to save web pages straight into `raw/`.

**Weekly tidy-up:** it runs only while your computer is on and Claude is open. If it's missed, just say **"dream sequence"**.

---

## ✅ Golden rules
- **Never rename or edit** files in `raw/`. Add a new dated file instead.
- **Save the article text**, not just the link, because links can break.
- **Check the AI's notes now and then.** It can make mistakes.
- **When it gets big** (around 100+ articles): group notes into sections like Health, Work and Money.
