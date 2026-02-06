<div align="center">
  <h1>⭐ Teracrawl</h1>
  <p>
    <strong>High-performance web crawler & scraper API optimized for LLMs.</strong>
  </p>
  <p>
    Powered by <a href="https://browser.cash/developers">Browser.cash</a> remote browsers.
  </p>
  
  <p>
    <a href="#features">Features</a> •
    <a href="#quick-start">Quick Start</a> •
    <a href="#api-reference">API Reference</a> •
    <a href="#configuration">Configuration</a> •
    <a href="#docker">Docker</a>
  </p>

  <p>
    <img src="https://img.shields.io/badge/license-MIT-blue.svg" alt="License">
    <img src="https://img.shields.io/badge/node-%3E%3D18.0.0-brightgreen" alt="Node.js Version">
    <img src="https://img.shields.io/badge/typescript-5.6-blue" alt="TypeScript">
    <img src="https://img.shields.io/badge/powered%20by-browser.cash-orange" alt="Visit Browser.cash">
  </p>
  
  <p>
    <a href="https://x.com/aibrowsers">
      <img src="https://img.shields.io/badge/Follow%20on%20X-000000?style=for-the-badge&logo=x&logoColor=white" alt="Follow on X" />
    </a>
    <a href="https://linkedin.com/company/megatera">
      <img src="https://img.shields.io/badge/Follow%20on%20LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white" alt="Follow on LinkedIn" />
    </a>
    <a href="https://discord.gg/F9afFJPtYb">
      <img src="https://img.shields.io/badge/Join%20our%20Discord-5865F2?style=for-the-badge&logo=discord&logoColor=white" alt="Join our Discord" />
    </a>
  </p>

  <br>

  <p>
     <strong>Important:</strong> Search functionality (`/crawl`) requires a running instance of 
    <a href="https://github.com/BrowserCash/browser-serp"><strong>browser-serp</strong></a>.
  </p>
</div>

---

##  Benchmarks

<div align="center">
  <img src="scrape-evals.png" alt="Teracrawl achieves #1 coverage at 82.1%" width="700">
  <p><strong>Teracrawl</strong> achieves <strong>#1 coverage (84.2%)</strong> across 14 scraping providers on the <a href="https://github.com/firecrawl/scrape-evals/pull/13">scrape-evals</a> benchmark, an open evaluation framework that tests web scrapers against 1,000 diverse URLs for success rate and content quality.</p>
</div>

---

##  What is Teracrawl?

**Teracrawl** is a production-ready API designed to turn websites into clean, LLM-ready Markdown. It handles the complexity of JavaScript rendering, anti-bot measures, and parallel execution allowing AI systems to access real-time data quickly.

Unlike simple HTML scrapers, Teracrawl uses real managed Chrome browsers, ensuring high success rates even across protected sites.

### Why use Teracrawl?

- ** LLM-Optimized Output**: Converts complex HTML into clean, semantic Markdown perfect for RAG and context windows.
- ** Smart Two-Phase Crawling**:
  - _Fast Mode_: Optimized for static/SSR pages (reuses contexts, blocks heavy assets).
  - _Dynamic Mode_: Automatic fallback for complex SPAs (waits for hydration/rendering).
- ** Search & Scrape**: Single endpoint to query Google and scrape the top results in parallel.
- **🏎 High Concurrency**: Built on a robust <a href="https://github.com/BrowserCash/browser-pool">session pool</a> to handle multiple pages simultaneously.

## <a name="features"></a>✨ Features

- **Search + Scrape**: Query Google and scrape top N results in a single API call.
- **Direct Scraping**: Convert any specific URL to Markdown.
- **Smart Content Extraction**: Automatically detects main content areas (article, main, etc.) and removes clutter (scripts, styles, navs).
- **Safety & Performance**:
  - Blocks ads, trackers, and analytics.
  - Removes base64 images to save token count.
  - Automatic timeout handling and error recovery.
- **Docker Ready**: Deploy anywhere with a lightweight container.

## <a name="quick-start"></a>🛠 Quick Start

### Prerequisites

1.  **Node.js 18+** installed.
2.  A **[Browser.cash](https://browser.cash/developers)** API Key.
3.  A running SERP service like [browser-serp](https://github.com/BrowserCash/browser-serp) on port 8080 (optional, only for `/crawl` endpoint).

### Installation

```bash
# Clone the repository
git clone https://github.com/BrowserCash/teracrawl.git
cd teracrawl

# Install dependencies
npm install
```

### Configuration

Copy the example environment file and configure your settings:

```bash
cp .env.example .env
```

Open `.env` and set your `BROWSER_API_KEY`:

```env
BROWSER_API_KEY=your_browser_cash_api_key_here
```

### Running the Server

```bash
# Development mode
npm run dev

# Production build & start
npm run build
npm start
```

The server will start at `http://0.0.0.0:8085`.

## <a name="api-reference"></a>📚 API Reference

### 1. Search & Crawl

Performs a Google search and scrapes the content of the top results.

**Endpoint:** `POST /crawl`

**CURL Request:**

```bash
curl -X POST http://localhost:8085/crawl \
  -H "Content-Type: application/json" \
  -d '{
    "q": "What is the capital of France?",
    "count": 3
  }'
```

| Field   | Type     | Default      | Description                           |
| :------ | :------- | :----------- | :------------------------------------ |
| `q`     | `string` | **Required** | The search query.                     |
| `count` | `number` | `3`          | Number of results to scrape (max 20). |

**Response:**

```json
{
  "query": "What is the capital of France?",
  "results": [
    {
      "url": "https://en.wikipedia.org/wiki/Paris",
      "title": "Paris - Wikipedia",
      "markdown": "# Paris\n\nParis is the capital and most populous city of France...",
      "status": "success"
    },
    {
      "url": "https://...",
      "status": "error",
      "error": "Timeout exceeded"
    }
  ]
}
```

### 2. Single Page Scrape

Scrapes a specific URL and converts it to Markdown.

**Endpoint:** `POST /scrape`

**CURL Request:**

```bash
curl -X POST http://localhost:8085/scrape \
  -H "Content-Type: application/json" \
  -d '{
    "url": "https://example.com/blog/post-1"
  }'
```

**Response:**

```json
{
  "url": "https://example.com/blog/post-1",
  "title": "My Blog Post",
  "markdown": "# My Blog Post\n\nContent of the post...",
  "status": "success"
}
```

### 3. SERP Search Only

Proxies a search request to the underlying SERP service without scraping content.

**Endpoint:** `POST /serp/search`

**CURL Request:**

```bash
curl -X POST http://localhost:8085/serp/search \
  -H "Content-Type: application/json" \
  -d '{
    "q": "browser automation",
    "count": 5
  }'
```

**Response:**

```json
{
  "results": [
    {
      "url": "https://...",
      "title": "Result Title",
      "description": "Result description..."
    }
  ]
}
```

### 4. Health Check

**Endpoint:** `GET /health`

**CURL Request:**

```bash
curl http://localhost:8085/health
```

**Response:**

```json
{
  "ok": true
}
```

## <a name="configuration"></a>⚙ Configuration

### Server & Infrastructure

| Variable           | Default                 | Description                                                           |
| :----------------- | :---------------------- | :-------------------------------------------------------------------- |
| `BROWSER_API_KEY`  | **Required**            | Your Browser.cash API key.                                            |
| `PORT`             | `8085`                  | Port for the API server.                                              |
| `HOST`             | `0.0.0.0`               | Host to bind to.                                                      |
| `SERP_SERVICE_URL` | `http://localhost:8080` | URL of the upstream SERP/Search service.                              |
| `POOL_SIZE`        | `1`                     | Number of concurrent browser sessions to maintain.                    |
| `DEBUG_LOG`        | `false`                 | Enable verbose logging for debugging.                                 |
| `DATALAB_API_KEY`  | _Optional_              | [Datalab](https://datalab.to) API key for PDF-to-Markdown conversion. |

### Crawler Tuning

| Variable                      | Default | Description                                                      |
| :---------------------------- | :------ | :--------------------------------------------------------------- |
| `CRAWL_TABS_PER_SESSION`      | `8`     | Max concurrent tabs per browser session.                         |
| `CRAWL_MIN_CONTENT_LENGTH`    | `200`   | Minimum markdown char length to consider a scrape successful.    |
| `CRAWL_NAVIGATION_TIMEOUT_MS` | `10000` | Timeout for "Fast" scraping mode (ms).                           |
| `CRAWL_SLOW_TIMEOUT_MS`       | `20000` | Timeout for "Slow" scraping mode (ms).                           |
| `CRAWL_JITTER_MS`             | `0`     | Max random delay (ms) between requests to avoid thundering herd. |

## <a name="docker"></a> Docker

You can run Teracrawl easily using Docker.

### Build & Run

```bash
# Build the image
docker build -t teracrawl .

# Run with env file
docker run -p 8085:8085 --env-file .env teracrawl
```

### Docker Compose

```yaml
version: "3.8"
services:
  teracrawl:
    build: .
    ports:
      - "8085:8085"
    environment:
      - BROWSER_API_KEY=${BROWSER_API_KEY}
      - SERP_SERVICE_URL=http://serp:8080
    depends_on:
      - serp

  serp:
    image: ghcr.io/mega-tera/browser-serp:latest
    ports:
      - "8080:8080"
```

## 🤝 Contributing

Contributions are welcome! We appreciate your help in making Teracrawl better.

### How to Contribute

1.  **Fork the Project**: click the 'Fork' button at the top right of this page.
2.  **Create your Feature Branch**: `git checkout -b feature/AmazingFeature`
3.  **Commit your Changes**: `git commit -m 'Add some AmazingFeature'`
4.  **Push to the Branch**: `git push origin feature/AmazingFeature`
5.  **Open a Pull Request**: Submit your changes for review.

##  License

This project is licensed under the MIT License - see the LICENSE file for details.
