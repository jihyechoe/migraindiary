# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a comprehensive Migraine Diary app implemented as a single HTML file with embedded CSS and JavaScript. The app helps track and analyze migraine patterns with detailed symptom/trigger data. Features include:
- Log entries with date, time, severity (1-10), duration, location, symptoms, triggers
- Complete migraine history with edit/delete capabilities
- Pattern analytics with stats, frequency charts, and severity tracking
- localStorage persistence across sessions
- Dark theme responsive design with no external dependencies

## Architecture

**Single File Structure:**
- `migraine-diary.html`: Contains all HTML markup, CSS styling, and JavaScript logic

### Data Model

Entries stored in localStorage under key `'migraine_diary_entries'`:
```js
{
  id: 1699564800000,              // unique timestamp ID
  date: '2025-03-03',
  time: '14:30',
  severity: 7,                    // 1-10 scale
  duration: 4,                    // hours (0.5 step increments)
  locations: ['temples'],         // from fixed list
  symptoms: ['nausea'],           // from fixed list
  triggers: ['stress'],           // from fixed list
  medications: 'Ibuprofen 400mg',
  notes: 'Free text notes'
}
```

### Code Organization

1. **Markup**: Header, nav tabs (Log Entry | History | Analytics), main content area, toast notification
2. **Styles**: Dark theme (#1a1a2e background, #16213e cards), responsive design, pill-button checkboxes, bar/SVG charts
3. **JavaScript**:
   - `loadEntries()` / `saveEntries()`: localStorage management
   - `setView(name)`: Switch between three views (log, history, analytics)
   - `renderView()`: Dispatch to view-specific render functions
   - `renderLogForm()`: Build form with pre-population for editing
   - `handleFormSubmit()`: Validate, create/update entry, persist, navigate
   - `renderHistory()`: List entries with edit/delete buttons
   - `renderAnalytics()`: Stats grid, frequency bar charts, severity SVG chart
   - `buildSeverityChart()`: Pure JS SVG bar chart generation

### Three Views

1. **Log Entry**: Form to log a new migraine or edit existing. Pre-populates when editing.
2. **History**: Chronological list of entries (newest first) with tags and action buttons.
3. **Analytics**: This Month count, All-Time count, Avg Severity, Most Common trigger, plus frequency charts.

## Running the App

Simply open the HTML file in a browser:
```bash
open migraine-diary.html
# or manually open the file in your browser
```

## Git Workflow

**IMPORTANT: Commit and push regularly to preserve all work and changes.**

After making any changes:
1. Test the changes by opening the file in a browser
2. Stage and commit with a clear, descriptive message: `git add . && git commit -m "Description"`
3. Push to GitHub immediately: `git push origin main`

### Commit Message Guidelines

- Write clear, descriptive commit messages that explain **what changed and why**
- Use imperative mood: "Add feature" not "Added feature"
- Keep messages concise (50 characters or less for the summary)
- Examples:
  - `Add AI opponent to game`
  - `Fix win detection bug for diagonal wins`
  - `Improve mobile responsiveness of game board`

### Why Regular Commits Matter

- **Never lose work**: Commits are the source of truth for project history
- **Easy rollback**: Can revert to any previous version if needed
- **Clear project timeline**: Easy to see what was done and when
- **Multiple sessions**: Future Claude instances can understand what's been done

Keep commits atomic and focused on single features, fixes, or improvements. Push to GitHub after each commit to ensure it's safely backed up.

## Key Development Notes

- **Pain Locations**: forehead, temples, back of head, behind eyes
- **Symptoms**: nausea, light sensitivity, sound sensitivity, aura, vomiting
- **Triggers**: stress, sleep deprivation, dehydration, food, caffeine, weather, hormones
- Checkbox groups use `:has(input:checked)` CSS for styling
- Edit mode sets `editingId` and pre-populates form with entry data
- History entries sorted by date/time (newest first)
- Analytics stats calculated on-the-fly from entries array
- SVG severity chart generated with pure JavaScript (no charting library)
- Responsive design handles mobile with single-column layout
- No external dependencies - fully self-contained
