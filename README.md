# Agentic OS Dashboard

A step-by-step guide to building your own Claude Code command center inside Obsidian. One screen for everything: live project status, one-click skill launchers, a news feed, meeting intelligence, and whatever metrics actually matter to your day.

Built on top of Claude Code as a custom Obsidian community plugin.

---

## How to use this guide

The fastest way is to paste the entire guide into a Claude Code session with this message:

> "Based on everything I'm going to tell you about my business and how I work, walk me through this guide step by step. Start with the three planning questions at the top. Wait for my answers before moving to any technical phase. Help me tune each decision to my specific setup as we go."

Claude picks up the full context, asks you the right questions, and walks you through every phase. You don't need to understand all the technical details yourself. Claude handles the code.

---

## Join the team

If you've made it this far and you're enjoying building with Claude, we're always looking for people to join PRGRMMD.

We're a growing AI agency installing AI operating systems into founder-led businesses. If you're comfortable with Claude Code, enjoy building automation systems, and want to apply that to real client work, we'd love to hear from you.

**[Apply to work with us →](https://forms.clickup.com/90161350719/f/2kz0j21z-21756/2CDXO69PY3T19A3I85)**

Or DM me directly on Instagram if you want to have a chat first.

---

## What you're building

A custom Obsidian plugin that gives you one screen for everything.

What I have on mine:

- Active client stages and delivery health
- Action queue from my morning brief
- Claude usage and task scorecard
- One-click skill launchers
- Today's calendar
- News and signals feed
- Meeting transcripts and email highlights

You'll build your own version. Different business, different cards.

---

## The key principle

Obsidian is the middle layer. The dashboard reads files in your vault. It doesn't pull data live from external tools directly. A headless Claude script runs in the background, queries your tools via MCP, and writes JSON files into the vault. The dashboard reads those files and displays them.

The more data you already route through your vault, the more powerful this becomes. If your morning brief writes to a file, the action queue can read it. If your meeting transcripts land in the vault, the Intelligence tab can surface them. Build the flows first. The dashboard is the window into them.

---

## Phase 1: Planning

Work through these three questions with Claude before touching anything technical.

**1. What do you want to see every day?**

Write a list. Not what sounds impressive. What would genuinely tell you, at a glance, whether your day is on track. Key metrics, live project status, today's calendar, whatever matters most.

**2. Where does that data live?**

For each item on your list, name the source. ClickUp? Google Calendar? A Slack channel? A social platform? If you don't have a connection to it yet, flag that. You'll need the data source before you can display it.

**3. What actions do you want one click away?**

These become your skill buttons. List your 5-10 highest-frequency Claude Code skills. The ones you use every single day.

Mine: `/daily-brief`, `/weekly-brief`, `/client-brief`, `/post-sd`, `/checkin-prep`, `/status-update`, `/systems-diagnostic-prep`.

Once you have answers to all three, move to Phase 2.

---

## Phase 2: Get Claude inside Obsidian

Before building anything, you need to be able to talk to Claude from inside your vault.

**Option A: Terminal plugin**

1. Open Obsidian.
2. Go to Settings > Community Plugins > Browse.
3. Search "Terminal" by Polymart. Install and enable it.
4. Open the terminal from the ribbon (`Ctrl+Shift+T` / `Cmd+Shift+T`).
5. You now have an integrated CLI. Run `claude` from here as normal.

**Option B: Claudian plugin**

1. Settings > Community Plugins > Browse.
2. Search "Claudian". Install and enable it.
3. Claudian gives you a Claude chat panel directly inside Obsidian. No terminal needed.

Terminal is better if you're comfortable with a CLI. Claudian is simpler if you're not.

---

## Phase 3: Build your moodboard

The dashboard's visual style comes from your moodboard. Claude Design reads it and builds the full design system. You don't need to design anything manually.

**Step 1: Gather reference images**

Go to Pinterest, Dribbble, or any site you like the look of. Collect 10-15+ images that match the aesthetic you're going for.

You can go any direction. My direction was pixel-art, Studio Ghibli-influenced, warm and light with technology in natural settings. I used [General Intelligence Company](https://generalintelligencecompany.com) and their product [Cofounder](https://cofounder.co) as references. Yours could be completely different. Dark and technical. Clean and minimal. Bold and colour-heavy. Claude Design works from any reference material.

**Step 2: Create a Moodboard folder in your vault**

```
Moodboard/
  [your reference images]
```

**Step 3: Ask Claude to build the moodboard files**

Open Claude inside Obsidian and give it this prompt:

> "I've dropped reference images into `Moodboard/`. Read all the images and create three files:
>
> 1. `Moodboard.md` — catalogue each image and describe what design elements it demonstrates: palette, layout, typography, illustration style, interaction patterns.
> 2. `Design-Brief.md` — a concise visual spec: colours, type, card styles, spacing, illustration style, motion. Write it as a handoff document.
> 3. `Fonts.md` — fonts visible in the reference images, with substitutions for anything not self-hostable.
>
> Only describe what you see in the images. Don't invent anything."

Review the three files when Claude is done. Correct anything that doesn't match your vision.

**Hero image tip**

For the hero banner, you want an ultra-wide image at roughly 20:9 ratio. Pinterest images are often square or portrait. What I did: found an image I liked, took it to [NanoBanana](https://nanobanan.com), stretched it wider, expanded the canvas, and sharpened it. That gives you the cinematic hero feel without needing a photographer.

**Your moodboard folder should look like:**

```
Moodboard/
  [reference images]
  Moodboard.md
  Design-Brief.md
  Fonts.md
```

---

## Phase 4: Feed the moodboard to Claude Design

Claude Design has a built-in "Create Design System" flow. You don't write a custom prompt.

1. Go to [Claude.ai](https://claude.ai) and open Claude Design.
2. Select **Create Design System**.
3. Drop in your entire `Moodboard/` folder. Include images, `Moodboard.md`, `Design-Brief.md`.
4. Claude Design reads everything, extracts the design language, and builds colour tokens, type scale, card patterns, and JSX UI kit stubs.
5. Download the zip when complete.

That zip is your design system. Claude Code uses it to build a plugin that looks exactly like your vision.

---

## Phase 5: Scaffold the plugin

Start a fresh Claude Code session. Have the design system zip ready.

**Step 1: Create the plugin folder**

Inside your Obsidian vault:

```
.obsidian/plugins/[your-name]-command-center/
```

Name it after your setup.

**Step 2: Kick off the build**

Paste the zip contents into the Claude Code session, then give Claude this prompt:

> "I have a design system in this folder. Build me an Obsidian community plugin called `[your-name]-command-center`. It should render a full-screen dashboard inside an Obsidian ItemView pane.
>
> Tech stack: Preact, TypeScript, Tailwind CSS, esbuild, framer-motion, lucide-react. Bundle everything into `main.js` and `styles.css`. Fonts must be bundled. The plugin must work with no internet connection.
>
> Start by scaffolding: `manifest.json`, `package.json`, `main.ts`, `tsconfig.json`, `tailwind.config.js`, `esbuild.config.mjs`. Apply the design tokens from `colors_and_type.css` to Tailwind. Set up hot-reload compatibility. Just get the empty shell loading in Obsidian."

Then run:

```bash
npm install
npm run dev
```

**Step 3: Enable in Obsidian**

Settings > Community Plugins. Your plugin appears in the list. Enable it.

If it doesn't appear: Settings > Community Plugins > turn off "Restricted mode". Then try again.

---

## Phase 6: Install community plugins

Install these from Settings > Community Plugins > Browse. Enable each after installing.

| Plugin | Author | What it does |
|--------|--------|--------------|
| Terminal | Polymart | Integrated CLI inside Obsidian. Keeps Claude Code in the same window as your dashboard. |
| Hot Reload | pjeby | Reloads the dashboard on every code change without restarting Obsidian. Essential during development. |
| Iconize | FlorianWoelki | Visual icons on vault folders and files. Makes navigation faster. |
| RSS Dashboard | (search "RSS Dashboard") | Powers the News and Signals tab. |
| Claudian | (optional) | Claude chat panel inside Obsidian. Good alternative to Terminal for non-CLI users. |

**Web Viewer (core plugin, not community)**

Already in Obsidian, just disabled. Settings > Core Plugins > scroll to "Web viewer" > enable it. Lets you pin browser tabs inside Obsidian.

---

## Phase 7: Build the cards

Build one card at a time with Claude. Recommended order:

### Tabs first

Decide on your tab structure before any cards. What I have:

- **Command Center** — main operational dashboard
- **News and Signals** — RSS feeds and signals
- **Intelligence** — meeting transcripts, email highlights, Slack activity

You don't have to copy mine. One good alternative: one tab per department. Content / Delivery / Intelligence. Or Sales / Operations / Research. Whatever reflects how your business runs.

Tell Claude: *"Add a tab bar with three tabs: Command Center, News and Signals, Intelligence. Command Center is active by default. The other two are empty placeholders."*

### Search bar

Tell Claude: *"Add a glass-pill styled search bar above the card grid. Show a drop-down results panel as I type. Results pull from vault files."*

### Hero card

Tell Claude: *"Add a hero banner at the top of the Command Center tab. Show my operator name, a live clock updating every second, and a status line. Use the pixel-art panoramic illustration as the background. Keep it compact, around 180px tall."*

### Scorecard

Key metrics you want eye-level. Personal to your setup. If there's an API, an MCP server, or a value you can pipe via Claude, it can show here.

Tell Claude: *"Add a Scorecard card showing [your chosen metrics]. Large stat number, label below, optional trend indicator. Read from `data/scorecard.json`."*

### Action Queue

How mine works: when my daily brief runs, it writes recommended green-light tasks to `data/action-queue.json`. The card reads that file. Each row has an approve button (fires the skill) and a dismiss button.

Tell Claude: *"Add an Action Queue card reading from `data/action-queue.json`. Each row shows suggestion text, an approve button, and a dismiss button. Approve fires a headless `claude -p` call with the skill name and args from the JSON row."*

JSON format for `action-queue.json`:

```json
[
  {
    "id": "1",
    "suggestion": "Send weekly status update to Rockford",
    "skill": "status-update",
    "args": {"client": "rockford"},
    "priority": 1
  }
]
```

### Skills tiles

Tell Claude: *"Add a Skills card with tiles for [your skill list]. Each tile shows an icon and skill name. Clicking fires a headless `claude -p` call. Show a loading state on the tile while it runs."*

### Calendar

Reads from `data/calendar.json`, written by a refresh script. See `starter/cc-refresh-calendar.sh` in this repo for the template.

The key detail: the calendar script needs its own dedicated MCP config that loads only the Google Calendar connector. Loading the full MCP server set alongside it causes a schema conflict.

Tell Claude: *"Add a Calendar card reading from `data/calendar.json`. Show a scrollable day rail and an agenda list for the selected day. Also automatically surface any daily brief files from `Briefings/Daily/` that match the selected date."*

### Delivery board / Engagements

Client or project status by stage. Build this if you run delivery work. If not, swap it for something that fits what you do.

Tell Claude: *"Add an Engagements card reading from `data/engagements.json`. Show each engagement as a row with: name, current stage, last activity date, blocker indicator. Clicking a row expands the detail inline."*

### Contribution heatmap (optional)

Year-at-a-glance view of vault activity. Good for spotting dead periods.

---

## Phase 8: The data layer

The plugin reads JSON files from a `data/` folder. Those files are written by headless Claude scripts that run on a schedule.

The pattern for every data card:

```
Refresh script → fires claude -p → Claude queries tool via MCP → writes JSON → Plugin reads JSON → Card displays it
```

Set up one refresh script per data source. Run it once manually to create the initial file. Then either cron it or add a manual refresh button on the card.

```bash
# Add to crontab for hourly refresh
0 * * * * /path/to/vault/.claude/scripts/cc-refresh-engagements.sh
```

See the `starter/` folder in this repo for script templates.

---

## Phase 9: Skill buttons and headless Claude

The skill tiles fire `claude -p`. This runs Claude in an isolated headless session. Your main interactive Claude session is completely untouched.

**Cost:** `claude -p` draws from a separate $200/month API credit pool, not your Max subscription. For a dashboard with 5-10 skill presses per day, you won't come close to using it up.

When you click a skill tile, the plugin runs:

```bash
claude -p "/skill-name [args]" --output-file /path/to/output.md
```

Claude runs the skill, writes output to a known path, exits. The plugin refreshes the relevant card from that file.

---

## Phase 10: The three tabs

### Command Center

Everything from Phases 7 and 8. The main operational view.

### News and Signals

RSS Dashboard plugin feeds this tab. The tab needs to feel like part of the same dashboard, not a bolted-on plugin.

Tell Claude: *"Build a News and Signals tab with: a search bar to filter articles, a source filter panel, grid and list view toggle, bookmark button on each article, and a timeline mode sorted by publish date. Style it to match the rest of the dashboard exactly: same card treatment, same typography, same colour system."*

Good starting feeds: Hacker News best, GitHub Trending, your industry news sources.

### Intelligence

Meeting transcripts, email highlights, Slack activity.

**Prerequisite:** for meeting transcripts to appear here, they need to already be landing inside your vault. If you use Fireflies or Granola, make sure they're writing transcript files into Obsidian before building this tab.

Tell Claude: *"Add an Intelligence tab showing recent meeting transcripts from `Operations/Meetings/`, Gmail highlights from `data/gmail-highlights.json`, and Slack activity from `data/slack-activity.json`. Each section is a list of recent items. Clicking any item expands the full content inline."*

---

## Phase 11: Go live

1. Run `npm run build` to generate the production bundle.
2. Settings > Community Plugins. Enable your plugin.
3. Settings > Options > Start-up > set your dashboard as the default view.
4. Open the dashboard. Switch to reading mode. This locks the layout.
5. Done. The dashboard is your Obsidian homepage.

---

## Tips for improving each card

Once the foundation is working, this is how to keep improving it.

For any card, ask Claude:

> "Look at this card. How could we make it more useful, more intuitive, or more visually interesting? Give me three concrete suggestions."

Claude will suggest things like popup detail panels, drill-down interactions, better data visualisation, hover states, filtering, sorting. Pick the ones that appeal to you and tell Claude to implement them.

That's exactly how the popup client detail panel and the day wheel on my calendar came to be. Start simple and iterate.

---

## Troubleshooting

**Plugin doesn't appear in community plugins list**
Settings > Community Plugins > turn off "Restricted mode".

**Dashboard is blank**
Check `npm run build` completed without errors. Open the developer console (`Ctrl+Shift+I` / `Cmd+Option+I`) and look for JS errors.

**Data cards show empty state**
The JSON files in `data/` don't exist yet. Run your refresh scripts manually once to create them.

**Skill buttons don't fire**
Check that `claude` is in your PATH. Run `which claude` in the Terminal plugin to verify.

**Hot reload isn't working**
Confirm Hot Reload is installed and enabled. Check that `npm run dev` is running, not `npm run build`.

**Calendar shows only daily briefs, no events**
Run `cc-refresh-calendar.sh` manually and check for errors. Most common cause: the MCP config is pointing to the wrong connector.


---

*Built by [Handro Vermeulen](https://instagram.com/handro.v) at [PRGRMMD](https://prgrmmd.com)*
