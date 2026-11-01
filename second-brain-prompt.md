Build me a self-improving knowledge base: a "second brain" that gets smarter every time I use it.
It follows Andrej Karpathy's "LLM Wiki" idea (summarized at the bottom of this prompt; read that first).
No databases, no plugins, no code. Just plain folders and markdown files.

I will use you in BOTH Claude Code in the terminal AND the Claude desktop app, on the same folder.
The topic is EVERYTHING IN MY LIFE.

========================================================
STEP 1: TELL ME THE PLAN, THEN WAIT FOR "GO"
========================================================
Don't interview me with a list of questions. In a few plain-English lines, tell me:
- WHERE you'll build it. The workspace root is the folder you're running in right now
  (state its full path). CLAUDE.md goes in that root. Everything else goes in a
  "knowledge-base/" folder inside it.
- WHAT you'll create (the folders and files listed under STEP 2).
- THE DEFAULTS: the topic is everything in my life; I mostly feed it by pasting links;
  the Dream Sequence runs weekly; version history (git) is turned on if git is already
  installed.
Then ask me to reply "go", and tell me I can change the folder name or any default in
that reply.
Build NOTHING until I say "go".

========================================================
STEP 2: THE STRUCTURE
========================================================
<workspace root>/
  CLAUDE.md                  <- the rulebook. It lives here, one level ABOVE knowledge-base/,
                                so you load it automatically when I open this folder in
                                the terminal or the desktop app.
  knowledge-base/
    raw/                     <- SOURCES ONLY. What I bring in: links (saved as text),
                                articles, files, notes, transcripts. A flat folder.
                                NEVER edited, renamed or deleted after it is saved.
                                (One exception: raw/assets/ may hold downloaded images.)
    sessions/                <- takeaways from our chats, written by you, one dated file
                                per saved session. Kept OUT of raw/ because you wrote them.
    pages/                   <- THE BRAIN'S CONTENT. Clean, linked notes you write and keep
                                up to date: topic pages, people/place/thing pages, source
                                summaries, saved answers, and hub pages.
    wiki/                    <- BOOKKEEPING ONLY. Exactly three files, nothing else:
      index.md               <-   table of contents (points to the pages in pages/)
      log.md                 <-   dated diary of everything that happened
      processed.md           <-   checklist of which raw/ and sessions/ files are filed
    outputs/                 <- finished briefings and reports you make for me.

HARD RULES ABOUT FOLDERS
1. raw/ never changes after a file is saved. You never put your own writing in raw/.
2. wiki/ holds ONLY index.md, log.md and processed.md.
3. Every page you write goes in pages/. Nothing you write goes in raw/.
4. "New material" means ONLY files in raw/ (top level, not raw/assets/) and sessions/
   that are not yet listed in wiki/processed.md. NEVER treat pages/, wiki/ or outputs/
   as new material.

========================================================
STEP 3: THE 5 OPERATIONS (explain these simply in CLAUDE.md)
========================================================
1. INGEST: I paste a link, file or text and say "add this".
   a. SAVE THE SOURCE FIRST, into raw/, named YYYY-MM-DD-short-title.md.
      - For a link: fetch the page and save the TEXT, not just the address, with this
        frontmatter at the top: source_url, fetched (date), title.
      - If the page won't load (paywall, login, blocked), tell me and ask me to paste
        the text or use the Obsidian Web Clipper. Never invent the contents.
      - For pasted text: save it as-is, with frontmatter: source: "pasted by me", date.
   b. CHECK FOR A REPEAT. If this source is already in processed.md, or a page already
      cites it, update the existing pages instead of making duplicates.
   c. Pull out the key points. Write a source-summary page, then create or update the
      related topic and people/place/thing pages in pages/, and link them together.
   d. If the new source DISAGREES with an existing page, keep BOTH claims, each with its
      source and date, and add it to that page's "Contradictions" section. Never quietly
      overwrite the old claim.
   e. Update wiki/index.md, then append to wiki/log.md.
   f. LAST STEP: add a row to wiki/processed.md listing every page you touched.
      (Doing this last means an interrupted run gets retried instead of skipped.)

2. QUERY: I ask "what do I know about ___?" (or any question).
   Read wiki/index.md first, then the relevant pages, then answer WITH links to the
   pages and sources you used. Say clearly when my notes don't cover something.
   If I say "save that", file the answer as a new page in pages/ (type: answer), link it
   from the related pages, update the index and log it.
   If I ask for a briefing or report, save it in outputs/ and log it.

3. DREAM SEQUENCE (tidy-up and health check): runs weekly, or when I say "dream sequence".
   a. Ingest any new material (by the definition in hard rule 4).
   b. CHECK THE CHECKLIST: every file in raw/ and sessions/ is in processed.md; every row
      in processed.md points to a file that exists; every source is cited by at least one
      page. Fix or flag anything that doesn't match.
   c. TIDY: look for contradictions, outdated claims, duplicate pages (merge them and keep
      the links working), orphan pages (nothing links to them), missing links, and
      important things mentioned often but without their own page.
   d. SCOPE: normally check only pages changed since the last dream (find them in log.md)
      plus the pages they link to. On the first dream of each month, check everything.
   e. Collect "Open questions" and gaps worth filling. Suggest up to 5 things I could add
      or look up next.
   f. Append ONE summary entry to log.md: what was filed, fixed and flagged.
   g. Never delete anything from raw/. Never resolve a contradiction about MY life (health,
      money, relationships, plans) on your own; flag it and ask me.

4. INDEX + LOG
   - wiki/index.md stays a clean table of contents, grouped by the life areas below, with
     one line per page: [[page-name]] - one-line summary (N sources, last updated).
   - Once a life area has more than ~30 pages, give it a hub page in pages/
     (e.g. hub-health.md) and have index.md point to the hub instead of every page.
   - wiki/log.md is append-only. Every entry starts with:
       ## [YYYY-MM-DD] ingest|query|dream|session|setup - short title
     followed by 1-3 lines saying what changed. At the start of each new year, move the
     old year's entries to the bottom under an "## Archive YYYY" heading.

5. SESSION CAPTURE: when I say "save this session", or at the end of any substantial
   chat (offer it: "Want me to save this session?"):
   write sessions/YYYY-MM-DD-short-title.md with the key takeaways, decisions and anything
   I said about myself. Mark it "source: chat with Claude (written by Claude)". Then
   ingest it like any other source. When a page uses it, cite it as "from our chat on
   <date>" so I can tell what I said apart from what a published source said.

THE SELF-IMPROVING RULE (mandatory): every ingest, every saved answer and every session
capture MUST update at least one page in pages/ AND append to wiki/log.md.

========================================================
STEP 4: FORMATS (put these in CLAUDE.md)
========================================================
File names: lowercase-with-hyphens.md, and unique across the whole knowledge base
(links find pages by file name, whatever the folder).

Every page in pages/ starts like this:
---
type: topic | person | place | thing | source-summary | answer | hub
area: <one of the life areas>
sources: <number>
created: YYYY-MM-DD
updated: YYYY-MM-DD
---
# Title
Short summary (2-4 sentences).
## Key points        (every claim cited: [[source-summary-page]] or "from our chat on <date>")
## Related           ([[links]])
## Contradictions    (only if any: both claims, sources, dates)
## Open questions    (gaps worth filling)

wiki/processed.md is a table:
| file | added | processed | pages touched |
|---|---|---|---|

LIFE AREAS (starting categories for index.md; add more when needed):
Health & Fitness · Work & Career · Money · Relationships & People · Learning & Ideas ·
Home & Life Admin · Hobbies & Interests · Goals & Plans · Travel · Journal & Reflections

PRIVACY RULE: this is about my whole life, so NEVER store passwords, PINs, full card or
bank numbers, ID or passport numbers, or login codes, even if I paste them. Leave them out
and tell me you did.

========================================================
STEP 5: BUILD IT (only after I say "go")
========================================================
- Create the folders: knowledge-base/raw/, knowledge-base/raw/assets/,
  knowledge-base/sessions/, knowledge-base/pages/, knowledge-base/wiki/,
  knowledge-base/outputs/.
- Write CLAUDE.md at the workspace root as a clear rulebook: the structure and hard rules,
  the 5 operations, the formats, the self-improving rule, the privacy rule, and the
  "missed dream" rule below. Write it so a future session with no memory of this chat can
  follow it exactly.
- Seed wiki/index.md with the life areas as empty headings, wiki/processed.md as an empty
  table, and wiki/log.md with a first entry: "## [today] setup - second brain created".
- If git is already installed, turn on version history for the workspace and save a first
  snapshot, so any change can be undone. If it isn't installed, skip this and tell me.
  Don't install anything.
- Folders and markdown only. No scripts.

========================================================
STEP 6: SCHEDULE THE DREAM SEQUENCE (be honest about what's possible)
========================================================
I use both the terminal and the desktop app on this folder.
- DESKTOP APP: if this session can create scheduled tasks, set up a weekly local task in
  THIS workspace that runs "dream sequence". If you can't, give me the exact clicks to do
  it myself in the desktop app. Remind me it only runs while the app is open and the
  computer is awake.
- TERMINAL: a schedule made inside a terminal session stops when the session closes, so
  don't rely on it. Only offer my computer's own scheduler if I ask for it, and explain
  plainly what it would do.
- SAFETY NET (always, in CLAUDE.md): "MISSED DREAM RULE: at the start of every session,
  check the date of the last dream entry in wiki/log.md. If it's more than 7 days old,
  say so and offer to run the dream sequence now."
- Tell me how to change the schedule (e.g. "make the Dream Sequence run daily").

========================================================
STEP 7: TEACH ME, IN 3 THINGS
========================================================
Explain in plain English, like to a smart friend who isn't technical (define any term in
one line). Give ONE concrete example for each:
1. FEED IT: paste a link and say "add this". Say "save this session" at the end of a good
   chat. Optional: the Obsidian Web Clipper (a browser add-on) can save web pages straight
   into knowledge-base/raw/.
2. ASK IT: "what do I know about ___?", with sources. Say "save that" to keep a good answer.
3. DREAM SEQUENCE: the weekly tidy-up, what it does, and how to run it by hand.
Then give me these tips:
- Always open the WORKSPACE ROOT folder (the one with CLAUDE.md) in both the terminal and
  the desktop app, so you always load the rules.
- To stop being asked permission for every file, allow file edits in this folder.
- Optional: open knowledge-base/ in Obsidian to browse the pages and see the links as a
  graph.
- Never rename or edit files in raw/. To correct something, add a new dated file.
End with my daily commands:
  "add this" · "what do I know about ___" · "save that" · "save this session" · "dream sequence"

========================================================
STEP 8: AFTER BUILDING, ASK ME ONE QUESTION
========================================================
"Want me to give your second brain a head start? Tell me 3-5 things in your life you care
about most right now (e.g. a fitness goal, your job, a trip, a skill). I can research them
online and write starter pages, clearly marked as 'researched by Claude', so it isn't empty
on day one. (yes / no, and which topics)"

========================================================
THE IDEA BEHIND THIS (based on Andrej Karpathy's "LLM Wiki")
========================================================
- Usually an AI re-reads your documents from scratch for every question, so nothing builds
  up. Here, the AI reads each source ONCE and works it into a growing set of linked notes:
  it updates summaries, links related ideas and flags where new information disagrees with
  old. The knowledge is put together once and then kept up to date.
- Three layers: RAW SOURCES (never changed, the source of truth), THE WIKI (pages the AI
  writes and maintains; I read them), and THE RULEBOOK (CLAUDE.md, which turns the AI into
  a careful librarian instead of a general chatbot).
- Three core moves: INGEST (add a source; one source may touch many pages), QUERY (answer
  from the pages with sources, and file good answers back in so they aren't lost in chat
  history), and LINT (regular health checks for contradictions, outdated claims, orphan
  pages, missing links and gaps).
- index.md is the table of contents you read first when answering. log.md is the diary;
  its consistent "## [date] type - title" format makes it easy to scan.
- People give up on wikis because the bookkeeping grows faster than the value. An AI
  doesn't get bored and can update 15 files in one go, so upkeep costs almost nothing.
  My job: choose sources, ask good questions and think about what it means. Your job:
  everything else.
- This approach works well up to roughly 100 sources and a few hundred pages. Past that,
  rely more on hub pages, and I may decide later to add a search tool.
