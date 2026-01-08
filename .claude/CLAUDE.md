# ATProto Posts Timeline

## Original Prompt

Build a web page that allows users to enter an ATProto/BlueSky handle, click a button, then fetch posts from the public BlueSky API and display them on a calendar showing when posts were made. When users click on a date, show posts for that day. When users click on the month heading, show all posts for that month.

## Technology Stack

- **No build tools**: Single HTML file with embedded CSS and JavaScript
- **AlpineJS 3.x** (CDN): Reactive UI framework
- **Modern CSS**: CSS Variables, Flexbox, Grid (no frameworks)
- **BlueSky Public API**: `https://public.api.bsky.app/`

## Key Implementation Details

### API Endpoints
1. **Resolve handle → DID**: `com.atproto.identity.resolveHandle?handle={handle}`
2. **Fetch posts**: `app.bsky.feed.getAuthorFeed?actor={did}&limit=100&cursor={cursor}`

### Features
- Calendar grid with post counts per day
- Click date → view posts for that day
- Click month heading → view all posts for that month
- Prev/Next month navigation
- Month heading styled as clickable button (hover effect: 0.15s transition)

### State Management (AlpineJS)
- `viewMode`: 'day' | 'month' (determines filtering)
- `selectedDate`: YYYY-MM-DD (day mode) or YYYY-MM (month mode)
- `posts`: All fetched posts (persists across navigation)
- `currentMonth/currentYear`: Controls calendar view

### Styling Notes
- Month button: Light background with border, blue hover with lift effect
- Transition: `all 0.15s ease` (fast, responsive)
- Transform: `translateY(-2px)` for GPU-accelerated hover lift
- Color scheme: BlueSky blue (#1185fe) with neutral grays

## Testing

**Test handle**: `vmois.dev`

**Manual test steps**:
1. Open `index.html` in browser
2. Enter test handle, click "Load Posts"
3. Verify calendar shows post counts
4. Click a date → should show that day's posts
5. Click month heading → should show all month's posts
6. Test Prev/Next navigation

**ChromeDevTools MCP Server available for automated testing**

## Documentation

- BlueSky API: https://docs.bsky.app/
- AlpineJS: https://alpinejs.dev/
- AT Protocol: https://atproto.com/
