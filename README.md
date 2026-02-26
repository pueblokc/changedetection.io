# changedetection.io UX Companion — Enhanced by KCCS

> Modern UX companion dashboard with folder organization, bulk operations, tag management, and inline diff viewing — built on top of the changedetection.io API.

![Dashboard](ux_companion/docs/screenshots/dashboard.png)

## What's New in This Fork

- **Folder organization** — group watches into collapsible folders (Price Tracking, GitHub Releases, News, Government, Competitors)
- **Bulk operations** — select multiple watches for move, tag, pause, resume, or delete
- **Tag management** — color-coded tag chips with filtering, bulk add/remove
- **Inline diff viewer** — click any watch to see recent changes with red/green diff highlighting
- **Dual view modes** — toggle between compact row view and card grid view
- **Real-time updates** — WebSocket connection pushes changes instantly
- **Keyboard shortcuts** — `/` to search, `N` to add, `Ctrl+A` to select all, `Delete` to remove, `Esc` to close
- **Demo mode** — 25 realistic watches with simulated change data out of the box
- **Dark theme** — GitHub-dark inspired palette (#0d1117), easy on the eyes
- **Responsive** — full mobile support with collapsing sidebar

## Quick Start

```bash
# Install dependencies
pip install fastapi uvicorn websockets

# Run the companion dashboard
python -m uvicorn ux_companion.app:app --host 127.0.0.1 --port 8510 --reload

# Open in browser
# http://127.0.0.1:8510
```

The dashboard starts in demo mode with 25 pre-configured watches across 5 folders.

## Screenshots

| Screenshot | Description |
|---|---|
| ![Dashboard](ux_companion/docs/screenshots/dashboard.png) | Main dashboard with folder sidebar, watch list, tag chips, and bulk operation toolbar |

## Features

- **Folder Organization** — Group watches into collapsible folders (Price Tracking, GitHub Releases, News, Government, Competitors)
- **Tag Management** — Color-coded tag chips with filtering, bulk add/remove
- **Bulk Operations** — Select multiple watches for move, tag, pause, resume, or delete
- **Inline Diff Viewer** — Click any watch to see recent changes with red/green diff highlighting
- **Dual View Modes** — Toggle between compact row view and card grid view
- **Real-time Updates** — WebSocket connection pushes changes instantly
- **Keyboard Shortcuts** — `/` to search, `N` to add, `Ctrl+A` to select all, `Delete` to remove, `Esc` to close
- **Responsive** — Full mobile support with collapsing sidebar
- **Demo Mode** — 25 realistic watches with simulated change data out of the box
- **Dark Theme** — GitHub-dark inspired palette, easy on the eyes

## API Reference

### Watches

| Method | Endpoint | Description |
|--------|----------|-------------|
| `GET` | `/api/watches` | List all watches (`?folder_id=`, `?tag=`, `?status=`, `?search=`) |
| `POST` | `/api/watches` | Add a new watch |
| `PUT` | `/api/watches/{id}` | Update watch metadata (folder, tags, notes, status) |
| `DELETE` | `/api/watches/{id}` | Remove a watch |

### Folders

| Method | Endpoint | Description |
|--------|----------|-------------|
| `GET` | `/api/folders` | List all folders with watch counts |
| `POST` | `/api/folders` | Create a new folder |

### Changes

| Method | Endpoint | Description |
|--------|----------|-------------|
| `GET` | `/api/changes/{id}` | Get change history for a watch (`?limit=10`) |

### Bulk Operations

| Method | Endpoint | Description |
|--------|----------|-------------|
| `POST` | `/api/bulk` | Bulk action on multiple watches |

**Bulk action payload:**

```json
{
  "watch_ids": ["uuid1", "uuid2"],
  "action": "move_folder|add_tag|remove_tag|pause|resume|delete",
  "value": "optional-folder-id-or-tag-name"
}
```

### Statistics

| Method | Endpoint | Description |
|--------|----------|-------------|
| `GET` | `/api/stats` | Dashboard statistics (totals, changes today, top tags) |

### WebSocket

| Protocol | Endpoint | Description |
|----------|----------|-------------|
| `ws` | `/ws` | Real-time change notifications |

**Event types:** `watch_created`, `watch_updated`, `watch_deleted`, `bulk_action`

## Docker

```dockerfile
FROM python:3.12-slim
WORKDIR /app
COPY ux_companion/ ./ux_companion/
RUN pip install --no-cache-dir fastapi uvicorn websockets
EXPOSE 8510
CMD ["python", "-m", "uvicorn", "ux_companion.app:app", "--host", "0.0.0.0", "--port", "8510"]
```

```bash
docker build -t changedetection-ux .
docker run -p 8510:8510 changedetection-ux
```

## Architecture

```
ux_companion/
  app.py              # FastAPI backend + demo data generator
  companion.db        # SQLite database (auto-created)
  static/
    index.html        # Single-file dark SPA (no build step)
  docs/
    screenshots/
      dashboard.png   # Dashboard screenshot
```

The companion dashboard runs as a standalone service. In production, it connects to a changedetection.io instance via its API. In demo mode (default), it generates 25 realistic watches with simulated change data.

## Tech Stack

- **Backend:** FastAPI + SQLite + WebSockets
- **Frontend:** Vanilla JS single-file SPA (zero dependencies, no build step)
- **Theme:** GitHub-dark inspired (#0d1117 base)

---

<details>
<summary>Original Project README</summary>

# Detect Website Changes Automatically -- Monitor Web Page Changes in Real Time

Monitor websites for updates -- get notified via Discord, Email, Slack, Telegram, Webhook and many more.

**Detect web page content changes and get instant alerts.**

Ideal for monitoring price changes, content edits, conditional changes and more.

[<img src="https://raw.githubusercontent.com/dgtlmoon/changedetection.io/master/docs/screenshot.png" style="max-width:100%;" alt="Web site page change monitoring" title="Web site page change monitoring" />](https://changedetection.io?src=github)

### Target specific parts of the webpage using the Visual Selector tool.

Available when connected to a playwright content fetcher (included as part of our subscription service)

[<img src="https://raw.githubusercontent.com/dgtlmoon/changedetection.io/master/docs/visualselector-anim.gif" style="max-width:100%;" alt="Select parts and elements of a web page to monitor for changes" title="Select parts and elements of a web page to monitor for changes" />](https://changedetection.io?src=github)

### Easily see what changed, examine by word, line, or individual character.

[<img src="https://raw.githubusercontent.com/dgtlmoon/changedetection.io/master/docs/screenshot-diff.png" style="max-width:100%;" alt="Self-hosted web page change monitoring context difference" title="Self-hosted web page change monitoring context difference" />](https://changedetection.io?src=github)

### Perform interactive browser steps

Fill in text boxes, click buttons and more, setup your changedetection scenario.

Using the **Browser Steps** configuration, add basic steps before performing change detection, such as logging into websites, adding a product to a cart, accept cookie logins, entering dates and refining searches.

### Awesome restock and price change notifications

Enable the "Re-stock & Price detection for single product pages" option to activate the best way to monitor product pricing, this will extract any meta-data in the HTML page and give you many options to follow the pricing of the product.

Easily organise and monitor prices for products from the dashboard, get alerts and notifications when the price of a product changes or comes back in stock again!

Set price change notification parameters, upper and lower price, price change percentage and more.

### Example use cases

- Products and services have a change in pricing
- Out of stock notification and Back In stock notification
- Monitor and track PDF file changes
- Governmental department updates
- New software releases, security advisories
- Discogs restock alerts and monitoring
- Realestate listing changes
- COVID related news from government websites
- University/organisation news
- Detect and monitor changes in JSON API responses
- Changes in legal and other documents
- Trigger API calls via notifications when text appears on a website
- Create RSS feeds based on changes in web content
- Monitor HTML source code for unexpected changes
- Get notified when certain keywords appear in search results
- Proactively search for jobs

#### Key Features

- Lots of trigger filters, such as "Trigger on text", "Remove text by selector", "Ignore text", "Extract text", also using regular-expressions!
- Target elements with xPath 1 and xPath 2, CSS Selectors, JSON with JSONPath or jq
- Switch between fast non-JS and Chrome JS based "fetchers"
- Track changes in PDF files
- Easily specify how often a site should be checked
- Execute JS before extracting text
- Override Request Headers, Specify POST or GET and other methods
- Use the "Visual Selector" to help target specific elements
- Configurable proxy per watch
- Send a screenshot with the notification when a change is detected

### Conditional web page changes

Easily configure conditional actions, for example, only trigger when a price is above or below a preset amount, or when a web page includes (or does not include) a keyword.

### Schedule web page watches in any timezone

Easily set a re-check schedule, for example you could limit the web page change detection to only operate during business hours.

### Installation

#### Docker

```bash
$ docker compose up -d
```

Docker standalone:
```bash
$ docker run -d --restart always -p "127.0.0.1:5000:5000" -v datastore-volume:/datastore --name changedetection.io dgtlmoon/changedetection.io
```

#### Python Pip

```bash
$ pip3 install changedetection.io
$ changedetection.io -d /path/to/empty/data/dir -p 5000
```

Then visit http://127.0.0.1:5000

### Filters

XPath(1.0), JSONPath, jq, and CSS support comes baked in!

### Notifications

ChangeDetection.io supports a massive amount of notifications (including email, office365, custom APIs, etc) thanks to the apprise library.

### JSON API Monitoring

Detect changes and monitor data in JSON API's by using either JSONPath or jq to filter, parse, and restructure JSON as needed.

### API Support

Full REST API for programmatic management of watches, tags, notifications and more.

### License

See LICENSE.md

### Commercial Support

Contact dgtlmoon@gmail.com for commercial support enquiries.

</details>

---

Developed by **[KCCS](https://kccsonline.com)** — [kccsonline.com](https://kccsonline.com)
