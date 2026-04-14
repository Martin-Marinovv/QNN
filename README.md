# QNN — Quantum News Network · OBS Stream Overlay

## File Structure
```
qnn-broadcast/
  index.html        ← OBS Browser Source (1920×1080)
  control.html      ← Config/control panel
  assets/
    terminal-frame.png   ← Terminal frame overlay (1920×1080)
    broadcast-01.mp4     ← Video segment 1
    broadcast-02.mp4     ← Video segment 2
    broadcast-03.mp4     ← Video segment 3 (add up to 06)
```

## Setup
1. Add assets/terminal-frame.png (1920×1080px)
2. Add your video files as broadcast-01.mp4, broadcast-02.mp4, etc.
3. Edit the PLAYLIST array at the top of index.html to match your filenames
4. Push to GitHub → Settings → Pages → main branch → Save
5. Open control.html → set timings → Generate URL → copy
6. OBS: Add Source → Browser → paste URL → set to 1920×1080
7. Right-click Browser Source → Properties → tick "Control audio via OBS"

## Broadcast Flow

### With videos
QNN standby (msg s) → [CRT] → Video plays to end → [CRT] → !apply (oi s) → [CRT] → QNN → next video → ...

- All videos loop in order indefinitely
- After every video, OI !apply screen shows for oi seconds (default 60s)
- Then QNN standby returns for msg seconds before the next video

### No videos (all PLAYLIST entries commented out)
QNN standby (msg s) → [CRT] → !apply (msg / 10 s) → [CRT] → QNN → ...

- !apply is always 1/10 of the QNN standby time
- Screen is ALWAYS showing something — CRT static only during 1s transition flashes

## URL Parameters

| Param    | Default | Description |
|----------|---------|-------------|
| msg      | 320     | QNN standby duration (s) — also time between videos |
| oi       | 60      | OI !apply duration after each video (s) |
| interval | 56      | CRT flash interval during QNN phase (% of msg). 0 = disabled. |
| crt      | 1       | CRT flash transition duration (s) |
| vidmax   | 600     | Per-video safety timeout (s) — fallback only |

## Changing Timing
Open control.html → adjust → Generate URL → paste into OBS Browser Source → right-click → Refresh
