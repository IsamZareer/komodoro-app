# Komodoro App — Session Context

## What was built
A single-file Pomodoro tracking web app (`index.html`) located at:
`/Users/isamnayef/Documents/Claude Outputs/pomodoro/index.html`

## Feature summary

### Timer
- 25-min focus / 5-min break (configurable in settings)
- Start / Pause button
- **Finish Early** button — triggers same flow as natural completion (alarm → break starts)
- Auto-transitions: focus ends → alarm → break auto-starts → break ends → resets to focus (does not auto-start)
- Session bar above timer showing **Pomodoro 1, 2, 3…** with dot indicators (gray = future, blue active, green done)
- **🔥 streak badge** (consecutive days with at least one completed pomodoro)
- Dynamic **favicon ring** — hollow ring, 10px stroke, transparent bg, updates every second:
  - Idle: dim gray ring
  - Focus running: blue arc filling clockwise
  - Break: green arc filling clockwise

### Settings (⚙ gear icon, inline panel)
- Focus duration (minutes)
- Break duration (minutes)
- **Ringtone selector** — 5 options: Classic, Bell, Pulse, Chime, Digital (all synthesized via Web Audio API). Clicking a ringtone previews it immediately. Selected tone is used for all alarms.
- Apply button — updates durations live if timer is not running

### Task Manager
- Subject field + task description field
- Add via Enter key or + button
- Tasks live in **To-Do** list
- Draggable reordering via ⠿ handle (drag-and-drop)
- Custom styled checkbox (dark theme, green on check) positioned on the **far right** to avoid misclicks while dragging
- When pomodoro ends (or Finish Early): all open tasks auto-move to **Completed**
- Completed tasks show a **⏱ time badge**: "Completed after Xm Xs of focus time"
- Manual checkbox check also records elapsed focus time at that moment

### Persistence (localStorage key: `pomo_v1`)
All of the following survive page refresh:
- Focus/break durations, ringtone choice
- Pomodoro count, total pomodoros completed, streak, last pomodoro date
- Full task list (todo + done, with time badges)
- Active countdown: saves `endTimestamp` (wall-clock ms), recomputes remaining on reload and **auto-resumes** the clock
- If timer expired while tab was closed: tasks quietly marked done, count incremented, resets to idle focus

## Visual design
- Dark theme (Tokyo Night palette)
- CSS variables: `--bg #1a1b26`, `--panel #24283b`, `--accent #7aa2f7`, `--good #9ece6a`, `--warn #e0af68`, `--danger #f7768e`
- Timer card border turns green during break mode
- Session bar uses dot indicators + label + streak badge

## File structure
```
pomodoro/
├── index.html    (entire app — no dependencies, no build step)
└── CONTEXT.md    (this file)
```

## What to do next (user's stated direction)
- Continue adding niche features and settings
- GitHub repo: **komodoro-app**

## Tech stack
- Vanilla HTML/CSS/JS, single file
- Web Audio API for alarm synthesis (no audio files needed)
- localStorage for persistence
- HTML5 Drag and Drop API for task reordering
- Canvas API for dynamic favicon
