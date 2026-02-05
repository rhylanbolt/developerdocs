<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Opti-X Developer Documentation</title>
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/highlight.js/11.9.0/styles/github.min.css">
  <style>
    *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

    :root {
      --sidebar-width: 280px;
      --sidebar-bg: #1a1a2e;
      --sidebar-text: #c8c8d4;
      --sidebar-hover: #16213e;
      --sidebar-active: #0f3460;
      --accent: #0066cc;
      --accent-light: #e8f0fe;
      --text: #1f2937;
      --text-light: #6b7280;
      --border: #e5e7eb;
      --bg: #ffffff;
      --code-bg: #f6f8fa;
    }

    html { scroll-behavior: smooth; scroll-padding-top: 1rem; }

    body {
      font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
      font-size: 16px;
      line-height: 1.7;
      color: var(--text);
      background: var(--bg);
    }

    .layout {
      display: grid;
      grid-template-columns: var(--sidebar-width) 1fr;
      min-height: 100vh;
    }

    /* ── Sidebar ─────────────────────────────── */
    #sidebar {
      position: fixed;
      top: 0;
      left: 0;
      width: var(--sidebar-width);
      height: 100vh;
      overflow-y: auto;
      background: var(--sidebar-bg);
      color: var(--sidebar-text);
      padding: 0;
      z-index: 100;
      transition: transform 0.3s ease;
    }

    .sidebar-header {
      padding: 1.5rem 1.25rem 1rem;
      border-bottom: 1px solid rgba(255,255,255,0.08);
    }

    .sidebar-header h2 {
      color: #fff;
      font-size: 1.25rem;
      font-weight: 700;
      margin-bottom: 0.15rem;
    }

    .sidebar-subtitle {
      font-size: 0.75rem;
      color: rgba(255,255,255,0.45);
      letter-spacing: 0.03em;
    }

    .nav-tree {
      list-style: none;
      padding: 0.5rem 0;
    }

    .nav-item, .nav-section { margin: 0; }

    .section-toggle {
      display: flex;
      align-items: center;
      justify-content: space-between;
      width: 100%;
      padding: 0.55rem 1.25rem;
      background: none;
      border: none;
      color: rgba(255,255,255,0.55);
      font-size: 0.7rem;
      font-weight: 700;
      letter-spacing: 0.08em;
      text-transform: uppercase;
      cursor: pointer;
      margin-top: 0.75rem;
      transition: color 0.15s;
    }

    .section-toggle:hover { color: rgba(255,255,255,0.85); }

    .toggle-icon { font-size: 0.65rem; }

    .section-children {
      list-style: none;
      padding: 0;
    }

    .nav-link {
      display: block;
      padding: 0.4rem 1.25rem 0.4rem 1.5rem;
      color: var(--sidebar-text);
      text-decoration: none;
      font-size: 0.875rem;
      border-left: 3px solid transparent;
      transition: all 0.15s;
    }

    .nav-link:hover {
      background: var(--sidebar-hover);
      color: #fff;
    }

    .nav-link.active {
      background: var(--sidebar-active);
      color: #fff;
      border-left-color: var(--accent);
      font-weight: 600;
    }

    /* ── Main Content ────────────────────────── */
    #content {
      grid-column: 2;
      max-width: 900px;
      padding: 2rem 2.5rem 4rem;
    }

    .doc-section {
      padding-bottom: 2.5rem;
      margin-bottom: 2.5rem;
      border-bottom: 1px solid var(--border);
    }

    .doc-section:last-child { border-bottom: none; }

    /* ── Typography ──────────────────────────── */
    h1 { font-size: 2rem; font-weight: 800; margin: 0 0 1rem; color: #111827; }
    h2 { font-size: 1.5rem; font-weight: 700; margin: 2rem 0 0.75rem; color: #111827; padding-bottom: 0.35rem; border-bottom: 1px solid var(--border); }
    h3 { font-size: 1.2rem; font-weight: 600; margin: 1.5rem 0 0.5rem; color: #1f2937; }
    h4 { font-size: 1.05rem; font-weight: 600; margin: 1.25rem 0 0.5rem; color: #374151; }
    p { margin: 0.75rem 0; }
    a { color: var(--accent); text-decoration: none; }
    a:hover { text-decoration: underline; }
    a.broken-link { color: #9ca3af; cursor: not-allowed; text-decoration: line-through; }
    hr { border: none; border-top: 1px solid var(--border); margin: 1.5rem 0; }
    ul, ol { margin: 0.5rem 0 0.75rem 1.5rem; }
    li { margin: 0.25rem 0; }
    strong { font-weight: 600; }

    /* ── Tables ───────────────────────────────── */
    table {
      width: 100%;
      border-collapse: collapse;
      margin: 1rem 0;
      font-size: 0.9rem;
      overflow-x: auto;
      display: block;
    }

    thead th {
      background: #f9fafb;
      font-weight: 600;
      text-align: left;
      padding: 0.65rem 0.85rem;
      border: 1px solid var(--border);
      white-space: nowrap;
    }

    tbody td {
      padding: 0.55rem 0.85rem;
      border: 1px solid var(--border);
      vertical-align: top;
    }

    tbody tr:nth-child(even) { background: #f9fafb; }

    /* ── Code ─────────────────────────────────── */
    code {
      font-family: "SF Mono", "Fira Code", "Cascadia Code", "JetBrains Mono", Consolas, monospace;
      font-size: 0.875em;
    }

    :not(pre) > code {
      background: var(--code-bg);
      padding: 0.15em 0.4em;
      border-radius: 4px;
      color: #d63384;
    }

    pre {
      background: var(--code-bg);
      border: 1px solid var(--border);
      border-radius: 8px;
      padding: 1rem 1.25rem;
      overflow-x: auto;
      margin: 1rem 0;
      line-height: 1.5;
    }

    pre code {
      background: none;
      padding: 0;
      color: inherit;
    }

    /* ── Blockquotes ──────────────────────────── */
    blockquote {
      border-left: 4px solid var(--accent);
      background: var(--accent-light);
      padding: 0.75rem 1rem;
      margin: 1rem 0;
      border-radius: 0 6px 6px 0;
    }

    blockquote p { margin: 0.25rem 0; }

    /* ── Mobile Toggle ────────────────────────── */
    #sidebar-toggle {
      display: none;
      position: fixed;
      top: 0.75rem;
      left: 0.75rem;
      z-index: 200;
      background: var(--sidebar-bg);
      color: #fff;
      border: none;
      border-radius: 6px;
      padding: 0.5rem 0.7rem;
      font-size: 1.25rem;
      cursor: pointer;
      box-shadow: 0 2px 8px rgba(0,0,0,0.2);
    }

    @media (max-width: 768px) {
      .layout { grid-template-columns: 1fr; }
      #sidebar { transform: translateX(-100%); }
      #sidebar.open { transform: translateX(0); box-shadow: 4px 0 24px rgba(0,0,0,0.3); }
      #sidebar-toggle { display: block; }
      #content { grid-column: 1; padding: 3.5rem 1.25rem 3rem; }
    }

    /* ── Scrollbar styling ────────────────────── */
    #sidebar::-webkit-scrollbar { width: 5px; }
    #sidebar::-webkit-scrollbar-thumb { background: rgba(255,255,255,0.15); border-radius: 3px; }
    #sidebar::-webkit-scrollbar-track { background: transparent; }
  </style>
</head>
<body>
  <div class="layout">
  <nav id="sidebar">
    <div class="sidebar-header">
      <h2>Opti-X Docs</h2>
      <p class="sidebar-subtitle">Developer Documentation</p>
    </div>
    <ul class="nav-tree">
    <li class="nav-item"><a href="#index" class="nav-link">Opti-X Developer Documentation</a></li>
    <li class="nav-section">
      <button class="section-toggle" aria-expanded="true">Introduction<span class="toggle-icon">&#9662;</span></button>
      <ul class="section-children">
        <li><a href="#what-is-optix" class="nav-link">What is Opti-X?</a></li>
        <li><a href="#key-concepts" class="nav-link">Key Concepts</a></li>
        <li><a href="#glossary" class="nav-link">Glossary</a></li>
      </ul>
    </li>
    <li class="nav-section">
      <button class="section-toggle" aria-expanded="true">Quickstart<span class="toggle-icon">&#9662;</span></button>
      <ul class="section-children">
        <li><a href="#prerequisites" class="nav-link">Prerequisites</a></li>
        <li><a href="#first-api-call" class="nav-link">First API Call</a></li>
      </ul>
    </li>
    <li class="nav-section">
      <button class="section-toggle" aria-expanded="true">Inventory<span class="toggle-icon">&#9662;</span></button>
      <ul class="section-children">
        <li><a href="#inventory-overview" class="nav-link">Inventory Overview</a></li>
        <li><a href="#gaming-inventory" class="nav-link">Gaming Inventory</a></li>
        <li><a href="#sports-inventory" class="nav-link">Sports Inventory</a></li>
        <li><a href="#ecommerce-inventory" class="nav-link">E-commerce Inventory</a></li>
        <li><a href="#lottery-bingo" class="nav-link">Lottery & Bingo</a></li>
        <li><a href="#availability-filters" class="nav-link">Availability Filters</a></li>
      </ul>
    </li>
    <li class="nav-section">
      <button class="section-toggle" aria-expanded="true">API Reference<span class="toggle-icon">&#9662;</span></button>
      <ul class="section-children">
        <li><a href="#api-reference-overview" class="nav-link">API Reference Overview</a></li>
        <li><a href="#authentication" class="nav-link">Authentication</a></li>
        <li><a href="#recommend-api" class="nav-link">Recommend API</a></li>
        <li><a href="#smart-search-api" class="nav-link">Smart Search API</a></li>
        <li><a href="#intelligent-layouts-api" class="nav-link">Intelligent Layouts API</a></li>
        <li><a href="#momentum-api" class="nav-link">Momentum API</a></li>
        <li><a href="#gaming-inventory-api" class="nav-link">Gaming Inventory API</a></li>
        <li><a href="#rate-limits" class="nav-link">Rate Limits</a></li>
        <li><a href="#error-handling" class="nav-link">Error Handling</a></li>
      </ul>
    </li>
    <li class="nav-section">
      <button class="section-toggle" aria-expanded="true">Events<span class="toggle-icon">&#9662;</span></button>
      <ul class="section-children">
        <li><a href="#events-overview" class="nav-link">Events Overview</a></li>
        <li><a href="#standard-events" class="nav-link">Standard Events</a></li>
        <li><a href="#gaming-events" class="nav-link">Gaming Events</a></li>
        <li><a href="#sports-events" class="nav-link">Sports Events</a></li>
        <li><a href="#ecommerce-events" class="nav-link">E-commerce Events</a></li>
        <li><a href="#kinesis-integration" class="nav-link">Kinesis Integration</a></li>
      </ul>
    </li>
    <li class="nav-section">
      <button class="section-toggle" aria-expanded="true">Filtering<span class="toggle-icon">&#9662;</span></button>
      <ul class="section-children">
        <li><a href="#filtering-overview" class="nav-link">Filtering Overview</a></li>
        <li><a href="#gaming-filtering" class="nav-link">Gaming Filtering</a></li>
        <li><a href="#sports-filtering" class="nav-link">Sports Filtering</a></li>
      </ul>
    </li>
    <li class="nav-section">
      <button class="section-toggle" aria-expanded="true">Banners<span class="toggle-icon">&#9662;</span></button>
      <ul class="section-children">
        <li><a href="#banner-deployment" class="nav-link">Banner Deployment</a></li>
      </ul>
    </li>
    <li class="nav-section">
      <button class="section-toggle" aria-expanded="true">Troubleshooting<span class="toggle-icon">&#9662;</span></button>
      <ul class="section-children">
        <li><a href="#common-issues" class="nav-link">Common Issues</a></li>
        <li><a href="#getting-help" class="nav-link">Getting Help</a></li>
      </ul>
    </li>
    </ul>
  </nav>
    <button id="sidebar-toggle" aria-label="Toggle sidebar">&#9776;</button>
    <main id="content">
<section id="index" class="doc-section">
<h1>Opti-X Developer Documentation</h1>
<p>Welcome to the Opti-X developer documentation. This guide helps you integrate AI-powered personalization into your gaming, sports betting, or e-commerce platform.</p>
<h2>What is Opti-X?</h2>
<p>Opti-X is Optimove&#39;s real-time personalization engine. It analyzes user behavior and inventory data to deliver personalized recommendations, search results, and dynamic layouts. Whether you&#39;re showing game suggestions to a casino player, match recommendations to a sports bettor, or product picks to an online shopper, Opti-X helps you show the right content to the right user at the right time.</p>
<hr>
<h2>Quick Links</h2>
<table>
<thead>
<tr>
<th>Resource</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td><a href="#first-api-call">Quickstart Guide</a></td>
<td>Make your first API call in 15 minutes</td>
</tr>
<tr>
<td><a href="#glossary">Glossary</a></td>
<td>Definitions for all Opti-X terms</td>
</tr>
<tr>
<td><a href="#key-concepts">Key Concepts</a></td>
<td>Understand the ABC framework</td>
</tr>
<tr>
<td><a href="#api-reference-overview">API Reference</a></td>
<td>Complete endpoint documentation</td>
</tr>
</tbody></table>
<hr>
<h2>Choose Your Path</h2>
<p>Select your industry to find relevant guides and examples:</p>
<h3>Gaming (iGaming / Online Casino)</h3>
<p>You want to recommend slots, table games, or live casino experiences to players.</p>
<ul>
<li><a href="#gaming-inventory">Gaming Integration Guide</a></li>
<li><a href="#gaming-events">Send Game Launch Events</a></li>
<li><a href="#recommend-api">Display Game Recommendations</a></li>
</ul>
<h3>Sports Betting</h3>
<p>You want to recommend matches, markets, or betting opportunities to users.</p>
<ul>
<li><a href="#sports-inventory">Sports Betting Integration Guide</a></li>
<li><a href="#sports-events">Send Bet Placement Events</a></li>
<li><a href="#recommend-api">Display Match Recommendations</a></li>
</ul>
<h3>E-commerce</h3>
<p>You want to recommend products, categories, or promotions to shoppers.</p>
<ul>
<li><a href="#ecommerce-inventory">E-commerce Integration Guide</a></li>
<li><a href="#ecommerce-events">Send Purchase Events</a></li>
<li><a href="#recommend-api">Display Product Recommendations</a></li>
</ul>
<hr>
<h2>Documentation Structure</h2>
<pre><code>Developer Docs/
├── 00-index.md                      # You are here
├── 01-introduction/
│   ├── what-is-optix.md             # Product overview
│   ├── key-concepts.md              # ABC framework and core concepts
│   └── glossary.md                  # Term definitions
├── 02-quickstart/
│   ├── prerequisites.md             # Setup checklist
│   └── first-api-call.md            # Your first recommendation request
├── 03-integration-guides/
│   ├── gaming-integration.md        # Full gaming setup
│   ├── sports-integration.md        # Full sports betting setup
│   └── ecommerce-integration.md     # Full e-commerce setup
├── 04-activity-tracking/
│   ├── overview.md                  # Activity API introduction
│   ├── gaming-events.md             # Game launch, session events
│   ├── sports-events.md             # Bet placement, view events
│   └── ecommerce-events.md          # Purchase, cart, view events
├── 05-recommendations/
│   ├── overview.md                  # Recommendations API introduction
│   ├── placements.md                # Configuring placements
│   ├── methods-and-models.md        # Personalization algorithms
│   └── filtering.md                 # Inclusions, exclusions, tags
├── 06-search/
│   ├── smart-search.md              # AI-powered search
│   └── autocomplete.md              # Search suggestions
├── 07-layouts/
│   └── dynamic-layouts.md           # Personalized page layouts
└── 08-advanced/
    ├── analytics.md                 # Tracking and reporting
    ├── testing.md                   # A/B testing recommendations
    └── troubleshooting.md           # Common issues and solutions
</code></pre>
<hr>
<h2>Getting Help</h2>
<ul>
<li><strong>Technical Support</strong>: Contact your Optimove Customer Success Manager</li>
<li><strong>API Status</strong>: Check the Opti-X Admin Panel for system status</li>
<li><strong>Changelog</strong>: Review recent updates in the Admin Panel under Release Notes</li>
</ul>
<hr>
<h2>Related Topics</h2>
<ul>
<li><a href="#what-is-optix">What is Opti-X?</a> - Learn about Opti-X capabilities</li>
<li><a href="#prerequisites">Prerequisites</a> - Get your API keys</li>
<li><a href="#first-api-call">First API Call</a> - Start integrating today</li>
</ul>

</section>
<section id="what-is-optix" class="doc-section">
<h1>What is Opti-X?</h1>
<p>Opti-X is Optimove&#39;s AI-powered personalization engine that delivers real-time recommendations, personalized search results, and dynamic layouts across gaming, sports betting, and e-commerce platforms.</p>
<hr>
<h2>The Business Problem</h2>
<p>Your platform has thousands of games, matches, or products. Your users have limited time and attention. Without personalization:</p>
<ul>
<li>Users struggle to find content they&#39;ll enjoy</li>
<li>Popular content dominates, hiding niche items that might convert better</li>
<li>Every user sees the same homepage, regardless of their preferences</li>
<li>Search returns generic results that don&#39;t account for user behavior</li>
</ul>
<p>Opti-X solves these problems by analyzing what each user does and recommending what they&#39;ll want next.</p>
<hr>
<h2>What Opti-X Does</h2>
<h3>Real-Time Recommendations</h3>
<p>Opti-X analyzes user behavior (game launches, bets placed, purchases made) and inventory data (games, matches, products) to generate personalized recommendations. These recommendations update in real-time as users interact with your platform.</p>
<p><strong>Example</strong>: A casino player who frequently plays high-volatility slots sees new high-volatility releases at the top of their homepage. A player who prefers table games sees blackjack and roulette recommendations instead.</p>
<h3>Smart Search</h3>
<p>Traditional search matches keywords. Opti-X Smart Search understands user intent and personalizes results based on behavior patterns. Two users searching for &quot;slots&quot; see different results based on their preferences.</p>
<p><strong>Example</strong>: User A searches &quot;football&quot; and sees Premier League matches because they frequently bet on English football. User B searches &quot;football&quot; and sees NFL games because they prefer American football.</p>
<h3>Dynamic Layouts</h3>
<p>Opti-X can personalize entire page layouts, not just individual recommendation carousels. The system determines which sections to show, in what order, based on each user&#39;s interests.</p>
<p><strong>Example</strong>: A sports bettor who primarily wagers on live events sees the &quot;Live Now&quot; section prominently displayed. A user who plans bets in advance sees upcoming fixtures first.</p>
<h3>Campaign Integration</h3>
<p>Opti-X integrates with Optimove&#39;s campaign management to ensure promotional content appears alongside personalized recommendations. Campaigns can target specific user segments with relevant offers.</p>
<hr>
<h2>Supported Verticals</h2>
<h3>Gaming (iGaming / Online Casino)</h3>
<p>Personalize the player experience across:</p>
<ul>
<li><strong>Slots</strong>: Recommend games based on themes, volatility, RTP preferences</li>
<li><strong>Table Games</strong>: Suggest blackjack, roulette, baccarat variants</li>
<li><strong>Live Casino</strong>: Recommend live dealer experiences</li>
<li><strong>Game Shows</strong>: Suggest interactive game show content</li>
</ul>
<p><strong>Key inventory attributes</strong>: Game name, provider, RTP, volatility, theme, category</p>
<h3>Sports Betting</h3>
<p>Personalize betting experiences across:</p>
<ul>
<li><strong>Pre-match Betting</strong>: Recommend upcoming matches and markets</li>
<li><strong>Live Betting</strong>: Suggest in-play opportunities</li>
<li><strong>Outrights</strong>: Recommend tournament and season-long bets</li>
<li><strong>Virtuals</strong>: Suggest virtual sports content</li>
</ul>
<p><strong>Key inventory attributes</strong>: Sport, competition, teams, markets, odds, event time</p>
<h3>E-commerce</h3>
<p>Personalize shopping experiences across:</p>
<ul>
<li><strong>Product Recommendations</strong>: Suggest items based on browse and purchase history</li>
<li><strong>Category Pages</strong>: Personalize product ordering within categories</li>
<li><strong>Search Results</strong>: Rank results by relevance to each shopper</li>
<li><strong>Cross-sell and Upsell</strong>: Recommend complementary products</li>
</ul>
<p><strong>Key inventory attributes</strong>: Product name, category, price, brand, attributes, availability</p>
<hr>
<h2>Why Personalization Matters</h2>
<h3>Increased Engagement</h3>
<p>Users who see relevant content spend more time on your platform. Personalized recommendations reduce the effort needed to find interesting content, keeping users engaged longer.</p>
<h3>Higher Conversion Rates</h3>
<p>When users see products, games, or matches aligned with their interests, they&#39;re more likely to convert. Personalization moves users from browsing to buying.</p>
<h3>Improved Retention</h3>
<p>Users return to platforms that understand them. Personalized experiences create loyalty by consistently delivering value.</p>
<h3>Revenue Growth</h3>
<p>Personalization directly impacts revenue through:</p>
<ul>
<li>Higher average order values (e-commerce)</li>
<li>Increased bet frequency (sports betting)</li>
<li>More game sessions (gaming)</li>
</ul>
<hr>
<h2>How Opti-X Works</h2>
<p>Opti-X operates on three core data flows:</p>
<ol>
<li><p><strong>Activity Data (Input)</strong>: Your platform sends user events to Opti-X. Every page view, game launch, bet placement, or purchase helps the system understand user preferences.</p>
</li>
<li><p><strong>Inventory Data (Input)</strong>: You provide your content catalog—games, matches, products—with relevant attributes. Opti-X uses this data to understand what&#39;s available and how to categorize it.</p>
</li>
<li><p><strong>Recommendations (Output)</strong>: Your platform requests personalized content from Opti-X. The system returns ranked recommendations based on user behavior, inventory attributes, and business rules.</p>
</li>
</ol>
<p>This cycle creates a feedback loop: as users interact with recommendations, Opti-X learns and improves future suggestions.</p>
<hr>
<h2>Architecture Overview</h2>
<pre><code>┌─────────────────┐     ┌─────────────────┐     ┌─────────────────┐
│   Your App      │     │    Opti-X       │     │   Admin Panel   │
│                 │     │                 │     │                 │
│  ┌───────────┐  │     │  ┌───────────┐  │     │  ┌───────────┐  │
│  │  Website  │──┼──▶──│  │  Activity │  │     │  │ Placements│  │
│  │  or App   │  │     │  │    API    │  │     │  │  Config   │  │
│  └───────────┘  │     │  └───────────┘  │     │  └───────────┘  │
│                 │     │        │        │     │                 │
│  ┌───────────┐  │     │        ▼        │     │  ┌───────────┐  │
│  │  Backend  │──┼──▶──│  ┌───────────┐  │     │  │  Methods  │  │
│  │  Server   │  │     │  │    AI     │  │     │  │  &amp; Models │  │
│  └───────────┘  │     │  │  Engine   │  │     │  └───────────┘  │
│        │        │     │  └───────────┘  │     │                 │
│        │        │     │        │        │     │  ┌───────────┐  │
│        ▼        │     │        ▼        │     │  │ Analytics │  │
│  ┌───────────┐  │     │  ┌───────────┐  │     │  │ Dashboard │  │
│  │   UI      │◀─┼──◀──│  │   Recs    │  │     │  └───────────┘  │
│  │ Display   │  │     │  │    API    │  │     │                 │
│  └───────────┘  │     │  └───────────┘  │     │                 │
└─────────────────┘     └─────────────────┘     └─────────────────┘
</code></pre>
<hr>
<h2>Key Capabilities Summary</h2>
<table>
<thead>
<tr>
<th>Capability</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>Recommendations</td>
<td>Personalized content suggestions based on user behavior</td>
</tr>
<tr>
<td>Smart Search</td>
<td>AI-powered search with personalized ranking</td>
</tr>
<tr>
<td>Dynamic Layouts</td>
<td>Personalized page structure and section ordering</td>
</tr>
<tr>
<td>Filtering</td>
<td>Include or exclude content based on tags and attributes</td>
</tr>
<tr>
<td>A/B Testing</td>
<td>Compare personalization strategies</td>
</tr>
<tr>
<td>Analytics</td>
<td>Measure recommendation performance</td>
</tr>
<tr>
<td>Campaign Integration</td>
<td>Combine personalization with marketing campaigns</td>
</tr>
</tbody></table>
<hr>
<h2>Related Topics</h2>
<ul>
<li><a href="#key-concepts">Key Concepts</a> - Learn the ABC framework</li>
<li><a href="#glossary">Glossary</a> - Understand Opti-X terminology</li>
<li><a href="#prerequisites">Prerequisites</a> - Get your API credentials</li>
<li><a href="#first-api-call">First API Call</a> - Start integrating</li>
</ul>

</section>
<section id="key-concepts" class="doc-section">
<h1>Key Concepts</h1>
<p>This guide explains the core concepts you need to understand before integrating Opti-X. Master these fundamentals, and the rest of the documentation will make sense.</p>
<hr>
<h2>The ABC Framework</h2>
<p>Opti-X integration follows the ABC pattern:</p>
<ul>
<li><strong>A</strong>ctivity - Send user events to Opti-X</li>
<li><strong>B</strong>ettable Content (Inventory) - Provide your content catalog</li>
<li><strong>C</strong>onsume - Request personalized recommendations</li>
</ul>
<p>Each component is essential. Activity data teaches Opti-X about user preferences. Inventory data tells Opti-X what content exists. Consumption APIs deliver personalized results.</p>
<h3>A - Activity (User Events)</h3>
<p>Activity data represents everything users do on your platform. When a user launches a game, places a bet, or purchases a product, you send that event to Opti-X. These events build a behavioral profile for each user.</p>
<p><strong>Common activity events by vertical:</strong></p>
<table>
<thead>
<tr>
<th>Gaming</th>
<th>Sports Betting</th>
<th>E-commerce</th>
</tr>
</thead>
<tbody><tr>
<td>Game launch</td>
<td>Bet placement</td>
<td>Product view</td>
</tr>
<tr>
<td>Game session end</td>
<td>Match view</td>
<td>Add to cart</td>
</tr>
<tr>
<td>Deposit</td>
<td>Cashout</td>
<td>Purchase</td>
</tr>
<tr>
<td>Bonus claim</td>
<td>Live bet</td>
<td>Wishlist add</td>
</tr>
</tbody></table>
<p><strong>Why Activity Matters</strong>: Without activity data, Opti-X can&#39;t personalize. A user with no tracked activity receives generic, non-personalized recommendations. More activity data leads to better personalization.</p>
<p><strong>Example Activity Event (Gaming)</strong>:</p>
<pre><code class="language-json">{
  &quot;event_type&quot;: &quot;game_launch&quot;,
  &quot;user_id&quot;: &quot;player_12345&quot;,
  &quot;game_id&quot;: &quot;starburst-xxxtreme&quot;,
  &quot;timestamp&quot;: &quot;2024-01-15T14:32:00Z&quot;,
  &quot;device&quot;: &quot;mobile&quot;,
  &quot;session_id&quot;: &quot;sess_abc123&quot;
}
</code></pre>
<h3>B - Bettable Content (Inventory)</h3>
<p>Inventory represents all the content you can recommend: games, sports events, products. You provide this data to Opti-X with attributes that describe each item.</p>
<p><strong>Inventory attributes by vertical:</strong></p>
<table>
<thead>
<tr>
<th>Gaming</th>
<th>Sports Betting</th>
<th>E-commerce</th>
</tr>
</thead>
<tbody><tr>
<td>Game ID, name</td>
<td>Event ID, name</td>
<td>Product ID, name</td>
</tr>
<tr>
<td>Provider</td>
<td>Sport, competition</td>
<td>Category, brand</td>
</tr>
<tr>
<td>RTP, volatility</td>
<td>Teams, markets</td>
<td>Price, SKU</td>
</tr>
<tr>
<td>Theme, category</td>
<td>Event time, odds</td>
<td>Availability</td>
</tr>
<tr>
<td>Release date</td>
<td>Live/pre-match</td>
<td>Attributes</td>
</tr>
</tbody></table>
<p><strong>Why Inventory Matters</strong>: Opti-X can only recommend items in your inventory. If a game isn&#39;t in the inventory feed, it won&#39;t appear in recommendations. Keep your inventory current and attribute-rich for better personalization.</p>
<p><strong>Example Inventory Item (Gaming)</strong>:</p>
<pre><code class="language-json">{
  &quot;game_id&quot;: &quot;starburst-xxxtreme&quot;,
  &quot;name&quot;: &quot;Starburst XXXtreme&quot;,
  &quot;provider&quot;: &quot;NetEnt&quot;,
  &quot;rtp&quot;: 96.45,
  &quot;volatility&quot;: &quot;high&quot;,
  &quot;theme&quot;: &quot;space&quot;,
  &quot;category&quot;: &quot;slots&quot;,
  &quot;release_date&quot;: &quot;2023-06-15&quot;
}
</code></pre>
<h3>C - Consume (Get Recommendations)</h3>
<p>Consume refers to requesting personalized content from Opti-X. When a user loads a page, your application calls the Opti-X API to get recommendations tailored to that user.</p>
<p><strong>Common consumption scenarios:</strong></p>
<table>
<thead>
<tr>
<th>Scenario</th>
<th>What You Request</th>
</tr>
</thead>
<tbody><tr>
<td>Homepage load</td>
<td>Personalized game/product carousel</td>
</tr>
<tr>
<td>Category page</td>
<td>Ranked items within category</td>
</tr>
<tr>
<td>Search query</td>
<td>Personalized search results</td>
</tr>
<tr>
<td>Post-purchase</td>
<td>Cross-sell recommendations</td>
</tr>
</tbody></table>
<p><strong>Why Consumption Matters</strong>: This is where personalization delivers value. The API response contains ranked content items that you display to users. The order reflects each user&#39;s predicted preferences.</p>
<p><strong>Example Recommendation Request</strong>:</p>
<pre><code class="language-bash">GET /v3/recommend/placements/homepage-carousel
?visitor_id=player_12345
&amp;num_items=10
</code></pre>
<p><strong>Example Response</strong>:</p>
<pre><code class="language-json">{
  &quot;items&quot;: [
    {
      &quot;item_id&quot;: &quot;starburst-xxxtreme&quot;,
      &quot;rec_id&quot;: &quot;rec_789xyz&quot;,
      &quot;position&quot;: 1
    },
    {
      &quot;item_id&quot;: &quot;book-of-dead&quot;,
      &quot;rec_id&quot;: &quot;rec_790xyz&quot;,
      &quot;position&quot;: 2
    }
  ]
}
</code></pre>
<hr>
<h2>Placements</h2>
<p>A placement represents a location on your platform where recommendations appear. Each placement has a unique identifier and configuration that controls what content appears and how it&#39;s selected.</p>
<p><strong>Examples of placements:</strong></p>
<table>
<thead>
<tr>
<th>Placement</th>
<th>Location</th>
<th>Purpose</th>
</tr>
</thead>
<tbody><tr>
<td><code>homepage-hero</code></td>
<td>Homepage top banner</td>
<td>Featured game/offer</td>
</tr>
<tr>
<td><code>homepage-carousel</code></td>
<td>Homepage recommendation row</td>
<td>Personalized suggestions</td>
</tr>
<tr>
<td><code>category-grid</code></td>
<td>Category page</td>
<td>Ranked items in category</td>
</tr>
<tr>
<td><code>search-results</code></td>
<td>Search page</td>
<td>Personalized search ranking</td>
</tr>
<tr>
<td><code>post-bet-recommendations</code></td>
<td>Bet slip confirmation</td>
<td>Cross-sell suggestions</td>
</tr>
</tbody></table>
<p><strong>Why Placements Matter</strong>: Placements let you configure different personalization strategies for different parts of your platform. Your homepage might prioritize new releases while a category page might prioritize user preferences.</p>
<p>You configure placements in the Opti-X Admin Panel, then reference them by ID in your API calls.</p>
<hr>
<h2>Methods</h2>
<p>A method defines the algorithm strategy used to select and rank recommendations. Different methods serve different business goals.</p>
<p><strong>Common methods:</strong></p>
<table>
<thead>
<tr>
<th>Method</th>
<th>Description</th>
<th>Best For</th>
</tr>
</thead>
<tbody><tr>
<td>Personalized</td>
<td>Uses user behavior to rank items</td>
<td>Homepage, logged-in users</td>
</tr>
<tr>
<td>Popular</td>
<td>Ranks by global popularity</td>
<td>New users, cold start</td>
</tr>
<tr>
<td>Trending</td>
<td>Ranks by recent popularity momentum</td>
<td>Highlighting rising content</td>
</tr>
<tr>
<td>Similar</td>
<td>Finds items similar to a reference</td>
<td>&quot;More like this&quot; carousels</td>
</tr>
<tr>
<td>Complementary</td>
<td>Finds items that go well together</td>
<td>Cross-sell, upsell</td>
</tr>
</tbody></table>
<p><strong>Why Methods Matter</strong>: The right method depends on context. A new user with no history benefits from Popular recommendations. A returning user benefits from Personalized. Similar recommendations work well on product detail pages.</p>
<hr>
<h2>Models</h2>
<p>A model is a trained machine learning algorithm that powers a method. While methods define the strategy, models are the actual implementations that generate recommendations.</p>
<p><strong>How models work:</strong></p>
<ol>
<li>Opti-X trains models on your activity and inventory data</li>
<li>Models learn patterns: &quot;Users who play Slot A also play Slot B&quot;</li>
<li>When you request recommendations, models score and rank items</li>
<li>The highest-scoring items appear in the response</li>
</ol>
<p><strong>Why Models Matter</strong>: Model quality directly impacts recommendation relevance. Models improve over time as they process more activity data. Opti-X handles model training automatically—your job is to send quality activity data.</p>
<hr>
<h2>Tags</h2>
<p>Tags are labels you attach to inventory items for filtering and targeting. Use tags to group content by business attributes that don&#39;t fit standard inventory fields.</p>
<p><strong>Tag examples:</strong></p>
<table>
<thead>
<tr>
<th>Tag Type</th>
<th>Example Tags</th>
<th>Purpose</th>
</tr>
</thead>
<tbody><tr>
<td><code>promotion</code></td>
<td><code>holiday-promo</code>, <code>vip-exclusive</code></td>
<td>Marketing campaigns</td>
</tr>
<tr>
<td><code>content-rating</code></td>
<td><code>mature</code>, <code>family-friendly</code></td>
<td>Regulatory compliance</td>
</tr>
<tr>
<td><code>feature</code></td>
<td><code>jackpot</code>, <code>megaways</code>, <code>bonus-buy</code></td>
<td>Game mechanics</td>
</tr>
<tr>
<td><code>availability</code></td>
<td><code>uk-only</code>, <code>de-restricted</code></td>
<td>Geo-restrictions</td>
</tr>
</tbody></table>
<p><strong>Tag types</strong>: Tags belong to tag types. The tag type <code>feature</code> might contain tags like <code>jackpot</code>, <code>megaways</code>, and <code>bonus-buy</code>. Tag types help organize tags and enable bulk operations.</p>
<p><strong>Why Tags Matter</strong>: Tags power filtering. You can request recommendations that include only items with certain tags, or exclude items with certain tags. This lets you combine personalization with business rules.</p>
<hr>
<h2>Inclusions and Exclusions</h2>
<p>Inclusions and exclusions filter recommendations based on tags, categories, or other attributes.</p>
<p><strong>Inclusions</strong>: Only show items matching these criteria</p>
<pre><code class="language-json">{
  &quot;inclusions&quot;: {
    &quot;tags&quot;: [&quot;jackpot&quot;],
    &quot;providers&quot;: [&quot;netent&quot;, &quot;pragmatic-play&quot;]
  }
}
</code></pre>
<p><strong>Exclusions</strong>: Never show items matching these criteria</p>
<pre><code class="language-json">{
  &quot;exclusions&quot;: {
    &quot;tags&quot;: [&quot;mature-content&quot;],
    &quot;categories&quot;: [&quot;live-casino&quot;]
  }
}
</code></pre>
<p><strong>Why Inclusions/Exclusions Matter</strong>: They enforce business rules. A &quot;New Releases&quot; carousel includes only games released in the last 30 days. A family-friendly landing page excludes mature content. Personalization operates within these constraints.</p>
<hr>
<h2>Context ID</h2>
<p>A context ID identifies a specific content item that provides context for recommendations. Use it for &quot;similar items&quot; or &quot;because you viewed X&quot; scenarios.</p>
<p><strong>Example</strong>: User views the game &quot;Book of Dead&quot;. You request recommendations with <code>context_id=book-of-dead</code>. Opti-X returns games similar to Book of Dead.</p>
<pre><code class="language-bash">GET /v3/recommend/placements/similar-games
?visitor_id=player_12345
&amp;context_id=book-of-dead
&amp;num_items=6
</code></pre>
<p><strong>Why Context ID Matters</strong>: Context IDs power contextual recommendations. They answer &quot;what&#39;s similar to this?&quot; rather than &quot;what does this user like?&quot; Both are valuable in different scenarios.</p>
<hr>
<h2>Visitor ID vs. User ID</h2>
<p>Opti-X tracks users with two identifiers:</p>
<p><strong>Visitor ID</strong>: An anonymous identifier for users who haven&#39;t logged in. Typically stored in a cookie or device ID. Allows personalization for anonymous browsing.</p>
<p><strong>User ID</strong>: A known identifier for logged-in users. Links activity across devices and sessions. Provides richer personalization.</p>
<p><strong>Best practice</strong>: Send both when available. Opti-X links visitor and user IDs when a user logs in, combining anonymous and authenticated behavior.</p>
<pre><code class="language-bash">GET /v3/recommend/placements/homepage-carousel
?visitor_id=anon_abc123
&amp;user_id=player_12345
&amp;num_items=10
</code></pre>
<hr>
<h2>Recommendation ID (recId)</h2>
<p>Every recommendation response includes a <code>rec_id</code> for each item. This unique identifier tracks which recommendations users saw and clicked.</p>
<p><strong>Why recId Matters</strong>: Send the <code>rec_id</code> back when users click recommendations. This closes the feedback loop—Opti-X learns which recommendations drive engagement.</p>
<p><strong>Example click tracking</strong>:</p>
<pre><code class="language-json">{
  &quot;event_type&quot;: &quot;recommendation_click&quot;,
  &quot;user_id&quot;: &quot;player_12345&quot;,
  &quot;rec_id&quot;: &quot;rec_789xyz&quot;,
  &quot;item_id&quot;: &quot;starburst-xxxtreme&quot;
}
</code></pre>
<hr>
<h2>Traits</h2>
<p>Traits are user attributes that enhance personalization. Beyond behavioral activity, traits provide explicit information about users.</p>
<p><strong>Example traits:</strong></p>
<table>
<thead>
<tr>
<th>Trait</th>
<th>Example Value</th>
<th>Impact</th>
</tr>
</thead>
<tbody><tr>
<td><code>preferred_language</code></td>
<td><code>de</code></td>
<td>Prioritize German-language content</td>
</tr>
<tr>
<td><code>vip_tier</code></td>
<td><code>gold</code></td>
<td>Show VIP-exclusive items</td>
</tr>
<tr>
<td><code>risk_profile</code></td>
<td><code>high-roller</code></td>
<td>Recommend high-stakes options</td>
</tr>
<tr>
<td><code>age_verified</code></td>
<td><code>true</code></td>
<td>Include age-restricted content</td>
</tr>
</tbody></table>
<p><strong>Why Traits Matter</strong>: Traits add dimensions to personalization beyond behavior. A user might not have played high-volatility slots recently, but if their trait indicates they&#39;re a high-roller, Opti-X can factor that in.</p>
<hr>
<h2>Skin ID</h2>
<p>A skin ID identifies a brand variant within a multi-brand platform. If you operate multiple casino or betting brands from the same backend, skin IDs separate their inventories and configurations.</p>
<p><strong>Example</strong>: You operate &quot;CasinoA&quot; and &quot;CasinoB&quot; from the same platform. Each skin has its own:</p>
<ul>
<li>Inventory (different game portfolios)</li>
<li>Placements (different homepage layouts)</li>
<li>Branding (different visual treatment)</li>
</ul>
<p><strong>Why Skin ID Matters</strong>: Multi-brand operators need separation. A game available on CasinoA might not be on CasinoB. Skin IDs ensure recommendations only include items available for that brand.</p>
<hr>
<h2>Regulation</h2>
<p>Regulation refers to compliance rules that restrict what content can be shown to users based on their jurisdiction.</p>
<p><strong>Example</strong>: A user in Germany (<code>regulation=de</code>) should only see games licensed for the German market. UK users (<code>regulation=uk</code>) should only see UK-licensed games.</p>
<p><strong>Why Regulation Matters</strong>: Gaming and betting are heavily regulated. Recommendations must respect licensing restrictions. Opti-X filters recommendations based on regulation parameters to ensure compliance.</p>
<hr>
<h2>Summary: How It All Fits Together</h2>
<ol>
<li><strong>Send Activity</strong>: Track user events (game launches, bets, purchases)</li>
<li><strong>Provide Inventory</strong>: Keep your content catalog updated with rich attributes</li>
<li><strong>Configure Placements</strong>: Set up recommendation locations in Admin Panel</li>
<li><strong>Choose Methods</strong>: Select algorithms that match your goals</li>
<li><strong>Apply Tags</strong>: Label content for filtering and targeting</li>
<li><strong>Request Recommendations</strong>: Call the API with user context</li>
<li><strong>Display Results</strong>: Show personalized content to users</li>
<li><strong>Track Engagement</strong>: Send click events with recIds</li>
</ol>
<p>This cycle runs continuously. More activity data improves models. Better recommendations increase engagement. Increased engagement generates more activity data.</p>
<hr>
<h2>Related Topics</h2>
<ul>
<li><a href="#glossary">Glossary</a> - Complete term definitions</li>
<li><a href="#first-api-call">First API Call</a> - Put concepts into practice</li>
<li><a href="#recommend-api">Placements Configuration</a> - Set up placements</li>
<li><a href="#recommend-api">Methods and Models</a> - Choose algorithms</li>
</ul>

</section>
<section id="glossary" class="doc-section">
<h1>Glossary</h1>
<p>This glossary defines terms used throughout the Opti-X documentation. Terms are organized alphabetically for quick reference.</p>
<hr>
<h2>A</h2>
<h3>Activity</h3>
<p>User events sent to Opti-X that describe behavior on your platform. Examples include game launches, bet placements, product views, and purchases. Activity data powers personalization by teaching Opti-X about user preferences.</p>
<h3>Activity API</h3>
<p>The API endpoint for sending user events to Opti-X. Activity events are sent as POST requests with event details in the request body.</p>
<h3>API Key</h3>
<p>A credential used to authenticate requests to Opti-X APIs. You receive API keys from the Admin Panel under Developer Tools &gt; API Keys. See also: x-api-key, x-brand-key.</p>
<h3>Autocomplete</h3>
<p>A search feature that suggests completions as users type. Opti-X Autocomplete provides personalized suggestions based on user behavior and popular searches.</p>
<hr>
<h2>B</h2>
<h3>Bettable Content</h3>
<p>Another term for inventory in sports betting contexts. Refers to matches, markets, and selections available for wagering.</p>
<h3>Brand Key</h3>
<p>See x-brand-key.</p>
<hr>
<h2>C</h2>
<h3>Campaign</h3>
<p>A targeted marketing initiative that combines personalization with promotional content. Campaigns can inject specific items into recommendations for targeted user segments.</p>
<h3>Category</h3>
<p>A classification level for inventory items. In gaming, categories include &quot;slots,&quot; &quot;table-games,&quot; and &quot;live-casino.&quot; In e-commerce, categories organize products into hierarchies like &quot;Electronics &gt; Phones &gt; Smartphones.&quot;</p>
<h3>Class</h3>
<p>In sports betting, a classification level below Category. For example, within the &quot;Football&quot; category, classes might include &quot;Premier League,&quot; &quot;La Liga,&quot; or &quot;Champions League.&quot;</p>
<h3>Cold Start</h3>
<p>The challenge of personalizing for users with little or no activity history. Opti-X addresses cold start with popularity-based methods and trait-based personalization.</p>
<h3>Competition</h3>
<p>In sports betting, a specific league, tournament, or cup. Examples: Premier League, NBA Finals, World Cup.</p>
<h3>Consume / Consumption</h3>
<p>The act of requesting personalized content from Opti-X. &quot;Consuming&quot; recommendations means calling the API to get personalized results for display.</p>
<h3>Context ID</h3>
<p>An identifier for a specific content item that provides context for recommendations. Used for &quot;similar items&quot; recommendations. If a user views Game A, passing <code>context_id=game-a</code> returns games similar to Game A.</p>
<hr>
<h2>D</h2>
<h3>Dynamic Layout</h3>
<p>A page layout where the structure and ordering of sections are personalized per user. Unlike static layouts, dynamic layouts adapt based on user preferences.</p>
<hr>
<h2>E</h2>
<h3>Event (Activity)</h3>
<p>A single user action tracked by the Activity API. Events include game launches, bet placements, purchases, page views, and more.</p>
<h3>Event (Sports)</h3>
<p>A specific match or fixture in sports betting. An event has teams, a start time, and associated markets. Example: &quot;Manchester United vs Liverpool, January 15, 2024.&quot;</p>
<h3>Exclusions</h3>
<p>Filters that remove items from recommendations based on tags, categories, or attributes. If you exclude the tag &quot;mature-content,&quot; no items with that tag appear in recommendations.</p>
<hr>
<h2>F</h2>
<h3>Fallback</h3>
<p>The backup strategy when personalized recommendations aren&#39;t available. Typically shows popular items when user-specific data is insufficient.</p>
<h3>Feed</h3>
<p>A data file (usually JSON or CSV) containing inventory items or activity events. Feeds are used for bulk data synchronization with Opti-X.</p>
<hr>
<h2>G</h2>
<h3>Game ID</h3>
<p>A unique identifier for a game in your inventory. Used consistently across activity events, inventory feeds, and recommendation responses.</p>
<hr>
<h2>H</h2>
<h3>Hot Start</h3>
<p>The opposite of cold start. A user with significant activity history, enabling highly personalized recommendations.</p>
<hr>
<h2>I</h2>
<h3>Impressions</h3>
<p>The number of times recommendations are displayed to users. Used for measuring recommendation visibility and calculating click-through rates.</p>
<h3>Inclusions</h3>
<p>Filters that restrict recommendations to items matching specified tags, categories, or attributes. If you include only the tag &quot;jackpot,&quot; only jackpot games appear in recommendations.</p>
<h3>Inventory</h3>
<p>The complete catalog of content items available for recommendation. In gaming, inventory includes games. In sports betting, inventory includes events and markets. In e-commerce, inventory includes products.</p>
<h3>Item ID</h3>
<p>A unique identifier for any inventory item (game, product, event). Used to reference specific items in API requests and responses.</p>
<hr>
<h2>J</h2>
<h3>Jackpot</h3>
<p>A gaming feature where prize pools accumulate until won. Often used as a tag to filter recommendations to jackpot games.</p>
<hr>
<h2>K</h2>
<h3>Key Concepts</h3>
<p>The foundational ideas in Opti-X: Activity, Bettable Content (Inventory), and Consume (the ABC framework).</p>
<hr>
<h2>L</h2>
<h3>Live Betting</h3>
<p>Sports betting on events currently in progress. Live betting inventory changes rapidly as events unfold.</p>
<h3>Live Casino</h3>
<p>A gaming category featuring real dealers streamed via video. Live casino games include live blackjack, live roulette, and live baccarat.</p>
<hr>
<h2>M</h2>
<h3>Market</h3>
<p>In sports betting, a specific betting opportunity within an event. Examples: Match Winner, Over/Under Goals, Both Teams to Score.</p>
<h3>Method</h3>
<p>The algorithm strategy used to generate recommendations. Methods include Personalized, Popular, Trending, Similar, and Complementary.</p>
<h3>Model</h3>
<p>A trained machine learning algorithm that implements a method. Models learn from activity and inventory data to generate personalized rankings.</p>
<hr>
<h2>N</h2>
<h3>Num Items</h3>
<p>A parameter specifying how many items to return in a recommendation response. Example: <code>num_items=10</code> returns 10 recommendations.</p>
<hr>
<h2>O</h2>
<h3>Odds</h3>
<p>In sports betting, the probability and potential payout for a selection. Odds affect which bets users find attractive and can influence recommendations.</p>
<h3>Opti-X Admin Panel</h3>
<p>The web interface for configuring Opti-X. Access placements, methods, analytics, and API keys through the Admin Panel.</p>
<hr>
<h2>P</h2>
<h3>Personalization</h3>
<p>The process of tailoring content to individual users based on their behavior, preferences, and attributes.</p>
<h3>Placement</h3>
<p>A configured location on your platform where recommendations appear. Each placement has a unique ID and settings that control what content appears. Examples: homepage-carousel, category-page, post-purchase.</p>
<h3>Popular Method</h3>
<p>A recommendation method that ranks items by global popularity. Useful for new users or cold start scenarios.</p>
<h3>Pre-match</h3>
<p>In sports betting, events that haven&#39;t started yet. Pre-match betting is the traditional form of sports wagering.</p>
<h3>Provider</h3>
<p>The company that created a game. Examples: NetEnt, Pragmatic Play, Evolution. Provider is a common filter for gaming recommendations.</p>
<hr>
<h2>Q</h2>
<h3>Query</h3>
<p>In Smart Search, the text a user enters to search for content. Opti-X personalizes search results based on the query and user behavior.</p>
<hr>
<h2>R</h2>
<h3>Ranking</h3>
<p>The order of items in a recommendation response. Higher-ranked items appear first and are predicted to be more relevant to the user.</p>
<h3>recId (Recommendation ID)</h3>
<p>A unique identifier assigned to each recommended item in a response. Send recId back with click events to track recommendation performance.</p>
<h3>Recommendation</h3>
<p>A suggested content item generated by Opti-X for a specific user. Recommendations are ranked by predicted relevance.</p>
<h3>Regulation</h3>
<p>Compliance rules that restrict content availability based on user jurisdiction. Different regulations (UK, DE, MT) may have different content requirements.</p>
<h3>Response</h3>
<p>The data returned by an Opti-X API call. Recommendation responses include ranked items with IDs, positions, and recIds.</p>
<h3>RTP (Return to Player)</h3>
<p>A percentage indicating the expected payout of a game over time. An RTP of 96% means the game returns $96 for every $100 wagered on average. RTP is a common attribute for gaming inventory.</p>
<hr>
<h2>S</h2>
<h3>Selection</h3>
<p>In sports betting, a specific outcome within a market. For a &quot;Match Winner&quot; market, selections might be &quot;Home Win,&quot; &quot;Draw,&quot; &quot;Away Win.&quot;</p>
<h3>Session ID</h3>
<p>An identifier for a user&#39;s browsing session. Used to group activity events that occur during the same visit.</p>
<h3>Similar Method</h3>
<p>A recommendation method that finds items similar to a reference item. Powered by context_id.</p>
<h3>Skin ID</h3>
<p>An identifier for a brand variant in multi-brand platforms. Skin IDs separate inventory, placements, and configurations between brands.</p>
<h3>SKU (Stock Keeping Unit)</h3>
<p>A unique identifier for a product variant in e-commerce. A shirt might have multiple SKUs for different sizes and colors.</p>
<h3>Slot</h3>
<p>A casino game category featuring spinning reels and symbol combinations. Slots are the most common game type in online casinos.</p>
<h3>Smart Search</h3>
<p>Opti-X&#39;s AI-powered search feature that personalizes results based on user behavior and intent understanding.</p>
<h3>Sport</h3>
<p>The top-level category in sports betting. Examples: Football, Basketball, Tennis, Horse Racing.</p>
<hr>
<h2>T</h2>
<h3>Table Games</h3>
<p>A casino game category including blackjack, roulette, baccarat, and poker. Table games typically have fixed rules and player decisions.</p>
<h3>Tag</h3>
<p>A label attached to inventory items for filtering and targeting. Tags enable business rules like &quot;show only VIP games&quot; or &quot;exclude mature content.&quot;</p>
<h3>Tag Type</h3>
<p>A category that groups related tags. The tag type &quot;feature&quot; might contain tags like &quot;jackpot,&quot; &quot;megaways,&quot; and &quot;bonus-buy.&quot;</p>
<h3>Theme</h3>
<p>A descriptive category for game aesthetics. Themes include &quot;ancient-egypt,&quot; &quot;adventure,&quot; &quot;fantasy,&quot; and &quot;sports.&quot;</p>
<h3>Traits</h3>
<p>User attributes that enhance personalization beyond behavior. Examples: VIP tier, preferred language, risk profile.</p>
<h3>Trending Method</h3>
<p>A recommendation method that ranks items by recent popularity momentum. Highlights content gaining traction.</p>
<h3>Type</h3>
<p>A classification level for inventory items. In sports betting, type sits between class and event. Example: Within &quot;Premier League&quot; class, types might be &quot;Matchday 20&quot; or &quot;FA Cup Round 4.&quot;</p>
<hr>
<h2>U</h2>
<h3>User ID</h3>
<p>A known identifier for authenticated users. Links activity across devices and sessions for richer personalization.</p>
<hr>
<h2>V</h2>
<h3>Vertical</h3>
<p>An industry category supported by Opti-X. Verticals include Gaming (iGaming), Sports Betting, and E-commerce.</p>
<h3>Visitor ID</h3>
<p>An anonymous identifier for users who haven&#39;t logged in. Typically a cookie or device ID. Enables personalization for anonymous users.</p>
<h3>Volatility</h3>
<p>A measure of risk and reward frequency in games. High volatility games pay larger amounts less frequently. Low volatility games pay smaller amounts more often.</p>
<hr>
<h2>W</h2>
<h3>Weighting</h3>
<p>The relative importance assigned to different factors in recommendation algorithms. Weighting determines how much user behavior, item popularity, and other signals influence rankings.</p>
<hr>
<h2>X</h2>
<h3>x-api-key</h3>
<p>An HTTP header containing your Opti-X API key. Required for all API requests. Obtained from Admin Panel &gt; Developer Tools &gt; API Keys.</p>
<h3>x-brand-key</h3>
<p>An HTTP header identifying your brand within Opti-X. Required for multi-brand setups. Works alongside x-api-key for authentication.</p>
<hr>
<h2>Related Topics</h2>
<ul>
<li><a href="#key-concepts">Key Concepts</a> - Understand core concepts in depth</li>
<li><a href="#what-is-optix">What is Opti-X?</a> - Product overview</li>
<li><a href="#prerequisites">Prerequisites</a> - Get your API keys</li>
<li><a href="#first-api-call">First API Call</a> - Start using these concepts</li>
</ul>

</section>
<section id="prerequisites" class="doc-section">
<h1>Prerequisites</h1>
<p>Before making your first Opti-X API call, complete this checklist. Setup takes about 15 minutes if you have admin access to your Opti-X account.</p>
<hr>
<h2>Checklist</h2>
<ul>
<li><input disabled="" type="checkbox"> Opti-X account access</li>
<li><input disabled="" type="checkbox"> Admin Panel login credentials</li>
<li><input disabled="" type="checkbox"> API keys obtained (x-api-key and x-brand-key)</li>
<li><input disabled="" type="checkbox"> Test environment identified</li>
<li><input disabled="" type="checkbox"> At least one placement configured</li>
</ul>
<hr>
<h2>Step 1: Opti-X Account Access</h2>
<p>Your organization needs an active Opti-X subscription. If you&#39;re unsure about your account status, contact your Optimove Customer Success Manager.</p>
<p><strong>Verify access</strong>: Navigate to <a href="https://admin.opti-x.optimove.net">admin.opti-x.optimove.net</a> and confirm you can log in.</p>
<hr>
<h2>Step 2: Get Your API Keys</h2>
<p>Opti-X uses two headers for authentication:</p>
<table>
<thead>
<tr>
<th>Header</th>
<th>Purpose</th>
<th>Required</th>
</tr>
</thead>
<tbody><tr>
<td><code>x-api-key</code></td>
<td>Authenticates your API requests</td>
<td>Yes</td>
</tr>
<tr>
<td><code>x-brand-key</code></td>
<td>Identifies your brand (for multi-brand setups)</td>
<td>Depends on setup</td>
</tr>
</tbody></table>
<h3>Finding Your Keys</h3>
<ol>
<li>Log in to the <a href="https://admin.opti-x.optimove.net">Opti-X Admin Panel</a></li>
<li>Navigate to <strong>Developer Tools</strong> in the left sidebar</li>
<li>Click <strong>API Keys</strong></li>
<li>Copy your keys for use in API calls</li>
</ol>
<h3>Key Types</h3>
<p>Opti-X provides different key types for different use cases:</p>
<table>
<thead>
<tr>
<th>Key Type</th>
<th>Use Case</th>
<th>Security Level</th>
</tr>
</thead>
<tbody><tr>
<td><strong>Public</strong></td>
<td>Client-side JavaScript</td>
<td>Lowest - safe for browser exposure</td>
</tr>
<tr>
<td><strong>User</strong></td>
<td>Server-side with user context</td>
<td>Medium - keep server-side</td>
</tr>
<tr>
<td><strong>Service</strong></td>
<td>Server-to-server integration</td>
<td>Highest - never expose to clients</td>
</tr>
</tbody></table>
<p><strong>Choose the right key type:</strong></p>
<ul>
<li><strong>Building a JavaScript widget?</strong> Use a Public key</li>
<li><strong>Building a backend integration?</strong> Use a User or Service key</li>
<li><strong>Running batch jobs?</strong> Use a Service key</li>
</ul>
<h3>Security Best Practices</h3>
<ul>
<li>Never commit API keys to source control</li>
<li>Use environment variables for key storage</li>
<li>Rotate keys periodically</li>
<li>Use the minimum permission level needed</li>
</ul>
<p><strong>Example: Storing keys in environment variables</strong></p>
<pre><code class="language-bash"># Add to your .env file (never commit this file)
OPTIX_API_KEY=your_api_key_here
OPTIX_BRAND_KEY=your_brand_key_here
</code></pre>
<pre><code class="language-javascript">// Access in your code
const apiKey = process.env.OPTIX_API_KEY;
const brandKey = process.env.OPTIX_BRAND_KEY;
</code></pre>
<hr>
<h2>Step 3: Identify Your Environment</h2>
<p>Opti-X provides separate environments for development and production:</p>
<table>
<thead>
<tr>
<th>Environment</th>
<th>Base URL</th>
<th>Purpose</th>
</tr>
</thead>
<tbody><tr>
<td>Production</td>
<td><code>api.opti-x.optimove.net</code></td>
<td>Live traffic</td>
</tr>
<tr>
<td>Staging</td>
<td><code>api.staging.opti-x.optimove.net</code></td>
<td>Testing (if enabled)</td>
</tr>
</tbody></table>
<p><strong>Note</strong>: Not all accounts have staging environments. Contact your Customer Success Manager if you need a staging setup.</p>
<p>For this quickstart, use the production URL with test user IDs to avoid affecting real user data.</p>
<hr>
<h2>Step 4: Verify Placement Configuration</h2>
<p>Placements define where recommendations appear on your platform. Before requesting recommendations, at least one placement must exist.</p>
<h3>Check Existing Placements</h3>
<ol>
<li>In the Admin Panel, navigate to <strong>Placements</strong></li>
<li>Review the list of configured placements</li>
<li>Note the placement ID you&#39;ll use (e.g., <code>homepage-carousel</code>)</li>
</ol>
<h3>If No Placements Exist</h3>
<p>Create a test placement:</p>
<ol>
<li>Click <strong>Create Placement</strong></li>
<li>Enter a name (e.g., &quot;Test Homepage Carousel&quot;)</li>
<li>Set the placement ID (e.g., <code>test-homepage-carousel</code>)</li>
<li>Configure basic settings:<ul>
<li>Method: Personalized</li>
<li>Default item count: 10</li>
</ul>
</li>
<li>Save the placement</li>
</ol>
<p>You can refine placement settings later. For now, a basic configuration is sufficient to test API calls.</p>
<hr>
<h2>Step 5: Understand Your Inventory</h2>
<p>Opti-X recommends items from your inventory. Before integration, confirm:</p>
<ul>
<li><strong>Inventory is loaded</strong>: Check Admin Panel &gt; Inventory to see your items</li>
<li><strong>Items have attributes</strong>: Games should have provider, RTP, category; products should have category, price, brand</li>
<li><strong>Items are active</strong>: Inactive items don&#39;t appear in recommendations</li>
</ul>
<p>If your inventory is empty or incomplete, work with your Customer Success Manager to set up the inventory feed.</p>
<hr>
<h2>Environment Setup Summary</h2>
<p>After completing these steps, you should have:</p>
<pre><code>API Key:      abc123def456ghi789...
Brand Key:    xyz987uvw654rst321... (if applicable)
Base URL:     https://api.opti-x.optimove.net
Placement:    homepage-carousel (or your test placement)
</code></pre>
<hr>
<h2>Quick Connectivity Test</h2>
<p>Verify your setup with this curl command:</p>
<pre><code class="language-bash">curl -X GET &quot;https://api.opti-x.optimove.net/v3/health&quot; \
  -H &quot;x-api-key: YOUR_API_KEY&quot; \
  -H &quot;x-brand-key: YOUR_BRAND_KEY&quot;
</code></pre>
<p><strong>Expected response</strong>:</p>
<pre><code class="language-json">{
  &quot;status&quot;: &quot;healthy&quot;
}
</code></pre>
<p>If you receive an authentication error, double-check your API keys.</p>
<hr>
<h2>What You Need for Each Vertical</h2>
<h3>Gaming Integration</h3>
<ul>
<li><input disabled="" type="checkbox"> Game inventory loaded with IDs, names, providers, categories</li>
<li><input disabled="" type="checkbox"> User ID strategy (how you identify players)</li>
<li><input disabled="" type="checkbox"> Placement for game recommendations</li>
</ul>
<h3>Sports Betting Integration</h3>
<ul>
<li><input disabled="" type="checkbox"> Event inventory with sports, competitions, markets</li>
<li><input disabled="" type="checkbox"> User ID strategy (how you identify bettors)</li>
<li><input disabled="" type="checkbox"> Placement for event/market recommendations</li>
<li><input disabled="" type="checkbox"> Understanding of your live betting requirements</li>
</ul>
<h3>E-commerce Integration</h3>
<ul>
<li><input disabled="" type="checkbox"> Product inventory with IDs, names, categories, prices</li>
<li><input disabled="" type="checkbox"> User ID strategy (customer IDs or anonymous visitors)</li>
<li><input disabled="" type="checkbox"> Placements for product recommendations</li>
</ul>
<hr>
<h2>Common Setup Issues</h2>
<h3>&quot;Invalid API Key&quot; Error</h3>
<ul>
<li>Verify you copied the complete key with no extra spaces</li>
<li>Confirm you&#39;re using the correct key type for your use case</li>
<li>Check that the key hasn&#39;t been rotated or deactivated</li>
</ul>
<h3>&quot;Placement Not Found&quot; Error</h3>
<ul>
<li>Verify the placement ID matches exactly (case-sensitive)</li>
<li>Confirm the placement is active in the Admin Panel</li>
<li>Check that your API key has access to the placement</li>
</ul>
<h3>Empty Recommendations</h3>
<ul>
<li>Verify inventory is loaded and items are active</li>
<li>Confirm the placement&#39;s filters aren&#39;t too restrictive</li>
<li>Check that the method is configured correctly</li>
</ul>
<hr>
<h2>Next Steps</h2>
<p>You&#39;re ready to make your first API call. Continue to:</p>
<ul>
<li><a href="#first-api-call">First API Call</a> - Make a recommendation request in 15 minutes</li>
</ul>
<hr>
<h2>Related Topics</h2>
<ul>
<li><a href="#what-is-optix">What is Opti-X?</a> - Product overview</li>
<li><a href="#key-concepts">Key Concepts</a> - Understand the ABC framework</li>
<li><a href="#glossary">Glossary</a> - Term definitions</li>
</ul>

</section>
<section id="first-api-call" class="doc-section">
<h1>Your First API Call</h1>
<p>This guide walks you through making your first Opti-X recommendation request. By the end, you&#39;ll have working code that fetches personalized recommendations.</p>
<p><strong>Time required</strong>: 15 minutes
<strong>Prerequisites</strong>: <a href="#prerequisites">Setup checklist completed</a></p>
<hr>
<h2>Goal</h2>
<p>Request personalized recommendations from Opti-X and understand the response. We&#39;ll use a simple curl command, then show implementations in JavaScript and Python.</p>
<hr>
<h2>Step 1: Prepare Your Request</h2>
<p>Gather these values from your setup:</p>
<table>
<thead>
<tr>
<th>Value</th>
<th>Example</th>
<th>Where to Find</th>
</tr>
</thead>
<tbody><tr>
<td>API Key</td>
<td><code>pk_live_abc123...</code></td>
<td>Admin Panel &gt; Developer Tools &gt; API Keys</td>
</tr>
<tr>
<td>Brand Key</td>
<td><code>bk_casino_xyz...</code></td>
<td>Admin Panel &gt; Developer Tools &gt; API Keys</td>
</tr>
<tr>
<td>Placement ID</td>
<td><code>homepage-carousel</code></td>
<td>Admin Panel &gt; Placements</td>
</tr>
<tr>
<td>User ID</td>
<td><code>player_12345</code></td>
<td>Your user database</td>
</tr>
</tbody></table>
<hr>
<h2>Step 2: Make the Request</h2>
<h3>Using curl</h3>
<p>Copy this command, replace the placeholder values, and run it in your terminal:</p>
<pre><code class="language-bash">curl -X GET &quot;https://api.opti-x.optimove.net/v3/recommend/placements/homepage-carousel?visitor_id=player_12345&amp;num_items=5&quot; \
  -H &quot;x-api-key: YOUR_API_KEY&quot; \
  -H &quot;x-brand-key: YOUR_BRAND_KEY&quot; \
  -H &quot;Content-Type: application/json&quot;
</code></pre>
<h3>Request Breakdown</h3>
<table>
<thead>
<tr>
<th>Component</th>
<th>Value</th>
<th>Purpose</th>
</tr>
</thead>
<tbody><tr>
<td>Method</td>
<td><code>GET</code></td>
<td>Read operation</td>
</tr>
<tr>
<td>Base URL</td>
<td><code>https://api.opti-x.optimove.net</code></td>
<td>Opti-X API server</td>
</tr>
<tr>
<td>Path</td>
<td><code>/v3/recommend/placements/homepage-carousel</code></td>
<td>Recommendations for specific placement</td>
</tr>
<tr>
<td><code>visitor_id</code></td>
<td><code>player_12345</code></td>
<td>Identifies the user for personalization</td>
</tr>
<tr>
<td><code>num_items</code></td>
<td><code>5</code></td>
<td>Number of recommendations to return</td>
</tr>
<tr>
<td><code>x-api-key</code></td>
<td>Your API key</td>
<td>Authenticates the request</td>
</tr>
<tr>
<td><code>x-brand-key</code></td>
<td>Your brand key</td>
<td>Identifies your brand</td>
</tr>
</tbody></table>
<hr>
<h2>Step 3: Understand the Response</h2>
<p>A successful request returns a JSON response like this:</p>
<pre><code class="language-json">{
  &quot;placement_id&quot;: &quot;homepage-carousel&quot;,
  &quot;visitor_id&quot;: &quot;player_12345&quot;,
  &quot;items&quot;: [
    {
      &quot;item_id&quot;: &quot;starburst-xxxtreme&quot;,
      &quot;rec_id&quot;: &quot;rec_7f8a9b0c1d2e3f4a&quot;,
      &quot;position&quot;: 1,
      &quot;metadata&quot;: {
        &quot;name&quot;: &quot;Starburst XXXtreme&quot;,
        &quot;provider&quot;: &quot;NetEnt&quot;,
        &quot;category&quot;: &quot;slots&quot;
      }
    },
    {
      &quot;item_id&quot;: &quot;book-of-dead&quot;,
      &quot;rec_id&quot;: &quot;rec_8g9b0c1d2e3f4a5b&quot;,
      &quot;position&quot;: 2,
      &quot;metadata&quot;: {
        &quot;name&quot;: &quot;Book of Dead&quot;,
        &quot;provider&quot;: &quot;Play&#39;n GO&quot;,
        &quot;category&quot;: &quot;slots&quot;
      }
    },
    {
      &quot;item_id&quot;: &quot;sweet-bonanza&quot;,
      &quot;rec_id&quot;: &quot;rec_9h0c1d2e3f4a5b6c&quot;,
      &quot;position&quot;: 3,
      &quot;metadata&quot;: {
        &quot;name&quot;: &quot;Sweet Bonanza&quot;,
        &quot;provider&quot;: &quot;Pragmatic Play&quot;,
        &quot;category&quot;: &quot;slots&quot;
      }
    },
    {
      &quot;item_id&quot;: &quot;lightning-roulette&quot;,
      &quot;rec_id&quot;: &quot;rec_0i1d2e3f4a5b6c7d&quot;,
      &quot;position&quot;: 4,
      &quot;metadata&quot;: {
        &quot;name&quot;: &quot;Lightning Roulette&quot;,
        &quot;provider&quot;: &quot;Evolution&quot;,
        &quot;category&quot;: &quot;live-casino&quot;
      }
    },
    {
      &quot;item_id&quot;: &quot;mega-moolah&quot;,
      &quot;rec_id&quot;: &quot;rec_1j2e3f4a5b6c7d8e&quot;,
      &quot;position&quot;: 5,
      &quot;metadata&quot;: {
        &quot;name&quot;: &quot;Mega Moolah&quot;,
        &quot;provider&quot;: &quot;Microgaming&quot;,
        &quot;category&quot;: &quot;slots&quot;
      }
    }
  ],
  &quot;method&quot;: &quot;personalized&quot;,
  &quot;model_version&quot;: &quot;v2.3.1&quot;
}
</code></pre>
<h3>Response Field Reference</h3>
<table>
<thead>
<tr>
<th>Field</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td><code>placement_id</code></td>
<td>The placement that generated these recommendations</td>
</tr>
<tr>
<td><code>visitor_id</code></td>
<td>The user ID from your request</td>
</tr>
<tr>
<td><code>items</code></td>
<td>Array of recommended items, ordered by relevance</td>
</tr>
<tr>
<td><code>items[].item_id</code></td>
<td>Unique identifier for the item in your inventory</td>
</tr>
<tr>
<td><code>items[].rec_id</code></td>
<td>Unique recommendation ID for tracking clicks</td>
</tr>
<tr>
<td><code>items[].position</code></td>
<td>Rank position (1 = most relevant)</td>
</tr>
<tr>
<td><code>items[].metadata</code></td>
<td>Item attributes from your inventory</td>
</tr>
<tr>
<td><code>method</code></td>
<td>Algorithm used (personalized, popular, etc.)</td>
</tr>
<tr>
<td><code>model_version</code></td>
<td>Version of the ML model that generated recommendations</td>
</tr>
</tbody></table>
<h3>Why This Matters</h3>
<ul>
<li><strong>item_id</strong>: Use this to fetch additional item details from your database or display the item</li>
<li><strong>rec_id</strong>: Send this back when users click items (enables recommendation analytics)</li>
<li><strong>position</strong>: Helps you verify items are displayed in the correct order</li>
<li><strong>metadata</strong>: Contains item details you can display directly without additional lookups</li>
</ul>
<hr>
<h2>Step 4: Display Recommendations</h2>
<p>Use the response to render recommendations in your UI. Here&#39;s a simple example:</p>
<h3>JavaScript Example</h3>
<pre><code class="language-javascript">async function getRecommendations(userId, numItems = 10) {
  const baseUrl = &#39;https://api.opti-x.optimove.net&#39;;
  const placementId = &#39;homepage-carousel&#39;;

  const url = `${baseUrl}/v3/recommend/placements/${placementId}?visitor_id=${userId}&amp;num_items=${numItems}`;

  const response = await fetch(url, {
    method: &#39;GET&#39;,
    headers: {
      &#39;x-api-key&#39;: process.env.OPTIX_API_KEY,
      &#39;x-brand-key&#39;: process.env.OPTIX_BRAND_KEY,
      &#39;Content-Type&#39;: &#39;application/json&#39;
    }
  });

  if (!response.ok) {
    throw new Error(`API error: ${response.status}`);
  }

  return response.json();
}

// Usage
const recommendations = await getRecommendations(&#39;player_12345&#39;, 5);

// Render recommendations
recommendations.items.forEach(item =&gt; {
  console.log(`${item.position}. ${item.metadata.name} (${item.item_id})`);
});
</code></pre>
<h3>Python Example</h3>
<pre><code class="language-python">import os
import requests

def get_recommendations(user_id: str, num_items: int = 10) -&gt; dict:
    base_url = &#39;https://api.opti-x.optimove.net&#39;
    placement_id = &#39;homepage-carousel&#39;

    url = f&#39;{base_url}/v3/recommend/placements/{placement_id}&#39;

    headers = {
        &#39;x-api-key&#39;: os.environ[&#39;OPTIX_API_KEY&#39;],
        &#39;x-brand-key&#39;: os.environ[&#39;OPTIX_BRAND_KEY&#39;],
        &#39;Content-Type&#39;: &#39;application/json&#39;
    }

    params = {
        &#39;visitor_id&#39;: user_id,
        &#39;num_items&#39;: num_items
    }

    response = requests.get(url, headers=headers, params=params)
    response.raise_for_status()

    return response.json()

# Usage
recommendations = get_recommendations(&#39;player_12345&#39;, 5)

# Display recommendations
for item in recommendations[&#39;items&#39;]:
    print(f&quot;{item[&#39;position&#39;]}. {item[&#39;metadata&#39;][&#39;name&#39;]} ({item[&#39;item_id&#39;]})&quot;)
</code></pre>
<hr>
<h2>Step 5: Track Clicks (Important!)</h2>
<p>When a user clicks a recommendation, send the <code>rec_id</code> back to Opti-X. This feedback improves future recommendations.</p>
<pre><code class="language-javascript">async function trackRecommendationClick(userId, recId, itemId) {
  const baseUrl = &#39;https://api.opti-x.optimove.net&#39;;

  await fetch(`${baseUrl}/v3/activity`, {
    method: &#39;POST&#39;,
    headers: {
      &#39;x-api-key&#39;: process.env.OPTIX_API_KEY,
      &#39;x-brand-key&#39;: process.env.OPTIX_BRAND_KEY,
      &#39;Content-Type&#39;: &#39;application/json&#39;
    },
    body: JSON.stringify({
      event_type: &#39;recommendation_click&#39;,
      visitor_id: userId,
      rec_id: recId,
      item_id: itemId,
      timestamp: new Date().toISOString()
    })
  });
}

// When user clicks a recommendation
trackRecommendationClick(&#39;player_12345&#39;, &#39;rec_7f8a9b0c1d2e3f4a&#39;, &#39;starburst-xxxtreme&#39;);
</code></pre>
<hr>
<h2>Common Parameters</h2>
<p>Customize your request with these parameters:</p>
<table>
<thead>
<tr>
<th>Parameter</th>
<th>Type</th>
<th>Description</th>
<th>Example</th>
</tr>
</thead>
<tbody><tr>
<td><code>visitor_id</code></td>
<td>string</td>
<td>Anonymous user identifier</td>
<td><code>anon_abc123</code></td>
</tr>
<tr>
<td><code>user_id</code></td>
<td>string</td>
<td>Authenticated user identifier</td>
<td><code>player_12345</code></td>
</tr>
<tr>
<td><code>num_items</code></td>
<td>integer</td>
<td>Number of items to return (1-100)</td>
<td><code>10</code></td>
</tr>
<tr>
<td><code>context_id</code></td>
<td>string</td>
<td>Item ID for &quot;similar items&quot; recommendations</td>
<td><code>book-of-dead</code></td>
</tr>
<tr>
<td><code>regulation</code></td>
<td>string</td>
<td>Jurisdiction for compliance filtering</td>
<td><code>uk</code></td>
</tr>
<tr>
<td><code>skin_id</code></td>
<td>string</td>
<td>Brand variant identifier</td>
<td><code>casino-a</code></td>
</tr>
</tbody></table>
<h3>Example with More Parameters</h3>
<pre><code class="language-bash">curl -X GET &quot;https://api.opti-x.optimove.net/v3/recommend/placements/homepage-carousel\
?visitor_id=anon_abc123\
&amp;user_id=player_12345\
&amp;num_items=10\
&amp;regulation=uk\
&amp;skin_id=casino-main&quot; \
  -H &quot;x-api-key: YOUR_API_KEY&quot; \
  -H &quot;x-brand-key: YOUR_BRAND_KEY&quot;
</code></pre>
<hr>
<h2>Error Handling</h2>
<p>Handle these common error responses:</p>
<table>
<thead>
<tr>
<th>Status</th>
<th>Meaning</th>
<th>Solution</th>
</tr>
</thead>
<tbody><tr>
<td><code>401</code></td>
<td>Invalid API key</td>
<td>Check your x-api-key header</td>
</tr>
<tr>
<td><code>403</code></td>
<td>Forbidden</td>
<td>Verify your API key has access to this placement</td>
</tr>
<tr>
<td><code>404</code></td>
<td>Placement not found</td>
<td>Check the placement ID exists</td>
</tr>
<tr>
<td><code>429</code></td>
<td>Rate limited</td>
<td>Reduce request frequency</td>
</tr>
<tr>
<td><code>500</code></td>
<td>Server error</td>
<td>Retry with exponential backoff</td>
</tr>
</tbody></table>
<h3>JavaScript Error Handling</h3>
<pre><code class="language-javascript">async function getRecommendationsWithRetry(userId, numItems, maxRetries = 3) {
  for (let attempt = 1; attempt &lt;= maxRetries; attempt++) {
    try {
      const response = await fetch(url, options);

      if (response.status === 429) {
        // Rate limited - wait and retry
        await sleep(1000 * attempt);
        continue;
      }

      if (!response.ok) {
        throw new Error(`API error: ${response.status}`);
      }

      return response.json();

    } catch (error) {
      if (attempt === maxRetries) throw error;
      await sleep(1000 * attempt);
    }
  }
}
</code></pre>
<hr>
<h2>What&#39;s Next?</h2>
<p>You&#39;ve made your first API call. Here&#39;s where to go based on your vertical:</p>
<h3>Gaming (iGaming)</h3>
<ol>
<li><a href="#gaming-events">Send Game Launch Events</a> - Track player activity</li>
<li><a href="#recommend-api">Configure Gaming Placements</a> - Optimize for casino</li>
<li><a href="#filtering-overview">Filter by Provider/Category</a> - Apply business rules</li>
</ol>
<h3>Sports Betting</h3>
<ol>
<li><a href="#sports-events">Send Bet Placement Events</a> - Track betting activity</li>
<li><a href="#recommend-api">Configure Sports Placements</a> - Optimize for betting</li>
<li><a href="#recommend-api">Handle Live Events</a> - Real-time updates</li>
</ol>
<h3>E-commerce</h3>
<ol>
<li><a href="#ecommerce-events">Send Purchase Events</a> - Track shopping activity</li>
<li><a href="#recommend-api">Configure Product Placements</a> - Optimize for shopping</li>
<li><a href="#recommend-api">Implement Cross-sell</a> - Increase basket size</li>
</ol>
<hr>
<h2>Quick Reference</h2>
<p><strong>Endpoint</strong>: <code>GET /v3/recommend/placements/{placement_id}</code></p>
<p><strong>Required Headers</strong>:</p>
<pre><code>x-api-key: YOUR_API_KEY
x-brand-key: YOUR_BRAND_KEY
Content-Type: application/json
</code></pre>
<p><strong>Required Parameters</strong>:</p>
<pre><code>visitor_id OR user_id
</code></pre>
<p><strong>Base URL</strong>: <code>https://api.opti-x.optimove.net</code></p>
<hr>
<h2>Related Topics</h2>
<ul>
<li><a href="#prerequisites">Prerequisites</a> - Setup checklist</li>
<li><a href="#key-concepts">Key Concepts</a> - Understand the ABC framework</li>
<li><a href="#recommend-api">Placements</a> - Configure recommendation locations</li>
<li><a href="#inventory-overview">Activity Tracking</a> - Send user events</li>
</ul>

</section>
<section id="inventory-overview" class="doc-section">
<h1>Inventory Overview</h1>
<p>Inventory is the foundation of personalized recommendations in Opti-X. Your inventory defines what items, games, events, or products you can recommend to users.</p>
<h2>What is Inventory?</h2>
<p>Inventory represents your catalog of recommendable items. It includes:</p>
<ul>
<li><strong>Item metadata</strong> - Names, descriptions, categories, and attributes</li>
<li><strong>Availability rules</strong> - Which users can see which items based on location, currency, or other traits</li>
<li><strong>Display settings</strong> - Images, URLs, and presentation data for rendering recommendations</li>
</ul>
<p>Without inventory data, Opti-X cannot generate recommendations. The quality and completeness of your inventory directly impacts recommendation relevance.</p>
<h2>Why Inventory Matters for Personalization</h2>
<p>Opti-X uses inventory data to:</p>
<ol>
<li><strong>Match users to relevant items</strong> - Algorithms analyze item attributes and user behavior to find the best matches</li>
<li><strong>Filter by eligibility</strong> - Availability rules ensure users only see items they can access</li>
<li><strong>Render recommendations</strong> - Metadata like images and descriptions power Smart Content and placement responses</li>
<li><strong>Train models</strong> - Rich item attributes improve machine learning model accuracy over time</li>
</ol>
<h2>Inventory Types</h2>
<p>Opti-X supports three inventory types, each designed for specific use cases:</p>
<h3>Gaming Inventory</h3>
<p>For online casinos, game aggregators, and gaming platforms.</p>
<ul>
<li>Tracks games with attributes like RTP (Return to Player), themes, and suppliers</li>
<li>Supports platform targeting (desktop, mobile, tablet)</li>
<li>Includes regulatory compliance fields (UKGC, MGA licenses)</li>
</ul>
<p><strong>Best for:</strong> Slot games, table games, live casino, lottery, and bingo</p>
<h3>Sports Inventory</h3>
<p>For sportsbooks and betting platforms.</p>
<ul>
<li>Hierarchical structure: Category &gt; Class &gt; Type &gt; Event &gt; Market &gt; Selection</li>
<li>Real-time updates for odds and event status</li>
<li>Supports pre-match and in-play betting scenarios</li>
</ul>
<p><strong>Best for:</strong> Sports betting, horse racing, esports</p>
<h3>E-commerce Inventory</h3>
<p>For retail, marketplaces, and subscription services.</p>
<ul>
<li>Product hierarchy: Product &gt; Variant &gt; SKU</li>
<li>Supports pricing, stock levels, and category taxonomies</li>
<li>Includes fields for promotions and new arrivals</li>
</ul>
<p><strong>Best for:</strong> Online retail, fashion, electronics, groceries</p>
<h2>How Inventory Connects to Recommendations</h2>
<pre><code>Inventory Data --&gt; Opti-X Processing --&gt; Recommendation API --&gt; Your Application
     |                    |                     |
     |                    |                     |
  Catalog of         Filtering,            Personalized
  all items          ranking,              item list for
                     ML models             each user
</code></pre>
<ol>
<li><strong>You send inventory</strong> - Upload your catalog via API or batch file</li>
<li><strong>Opti-X processes it</strong> - Items are indexed, validated, and made available for recommendations</li>
<li><strong>Users request recommendations</strong> - Your application calls the Recommendation API with user context</li>
<li><strong>Opti-X returns personalized items</strong> - Algorithms select and rank the best items for that user</li>
</ol>
<h2>Data Freshness Requirements</h2>
<p>Keep your inventory synchronized with your source systems:</p>
<table>
<thead>
<tr>
<th>Inventory Type</th>
<th>Recommended Update Frequency</th>
<th>Why It Matters</th>
</tr>
</thead>
<tbody><tr>
<td>Gaming</td>
<td>Daily</td>
<td>Game availability and new releases change regularly</td>
</tr>
<tr>
<td>Sports</td>
<td>Real-time (seconds)</td>
<td>Odds and event status change constantly during live events</td>
</tr>
<tr>
<td>E-commerce</td>
<td>Hourly to daily</td>
<td>Stock levels and pricing affect user experience</td>
</tr>
</tbody></table>
<p><strong>Stale inventory leads to poor experiences.</strong> If Opti-X recommends an out-of-stock product or a game that is no longer available, users lose trust in your recommendations.</p>
<h2>Getting Started</h2>
<p>Choose the inventory type that matches your business:</p>
<ol>
<li>Review the field requirements for your inventory type</li>
<li>Map your existing data to the Opti-X schema</li>
<li>Implement the appropriate API integration</li>
<li>Set up automated updates to keep data fresh</li>
</ol>
<hr>
<h2>Related Topics</h2>
<ul>
<li><a href="#gaming-inventory">Gaming Inventory</a> - Field reference and setup for gaming platforms</li>
<li><a href="#sports-inventory">Sports Inventory</a> - Hierarchical structure and API for sportsbooks</li>
<li><a href="#ecommerce-inventory">E-commerce Inventory</a> - Product catalog setup for retail</li>
<li><a href="#availability-filters">Availability Filters</a> - Control which users see which items</li>
<li><a href="#lottery-bingo">Lottery and Bingo</a> - Special considerations for lottery and bingo games</li>
</ul>

</section>
<section id="gaming-inventory" class="doc-section">
<h1>Gaming Inventory</h1>
<p>This document details the data formats for preparing your Gaming Inventory for Opti-X.</p>
<h2>Overview</h2>
<p>Gaming Inventory provides a daily snapshot of available games and their associated metadata. Opti-X uses this data to power personalized game recommendations across your platform.</p>
<h3>Why This Matters</h3>
<p>Your gaming inventory is the foundation of game recommendations. Complete and accurate inventory data enables Opti-X to:</p>
<ul>
<li>Match players with games they are likely to enjoy</li>
<li>Filter games by platform, regulation, and player eligibility</li>
<li>Display rich game information in recommendations</li>
<li>Train models that improve over time</li>
</ul>
<h2>Example Inventory Record</h2>
<pre><code class="language-json">{
  &quot;game_code&quot;: &quot;123456&quot;,
  &quot;game_name&quot;: &quot;Adventure Quest&quot;,
  &quot;game_category&quot;: &quot;Slots&quot;,
  &quot;game_class&quot;: &quot;premium&quot;,
  &quot;game_type&quot;: &quot;3D&quot;,
  &quot;description&quot;: &quot;A thrilling adventure game with a progressive jackpot.&quot;,
  &quot;desktop&quot;: 1,
  &quot;mobile&quot;: 0,
  &quot;tablet&quot;: 1,
  &quot;extra_channels&quot;: &quot;iOS16|iOS17&quot;,
  &quot;rtp&quot;: 0.95,
  &quot;themes&quot;: [&quot;Adventure&quot;],
  &quot;launch_date&quot;: &quot;2023-05-17&quot;,
  &quot;new&quot;: true,
  &quot;supplier&quot;: &quot;Supplier Inc.&quot;,
  &quot;default_order&quot;: 1,
  &quot;jackpot_type&quot;: &quot;progressive&quot;,
  &quot;formatted_summary&quot;: &quot;Adventure Quest is a thrilling...&quot;,
  &quot;formatted_summary_short&quot;: &quot;Thrilling adventure game...&quot;,
  &quot;image_url&quot;: &quot;https://game.example.com/image.jpg&quot;,
  &quot;game_features&quot;: [{&quot;feature1&quot;: &quot;feature_details&quot;}],
  &quot;tags&quot;: [{&quot;tag1&quot;: &quot;value1&quot;}, {&quot;tag2&quot;: &quot;value2&quot;}],
  &quot;skin_id&quot;: [&quot;21&quot;, &quot;23&quot;],
  &quot;regulation&quot;: [&quot;UKGC&quot;, &quot;MGA&quot;],
  &quot;inclusions&quot;: {&quot;country&quot;: [&quot;UK&quot;, &quot;DE&quot;]},
  &quot;exclusions&quot;: {&quot;currency&quot;: &quot;USD&quot;},
  &quot;extra&quot;: {&quot;key1&quot;: &quot;value1&quot;, &quot;key2&quot;: &quot;value2&quot;}
}
</code></pre>
<h2>Sending Inventory Data</h2>
<p>Exchange inventory data with Opti-X through the Gaming Inventory API.</p>
<blockquote>
<p><strong>Smart Content Requirement</strong></p>
<p>If you plan to use Smart Content, include a full, absolute (HTTPS) <code>image_url</code> for each game in your Gaming Inventory. Without <code>image_url</code>, Smart Content placements cannot render the game&#39;s image and may show blank or fallback content.</p>
</blockquote>
<h2>Field Reference</h2>
<h3>Understanding the Columns</h3>
<ul>
<li><p><strong>Automatic Tag Creation</strong>: When marked with a checkmark, Opti-X automatically creates searchable tags from this field&#39;s values. Tags enable filtering and grouping in recommendations. For example, if you set <code>game_category</code> to &quot;Slots&quot;, Opti-X creates a &quot;Slots&quot; tag that you can use to filter recommendations.</p>
</li>
<li><p><strong>Availability Filters</strong>: When marked with a checkmark, this field can be used to control which users see this game based on their attributes (location, currency, skin). See <a href="#availability-filters">Availability Filters</a> for details.</p>
</li>
</ul>
<table>
<thead>
<tr>
<th>Field Name</th>
<th>Required</th>
<th>Data Type</th>
<th>Example Value</th>
<th>Description</th>
<th align="center">Automatic Tag Creation</th>
<th align="center">Availability Filters</th>
</tr>
</thead>
<tbody><tr>
<td>game_code</td>
<td>Yes</td>
<td>string</td>
<td><code>2345994</code></td>
<td>Unique identifier for the game. Can be game code, game ID, or any unique identifier.</td>
<td align="center">Yes</td>
<td align="center"></td>
</tr>
<tr>
<td>game_name</td>
<td>No</td>
<td>string</td>
<td><code>Adventure Quest</code></td>
<td>Display name of the game</td>
<td align="center">Yes</td>
<td align="center"></td>
</tr>
<tr>
<td>game_category</td>
<td>No</td>
<td>string</td>
<td><code>Slots</code></td>
<td>Category the game belongs to (e.g., Slots, Table Games, Live Casino)</td>
<td align="center">Yes</td>
<td align="center"></td>
</tr>
<tr>
<td>game_class</td>
<td>No</td>
<td>string</td>
<td><code>Premium</code></td>
<td>Classification tier of the game</td>
<td align="center">Yes</td>
<td align="center"></td>
</tr>
<tr>
<td>game_type</td>
<td>No</td>
<td>string</td>
<td><code>3D</code></td>
<td>Type or style of the game</td>
<td align="center"></td>
<td align="center"></td>
</tr>
<tr>
<td>description</td>
<td>No</td>
<td>string</td>
<td><code>A thrilling adventure game with a progressive jackpot</code></td>
<td>Short explanation of what the game is</td>
<td align="center"></td>
<td align="center"></td>
</tr>
<tr>
<td>desktop</td>
<td>No</td>
<td>integer</td>
<td><code>1</code></td>
<td>Whether the game is available on desktop. Use <code>1</code> for true, <code>0</code> for false. At least one platform should be <code>1</code>.</td>
<td align="center"></td>
<td align="center"></td>
</tr>
<tr>
<td>mobile</td>
<td>No</td>
<td>integer</td>
<td><code>0</code></td>
<td>Whether the game is available on mobile. Use <code>1</code> for true, <code>0</code> for false.</td>
<td align="center"></td>
<td align="center"></td>
</tr>
<tr>
<td>tablet</td>
<td>No</td>
<td>integer</td>
<td><code>0</code></td>
<td>Whether the game is available on tablet. Use <code>1</code> for true, <code>0</code> for false.</td>
<td align="center"></td>
<td align="center"></td>
</tr>
<tr>
<td>extra_channels</td>
<td>No</td>
<td>string</td>
<td><code>iOS16|iOS17</code></td>
<td>Custom channels, separated by pipe symbol (<code>|</code>)</td>
<td align="center"></td>
<td align="center"></td>
</tr>
<tr>
<td>rtp</td>
<td>No</td>
<td>float</td>
<td><code>0.95</code></td>
<td>Return to Player percentage expressed as a decimal. Example: <code>0.95</code> means 95% RTP (the casino&#39;s expected profit is 5%).</td>
<td align="center">Yes</td>
<td align="center"></td>
</tr>
<tr>
<td>themes</td>
<td>No</td>
<td>list of strings</td>
<td><code>[&quot;Adventure&quot;]</code></td>
<td>Theme tags for the game</td>
<td align="center">Yes</td>
<td align="center"></td>
</tr>
<tr>
<td>launch_date</td>
<td>No</td>
<td>string</td>
<td><code>2023-05-17</code></td>
<td>Date the game became available. Use ISO 8601 format (YYYY-MM-DD).</td>
<td align="center"></td>
<td align="center"></td>
</tr>
<tr>
<td>new</td>
<td>No</td>
<td>boolean</td>
<td><code>true</code></td>
<td>Whether the game is marked as new</td>
<td align="center"></td>
<td align="center"></td>
</tr>
<tr>
<td>supplier</td>
<td>No</td>
<td>string</td>
<td><code>Supplier Inc.</code></td>
<td>Game supplier or provider name</td>
<td align="center">Yes</td>
<td align="center"></td>
</tr>
<tr>
<td>default_order</td>
<td>No</td>
<td>integer</td>
<td><code>50</code></td>
<td>Display order when using manual sorting. Lower values appear first.</td>
<td align="center"></td>
<td align="center"></td>
</tr>
<tr>
<td>jackpot_type</td>
<td>No</td>
<td>string</td>
<td><code>progressive</code></td>
<td>Type of jackpot (e.g., progressive, fixed, none)</td>
<td align="center"></td>
<td align="center"></td>
</tr>
<tr>
<td>formatted_summary</td>
<td>No</td>
<td>string</td>
<td><code>Adventure Quest is a thrilling....</code></td>
<td>Full formatted description for display</td>
<td align="center"></td>
<td align="center"></td>
</tr>
<tr>
<td>formatted_summary_short</td>
<td>No</td>
<td>string</td>
<td><code>Thrilling adventure game</code></td>
<td>Short summary for compact displays</td>
<td align="center"></td>
<td align="center"></td>
</tr>
<tr>
<td>image_url</td>
<td>Conditional</td>
<td>string</td>
<td><code>https://image.game.com/adventure.jpg</code></td>
<td>Game image URL. <strong>Required if using Smart Content.</strong> Must be an absolute HTTPS URL accessible by Optimove services.</td>
<td align="center"></td>
<td align="center"></td>
</tr>
<tr>
<td>game_features</td>
<td>No</td>
<td>list of objects</td>
<td><code>[{&quot;feature1&quot;: &quot;feature_details&quot;}]</code></td>
<td>Additional game features as key-value pairs</td>
<td align="center">Yes</td>
<td align="center"></td>
</tr>
<tr>
<td>tags</td>
<td>No</td>
<td>list of objects</td>
<td><code>[{&quot;tag1&quot;: &quot;value1&quot;}]</code></td>
<td>Custom tags for filtering and categorization</td>
<td align="center">Yes</td>
<td align="center"></td>
</tr>
<tr>
<td>skin_id</td>
<td>No</td>
<td>list of strings</td>
<td><code>[&quot;21&quot;, &quot;23&quot;]</code></td>
<td>List of skin IDs where this game is available</td>
<td align="center"></td>
<td align="center">Yes</td>
</tr>
<tr>
<td>regulation</td>
<td>No</td>
<td>list of strings</td>
<td><code>[&quot;UKGC&quot;, &quot;MGA&quot;]</code></td>
<td>Regulatory jurisdictions where the game is licensed</td>
<td align="center"></td>
<td align="center">Yes</td>
</tr>
<tr>
<td>inclusions</td>
<td>No</td>
<td>object</td>
<td><code>{&quot;country&quot;: [&quot;UK&quot;, &quot;DE&quot;]}</code></td>
<td>Availability filter inclusions (IN operator)</td>
<td align="center"></td>
<td align="center">Yes</td>
</tr>
<tr>
<td>exclusions</td>
<td>No</td>
<td>object</td>
<td><code>{&quot;currency&quot;: &quot;USD&quot;}</code></td>
<td>Availability filter exclusions (NOT IN operator)</td>
<td align="center"></td>
<td align="center">Yes</td>
</tr>
<tr>
<td>extra</td>
<td>No</td>
<td>object</td>
<td><code>{&quot;key_1&quot;: &quot;value_1&quot;}</code></td>
<td>Additional data returned in recommendations but not used for personalization</td>
<td align="center"></td>
<td align="center"></td>
</tr>
</tbody></table>
<h3>Why Each Section Matters</h3>
<p><strong>Identification Fields</strong> (<code>game_code</code>, <code>game_name</code>)
These fields identify and display the game. Without a unique <code>game_code</code>, Opti-X cannot track the game or its performance.</p>
<p><strong>Platform Fields</strong> (<code>desktop</code>, <code>mobile</code>, <code>tablet</code>, <code>extra_channels</code>)
Platform data ensures users only see games compatible with their device. Recommending a desktop-only game to a mobile user creates a poor experience.</p>
<p><strong>Categorization Fields</strong> (<code>game_category</code>, <code>game_class</code>, <code>game_type</code>, <code>themes</code>)
Categories power filtering rules and help the recommendation engine understand game similarities. Well-categorized inventory improves recommendation quality.</p>
<p><strong>Availability Fields</strong> (<code>skin_id</code>, <code>regulation</code>, <code>inclusions</code>, <code>exclusions</code>)
These fields control which users can see each game based on their attributes. Proper availability configuration prevents compliance issues and ensures users only see relevant games.</p>
<h2>Date Format</h2>
<p>Use ISO 8601 format for all date fields:</p>
<ul>
<li><strong>Format</strong>: <code>YYYY-MM-DD</code></li>
<li><strong>Example</strong>: <code>2023-05-17</code></li>
</ul>
<p>This ensures consistent parsing across all systems.</p>
<hr>
<h2>Related Topics</h2>
<ul>
<li><a href="#availability-filters">Availability Filters</a> - Configure which users see which games</li>
<li><a href="#lottery-bingo">Lottery and Bingo</a> - Special considerations for lottery and bingo games</li>
<li><a href="#inventory-overview">Inventory Overview</a> - Introduction to inventory concepts</li>
</ul>

</section>
<section id="sports-inventory" class="doc-section">
<h1>Sports Inventory</h1>
<p>Opti-X uses sports inventory data to provide personalized betting recommendations to your users. The Sports Inventory API ensures Opti-X always has the most up-to-date information for your sportsbook.</p>
<h2>Overview</h2>
<p>Sports inventory follows a hierarchical structure that mirrors how sportsbooks organize betting options. Understanding this hierarchy is essential for successful integration.</p>
<h3>Why This Matters</h3>
<p>Sports data changes rapidly. Events start and finish, odds shift constantly, and markets open and close throughout the day. Your inventory integration must handle real-time updates to ensure users see accurate, actionable recommendations.</p>
<h2>Inventory Hierarchy</h2>
<p>Sports inventory organizes data in six levels, from broadest to most specific:</p>
<pre><code>Category (Football)
    |
    +-- Class (England)
           |
           +-- Type (Premier League)
                  |
                  +-- Event (Arsenal vs Chelsea, 2024-03-15)
                         |
                         +-- Market (Match Winner)
                                |
                                +-- Selection (Arsenal to Win, Odds: 2.10)
</code></pre>
<h3>Category</h3>
<p>The top-level sports category in your inventory.</p>
<p><strong>Examples:</strong> Football, Tennis, Golf, Basketball, Horse Racing</p>
<p><strong>Why it matters:</strong> Categories group all related betting activity. Users who bet on Football events likely want Football recommendations.</p>
<h3>Class</h3>
<p>A subclass of the sports category, typically used to group by country or region.</p>
<p><strong>Examples:</strong> England, Spain, USA, Australia</p>
<p><strong>Why it matters:</strong> Classes help target recommendations geographically. A user betting on English football probably prefers English leagues over Spanish ones.</p>
<blockquote>
<p><strong>Note:</strong> If Class is not relevant to your sportsbook, you can set it equal to Category to create a 1:1 relationship.</p>
</blockquote>
<h3>Type</h3>
<p>The competition, league, or championship that events belong to.</p>
<p><strong>Examples:</strong> Premier League, La Liga, NBA Finals, Wimbledon</p>
<p><strong>Why it matters:</strong> Types represent the competitions users follow. Fans often bet consistently on specific leagues.</p>
<h3>Event</h3>
<p>A specific sporting event occurring at a defined date and time.</p>
<p><strong>Examples:</strong> Arsenal vs Chelsea (March 15, 2024), Nadal vs Djokovic (June 10, 2024)</p>
<p><strong>Why it matters:</strong> Events are the primary unit users bet on. Each event has multiple markets and selections.</p>
<h3>Market</h3>
<p>The outcome type that users can bet on within an event.</p>
<p><strong>Examples:</strong> Match Winner, First Goalscorer, Total Goals Over/Under, Correct Score</p>
<p><strong>Why it matters:</strong> Markets define what users are betting on. Some users prefer simple markets (Match Winner) while others seek value in complex markets (Correct Score).</p>
<h3>Selection</h3>
<p>The specific option within a market that users place bets on.</p>
<p><strong>Examples:</strong> Arsenal to Win (2.10), Draw (3.50), Chelsea to Win (3.20)</p>
<p><strong>Why it matters:</strong> Selections are what users actually bet on. Each selection has odds that determine the potential payout.</p>
<h2>Getting Started</h2>
<h3>Prerequisites</h3>
<p>You need API credentials from the Opti-X Developer Tools at <code>opti-x.optimove.net</code>:</p>
<ul>
<li><code>x-brand-key</code> - Identifies your brand</li>
<li><code>x-api-key</code> - Authenticates API requests</li>
</ul>
<h3>Base URL</h3>
<pre><code>https://api.opti-x.optimove.net/sports-inventory/v1/records
</code></pre>
<h3>Rate Limits</h3>
<p>The API allows <strong>50 requests per 10 seconds</strong>. If you exceed this limit, requests will be rejected until the rate window resets.</p>
<p><strong>Handling rate limits:</strong></p>
<ul>
<li>Batch multiple records into single requests (up to 500 records per request)</li>
<li>Implement exponential backoff when you receive rate limit errors</li>
<li>Spread updates across time rather than sending bursts</li>
</ul>
<h2>API Methods</h2>
<p>The Records API supports three operations for managing inventory data.</p>
<table>
<thead>
<tr>
<th>Method</th>
<th>Purpose</th>
<th>When to Use</th>
</tr>
</thead>
<tbody><tr>
<td><code>POST</code></td>
<td>Create new records</td>
<td>Adding new events, markets, or selections</td>
</tr>
<tr>
<td><code>PUT</code></td>
<td>Update existing records</td>
<td>Changing odds, status, or display settings</td>
</tr>
<tr>
<td><code>DELETE</code></td>
<td>Remove records</td>
<td>Removing cancelled events or settled markets</td>
</tr>
</tbody></table>
<h3>Request Headers</h3>
<p>All requests require these headers:</p>
<table>
<thead>
<tr>
<th>Header</th>
<th>Type</th>
<th align="center">Required</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>x-api-key</td>
<td>string</td>
<td align="center">Yes</td>
<td>Your API authentication key</td>
</tr>
<tr>
<td>x-brand-key</td>
<td>string</td>
<td align="center">Yes</td>
<td>Your brand identifier</td>
</tr>
<tr>
<td>Content-Type</td>
<td>string</td>
<td align="center">Yes</td>
<td>Must be <code>application/json</code></td>
</tr>
<tr>
<td>Accept</td>
<td>string</td>
<td align="center">Yes</td>
<td>Must be <code>application/json</code></td>
</tr>
</tbody></table>
<h3>Record Ordering</h3>
<p>Each request can contain up to <strong>500 records</strong>. Records must be ordered so that parent entities appear before their children.</p>
<p><strong>Correct order:</strong></p>
<ol>
<li>Category</li>
<li>Class</li>
<li>Type</li>
<li>Event</li>
<li>Market</li>
<li>Selection</li>
</ol>
<p><strong>Example:</strong> When creating a new event with markets and selections, include the Event record before any Market records, and Market records before their Selection records.</p>
<h2>POST: Create Records</h2>
<p>Create new inventory records.</p>
<h3>Endpoint</h3>
<pre><code>POST https://api.opti-x.optimove.net/sports-inventory/v1/records
</code></pre>
<h3>Example Request</h3>
<pre><code class="language-bash">curl --request POST \
  --url https://api.opti-x.optimove.net/sports-inventory/v1/records \
  --header &#39;accept: application/json&#39; \
  --header &#39;content-type: application/json&#39; \
  --header &#39;x-api-key: your-api-key&#39; \
  --header &#39;x-brand-key: your-brand-key&#39; \
  --data &#39;[
    {
      &quot;categoryKey&quot;: &quot;football&quot;,
      &quot;categoryName&quot;: &quot;Football&quot;,
      &quot;displayStatus&quot;: &quot;Displayed&quot;,
      &quot;displayOrder&quot;: 1
    },
    {
      &quot;classKey&quot;: &quot;england&quot;,
      &quot;categoryKey&quot;: &quot;football&quot;,
      &quot;className&quot;: &quot;England&quot;,
      &quot;displayStatus&quot;: &quot;Displayed&quot;
    },
    {
      &quot;typeKey&quot;: &quot;premier-league&quot;,
      &quot;categoryKey&quot;: &quot;football&quot;,
      &quot;classKey&quot;: &quot;england&quot;,
      &quot;typeName&quot;: &quot;Premier League&quot;,
      &quot;displayStatus&quot;: &quot;Displayed&quot;
    },
    {
      &quot;eventKey&quot;: &quot;ars-che-20240315&quot;,
      &quot;categoryKey&quot;: &quot;football&quot;,
      &quot;classKey&quot;: &quot;england&quot;,
      &quot;typeKey&quot;: &quot;premier-league&quot;,
      &quot;eventName&quot;: &quot;Arsenal vs Chelsea&quot;,
      &quot;eventDateTime&quot;: &quot;2024-03-15T15:00:00Z&quot;,
      &quot;homeName&quot;: &quot;Arsenal&quot;,
      &quot;awayName&quot;: &quot;Chelsea&quot;,
      &quot;displayStatus&quot;: &quot;Displayed&quot;
    }
  ]&#39;
</code></pre>
<h2>PUT: Update Records</h2>
<p>Update existing inventory records. Only include fields that have changed.</p>
<h3>Endpoint</h3>
<pre><code>PUT https://api.opti-x.optimove.net/sports-inventory/v1/records
</code></pre>
<h3>Example Request</h3>
<pre><code class="language-bash">curl --request PUT \
  --url https://api.opti-x.optimove.net/sports-inventory/v1/records \
  --header &#39;accept: application/json&#39; \
  --header &#39;content-type: application/json&#39; \
  --header &#39;x-api-key: your-api-key&#39; \
  --header &#39;x-brand-key: your-brand-key&#39; \
  --data &#39;[
    {
      &quot;selectionKey&quot;: &quot;ars-win-001&quot;,
      &quot;eventKey&quot;: &quot;ars-che-20240315&quot;,
      &quot;decPrice&quot;: 2.15,
      &quot;displayStatus&quot;: &quot;Displayed&quot;
    },
    {
      &quot;eventKey&quot;: &quot;ars-che-20240315&quot;,
      &quot;isEventStarted&quot;: true
    }
  ]&#39;
</code></pre>
<h2>DELETE: Remove Records</h2>
<p>Remove records from inventory.</p>
<h3>Endpoint</h3>
<pre><code>DELETE https://api.opti-x.optimove.net/sports-inventory/v1/records
</code></pre>
<h3>Example Request</h3>
<pre><code class="language-bash">curl --request DELETE \
  --url https://api.opti-x.optimove.net/sports-inventory/v1/records \
  --header &#39;accept: application/json&#39; \
  --header &#39;content-type: application/json&#39; \
  --header &#39;x-api-key: your-api-key&#39; \
  --header &#39;x-brand-key: your-brand-key&#39; \
  --data &#39;[
    {
      &quot;eventKey&quot;: &quot;cancelled-event-001&quot;
    }
  ]&#39;
</code></pre>
<h2>Entity Schemas</h2>
<h3>Category Schema</h3>
<table>
<thead>
<tr>
<th>Field</th>
<th>Type</th>
<th align="center">Required</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>categoryKey</td>
<td>string (min 1 char)</td>
<td align="center">Yes</td>
<td>Unique identifier for this Category</td>
</tr>
<tr>
<td>categoryName</td>
<td>string (min 1 char)</td>
<td align="center">No</td>
<td>Display name of this Category</td>
</tr>
<tr>
<td>categoryNameTranslated</td>
<td>object</td>
<td align="center">No</td>
<td>Translated names for other languages</td>
</tr>
<tr>
<td>displayStatus</td>
<td>string (enum)</td>
<td align="center">No</td>
<td><code>Displayed</code> or <code>NotDisplayed</code>. Propagates to children.</td>
</tr>
<tr>
<td>displayOrder</td>
<td>int32</td>
<td align="center">No</td>
<td>Sort order. Lower values display first.</td>
</tr>
<tr>
<td>extra</td>
<td>object</td>
<td align="center">No</td>
<td>Custom metadata passed through for your use</td>
</tr>
</tbody></table>
<h3>Class Schema</h3>
<table>
<thead>
<tr>
<th>Field</th>
<th>Type</th>
<th align="center">Required</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>classKey</td>
<td>string (min 1 char)</td>
<td align="center">Yes</td>
<td>Unique identifier for this Class</td>
</tr>
<tr>
<td>categoryKey</td>
<td>string (min 1 char)</td>
<td align="center">Yes</td>
<td>Parent Category identifier</td>
</tr>
<tr>
<td>className</td>
<td>string (min 1 char)</td>
<td align="center">No</td>
<td>Display name of this Class</td>
</tr>
<tr>
<td>classNameTranslated</td>
<td>object</td>
<td align="center">No</td>
<td>Translated names for other languages</td>
</tr>
<tr>
<td>classStatus</td>
<td>string (enum)</td>
<td align="center">No</td>
<td><code>Active</code> or <code>Inactive</code></td>
</tr>
<tr>
<td>displayStatus</td>
<td>string (enum)</td>
<td align="center">No</td>
<td><code>Displayed</code> or <code>NotDisplayed</code>. Propagates to children.</td>
</tr>
<tr>
<td>displayOrder</td>
<td>int32</td>
<td align="center">No</td>
<td>Sort order. Lower values display first.</td>
</tr>
<tr>
<td>extra</td>
<td>object</td>
<td align="center">No</td>
<td>Custom metadata passed through for your use</td>
</tr>
</tbody></table>
<h3>Type Schema</h3>
<table>
<thead>
<tr>
<th>Field</th>
<th>Type</th>
<th align="center">Required</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>typeKey</td>
<td>string (min 1 char)</td>
<td align="center">Yes</td>
<td>Unique identifier for this Type</td>
</tr>
<tr>
<td>categoryKey</td>
<td>string (min 1 char)</td>
<td align="center">Yes</td>
<td>Parent Category identifier</td>
</tr>
<tr>
<td>classKey</td>
<td>string (min 1 char)</td>
<td align="center">No</td>
<td>Parent Class identifier</td>
</tr>
<tr>
<td>typeName</td>
<td>string (min 1 char)</td>
<td align="center">No</td>
<td>Display name of this Type</td>
</tr>
<tr>
<td>typeNameTranslated</td>
<td>object</td>
<td align="center">No</td>
<td>Translated names for other languages</td>
</tr>
<tr>
<td>displayStatus</td>
<td>string (enum)</td>
<td align="center">No</td>
<td><code>Displayed</code> or <code>NotDisplayed</code>. Propagates to children.</td>
</tr>
<tr>
<td>displayOrder</td>
<td>int32</td>
<td align="center">No</td>
<td>Sort order. Lower values display first.</td>
</tr>
<tr>
<td>extra</td>
<td>object</td>
<td align="center">No</td>
<td>Custom metadata passed through for your use</td>
</tr>
</tbody></table>
<h3>Event Schema</h3>
<table>
<thead>
<tr>
<th>Field</th>
<th>Type</th>
<th align="center">Required</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>eventKey</td>
<td>string (min 1 char)</td>
<td align="center">Yes</td>
<td>Unique identifier for this Event</td>
</tr>
<tr>
<td>categoryKey</td>
<td>string (min 1 char)</td>
<td align="center">No</td>
<td>Parent Category identifier</td>
</tr>
<tr>
<td>classKey</td>
<td>string (min 1 char)</td>
<td align="center">No</td>
<td>Parent Class identifier</td>
</tr>
<tr>
<td>typeKey</td>
<td>string (min 1 char)</td>
<td align="center">No</td>
<td>Parent Type identifier</td>
</tr>
<tr>
<td>eventName</td>
<td>string (min 1 char)</td>
<td align="center">No</td>
<td>Display name of this Event</td>
</tr>
<tr>
<td>eventNameTranslated</td>
<td>object</td>
<td align="center">No</td>
<td>Translated names for other languages</td>
</tr>
<tr>
<td>eventDateTime</td>
<td>date-time</td>
<td align="center">No</td>
<td>When the event takes place (ISO 8601 format)</td>
</tr>
<tr>
<td>eventStatus</td>
<td>string (enum)</td>
<td align="center">No</td>
<td><code>Active</code> or <code>Inactive</code></td>
</tr>
<tr>
<td>eventSort</td>
<td>string</td>
<td align="center">No</td>
<td>Custom sort order</td>
</tr>
<tr>
<td>classSortCode</td>
<td>string</td>
<td align="center">No</td>
<td>Sort code for class ordering</td>
</tr>
<tr>
<td>displayStatus</td>
<td>string (enum)</td>
<td align="center">No</td>
<td><code>Displayed</code> or <code>NotDisplayed</code>. Propagates to children.</td>
</tr>
<tr>
<td>displayOrder</td>
<td>int32</td>
<td align="center">No</td>
<td>Sort order. Lower values display first.</td>
</tr>
<tr>
<td>homeName</td>
<td>string</td>
<td align="center">No</td>
<td>Home team name</td>
</tr>
<tr>
<td>awayName</td>
<td>string</td>
<td align="center">No</td>
<td>Away team name</td>
</tr>
<tr>
<td>participants</td>
<td>string</td>
<td align="center">No</td>
<td>Event participants</td>
</tr>
<tr>
<td>isEventStarted</td>
<td>boolean</td>
<td align="center">No</td>
<td>Whether the event has started</td>
</tr>
<tr>
<td>isEventFinished</td>
<td>boolean</td>
<td align="center">No</td>
<td>Whether the event has finished</td>
</tr>
<tr>
<td>extra</td>
<td>object</td>
<td align="center">No</td>
<td>Custom metadata passed through for your use</td>
</tr>
</tbody></table>
<h3>Market Schema</h3>
<table>
<thead>
<tr>
<th>Field</th>
<th>Type</th>
<th align="center">Required</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>marketKey</td>
<td>string (min 1 char)</td>
<td align="center">Yes</td>
<td>Unique identifier for this Market</td>
</tr>
<tr>
<td>eventKey</td>
<td>string (min 1 char)</td>
<td align="center">Yes</td>
<td>Parent Event identifier</td>
</tr>
<tr>
<td>categoryKey</td>
<td>string (min 1 char)</td>
<td align="center">No</td>
<td>Parent Category identifier</td>
</tr>
<tr>
<td>classKey</td>
<td>string (min 1 char)</td>
<td align="center">No</td>
<td>Parent Class identifier</td>
</tr>
<tr>
<td>typeKey</td>
<td>string (min 1 char)</td>
<td align="center">No</td>
<td>Parent Type identifier</td>
</tr>
<tr>
<td>marketName</td>
<td>string (min 1 char)</td>
<td align="center">No</td>
<td>Display name of this Market</td>
</tr>
<tr>
<td>marketNameTranslated</td>
<td>object</td>
<td align="center">No</td>
<td>Translated names for other languages</td>
</tr>
<tr>
<td>marketStatus</td>
<td>string (enum)</td>
<td align="center">No</td>
<td><code>Active</code> or <code>Inactive</code></td>
</tr>
<tr>
<td>marketSort</td>
<td>string</td>
<td align="center">No</td>
<td>Custom sort order</td>
</tr>
<tr>
<td>displayStatus</td>
<td>string (enum)</td>
<td align="center">No</td>
<td><code>Displayed</code> or <code>NotDisplayed</code>. Propagates to children.</td>
</tr>
<tr>
<td>displayOrder</td>
<td>int32</td>
<td align="center">No</td>
<td>Sort order. Lower values display first.</td>
</tr>
<tr>
<td>extra</td>
<td>object</td>
<td align="center">No</td>
<td>Custom metadata passed through for your use</td>
</tr>
</tbody></table>
<h3>Selection Schema</h3>
<table>
<thead>
<tr>
<th>Field</th>
<th>Type</th>
<th align="center">Required</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>selectionKey</td>
<td>string (min 1 char)</td>
<td align="center">Yes</td>
<td>Unique identifier for this Selection</td>
</tr>
<tr>
<td>eventKey</td>
<td>string (min 1 char)</td>
<td align="center">Yes</td>
<td>Parent Event identifier</td>
</tr>
<tr>
<td>marketKey</td>
<td>string (min 1 char)</td>
<td align="center">No</td>
<td>Parent Market identifier</td>
</tr>
<tr>
<td>selectionName</td>
<td>string (min 1 char)</td>
<td align="center">No</td>
<td>Display name of this Selection</td>
</tr>
<tr>
<td>selectionNameTranslated</td>
<td>object</td>
<td align="center">No</td>
<td>Translated names for other languages</td>
</tr>
<tr>
<td>selectionStatus</td>
<td>string (enum)</td>
<td align="center">No</td>
<td><code>Active</code> or <code>Inactive</code></td>
</tr>
<tr>
<td>selectionPriceType</td>
<td>string</td>
<td align="center">No</td>
<td>Price type identifier</td>
</tr>
<tr>
<td>displayStatus</td>
<td>string (enum)</td>
<td align="center">No</td>
<td><code>Displayed</code> or <code>NotDisplayed</code></td>
</tr>
<tr>
<td>displayOrder</td>
<td>int32</td>
<td align="center">No</td>
<td>Sort order. Lower values display first.</td>
</tr>
<tr>
<td>numPrice</td>
<td>int32</td>
<td align="center">No</td>
<td>Odds numerator (fractional odds)</td>
</tr>
<tr>
<td>denPrice</td>
<td>int32</td>
<td align="center">No</td>
<td>Odds denominator (fractional odds)</td>
</tr>
<tr>
<td>decPrice</td>
<td>number</td>
<td align="center">No</td>
<td>Decimal odds</td>
</tr>
<tr>
<td>outcomeMeaningMajorCode</td>
<td>string</td>
<td align="center">No</td>
<td>Outcome major code</td>
</tr>
<tr>
<td>extra</td>
<td>object</td>
<td align="center">No</td>
<td>Custom metadata passed through for your use</td>
</tr>
</tbody></table>
<h2>API Responses</h2>
<h3>Success Response (202)</h3>
<pre><code class="language-json">{
  &quot;success&quot;: true
}
</code></pre>
<p>The API returns <code>202 Accepted</code> when all records pass validation.</p>
<h3>Validation Error Response (400)</h3>
<pre><code class="language-json">{
  &quot;error&quot;: {
    &quot;message&quot;: &quot;Validation failed&quot;,
    &quot;errors&quot;: &quot;Field &#39;eventKey&#39; is required for Market records&quot;
  }
}
</code></pre>
<p>The API returns <code>400 Bad Request</code> when records fail validation. Review the error message and correct your data.</p>
<h3>Partial Failure Response</h3>
<pre><code class="language-json">{
  &quot;success&quot;: false,
  &quot;message&quot;: &quot;Not all records were processed successfully&quot;
}
</code></pre>
<p>This occurs during high load. Implement retry logic with exponential backoff.</p>
<h2>Error Handling</h2>
<h3>Common Errors and Solutions</h3>
<table>
<thead>
<tr>
<th>Error</th>
<th>Cause</th>
<th>Solution</th>
</tr>
</thead>
<tbody><tr>
<td>Missing required field</td>
<td>A required field like <code>eventKey</code> is not provided</td>
<td>Add the missing field to your request</td>
</tr>
<tr>
<td>Invalid field type</td>
<td>Field value does not match expected type</td>
<td>Check the schema and correct the data type</td>
</tr>
<tr>
<td>Parent not found</td>
<td>Child record references a parent that does not exist</td>
<td>Ensure parent records are created first or included earlier in the same request</td>
</tr>
<tr>
<td>Rate limit exceeded</td>
<td>Too many requests in 10-second window</td>
<td>Implement exponential backoff and batch records</td>
</tr>
<tr>
<td>Record not found (PUT/DELETE)</td>
<td>Trying to update or delete a non-existent record</td>
<td>Verify the record exists before updating or deleting</td>
</tr>
</tbody></table>
<h3>Retry Strategy</h3>
<p>For <code>success: false</code> responses or 5xx errors:</p>
<ol>
<li>Wait 1 second</li>
<li>Retry the request</li>
<li>If it fails again, wait 2 seconds</li>
<li>Continue doubling the wait time up to 60 seconds</li>
<li>After 5 failures, log the error and alert your operations team</li>
</ol>
<h2>Best Practices</h2>
<ol>
<li><strong>Batch updates</strong> - Combine multiple record changes into single requests to reduce API calls</li>
<li><strong>Order records correctly</strong> - Always include parent records before children in the same request</li>
<li><strong>Update only changed fields</strong> - PUT requests only need fields that changed, plus the identifying key</li>
<li><strong>Monitor for failures</strong> - Log all API responses and alert on repeated failures</li>
<li><strong>Use display status</strong> - Set <code>displayStatus</code> to <code>NotDisplayed</code> rather than deleting records you might need later</li>
</ol>
<hr>
<h2>Related Topics</h2>
<ul>
<li><a href="#inventory-overview">Inventory Overview</a> - Introduction to inventory concepts</li>
<li><a href="#availability-filters">Availability Filters</a> - Configure user-based filtering</li>
</ul>

</section>
<section id="ecommerce-inventory" class="doc-section">
<h1>E-commerce Inventory</h1>
<p>This document details the data formats for preparing your e-commerce product catalog for Opti-X.</p>
<h2>Overview</h2>
<p>E-commerce inventory provides Opti-X with your product catalog data. Opti-X uses this data to generate personalized product recommendations across your website, app, and marketing channels.</p>
<h3>Why This Matters</h3>
<p>Your product inventory is the foundation of all recommendations. Complete and accurate inventory data enables Opti-X to:</p>
<ul>
<li>Match shoppers with products they are likely to purchase</li>
<li>Filter products by availability, price, and category</li>
<li>Display rich product information in recommendations</li>
<li>Power use cases like &quot;new arrivals,&quot; &quot;back in stock,&quot; and &quot;price drops&quot;</li>
</ul>
<blockquote>
<p><strong>Important:</strong> Inventory field names must map to your real-time event field names. Consistent naming ensures Opti-X can connect user behavior to the correct products.</p>
</blockquote>
<h2>Product Hierarchy</h2>
<p>E-commerce inventory supports three levels of product granularity:</p>
<pre><code>Product (Ripped Jeans - Style #1934256)
    |
    +-- Variant (Blue Ripped Jeans)
           |
           +-- SKU (Blue Ripped Jeans, W28 H30)
</code></pre>
<h3>Product</h3>
<p>The base item in your catalog. Products represent a distinct item regardless of size, color, or other variations.</p>
<p><strong>Example:</strong> &quot;Ripped Jeans&quot; (Style #1934256)</p>
<h3>Variant</h3>
<p>A variation of the product, typically differentiated by color, material, or style.</p>
<p><strong>Example:</strong> &quot;Blue Ripped Jeans&quot; - the blue version of Style #1934256</p>
<h3>SKU (Stock Keeping Unit)</h3>
<p>The most specific level, representing a unique purchasable item with exact attributes.</p>
<p><strong>Example:</strong> &quot;Blue Ripped Jeans, W28 H30&quot; - blue jeans in waist 28, height 30</p>
<h3>Handling Missing Levels</h3>
<p>Not all businesses use all three levels. Here is how to handle each scenario:</p>
<table>
<thead>
<tr>
<th>Your Data</th>
<th>How to Map</th>
</tr>
</thead>
<tbody><tr>
<td>Product only</td>
<td>Set <code>PRODUCT_ID</code>, <code>VARIANT_ID</code>, and <code>SKU_ID</code> to the same value</td>
</tr>
<tr>
<td>Product + Variant</td>
<td>Set <code>SKU_ID</code> equal to <code>VARIANT_ID</code></td>
</tr>
<tr>
<td>All three levels</td>
<td>Use distinct values for each field</td>
</tr>
</tbody></table>
<h2>Example Inventory Record</h2>
<pre><code class="language-json">{
  &quot;SKU_ID&quot;: &quot;RippedJeans1934256-Blue-W28H30&quot;,
  &quot;VARIANT_ID&quot;: &quot;RippedJeans1934256-Blue&quot;,
  &quot;PRODUCT_ID&quot;: &quot;RippedJeans1934256&quot;,
  &quot;ITEM_NAME&quot;: &quot;Ripped Jeans&quot;,
  &quot;ITEM_DESCRIPTION&quot;: &quot;100% Soft Denim Fabric!&quot;,
  &quot;SKU_NAME&quot;: &quot;Blue Ripped Jeans, W28 H30&quot;,
  &quot;VARIANT_NAME&quot;: &quot;Blue Ripped Jeans&quot;,
  &quot;CATEGORYID&quot;: &quot;050102&quot;,
  &quot;CATEGORY&quot;: &quot;Jeans&quot;,
  &quot;DEPARTMENTID&quot;: &quot;05&quot;,
  &quot;DEPARTMENT&quot;: &quot;Clothing&quot;,
  &quot;CATEGORY_LIST&quot;: &quot;Clothing &gt; Trousers &gt; Jeans&quot;,
  &quot;CATEGORY_KEY_LIST&quot;: &quot;05 &gt; 0501 &gt; 050102&quot;,
  &quot;BRAND&quot;: &quot;Example Brand&quot;,
  &quot;CURRENCY&quot;: &quot;USD&quot;,
  &quot;PRICE&quot;: 40,
  &quot;SIZE&quot;: &quot;W28 H30&quot;,
  &quot;COLOUR&quot;: &quot;Blue&quot;,
  &quot;STOCK&quot;: 826,
  &quot;RELEASE_DATE&quot;: &quot;2024-10-15&quot;,
  &quot;ISAVAILABLE&quot;: true,
  &quot;PRODUCT_URL&quot;: &quot;https://www.example.com/products/ripped-jeans-1934256&quot;,
  &quot;PRODUCT_IMAGE&quot;: &quot;https://www.example.com/images/ripped-jeans-blue.jpg&quot;,
  &quot;RAW_DATA&quot;: [
    {&quot;key&quot;: &quot;is_sustainable&quot;, &quot;value&quot;: &quot;true&quot;, &quot;level&quot;: &quot;product&quot;, &quot;type&quot;: &quot;boolean&quot;},
    {&quot;key&quot;: &quot;fabric_type&quot;, &quot;value&quot;: &quot;denim&quot;, &quot;level&quot;: &quot;variant&quot;, &quot;type&quot;: &quot;text&quot;}
  ]
}
</code></pre>
<h2>Field Reference</h2>
<h3>Identification Fields</h3>
<p>These fields identify products at each level of the hierarchy.</p>
<table>
<thead>
<tr>
<th>Field</th>
<th align="center">Required</th>
<th>Type</th>
<th>Example</th>
<th>Description</th>
<th>Opti-X Impact</th>
</tr>
</thead>
<tbody><tr>
<td>SKU_ID</td>
<td align="center">No</td>
<td>String</td>
<td><code>RippedJeans1934256-Blue-W28H30</code></td>
<td>Unique identifier for the most specific product level. If not applicable, set to <code>VARIANT_ID</code> value.</td>
<td>Enables SKU-level recommendation configuration</td>
</tr>
<tr>
<td>VARIANT_ID</td>
<td align="center">No</td>
<td>String</td>
<td><code>RippedJeans1934256-Blue</code></td>
<td>Unique identifier for the product variant. If not applicable, set to <code>PRODUCT_ID</code> value.</td>
<td>Enables variant-level recommendation configuration</td>
</tr>
<tr>
<td>PRODUCT_ID</td>
<td align="center">Yes</td>
<td>String</td>
<td><code>RippedJeans1934256</code></td>
<td>Unique identifier for the base product</td>
<td>Core identifier for personalization. Returned in recommendation responses.</td>
</tr>
</tbody></table>
<h4>Why This Matters</h4>
<p>Product identification determines the granularity of recommendations. If you want to recommend &quot;Blue Jeans in size W28&quot; specifically (not just &quot;Jeans&quot;), you need proper SKU-level data.</p>
<h3>Display Fields</h3>
<p>These fields provide information shown to users in recommendations.</p>
<table>
<thead>
<tr>
<th>Field</th>
<th align="center">Required</th>
<th>Type</th>
<th>Example</th>
<th>Description</th>
<th>Opti-X Impact</th>
</tr>
</thead>
<tbody><tr>
<td>ITEM_NAME</td>
<td align="center">Yes</td>
<td>String</td>
<td><code>Ripped Jeans</code></td>
<td>Product display name</td>
<td>Returned in recommendation responses. Used in filtering rules.</td>
</tr>
<tr>
<td>ITEM_DESCRIPTION</td>
<td align="center">No</td>
<td>String</td>
<td><code>100% Soft Denim Fabric!</code></td>
<td>Product description</td>
<td>Returned in recommendation responses</td>
</tr>
<tr>
<td>SKU_NAME</td>
<td align="center">No</td>
<td>String</td>
<td><code>Blue Ripped Jeans, W28 H30</code></td>
<td>SKU display name</td>
<td>Returned in recommendation responses</td>
</tr>
<tr>
<td>VARIANT_NAME</td>
<td align="center">No</td>
<td>String</td>
<td><code>Blue Ripped Jeans</code></td>
<td>Variant display name</td>
<td>Returned in recommendation responses</td>
</tr>
<tr>
<td>PRODUCT_URL</td>
<td align="center">No</td>
<td>String</td>
<td><code>https://www.example.com/products/afjoi239</code></td>
<td>Product page URL</td>
<td>Returned in recommendations. Required for Smart Banners.</td>
</tr>
<tr>
<td>PRODUCT_IMAGE</td>
<td align="center">No</td>
<td>String</td>
<td><code>https://www.example.com/images/product.jpg</code></td>
<td>Product image URL</td>
<td>Returned in recommendations. Required for Smart Banners.</td>
</tr>
<tr>
<td>VIDEO_URL</td>
<td align="center">No</td>
<td>String</td>
<td><code>https://www.example.com/videos/product.mov</code></td>
<td>Product video URL</td>
<td>Optional for enhanced content</td>
</tr>
</tbody></table>
<h4>Why This Matters</h4>
<p>Display fields populate the recommendation response. Missing fields mean missing content in your personalized experiences. <code>PRODUCT_IMAGE</code> is essential for visual merchandising use cases.</p>
<h3>Category Fields</h3>
<p>These fields define your product taxonomy and enable category-based filtering.</p>
<table>
<thead>
<tr>
<th>Field</th>
<th align="center">Required</th>
<th>Type</th>
<th>Example</th>
<th>Description</th>
<th>Opti-X Impact</th>
</tr>
</thead>
<tbody><tr>
<td>CATEGORYID</td>
<td align="center">Yes</td>
<td>String</td>
<td><code>050102</code></td>
<td>Unique category identifier</td>
<td>Returned in responses</td>
</tr>
<tr>
<td>CATEGORY</td>
<td align="center">Yes</td>
<td>String</td>
<td><code>Jeans</code></td>
<td>Category name</td>
<td>Returned in responses. Used in filtering rules.</td>
</tr>
<tr>
<td>DEPARTMENTID</td>
<td align="center">Yes</td>
<td>String</td>
<td><code>05</code></td>
<td>Department identifier (top-level category)</td>
<td>Returned in responses</td>
</tr>
<tr>
<td>DEPARTMENT</td>
<td align="center">Yes</td>
<td>String</td>
<td><code>Clothing</code></td>
<td>Department name</td>
<td>Returned in responses. Used in filtering rules.</td>
</tr>
<tr>
<td>CATEGORY_LIST</td>
<td align="center">Yes</td>
<td>String</td>
<td><code>Clothing &gt; Trousers &gt; Jeans</code></td>
<td>Full category path with <code>&gt;</code> delimiter</td>
<td>Powers parent category filtering rules</td>
</tr>
<tr>
<td>CATEGORY_KEY_LIST</td>
<td align="center">Yes</td>
<td>String</td>
<td><code>05 &gt; 0501 &gt; 050102</code></td>
<td>Category ID path with <code>&gt;</code> delimiter</td>
<td>Powers parent category filtering rules</td>
</tr>
</tbody></table>
<h4>Why This Matters</h4>
<p>Category data enables rules like &quot;recommend products from the same category&quot; or &quot;exclude products from a specific department.&quot; The <code>CATEGORY_LIST</code> path enables hierarchical filtering.</p>
<h3>Product Attributes</h3>
<p>These fields describe product characteristics for filtering and display.</p>
<table>
<thead>
<tr>
<th>Field</th>
<th align="center">Required</th>
<th>Type</th>
<th>Example</th>
<th>Description</th>
<th>Opti-X Impact</th>
</tr>
</thead>
<tbody><tr>
<td>BRAND</td>
<td align="center">Yes</td>
<td>String</td>
<td><code>Example Brand</code></td>
<td>Product brand</td>
<td>Returned in responses. Used in filtering rules.</td>
</tr>
<tr>
<td>SIZE</td>
<td align="center">No</td>
<td>String</td>
<td><code>W28 H30</code></td>
<td>Product size</td>
<td>Returned in responses. Used in filtering rules.</td>
</tr>
<tr>
<td>COLOUR</td>
<td align="center">No</td>
<td>String</td>
<td><code>Blue</code></td>
<td>Product color</td>
<td>Returned in responses. Used in filtering rules.</td>
</tr>
<tr>
<td>FEATURES</td>
<td align="center">No</td>
<td>String</td>
<td><code>Jeans, Ripped, Blue, Baggy</code></td>
<td>Comma-separated product features</td>
<td>Returned in responses. May improve model training.</td>
</tr>
<tr>
<td>RATING</td>
<td align="center">No</td>
<td>Number</td>
<td><code>3</code></td>
<td>Product rating (scale defined by you)</td>
<td>Used for rating-based filtering</td>
</tr>
</tbody></table>
<h3>Pricing and Availability</h3>
<p>These fields track pricing, stock, and availability status.</p>
<table>
<thead>
<tr>
<th>Field</th>
<th align="center">Required</th>
<th>Type</th>
<th>Example</th>
<th>Description</th>
<th>Opti-X Impact</th>
</tr>
</thead>
<tbody><tr>
<td>CURRENCY</td>
<td align="center">No</td>
<td>String</td>
<td><code>USD</code></td>
<td>Price currency code. Required if you have multiple currencies.</td>
<td>Associates prices with correct currency</td>
</tr>
<tr>
<td>PRICE</td>
<td align="center">No</td>
<td>Number</td>
<td><code>40</code></td>
<td>Standard price before discounts</td>
<td>Used in filtering rules. Powers price-related campaigns.</td>
</tr>
<tr>
<td>STOCK</td>
<td align="center">No</td>
<td>Number</td>
<td><code>826</code></td>
<td>Current inventory quantity</td>
<td>Used in filtering rules. Powers stock-related use cases.</td>
</tr>
<tr>
<td>ISAVAILABLE</td>
<td align="center">No</td>
<td>Boolean</td>
<td><code>true</code></td>
<td>Whether the item should appear in recommendations. Defaults to <code>true</code>.</td>
<td>Controls recommendation eligibility</td>
</tr>
<tr>
<td>DISPLAY_STATUS</td>
<td align="center">No</td>
<td>Boolean</td>
<td><code>true</code></td>
<td>Whether the item is displayed on your site. Defaults to <code>true</code>.</td>
<td>Used in filtering rules</td>
</tr>
<tr>
<td>ISDISCONTINUED</td>
<td align="center">No</td>
<td>Boolean</td>
<td><code>false</code></td>
<td>Whether the item is discontinued. Defaults to <code>false</code>.</td>
<td>Used in filtering rules</td>
</tr>
</tbody></table>
<h4>Why This Matters</h4>
<p>Availability fields prevent embarrassing recommendations. Recommending out-of-stock or discontinued products damages user trust. Keep <code>STOCK</code> and <code>ISAVAILABLE</code> current.</p>
<h3>Date Fields</h3>
<p>These fields track product lifecycle dates.</p>
<table>
<thead>
<tr>
<th>Field</th>
<th align="center">Required</th>
<th>Type</th>
<th>Example</th>
<th>Description</th>
<th>Opti-X Impact</th>
</tr>
</thead>
<tbody><tr>
<td>RELEASE_DATE</td>
<td align="center">No</td>
<td>String</td>
<td><code>2024-10-15</code></td>
<td>When the product launched. ISO 8601 format (YYYY-MM-DD).</td>
<td>Powers &quot;new arrivals&quot; campaigns and models</td>
</tr>
<tr>
<td>DISCONTINUE_DATE</td>
<td align="center">No</td>
<td>String</td>
<td><code>2024-10-20</code></td>
<td>When the product was or will be discontinued. ISO 8601 format.</td>
<td>Used for tracking and filtering</td>
</tr>
<tr>
<td>LAST_UPDATED</td>
<td align="center">No</td>
<td>String</td>
<td><code>2024-10-16 08:02:30</code></td>
<td>Last inventory update timestamp</td>
<td>Internal tracking and debugging</td>
</tr>
</tbody></table>
<h4>Why This Matters</h4>
<p><code>RELEASE_DATE</code> enables &quot;new arrivals&quot; recommendations. Without this field, Opti-X cannot identify which products are new.</p>
<h3>Custom Data</h3>
<p>Use <code>RAW_DATA</code> to include additional attributes not covered by standard fields.</p>
<table>
<thead>
<tr>
<th>Field</th>
<th align="center">Required</th>
<th>Type</th>
<th>Example</th>
<th>Description</th>
<th>Opti-X Impact</th>
</tr>
</thead>
<tbody><tr>
<td>RAW_DATA</td>
<td align="center">No</td>
<td>List of objects</td>
<td>See below</td>
<td>Custom key-value pairs with level and type metadata</td>
<td>Used in filtering and returned in responses</td>
</tr>
</tbody></table>
<h4>RAW_DATA Structure</h4>
<pre><code class="language-json">[
  {
    &quot;key&quot;: &quot;is_sustainable&quot;,
    &quot;value&quot;: &quot;true&quot;,
    &quot;level&quot;: &quot;product&quot;,
    &quot;type&quot;: &quot;boolean&quot;
  },
  {
    &quot;key&quot;: &quot;fabric_weight&quot;,
    &quot;value&quot;: &quot;12&quot;,
    &quot;level&quot;: &quot;variant&quot;,
    &quot;type&quot;: &quot;numeric&quot;
  }
]
</code></pre>
<table>
<thead>
<tr>
<th>Property</th>
<th>Description</th>
<th>Allowed Values</th>
</tr>
</thead>
<tbody><tr>
<td>key</td>
<td>Attribute name</td>
<td>Any string</td>
</tr>
<tr>
<td>value</td>
<td>Attribute value</td>
<td>String representation of the value</td>
</tr>
<tr>
<td>level</td>
<td>Which hierarchy level this applies to</td>
<td><code>product</code>, <code>variant</code>, <code>sku</code></td>
</tr>
<tr>
<td>type</td>
<td>Data type for filtering</td>
<td><code>text</code>, <code>numeric</code>, <code>boolean</code></td>
</tr>
</tbody></table>
<h4>Why This Matters</h4>
<p><code>RAW_DATA</code> extends your inventory schema without changing the core format. Use it for brand-specific attributes like &quot;is_sustainable,&quot; &quot;material_type,&quot; or &quot;collection_name.&quot;</p>
<h2>Date Format</h2>
<p>Use ISO 8601 format for all date fields:</p>
<ul>
<li><strong>Date only:</strong> <code>YYYY-MM-DD</code> (e.g., <code>2024-10-15</code>)</li>
<li><strong>Date and time:</strong> <code>YYYY-MM-DD HH:MM:SS</code> (e.g., <code>2024-10-16 08:02:30</code>)</li>
</ul>
<h2>Best Practices</h2>
<ol>
<li><strong>Keep inventory current</strong> - Update at least daily, preferably more often for stock and price changes</li>
<li><strong>Use consistent IDs</strong> - Product IDs in inventory must match IDs in your real-time events</li>
<li><strong>Include images</strong> - <code>PRODUCT_IMAGE</code> is essential for Smart Banners and visual recommendations</li>
<li><strong>Set availability correctly</strong> - Use <code>ISAVAILABLE: false</code> for items that should not be recommended</li>
<li><strong>Complete category paths</strong> - Full <code>CATEGORY_LIST</code> paths enable powerful filtering rules</li>
</ol>
<hr>
<h2>Related Topics</h2>
<ul>
<li><a href="#inventory-overview">Inventory Overview</a> - Introduction to inventory concepts</li>
<li><a href="#availability-filters">Availability Filters</a> - Configure user-based filtering</li>
</ul>

</section>
<section id="lottery-bingo" class="doc-section">
<h1>Lottery and Bingo Inventory</h1>
<p>Lottery and Bingo products use the Gaming Inventory structure within Opti-X. This guide explains how to configure your lottery draws and bingo games for optimal personalization.</p>
<h2>Overview</h2>
<p>Lottery and Bingo are categorized as Gaming within Opti-X. Rather than a separate inventory type, you use the standard Gaming Inventory schema with specific field mappings for lottery draws and bingo games.</p>
<h3>Why This Matters</h3>
<p>Using the Gaming Inventory structure for lottery and bingo provides:</p>
<ul>
<li>Consistent personalization across all gaming products</li>
<li>Shared user behavior models between games, lottery, and bingo</li>
<li>Unified reporting and analytics</li>
<li>Simplified integration with a single inventory format</li>
</ul>
<h2>Field Mapping</h2>
<p>Map your lottery and bingo data to Gaming Inventory fields:</p>
<table>
<thead>
<tr>
<th>Gaming Inventory Field</th>
<th>Lottery/Bingo Meaning</th>
<th>Example</th>
</tr>
</thead>
<tbody><tr>
<td>game_code</td>
<td>Unique identifier for the draw or game</td>
<td><code>LOTTO-2024-03-15-EVE</code></td>
</tr>
<tr>
<td>game_name</td>
<td>Name of the lottery game or bingo room</td>
<td><code>Daily Jackpot Draw</code></td>
</tr>
<tr>
<td>game_category</td>
<td>Must be <code>Lottery</code> or <code>Bingo</code></td>
<td><code>Lottery</code></td>
</tr>
<tr>
<td>extra</td>
<td>Additional data including draw time</td>
<td><code>{&quot;draw_time&quot;: &quot;2024-03-15T19:00:00Z&quot;}</code></td>
</tr>
</tbody></table>
<h2>Example Inventory Records</h2>
<h3>Lottery Draw</h3>
<pre><code class="language-json">{
  &quot;game_code&quot;: &quot;LOTTO-2024-03-15-EVE&quot;,
  &quot;game_name&quot;: &quot;Daily Jackpot Draw&quot;,
  &quot;game_category&quot;: &quot;Lottery&quot;,
  &quot;game_class&quot;: &quot;Daily&quot;,
  &quot;game_type&quot;: &quot;Jackpot&quot;,
  &quot;description&quot;: &quot;Evening draw with a guaranteed $1M jackpot&quot;,
  &quot;desktop&quot;: 1,
  &quot;mobile&quot;: 1,
  &quot;tablet&quot;: 1,
  &quot;launch_date&quot;: &quot;2024-03-15&quot;,
  &quot;image_url&quot;: &quot;https://lottery.example.com/images/daily-jackpot.jpg&quot;,
  &quot;supplier&quot;: &quot;National Lottery&quot;,
  &quot;extra&quot;: {
    &quot;draw_time&quot;: &quot;2024-03-15T19:00:00Z&quot;,
    &quot;jackpot_amount&quot;: 1000000,
    &quot;ticket_price&quot;: 2.00,
    &quot;closing_time&quot;: &quot;2024-03-15T18:30:00Z&quot;
  },
  &quot;inclusions&quot;: {&quot;country&quot;: [&quot;US&quot;, &quot;CA&quot;]},
  &quot;regulation&quot;: [&quot;STATE_LOTTERY&quot;]
}
</code></pre>
<h3>Bingo Room</h3>
<pre><code class="language-json">{
  &quot;game_code&quot;: &quot;BINGO-RUBY-ROOM&quot;,
  &quot;game_name&quot;: &quot;Ruby Room - 75 Ball Bingo&quot;,
  &quot;game_category&quot;: &quot;Bingo&quot;,
  &quot;game_class&quot;: &quot;75-Ball&quot;,
  &quot;game_type&quot;: &quot;Room&quot;,
  &quot;description&quot;: &quot;Fast-paced 75-ball bingo with hourly jackpots&quot;,
  &quot;desktop&quot;: 1,
  &quot;mobile&quot;: 1,
  &quot;tablet&quot;: 1,
  &quot;image_url&quot;: &quot;https://bingo.example.com/images/ruby-room.jpg&quot;,
  &quot;supplier&quot;: &quot;Bingo Provider Inc.&quot;,
  &quot;extra&quot;: {
    &quot;room_type&quot;: &quot;75-ball&quot;,
    &quot;min_buy_in&quot;: 0.50,
    &quot;max_players&quot;: 200,
    &quot;next_game&quot;: &quot;2024-03-15T10:15:00Z&quot;,
    &quot;jackpot_type&quot;: &quot;progressive&quot;
  },
  &quot;skin_id&quot;: [&quot;21&quot;, &quot;23&quot;],
  &quot;regulation&quot;: [&quot;UKGC&quot;, &quot;MGA&quot;]
}
</code></pre>
<h2>Required Fields</h2>
<p>These fields are mandatory for lottery and bingo inventory:</p>
<table>
<thead>
<tr>
<th>Field</th>
<th align="center">Required</th>
<th>Why It Matters</th>
</tr>
</thead>
<tbody><tr>
<td>game_code</td>
<td align="center">Yes</td>
<td>Unique identifier for tracking and recommendations</td>
</tr>
<tr>
<td>game_name</td>
<td align="center">Yes</td>
<td>Display name shown in recommendations</td>
</tr>
<tr>
<td>game_category</td>
<td align="center">Yes</td>
<td>Must be <code>Lottery</code> or <code>Bingo</code> to categorize correctly</td>
</tr>
<tr>
<td>extra.draw_time</td>
<td align="center">Yes (Lottery)</td>
<td>Enables time-based filtering and &quot;upcoming draws&quot; recommendations</td>
</tr>
</tbody></table>
<p>All other Gaming Inventory fields are optional but recommended for richer personalization.</p>
<h2>Draw Time Handling</h2>
<p>For lottery products, the draw time is critical for recommendations. Include it in the <code>extra</code> field:</p>
<pre><code class="language-json">{
  &quot;extra&quot;: {
    &quot;draw_time&quot;: &quot;2024-03-15T19:00:00Z&quot;,
    &quot;closing_time&quot;: &quot;2024-03-15T18:30:00Z&quot;
  }
}
</code></pre>
<h3>Why This Matters</h3>
<p>Draw times enable Opti-X to:</p>
<ul>
<li>Show only upcoming draws (not past ones)</li>
<li>Prioritize draws closing soon for urgency messaging</li>
<li>Filter draws by time of day based on user preferences</li>
<li>Avoid recommending draws after ticket sales close</li>
</ul>
<h2>Real-Time Event Tracking</h2>
<p>Track user interactions with lottery and bingo using the standard gaming event <code>core_game_launch</code>:</p>
<pre><code class="language-json">{
  &quot;event&quot;: &quot;core_game_launch&quot;,
  &quot;user_id&quot;: &quot;user-12345&quot;,
  &quot;game_code&quot;: &quot;LOTTO-2024-03-15-EVE&quot;,
  &quot;game_name&quot;: &quot;Daily Jackpot Draw&quot;,
  &quot;game_category&quot;: &quot;Lottery&quot;,
  &quot;timestamp&quot;: &quot;2024-03-15T14:30:00Z&quot;
}
</code></pre>
<p>The <code>game_code</code>, <code>game_name</code>, and <code>game_category</code> in your events must match your inventory data exactly.</p>
<h2>Availability Filters</h2>
<p>Use standard Gaming Inventory availability filters for lottery and bingo:</p>
<pre><code class="language-json">{
  &quot;game_code&quot;: &quot;LOTTO-UK-EVENING&quot;,
  &quot;game_name&quot;: &quot;UK Evening Draw&quot;,
  &quot;game_category&quot;: &quot;Lottery&quot;,
  &quot;inclusions&quot;: {
    &quot;country&quot;: [&quot;UK&quot;],
    &quot;age_verified&quot;: true
  },
  &quot;exclusions&quot;: {
    &quot;self_excluded&quot;: true
  },
  &quot;regulation&quot;: [&quot;UKGC&quot;]
}
</code></pre>
<p>This ensures lottery products only appear to eligible users based on location, age verification, and regulatory requirements.</p>
<h2>Best Practices</h2>
<ol>
<li><strong>Update inventory frequently</strong> - Add new draws as they become available and remove past draws</li>
<li><strong>Include draw times</strong> - Essential for time-sensitive recommendations</li>
<li><strong>Set closing times</strong> - Prevent recommendations after ticket sales end</li>
<li><strong>Use regulation fields</strong> - Ensure compliance with jurisdictional requirements</li>
<li><strong>Include images</strong> - Required for Smart Content placements</li>
</ol>
<hr>
<h2>Related Topics</h2>
<ul>
<li><a href="#gaming-inventory">Gaming Inventory</a> - Complete Gaming Inventory field reference</li>
<li><a href="#availability-filters">Availability Filters</a> - Configure user-based filtering</li>
<li><a href="#inventory-overview">Inventory Overview</a> - Introduction to inventory concepts</li>
</ul>

</section>
<section id="availability-filters" class="doc-section">
<h1>Availability Filters</h1>
<p>Availability filters control which users can see which inventory items based on user attributes. They ensure users only receive recommendations for items they can access, purchase, or legally use.</p>
<h2>Overview</h2>
<h3>What Are Traits?</h3>
<p>Traits are user attributes sent with recommendation requests that describe the user&#39;s context. Common traits include:</p>
<ul>
<li><strong>Currency</strong> - The user&#39;s preferred or account currency (e.g., <code>USD</code>, <code>EUR</code>, <code>GBP</code>)</li>
<li><strong>Language</strong> - The user&#39;s language preference (e.g., <code>en</code>, <code>fr</code>, <code>es</code>)</li>
<li><strong>Country</strong> - The user&#39;s location country code (e.g., <code>US</code>, <code>UK</code>, <code>DE</code>)</li>
<li><strong>License</strong> - Regulatory jurisdiction (e.g., <code>UKGC</code>, <code>MGA</code>)</li>
<li><strong>Age Verified</strong> - Whether the user has completed age verification</li>
</ul>
<p>Opti-X matches these traits against inventory availability rules to filter recommendations.</p>
<h3>Why This Matters</h3>
<p>Availability filters solve critical business problems:</p>
<ol>
<li><strong>Regulatory compliance</strong> - Ensure users only see items licensed for their jurisdiction</li>
<li><strong>Localization</strong> - Show items in the user&#39;s language and currency</li>
<li><strong>Eligibility</strong> - Filter by age verification, account status, or membership level</li>
<li><strong>Multi-brand support</strong> - Control which items appear on which site skin or brand</li>
</ol>
<p>Without availability filters, you risk showing users items they cannot access, leading to poor experiences and potential compliance violations.</p>
<h2>How Filtering Works</h2>
<h3>Inclusions vs Exclusions</h3>
<p>Availability filters use two mechanisms:</p>
<table>
<thead>
<tr>
<th>Type</th>
<th>Operator</th>
<th>Meaning</th>
<th>Use Case</th>
</tr>
</thead>
<tbody><tr>
<td><strong>Inclusions</strong></td>
<td>IN</td>
<td>User trait must be in this list to see the item</td>
<td>&quot;Only show this game to users in UK or DE&quot;</td>
</tr>
<tr>
<td><strong>Exclusions</strong></td>
<td>NOT IN</td>
<td>User trait must NOT be in this list to see the item</td>
<td>&quot;Hide this game from users with French language&quot;</td>
</tr>
</tbody></table>
<h3>Evaluation Logic</h3>
<ol>
<li><strong>Check inclusions first</strong> - If inclusions are defined for a trait, the user&#39;s trait value must match one of the included values</li>
<li><strong>Check exclusions second</strong> - If exclusions are defined, the user&#39;s trait value must NOT match any excluded value</li>
<li><strong>No filter = no restriction</strong> - If neither inclusion nor exclusion is defined for a trait, all users pass that filter</li>
</ol>
<h3>Filter Precedence</h3>
<p>When both inclusions and exclusions exist for the same trait:</p>
<ol>
<li>Inclusions are evaluated first</li>
<li>If the user passes inclusions, exclusions are then checked</li>
<li>User must pass both to see the item</li>
</ol>
<h2>User Attributes in Requests</h2>
<p>Recommendation requests include user attributes in several locations:</p>
<pre><code class="language-json">{
  &quot;userId&quot;: &quot;156784322&quot;,
  &quot;type&quot;: &quot;recommendation&quot;,
  &quot;context&quot;: {
    &quot;channel&quot;: &quot;Desktop&quot;
  },
  &quot;skinId&quot;: &quot;98761234&quot;,
  &quot;location&quot;: {
    &quot;country&quot;: &quot;CA&quot;,
    &quot;state&quot;: &quot;QC&quot;
  },
  &quot;traits&quot;: {
    &quot;currency&quot;: &quot;CAD&quot;,
    &quot;language&quot;: &quot;en&quot;,
    &quot;license&quot;: &quot;CA&quot;,
    &quot;ageVerified&quot;: true
  },
  &quot;recommendation&quot;: {
    &quot;target&quot;: {
      &quot;getDetails&quot;: true
    }
  }
}
</code></pre>
<h3>Attribute Mapping</h3>
<table>
<thead>
<tr>
<th>User Attribute</th>
<th>Request Location</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>country</td>
<td><code>location.country</code></td>
<td>User&#39;s country code</td>
</tr>
<tr>
<td>state</td>
<td><code>location.state</code></td>
<td>User&#39;s state or province code</td>
</tr>
<tr>
<td>currency</td>
<td><code>traits.currency</code></td>
<td>User&#39;s currency preference</td>
</tr>
<tr>
<td>language</td>
<td><code>traits.language</code></td>
<td>User&#39;s language preference</td>
</tr>
<tr>
<td>license</td>
<td><code>traits.license</code></td>
<td>Regulatory license applicable to user</td>
</tr>
<tr>
<td>age_verified</td>
<td><code>traits.ageVerified</code></td>
<td>Whether user completed age verification</td>
</tr>
<tr>
<td>skin_id</td>
<td><code>skinId</code></td>
<td>Site skin or brand identifier</td>
</tr>
</tbody></table>
<h2>Defining Filters in Inventory</h2>
<p>Add availability filters to your inventory items using these fields:</p>
<h3>Gaming Inventory Example</h3>
<pre><code class="language-json">{
  &quot;game_code&quot;: &quot;123456&quot;,
  &quot;game_name&quot;: &quot;Adventure Quest&quot;,
  &quot;skin_id&quot;: [&quot;21&quot;, &quot;23&quot;],
  &quot;regulation&quot;: [&quot;UKGC&quot;, &quot;MGA&quot;],
  &quot;inclusions&quot;: {
    &quot;country&quot;: [&quot;UK&quot;, &quot;DE&quot;, &quot;MT&quot;],
    &quot;age_verified&quot;: true
  },
  &quot;exclusions&quot;: {
    &quot;language&quot;: &quot;fr&quot;,
    &quot;currency&quot;: [&quot;USD&quot;, &quot;CAD&quot;]
  }
}
</code></pre>
<p>This game:</p>
<ul>
<li>Only appears on skins 21 and 23</li>
<li>Only appears for users in UKGC or MGA regulated jurisdictions</li>
<li>Only appears for users in UK, Germany, or Malta</li>
<li>Only appears for age-verified users</li>
<li>Never appears for French-language users</li>
<li>Never appears for users with USD or CAD currency</li>
</ul>
<h3>Filter Fields</h3>
<table>
<thead>
<tr>
<th>Field</th>
<th>Type</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>skin_id</td>
<td>list of strings</td>
<td>List of skin IDs where item is available</td>
</tr>
<tr>
<td>regulation</td>
<td>list of strings</td>
<td>List of regulatory jurisdictions</td>
</tr>
<tr>
<td>inclusions</td>
<td>object</td>
<td>Key-value pairs for inclusion filters</td>
</tr>
<tr>
<td>exclusions</td>
<td>object</td>
<td>Key-value pairs for exclusion filters</td>
</tr>
</tbody></table>
<h3>Value Formats</h3>
<p>Inclusion and exclusion values can be:</p>
<ul>
<li><strong>Single value</strong>: <code>&quot;country&quot;: &quot;UK&quot;</code></li>
<li><strong>List of values</strong>: <code>&quot;country&quot;: [&quot;UK&quot;, &quot;DE&quot;, &quot;MT&quot;]</code></li>
<li><strong>Boolean</strong>: <code>&quot;age_verified&quot;: true</code></li>
</ul>
<h2>Detailed Example</h2>
<h3>Inventory Setup</h3>
<p>Two games with different availability rules:</p>
<pre><code class="language-json">{
  &quot;123456&quot;: {
    &quot;game_code&quot;: &quot;123456&quot;,
    &quot;game_name&quot;: &quot;Adventure Quest&quot;,
    &quot;skin_id&quot;: [&quot;21&quot;, &quot;23&quot;],
    &quot;inclusions&quot;: {
      &quot;country&quot;: &quot;CA&quot;,
      &quot;state&quot;: [&quot;QC&quot;, &quot;ON&quot;]
    },
    &quot;exclusions&quot;: {
      &quot;language&quot;: &quot;fr&quot;
    }
  },
  &quot;654321&quot;: {
    &quot;game_code&quot;: &quot;654321&quot;,
    &quot;game_name&quot;: &quot;King Slots&quot;,
    &quot;skin_id&quot;: [&quot;21&quot;],
    &quot;inclusions&quot;: {
      &quot;country&quot;: [&quot;CA&quot;, &quot;US&quot;]
    },
    &quot;exclusions&quot;: {
      &quot;language&quot;: &quot;fr&quot;
    }
  }
}
</code></pre>
<h3>Request</h3>
<pre><code class="language-json">{
  &quot;userId&quot;: &quot;156784322&quot;,
  &quot;skinId&quot;: &quot;21&quot;,
  &quot;location&quot;: {
    &quot;country&quot;: &quot;CA&quot;,
    &quot;state&quot;: &quot;BC&quot;
  },
  &quot;traits&quot;: {
    &quot;language&quot;: &quot;en&quot;
  }
}
</code></pre>
<h3>Result</h3>
<table>
<thead>
<tr>
<th>Game</th>
<th>Returned?</th>
<th>Reason</th>
</tr>
</thead>
<tbody><tr>
<td>Adventure Quest</td>
<td>No</td>
<td>User&#39;s state (BC) is not in inclusions (QC, ON)</td>
</tr>
<tr>
<td>King Slots</td>
<td>Yes</td>
<td>User matches all criteria: skin_id=21, country=CA, language not fr</td>
</tr>
</tbody></table>
<h3>Different Scenario</h3>
<p>If the same user had <code>&quot;language&quot;: &quot;fr&quot;</code>:</p>
<table>
<thead>
<tr>
<th>Game</th>
<th>Returned?</th>
<th>Reason</th>
</tr>
</thead>
<tbody><tr>
<td>Adventure Quest</td>
<td>No</td>
<td>State mismatch AND language excluded</td>
</tr>
<tr>
<td>King Slots</td>
<td>No</td>
<td>Language &quot;fr&quot; is in exclusions</td>
</tr>
</tbody></table>
<h2>Common Use Cases</h2>
<h3>Geographic Restrictions</h3>
<p>Limit items to specific countries:</p>
<pre><code class="language-json">{
  &quot;inclusions&quot;: {
    &quot;country&quot;: [&quot;US&quot;, &quot;CA&quot;, &quot;UK&quot;]
  }
}
</code></pre>
<h3>Regulatory Compliance</h3>
<p>Ensure items only appear for properly licensed jurisdictions:</p>
<pre><code class="language-json">{
  &quot;regulation&quot;: [&quot;UKGC&quot;],
  &quot;inclusions&quot;: {
    &quot;country&quot;: &quot;UK&quot;,
    &quot;age_verified&quot;: true
  }
}
</code></pre>
<h3>Multi-Brand/Multi-Skin</h3>
<p>Different items for different site skins:</p>
<pre><code class="language-json">{
  &quot;skin_id&quot;: [&quot;premium-brand&quot;, &quot;vip-brand&quot;]
}
</code></pre>
<h3>Language-Based Exclusions</h3>
<p>Hide items that are not translated:</p>
<pre><code class="language-json">{
  &quot;exclusions&quot;: {
    &quot;language&quot;: [&quot;ja&quot;, &quot;ko&quot;, &quot;zh&quot;]
  }
}
</code></pre>
<h2>Best Practices</h2>
<ol>
<li><strong>Start broad, then restrict</strong> - Begin with minimal filters and add restrictions as needed</li>
<li><strong>Test filter combinations</strong> - Verify that filter logic produces expected results for edge cases</li>
<li><strong>Document your rules</strong> - Maintain a reference of which filters apply to which items and why</li>
<li><strong>Use inclusions for compliance</strong> - Regulatory requirements should use inclusions to explicitly allow</li>
<li><strong>Use exclusions for exceptions</strong> - Block specific cases rather than listing all allowed values</li>
</ol>
<h2>Troubleshooting</h2>
<h3>Item Not Appearing in Recommendations</h3>
<p>Check these common causes:</p>
<ol>
<li><strong>Skin ID mismatch</strong> - Is the user&#39;s skinId in the item&#39;s skin_id list?</li>
<li><strong>Country not included</strong> - Is the user&#39;s country in inclusions?</li>
<li><strong>Trait excluded</strong> - Is any user trait in the exclusions list?</li>
<li><strong>Missing trait</strong> - If inclusions require a trait, is it present in the request?</li>
</ol>
<h3>All Items Being Filtered Out</h3>
<ol>
<li>Verify the request includes all required user attributes</li>
<li>Check for overly restrictive inclusion rules</li>
<li>Ensure at least some inventory items match the user&#39;s traits</li>
</ol>
<hr>
<h2>Related Topics</h2>
<ul>
<li><a href="#gaming-inventory">Gaming Inventory</a> - Gaming inventory field reference including availability fields</li>
<li><a href="#sports-inventory">Sports Inventory</a> - Sports inventory structure</li>
<li><a href="#ecommerce-inventory">E-commerce Inventory</a> - E-commerce product catalog setup</li>
<li><a href="#inventory-overview">Inventory Overview</a> - Introduction to inventory concepts</li>
</ul>

</section>
<section id="api-reference-overview" class="doc-section">
<h1>API Overview</h1>
<p>Opti-X provides a suite of APIs that enable you to deliver personalized experiences across your digital properties. Whether you need product recommendations, intelligent page layouts, AI-powered search, or inventory management, these APIs give you programmatic access to Opti-X&#39;s personalization engine.</p>
<h2>Why This Matters</h2>
<p>Integrating directly with Opti-X APIs gives you complete control over how and where personalization appears in your application. You can embed recommendations in any page, power search experiences, and manage your content inventory programmatically.</p>
<h2>Available APIs</h2>
<h3>Recommend API</h3>
<p>Delivers personalized item recommendations for configured placements in your application.</p>
<p><strong>Use cases:</strong></p>
<ul>
<li>Homepage carousels showing personalized products</li>
<li>&quot;You might also like&quot; sections on product pages</li>
<li>Personalized bet suggestions on sports pages</li>
<li>Game recommendations in casino lobbies</li>
</ul>
<p><a href="#recommend-api">View Recommend API Documentation</a></p>
<h3>Intelligent Layouts API</h3>
<p>Returns complete page layouts with multiple placements, enabling full-page personalization.</p>
<p><strong>Use cases:</strong></p>
<ul>
<li>Dynamically assembled homepage sections</li>
<li>Personalized landing pages with multiple recommendation areas</li>
<li>A/B testing different page configurations</li>
</ul>
<p><a href="#intelligent-layouts-api">View Intelligent Layouts API Documentation</a></p>
<h3>Smart Search API</h3>
<p>AI-powered search engine built specifically for betting and gaming sites with real-time personalization.</p>
<p><strong>Use cases:</strong></p>
<ul>
<li>Site-wide search functionality</li>
<li>Instant search suggestions as users type</li>
<li>Personalized search results based on user history</li>
</ul>
<p><a href="#smart-search-api">View Smart Search API Documentation</a></p>
<h3>Momentum API</h3>
<p>Provides access to Popular and Trending data through the Recommend API infrastructure.</p>
<p><strong>Use cases:</strong></p>
<ul>
<li>&quot;Most Popular&quot; sections</li>
<li>&quot;Trending Now&quot; widgets</li>
<li>Real-time popularity rankings</li>
</ul>
<p><a href="#momentum-api">View Momentum API Documentation</a></p>
<h3>Gaming Inventory API</h3>
<p>Enables uploading and managing your gaming inventory data within Opti-X.</p>
<p><strong>Use cases:</strong></p>
<ul>
<li>Syncing game catalogs</li>
<li>Updating game metadata</li>
<li>Validating inventory data before upload</li>
</ul>
<p><a href="#gaming-inventory-api">View Gaming Inventory API Documentation</a></p>
<h2>Authentication Summary</h2>
<p>All Opti-X APIs use header-based authentication with two required keys:</p>
<table>
<thead>
<tr>
<th>Header</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td><code>x-api-key</code></td>
<td>Your API key for authentication</td>
</tr>
<tr>
<td><code>x-brand-key</code></td>
<td>Identifies your brand within Opti-X</td>
</tr>
</tbody></table>
<p>Find your keys in the Opti-X Admin panel under <strong>Developer Tools &gt; API Keys</strong>.</p>
<p><a href="#authentication">View Full Authentication Guide</a></p>
<h2>Base URL</h2>
<p>All API requests should be made to:</p>
<pre><code>https://api.opti-x.optimove.net
</code></pre>
<h2>Response Format</h2>
<p>All APIs return JSON responses. Successful responses typically include:</p>
<ul>
<li>The requested data</li>
<li>Metadata such as request IDs and timestamps</li>
<li>For recommendations, explanations of why items were selected</li>
</ul>
<h2>Error Handling</h2>
<p>Opti-X APIs use standard HTTP status codes. Common responses include:</p>
<table>
<thead>
<tr>
<th>Code</th>
<th>Meaning</th>
</tr>
</thead>
<tbody><tr>
<td>200</td>
<td>Success</td>
</tr>
<tr>
<td>400</td>
<td>Bad request - check your request parameters</td>
</tr>
<tr>
<td>401</td>
<td>Unauthorized - check your API keys</td>
</tr>
<tr>
<td>429</td>
<td>Rate limited - slow down your requests</td>
</tr>
<tr>
<td>500</td>
<td>Server error - retry with exponential backoff</td>
</tr>
</tbody></table>
<p><a href="#error-handling">View Error Handling Guide</a></p>
<h2>Rate Limits</h2>
<p>APIs have rate limits to ensure system stability. See the <a href="#rate-limits">Rate Limits Guide</a> for details on limits per API and how to handle rate limiting.</p>
<h2>Getting Started</h2>
<ol>
<li><strong>Obtain your API keys</strong> from the Opti-X Admin panel</li>
<li><strong>Configure placements</strong> in the Admin panel for areas where you want recommendations</li>
<li><strong>Make your first API call</strong> using the examples in each API guide</li>
<li><strong>Implement feedback loops</strong> to improve personalization over time</li>
</ol>
<hr>
<h2>Related Topics</h2>
<ul>
<li><a href="#authentication">Authentication Guide</a></li>
<li><a href="#error-handling">Error Handling</a></li>
<li><a href="#rate-limits">Rate Limits</a></li>
</ul>

</section>
<section id="authentication" class="doc-section">
<h1>Authentication Guide</h1>
<p>All Opti-X APIs use header-based authentication. Every request must include valid API keys to identify your application and brand.</p>
<h2>Why This Matters</h2>
<p>Proper authentication protects your data and ensures that only authorized applications can access your personalization services. Different key types provide different access levels, allowing you to follow the principle of least privilege.</p>
<h2>Required Headers</h2>
<p>Include these headers in every API request:</p>
<table>
<thead>
<tr>
<th>Header</th>
<th>Description</th>
<th>Required</th>
</tr>
</thead>
<tbody><tr>
<td><code>x-api-key</code></td>
<td>Your API key for authentication</td>
<td>Yes</td>
</tr>
<tr>
<td><code>x-brand-key</code></td>
<td>Identifies your brand within Opti-X</td>
<td>Yes</td>
</tr>
<tr>
<td><code>content-type</code></td>
<td>Set to <code>application/json</code> for POST requests</td>
<td>Yes (for POST)</td>
</tr>
</tbody></table>
<h3>Example Request Headers</h3>
<pre><code class="language-http">POST /recommend/v1/placements/your-placement-key/recommendations HTTP/1.1
Host: api.opti-x.optimove.net
x-api-key: your-api-key-here
x-brand-key: your-brand-key-here
Content-Type: application/json
</code></pre>
<h2>API Key Types</h2>
<p>Opti-X provides three types of API keys, each with different permission levels:</p>
<h3>Public Keys (Read-Only)</h3>
<p><strong>Permissions:</strong> Read-only access to recommendation endpoints</p>
<p><strong>Use for:</strong></p>
<ul>
<li>Frontend integrations where the key may be visible in browser requests</li>
<li>Mobile applications</li>
<li>Any client-side code</li>
</ul>
<p><strong>Cannot:</strong></p>
<ul>
<li>Create or modify placements</li>
<li>Upload inventory data</li>
<li>Access administrative endpoints</li>
</ul>
<h3>User Keys (Read/Write)</h3>
<p><strong>Permissions:</strong> Read and write access to most endpoints</p>
<p><strong>Use for:</strong></p>
<ul>
<li>Backend integrations</li>
<li>Creating and editing placements programmatically</li>
<li>Managing layouts</li>
</ul>
<p><strong>Cannot:</strong></p>
<ul>
<li>Access service-level administrative functions</li>
</ul>
<h3>Service Keys (Full Access)</h3>
<p><strong>Permissions:</strong> Complete access to all API endpoints</p>
<p><strong>Use for:</strong></p>
<ul>
<li>Server-to-server integrations only</li>
<li>Inventory uploads</li>
<li>Administrative automation</li>
</ul>
<p><strong>Warning:</strong> Never expose Service keys in client-side code.</p>
<h2>Finding Your Keys</h2>
<ol>
<li>Log in to the <strong>Opti-X Admin panel</strong></li>
<li>Navigate to <strong>Developer Tools</strong> in the main menu</li>
<li>Select <strong>API Keys</strong></li>
<li>Copy the appropriate key for your use case</li>
</ol>
<p>Each brand in your organization has its own set of keys. Ensure you use the correct brand key for the property you are integrating.</p>
<h2>Security Best Practices</h2>
<h3>Never Expose Keys in Client-Side Code</h3>
<p>Public keys are designed for frontend use, but User and Service keys must stay on your server.</p>
<p><strong>Dangerous - Do not do this:</strong></p>
<pre><code class="language-javascript">// Frontend code - NEVER put User/Service keys here
const apiKey = &quot;sk_live_your_service_key&quot;; // Exposed to anyone viewing page source
</code></pre>
<p><strong>Safe approach:</strong></p>
<pre><code class="language-javascript">// Frontend code - only use Public keys
const apiKey = &quot;pk_live_your_public_key&quot;; // Safe for client-side use
</code></pre>
<p>For operations requiring User or Service keys, route requests through your backend:</p>
<pre><code class="language-javascript">// Frontend calls your backend
const response = await fetch(&#39;/api/recommendations&#39;, {
  method: &#39;POST&#39;,
  body: JSON.stringify(requestData)
});

// Your backend adds the secure key
// (server-side code)
const optixResponse = await fetch(&#39;https://api.opti-x.optimove.net/recommend/v1/...&#39;, {
  headers: {
    &#39;x-api-key&#39;: process.env.OPTIX_SERVICE_KEY, // Stored securely
    &#39;x-brand-key&#39;: process.env.OPTIX_BRAND_KEY
  }
});
</code></pre>
<h3>Rotate Keys Periodically</h3>
<ul>
<li>Rotate API keys every 90 days as a security best practice</li>
<li>Immediately rotate keys if you suspect they have been compromised</li>
<li>Update all integrations before revoking old keys</li>
</ul>
<h3>Use Environment Variables</h3>
<p>Store keys in environment variables, not in code:</p>
<pre><code class="language-bash"># .env file (never commit to version control)
OPTIX_API_KEY=your-api-key-here
OPTIX_BRAND_KEY=your-brand-key-here
</code></pre>
<pre><code class="language-javascript">// Access in code
const apiKey = process.env.OPTIX_API_KEY;
const brandKey = process.env.OPTIX_BRAND_KEY;
</code></pre>
<h3>Monitor Key Usage</h3>
<p>Review API usage in the Admin panel regularly to identify:</p>
<ul>
<li>Unexpected spikes in requests</li>
<li>Requests from unknown IP addresses</li>
<li>Failed authentication attempts</li>
</ul>
<h2>CORS Considerations</h2>
<p>When calling Opti-X APIs directly from frontend code, browsers perform CORS (Cross-Origin Resource Sharing) checks.</p>
<h3>How CORS Works with Opti-X</h3>
<ol>
<li>Your frontend JavaScript makes a request to <code>api.opti-x.optimove.net</code></li>
<li>The browser sends a preflight OPTIONS request to check permissions</li>
<li>Opti-X responds with appropriate CORS headers</li>
<li>The browser allows your actual request to proceed</li>
</ol>
<h3>Preflight Caching</h3>
<p>Browsers cache preflight responses for at least 10 minutes. This means:</p>
<ul>
<li>The first request to a new endpoint triggers a preflight check</li>
<li>Subsequent requests within the cache period skip the preflight</li>
<li>Performance impact is minimal after the initial request</li>
</ul>
<h3>Backend Proxy Alternative</h3>
<p>If you prefer to avoid CORS complexity, route requests through your own backend:</p>
<pre><code>Frontend -&gt; Your Backend -&gt; Opti-X API
</code></pre>
<p>This approach also allows you to:</p>
<ul>
<li>Use Service keys securely</li>
<li>Add custom logging</li>
<li>Implement additional caching</li>
</ul>
<h2>Authentication Errors</h2>
<table>
<thead>
<tr>
<th>Error Code</th>
<th>Meaning</th>
<th>Solution</th>
</tr>
</thead>
<tbody><tr>
<td>401</td>
<td>Missing or invalid API key</td>
<td>Verify your <code>x-api-key</code> header is present and correct</td>
</tr>
<tr>
<td>403</td>
<td>Key lacks required permissions</td>
<td>Use a key type with appropriate access level</td>
</tr>
<tr>
<td>403</td>
<td>Invalid brand key</td>
<td>Verify your <code>x-brand-key</code> matches your brand</td>
</tr>
</tbody></table>
<h3>Example Error Response</h3>
<pre><code class="language-json">{
  &quot;error&quot;: {
    &quot;code&quot;: &quot;UNAUTHORIZED&quot;,
    &quot;message&quot;: &quot;Invalid API key provided&quot;,
    &quot;details&quot;: &quot;The x-api-key header is missing or contains an invalid key&quot;
  }
}
</code></pre>
<hr>
<h2>Related Topics</h2>
<ul>
<li><a href="#api-reference-overview">API Overview</a></li>
<li><a href="#error-handling">Error Handling</a></li>
<li><a href="#rate-limits">Rate Limits</a></li>
</ul>

</section>
<section id="recommend-api" class="doc-section">
<h1>Recommend API</h1>
<p>The Recommend API delivers personalized item recommendations for configured placements in your application.</p>
<h2>What is a Placement?</h2>
<p>A <strong>placement</strong> is a configured location in your application where personalized recommendations appear. Examples include:</p>
<ul>
<li>A homepage carousel showing &quot;Recommended for You&quot;</li>
<li>A product page sidebar with &quot;You Might Also Like&quot;</li>
<li>A checkout page with &quot;Frequently Bought Together&quot;</li>
<li>A sports betting page with &quot;Bets for You&quot;</li>
</ul>
<p>You configure placements in the Opti-X Admin panel, defining rules like:</p>
<ul>
<li>What type of items to recommend (games, products, bets)</li>
<li>How many items to return</li>
<li>What recommendation strategy to use (personalized, popular, similar items)</li>
</ul>
<p>Each placement receives a unique <code>placementKey</code> that you use when calling this API.</p>
<h2>Why This Matters</h2>
<p>The Recommend API is the core of Opti-X personalization. By providing context about where the user is and what they are doing, you enable the recommendation engine to deliver highly relevant suggestions that increase engagement and conversion.</p>
<h2>Endpoint</h2>
<pre><code>POST https://api.opti-x.optimove.net/recommend/v1/placements/{placementKey}/recommendations
</code></pre>
<p>Replace <code>{placementKey}</code> with your placement&#39;s unique key from the Admin panel.</p>
<h2>Headers</h2>
<table>
<thead>
<tr>
<th>Header</th>
<th>Description</th>
<th>Required</th>
</tr>
</thead>
<tbody><tr>
<td><code>x-api-key</code></td>
<td>Your API key</td>
<td>Yes</td>
</tr>
<tr>
<td><code>x-brand-key</code></td>
<td>Your brand identifier</td>
<td>Yes</td>
</tr>
<tr>
<td><code>content-type</code></td>
<td>Must be <code>application/json</code></td>
<td>Yes</td>
</tr>
</tbody></table>
<h2>Request Parameters</h2>
<h3>Core Parameters</h3>
<table>
<thead>
<tr>
<th>Parameter</th>
<th>Type</th>
<th>Required</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td><code>userId</code></td>
<td>String</td>
<td>Yes</td>
<td>Unique identifier for the user. For anonymous users, use a session ID.</td>
</tr>
<tr>
<td><code>type</code></td>
<td>String</td>
<td>Yes</td>
<td>Set to <code>&quot;recommendation&quot;</code> for this endpoint.</td>
</tr>
<tr>
<td><code>context</code></td>
<td>Object</td>
<td>Yes</td>
<td>Information about where the user currently is in your application.</td>
</tr>
</tbody></table>
<h3>Context Object</h3>
<p>The context object tells the recommendation engine about the user&#39;s current situation.</p>
<table>
<thead>
<tr>
<th>Parameter</th>
<th>Type</th>
<th>Required</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td><code>context.product</code></td>
<td>String</td>
<td>No</td>
<td>The product vertical: <code>&quot;Gaming&quot;</code>, <code>&quot;Sports&quot;</code>, or <code>&quot;Ecommerce&quot;</code></td>
</tr>
<tr>
<td><code>context.category</code></td>
<td>String</td>
<td>No</td>
<td>The category the user is viewing (e.g., <code>&quot;Slots&quot;</code>, <code>&quot;Football&quot;</code>, <code>&quot;Laptops&quot;</code>)</td>
</tr>
<tr>
<td><code>context.currentItemId</code></td>
<td>String</td>
<td>No</td>
<td>For product pages, the ID of the item being viewed</td>
</tr>
<tr>
<td><code>context.page</code></td>
<td>Object</td>
<td>No</td>
<td>Details about the current page</td>
</tr>
<tr>
<td><code>context.page.url</code></td>
<td>String</td>
<td>No</td>
<td>URL of the current page</td>
</tr>
<tr>
<td><code>context.page.title</code></td>
<td>String</td>
<td>No</td>
<td>Title of the current page</td>
</tr>
<tr>
<td><code>context.channel</code></td>
<td>String</td>
<td>No</td>
<td>Device type: <code>&quot;Mobile&quot;</code>, <code>&quot;Desktop&quot;</code>, <code>&quot;Tablet&quot;</code>, or <code>&quot;App&quot;</code></td>
</tr>
</tbody></table>
<h3>Traits Object (Optional)</h3>
<p>Use traits to pass additional context that does not fit standard fields.</p>
<table>
<thead>
<tr>
<th>Parameter</th>
<th>Type</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td><code>traits.contextId</code></td>
<td>String</td>
<td>A session or page-specific identifier</td>
</tr>
<tr>
<td><code>traits.customerSegment</code></td>
<td>String</td>
<td>Custom segment identifier</td>
</tr>
</tbody></table>
<h3>Exclusions (Optional)</h3>
<p>Prevent specific items from appearing in recommendations.</p>
<table>
<thead>
<tr>
<th>Parameter</th>
<th>Type</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td><code>recommendation.target.exclusions.additionalItemList</code></td>
<td>Array</td>
<td>List of item IDs to exclude (e.g., items already in cart)</td>
</tr>
<tr>
<td><code>recommendation.target.exclusions.inBetSlip</code></td>
<td>Boolean</td>
<td>Sports only: Set to <code>true</code> if displaying on bet slip</td>
</tr>
</tbody></table>
<hr>
<h2>Gaming Example</h2>
<p>Request recommendations for a user browsing the Slots category on mobile.</p>
<h3>Request</h3>
<pre><code class="language-bash">curl -X POST &quot;https://api.opti-x.optimove.net/recommend/v1/placements/slots-homepage-carousel/recommendations&quot; \
  -H &quot;x-api-key: your-api-key&quot; \
  -H &quot;x-brand-key: your-brand-key&quot; \
  -H &quot;Content-Type: application/json&quot; \
  -d &#39;{
    &quot;userId&quot;: &quot;user_12345&quot;,
    &quot;type&quot;: &quot;recommendation&quot;,
    &quot;context&quot;: {
      &quot;product&quot;: &quot;Gaming&quot;,
      &quot;category&quot;: &quot;Slots&quot;,
      &quot;page&quot;: {
        &quot;url&quot;: &quot;https://casino.example.com/slots&quot;,
        &quot;title&quot;: &quot;Slots - Our Casino&quot;
      },
      &quot;channel&quot;: &quot;Mobile&quot;
    }
  }&#39;
</code></pre>
<h3>Response</h3>
<pre><code class="language-json">{
  &quot;recommendation&quot;: {
    &quot;result&quot;: [
      {
        &quot;game&quot;: {
          &quot;game_code&quot;: &quot;megaways_fortune&quot;,
          &quot;name&quot;: &quot;Megaways Fortune&quot;,
          &quot;score&quot;: 0.89,
          &quot;rank&quot;: 1
        }
      },
      {
        &quot;game&quot;: {
          &quot;game_code&quot;: &quot;rainbow_jackpot&quot;,
          &quot;name&quot;: &quot;Rainbow Jackpot&quot;,
          &quot;score&quot;: 0.82,
          &quot;rank&quot;: 2
        }
      }
    ],
    &quot;recId&quot;: &quot;rec-gaming-a1b2c3d4-e5f6-7890-abcd-ef1234567890&quot;,
    &quot;recDateTime&quot;: &quot;2025-01-15T14:30:00Z&quot;,
    &quot;explanation&quot;: {
      &quot;reason&quot;: &quot;personalized&quot;,
      &quot;tag_type&quot;: &quot;portlet&quot;,
      &quot;tag&quot;: &quot;Recommended for You&quot;
    }
  }
}
</code></pre>
<hr>
<h2>Sports Example</h2>
<p>Request recommendations for a Football page, excluding items already in the user&#39;s bet slip.</p>
<h3>Request</h3>
<pre><code class="language-bash">curl -X POST &quot;https://api.opti-x.optimove.net/recommend/v1/placements/football-suggestions/recommendations&quot; \
  -H &quot;x-api-key: your-api-key&quot; \
  -H &quot;x-brand-key: your-brand-key&quot; \
  -H &quot;Content-Type: application/json&quot; \
  -d &#39;{
    &quot;userId&quot;: &quot;user_67890&quot;,
    &quot;type&quot;: &quot;recommendation&quot;,
    &quot;context&quot;: {
      &quot;product&quot;: &quot;Sports&quot;,
      &quot;category&quot;: &quot;Football&quot;,
      &quot;page&quot;: {
        &quot;url&quot;: &quot;https://sports.example.com/football&quot;,
        &quot;title&quot;: &quot;Football Betting&quot;
      }
    },
    &quot;recommendation&quot;: {
      &quot;target&quot;: {
        &quot;exclusions&quot;: {
          &quot;inBetSlip&quot;: false,
          &quot;additionalItemList&quot;: [832831914, 832831920]
        }
      }
    }
  }&#39;
</code></pre>
<h3>Response</h3>
<pre><code class="language-json">{
  &quot;recommendation&quot;: {
    &quot;result&quot;: [
      {
        &quot;selection&quot;: {
          &quot;selectionKey&quot;: 1196055705,
          &quot;selectionName&quot;: &quot;Manchester United&quot;,
          &quot;marketName&quot;: &quot;Match Result&quot;,
          &quot;eventName&quot;: &quot;Man Utd vs Liverpool&quot;,
          &quot;score&quot;: 0.75,
          &quot;rank&quot;: 1
        }
      }
    ],
    &quot;recId&quot;: &quot;rec-sports-d4e5f6a7-b8c9-0123-defg-456789abcdef&quot;,
    &quot;recDateTime&quot;: &quot;2025-01-15T14:35:00Z&quot;
  }
}
</code></pre>
<p>The <code>additionalItemList</code> ensures that selections 832831914 and 832831920 (already in the bet slip) are not recommended again.</p>
<hr>
<h2>E-commerce Example</h2>
<p>Request recommendations for a user viewing a specific laptop, excluding items already in their cart.</p>
<h3>Request</h3>
<pre><code class="language-bash">curl -X POST &quot;https://api.opti-x.optimove.net/recommend/v1/placements/pdp-also-like/recommendations&quot; \
  -H &quot;x-api-key: your-api-key&quot; \
  -H &quot;x-brand-key: your-brand-key&quot; \
  -H &quot;Content-Type: application/json&quot; \
  -d &#39;{
    &quot;userId&quot;: &quot;user_ecom_12345&quot;,
    &quot;type&quot;: &quot;recommendation&quot;,
    &quot;context&quot;: {
      &quot;product&quot;: &quot;Ecommerce&quot;,
      &quot;category&quot;: &quot;Electronics - Laptops&quot;,
      &quot;currentItemId&quot;: &quot;SKU_LAPTOP_PRO_15&quot;,
      &quot;page&quot;: {
        &quot;url&quot;: &quot;https://shop.example.com/products/laptop-pro-15&quot;,
        &quot;title&quot;: &quot;Laptop Pro 15 - Product Details&quot;
      },
      &quot;channel&quot;: &quot;Desktop&quot;
    },
    &quot;traits&quot;: {
      &quot;customerSegment&quot;: &quot;premium_member&quot;
    },
    &quot;recommendation&quot;: {
      &quot;target&quot;: {
        &quot;exclusions&quot;: {
          &quot;additionalItemList&quot;: [&quot;SKU_MOUSE_WIRELESS&quot;, &quot;SKU_USB_HUB&quot;]
        }
      }
    }
  }&#39;
</code></pre>
<h3>Response</h3>
<pre><code class="language-json">{
  &quot;recommendation&quot;: {
    &quot;result&quot;: [
      {
        &quot;item&quot;: {
          &quot;item_id&quot;: &quot;SKU_LAPTOP_STAND&quot;,
          &quot;name&quot;: &quot;Ergonomic Laptop Stand&quot;,
          &quot;brand_name&quot;: &quot;ComfortView&quot;,
          &quot;category_path&quot;: &quot;Accessories - Stands&quot;,
          &quot;price&quot;: 49.99,
          &quot;currency_code&quot;: &quot;USD&quot;,
          &quot;thumbnail_url&quot;: &quot;https://shop.example.com/images/laptop-stand.jpg&quot;,
          &quot;product_url&quot;: &quot;https://shop.example.com/products/laptop-stand&quot;,
          &quot;in_stock&quot;: true,
          &quot;score&quot;: 0.92,
          &quot;rank&quot;: 1
        }
      },
      {
        &quot;item&quot;: {
          &quot;item_id&quot;: &quot;SKU_LAPTOP_SLEEVE&quot;,
          &quot;name&quot;: &quot;Premium Laptop Sleeve 15\&quot;&quot;,
          &quot;brand_name&quot;: &quot;TechCarry&quot;,
          &quot;category_path&quot;: &quot;Accessories - Cases&quot;,
          &quot;price&quot;: 39.99,
          &quot;currency_code&quot;: &quot;USD&quot;,
          &quot;thumbnail_url&quot;: &quot;https://shop.example.com/images/laptop-sleeve.jpg&quot;,
          &quot;product_url&quot;: &quot;https://shop.example.com/products/laptop-sleeve&quot;,
          &quot;in_stock&quot;: true,
          &quot;score&quot;: 0.88,
          &quot;rank&quot;: 2
        }
      }
    ],
    &quot;recId&quot;: &quot;rec-ecom-f7g8h9i0-j1k2-3456-lmno-789012pqrstu&quot;,
    &quot;recDateTime&quot;: &quot;2025-01-15T14:40:00Z&quot;,
    &quot;explanation&quot;: {
      &quot;reason&quot;: &quot;Cross-sell based on viewed item SKU_LAPTOP_PRO_15&quot;,
      &quot;tag_type&quot;: &quot;product_detail_page&quot;,
      &quot;tag&quot;: &quot;Frequently Bought Together&quot;
    }
  }
}
</code></pre>
<hr>
<h2>Response Fields</h2>
<h3>Common Fields</h3>
<table>
<thead>
<tr>
<th>Field</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td><code>recommendation.result</code></td>
<td>Array of recommended items</td>
</tr>
<tr>
<td><code>recommendation.recId</code></td>
<td>Unique identifier for this recommendation (use for logging and feedback)</td>
</tr>
<tr>
<td><code>recommendation.recDateTime</code></td>
<td>When the recommendation was generated</td>
</tr>
<tr>
<td><code>recommendation.explanation</code></td>
<td>Why these items were recommended</td>
</tr>
</tbody></table>
<h3>Item Fields</h3>
<p>Each item in the result array contains fields specific to its type:</p>
<p><strong>Gaming:</strong></p>
<ul>
<li><code>game.game_code</code> - Unique game identifier</li>
<li><code>game.name</code> - Display name</li>
<li><code>game.score</code> - Relevance score (0-1)</li>
<li><code>game.rank</code> - Position in recommendation list</li>
</ul>
<p><strong>Sports:</strong></p>
<ul>
<li><code>selection.selectionKey</code> - Unique selection identifier</li>
<li><code>selection.selectionName</code> - Selection name (e.g., team name)</li>
<li><code>selection.marketName</code> - Market type (e.g., &quot;Match Result&quot;)</li>
<li><code>selection.eventName</code> - Event name</li>
</ul>
<p><strong>E-commerce:</strong></p>
<ul>
<li><code>item.item_id</code> - Product SKU</li>
<li><code>item.name</code> - Product name</li>
<li><code>item.price</code> - Current price</li>
<li><code>item.in_stock</code> - Availability status</li>
</ul>
<hr>
<h2>Error Handling</h2>
<h3>Empty Results</h3>
<p>A 200 response with an empty <code>result</code> array indicates no suitable recommendations were found:</p>
<pre><code class="language-json">{
  &quot;recommendation&quot;: {
    &quot;result&quot;: [],
    &quot;recId&quot;: &quot;rec-empty-a1b2c3d4&quot;,
    &quot;recDateTime&quot;: &quot;2025-01-15T14:45:00Z&quot;
  }
}
</code></pre>
<p>Your application should handle this gracefully, perhaps showing a fallback section or hiding the recommendation area.</p>
<h3>Error Responses</h3>
<table>
<thead>
<tr>
<th>Status Code</th>
<th>Meaning</th>
<th>Action</th>
</tr>
</thead>
<tbody><tr>
<td>400</td>
<td>Invalid request body</td>
<td>Check your JSON structure and required fields</td>
</tr>
<tr>
<td>401</td>
<td>Authentication failed</td>
<td>Verify your API keys</td>
</tr>
<tr>
<td>404</td>
<td>Placement not found</td>
<td>Check the placementKey exists in your Admin panel</td>
</tr>
<tr>
<td>429</td>
<td>Rate limited</td>
<td>Implement backoff and retry</td>
</tr>
<tr>
<td>500</td>
<td>Server error</td>
<td>Retry with exponential backoff</td>
</tr>
</tbody></table>
<h3>Example Error Response</h3>
<pre><code class="language-json">{
  &quot;error&quot;: {
    &quot;code&quot;: &quot;INVALID_REQUEST&quot;,
    &quot;message&quot;: &quot;Missing required field: userId&quot;,
    &quot;details&quot;: &quot;The userId field is required for all recommendation requests&quot;
  }
}
</code></pre>
<hr>
<h2>Best Practices</h2>
<h3>Provide Rich Context</h3>
<p>The more context you provide, the better the recommendations:</p>
<pre><code class="language-json">{
  &quot;context&quot;: {
    &quot;product&quot;: &quot;Gaming&quot;,
    &quot;category&quot;: &quot;Slots&quot;,
    &quot;page&quot;: {
      &quot;url&quot;: &quot;https://casino.example.com/slots/megaways&quot;,
      &quot;title&quot;: &quot;Megaways Slots&quot;
    },
    &quot;channel&quot;: &quot;Mobile&quot;
  }
}
</code></pre>
<h3>Always Send User ID</h3>
<p>Even for anonymous users, send a consistent session-based ID to enable session personalization:</p>
<pre><code class="language-json">{
  &quot;userId&quot;: &quot;anon_session_abc123xyz&quot;
}
</code></pre>
<h3>Keep Exclusions Updated</h3>
<p>For sports betting, always send the current bet slip contents in <code>additionalItemList</code> to avoid redundant recommendations.</p>
<h3>Log the recId</h3>
<p>Store the <code>recId</code> from responses for:</p>
<ul>
<li>Debugging issues</li>
<li>Implementing feedback loops</li>
<li>Analytics and reporting</li>
</ul>
<hr>
<h2>Related Topics</h2>
<ul>
<li><a href="#api-reference-overview">API Overview</a></li>
<li><a href="#authentication">Authentication Guide</a></li>
<li><a href="#intelligent-layouts-api">Intelligent Layouts API</a> - For multiple placements in one request</li>
<li><a href="#error-handling">Error Handling</a></li>
</ul>

</section>
<section id="smart-search-api" class="doc-section">
<h1>Smart Search API</h1>
<p>The Smart Search API provides AI-powered search functionality built specifically for betting and gaming sites.</p>
<h2>What is Smart Search?</h2>
<p>Smart Search is an intelligent search engine that goes beyond simple keyword matching. It provides:</p>
<h3>AI-Powered Personalization</h3>
<p>Smart Search learns from each user&#39;s behavior to deliver personalized results. If a user frequently bets on Premier League football, their search for &quot;match&quot; will prioritize Premier League matches over other sports.</p>
<h3>Typo Correction and Fuzzy Matching</h3>
<p>Users often misspell team names or make typing errors on mobile devices. Smart Search automatically corrects common mistakes:</p>
<ul>
<li>&quot;Mancehster&quot; matches &quot;Manchester&quot;</li>
<li>&quot;Liverpol&quot; matches &quot;Liverpool&quot;</li>
<li>&quot;Arsneal&quot; matches &quot;Arsenal&quot;</li>
</ul>
<h3>Self-Learning Optimization</h3>
<p>The search engine improves over time by analyzing:</p>
<ul>
<li>Which results users click on</li>
<li>Conversion rates (bets placed, games launched)</li>
<li>Search patterns and trends</li>
</ul>
<p>When users consistently click on a specific result for a query, Smart Search learns that association and ranks that result higher for future searches.</p>
<h3>Real-Time Inventory Indexing</h3>
<p>Smart Search maintains a constantly updated index of your inventory:</p>
<ul>
<li>Sports events, markets, and selections as they become available</li>
<li>Gaming catalogs with new releases</li>
<li>Results returned in approximately 10ms</li>
</ul>
<h3>Partial Matching</h3>
<p>Users can find results without typing complete terms:</p>
<ul>
<li>&quot;rom&quot; matches &quot;Roma&quot;, &quot;Roman&quot;, &quot;Romania&quot;</li>
<li>&quot;kin&quot; matches &quot;King&quot;, &quot;Kingdom&quot;, &quot;Viking&quot;</li>
</ul>
<h2>Why This Matters</h2>
<p>A fast, accurate search experience directly impacts user engagement and conversion. Users who find what they want quickly are more likely to complete bets or play games. Smart Search reduces friction and increases the likelihood of conversion.</p>
<h2>Inventory Integration</h2>
<p>Smart Search requires access to your inventory data to function. For gaming, this means your game catalog. For sports, this means your events, markets, and selections feed.</p>
<p>If you have already integrated inventory data for other Opti-X products (Recommend, Intelligent Layouts), Smart Search can use that same data source.</p>
<h2>Search Endpoint</h2>
<pre><code>POST https://api.opti-x.optimove.net/search/v1/query
</code></pre>
<h3>Headers</h3>
<table>
<thead>
<tr>
<th>Header</th>
<th>Description</th>
<th>Required</th>
</tr>
</thead>
<tbody><tr>
<td><code>x-api-key</code></td>
<td>Your API key</td>
<td>Yes</td>
</tr>
<tr>
<td><code>x-brand-key</code></td>
<td>Your brand identifier</td>
<td>Yes</td>
</tr>
<tr>
<td><code>content-type</code></td>
<td>Must be <code>application/json</code></td>
<td>Yes</td>
</tr>
</tbody></table>
<h3>Request Parameters</h3>
<table>
<thead>
<tr>
<th>Parameter</th>
<th>Type</th>
<th>Required</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td><code>query</code></td>
<td>String</td>
<td>Yes</td>
<td>The user&#39;s search text (minimum 2 characters)</td>
</tr>
<tr>
<td><code>userId</code></td>
<td>String</td>
<td>Yes</td>
<td>User identifier for personalization</td>
</tr>
<tr>
<td><code>type</code></td>
<td>String</td>
<td>Yes</td>
<td>Must be <code>&quot;search&quot;</code></td>
</tr>
<tr>
<td><code>context</code></td>
<td>Object</td>
<td>No</td>
<td>Current page and device context</td>
</tr>
<tr>
<td><code>context.product</code></td>
<td>String</td>
<td>No</td>
<td><code>&quot;Sports&quot;</code> or <code>&quot;Gaming&quot;</code></td>
</tr>
<tr>
<td><code>context.category</code></td>
<td>String</td>
<td>No</td>
<td>Current category</td>
</tr>
<tr>
<td><code>context.channel</code></td>
<td>String</td>
<td>No</td>
<td>Device type</td>
</tr>
</tbody></table>
<h3>Example Request</h3>
<pre><code class="language-bash">curl -X POST &quot;https://api.opti-x.optimove.net/search/v1/query&quot; \
  -H &quot;x-api-key: your-api-key&quot; \
  -H &quot;x-brand-key: your-brand-key&quot; \
  -H &quot;Content-Type: application/json&quot; \
  -d &#39;{
    &quot;query&quot;: &quot;manchester&quot;,
    &quot;userId&quot;: &quot;user_12345&quot;,
    &quot;type&quot;: &quot;search&quot;,
    &quot;context&quot;: {
      &quot;product&quot;: &quot;Sports&quot;,
      &quot;category&quot;: &quot;Football&quot;,
      &quot;channel&quot;: &quot;Mobile&quot;
    }
  }&#39;
</code></pre>
<h2>Sports Search Response</h2>
<pre><code class="language-json">{
  &quot;results&quot;: {
    &quot;searchId&quot;: &quot;search-a1b2c3d4-e5f6-7890-abcd-ef1234567890&quot;,
    &quot;result_count&quot;: 45,
    &quot;execution_time&quot;: 8.5,
    &quot;query&quot;: &quot;manchester&quot;,
    &quot;matched_tokens&quot;: [&quot;manchester&quot;],
    &quot;search_results&quot;: [
      {
        &quot;categoryName&quot;: &quot;Football&quot;,
        &quot;classes&quot;: [
          {
            &quot;className&quot;: &quot;English&quot;,
            &quot;types&quot;: [
              {
                &quot;typeName&quot;: &quot;Premier League&quot;,
                &quot;matched_events&quot;: [
                  {
                    &quot;eventKey&quot;: &quot;evt_123456&quot;,
                    &quot;eventName&quot;: &quot;Manchester United vs Liverpool&quot;,
                    &quot;eventDateTime&quot;: &quot;2025-01-20T15:00:00Z&quot;,
                    &quot;typeName&quot;: &quot;Premier League&quot;,
                    &quot;className&quot;: &quot;English&quot;,
                    &quot;categoryName&quot;: &quot;Football&quot;,
                    &quot;markets&quot;: [
                      {
                        &quot;marketName&quot;: &quot;Match Result&quot;,
                        &quot;marketKey&quot;: &quot;mkt_789012&quot;,
                        &quot;selections&quot;: [
                          {
                            &quot;selectionKey&quot;: &quot;sel_111111&quot;,
                            &quot;selectionName&quot;: &quot;Manchester United&quot;,
                            &quot;decPrice&quot;: 2.50,
                            &quot;score&quot;: 0.95
                          },
                          {
                            &quot;selectionKey&quot;: &quot;sel_222222&quot;,
                            &quot;selectionName&quot;: &quot;Draw&quot;,
                            &quot;decPrice&quot;: 3.25,
                            &quot;score&quot;: 0.85
                          },
                          {
                            &quot;selectionKey&quot;: &quot;sel_333333&quot;,
                            &quot;selectionName&quot;: &quot;Liverpool&quot;,
                            &quot;decPrice&quot;: 2.75,
                            &quot;score&quot;: 0.80
                          }
                        ]
                      }
                    ]
                  }
                ],
                &quot;matched_selections&quot;: []
              }
            ]
          }
        ]
      }
    ]
  }
}
</code></pre>
<h3>Sports Response Fields</h3>
<table>
<thead>
<tr>
<th>Field</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td><code>searchId</code></td>
<td>Unique identifier for this search (use for click tracking)</td>
</tr>
<tr>
<td><code>result_count</code></td>
<td>Total number of matching items</td>
</tr>
<tr>
<td><code>execution_time</code></td>
<td>Search time in milliseconds</td>
</tr>
<tr>
<td><code>matched_tokens</code></td>
<td>Terms that matched in the search</td>
</tr>
<tr>
<td><code>search_results</code></td>
<td>Hierarchical results organized by category &gt; class &gt; type</td>
</tr>
<tr>
<td><code>matched_events</code></td>
<td>Events matching the search term</td>
</tr>
<tr>
<td><code>matched_selections</code></td>
<td>Individual selections matching the search term</td>
</tr>
</tbody></table>
<h2>Gaming Search Response</h2>
<pre><code class="language-json">{
  &quot;results&quot;: {
    &quot;searchId&quot;: &quot;search-g1h2i3j4-k5l6-7890-mnop-qr1234567890&quot;,
    &quot;result_count&quot;: 12,
    &quot;rec_count&quot;: 8,
    &quot;execution_time&quot;: 6.2,
    &quot;query&quot;: &quot;rainbow&quot;,
    &quot;matched_tokens&quot;: [&quot;rainbow&quot;],
    &quot;search_results&quot;: [
      {
        &quot;gamecode&quot;: &quot;rainbow_riches_megaways&quot;,
        &quot;gamename&quot;: &quot;Rainbow Riches Megaways&quot;,
        &quot;game_category&quot;: &quot;Casino&quot;,
        &quot;game_class&quot;: &quot;Slots&quot;,
        &quot;theme&quot;: &quot;Irish&quot;,
        &quot;provider&quot;: &quot;Barcrest&quot;,
        &quot;score&quot;: 0.95
      },
      {
        &quot;gamecode&quot;: &quot;rainbow_jackpots&quot;,
        &quot;gamename&quot;: &quot;Rainbow Jackpots&quot;,
        &quot;game_category&quot;: &quot;Casino&quot;,
        &quot;game_class&quot;: &quot;Slots&quot;,
        &quot;theme&quot;: &quot;Irish&quot;,
        &quot;provider&quot;: &quot;Red Tiger&quot;,
        &quot;score&quot;: 0.88
      }
    ],
    &quot;rec_results&quot;: [
      {
        &quot;gamecode&quot;: &quot;luck_o_irish&quot;,
        &quot;gamename&quot;: &quot;Luck O&#39; The Irish&quot;,
        &quot;game_category&quot;: &quot;Casino&quot;,
        &quot;game_class&quot;: &quot;Slots&quot;,
        &quot;theme&quot;: &quot;Irish&quot;,
        &quot;provider&quot;: &quot;Blueprint&quot;,
        &quot;score&quot;: 0.72
      }
    ]
  }
}
</code></pre>
<h3>Gaming Response Fields</h3>
<table>
<thead>
<tr>
<th>Field</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td><code>search_results</code></td>
<td>Games directly matching the search term</td>
</tr>
<tr>
<td><code>rec_results</code></td>
<td>Additional recommended games based on the search and user preferences</td>
</tr>
</tbody></table>
<p>We recommend displaying both sections in your UI. Show <code>search_results</code> as the primary results, then show <code>rec_results</code> under a heading like &quot;Also Recommended&quot; or &quot;You Might Like&quot;.</p>
<h2>Advanced Search Syntax</h2>
<p>Power users can use special syntax in their queries:</p>
<table>
<thead>
<tr>
<th>Syntax</th>
<th>Description</th>
<th>Example</th>
</tr>
</thead>
<tbody><tr>
<td><code>price:X-Y</code></td>
<td>Filter by odds range</td>
<td><code>tottenham price:2-5</code></td>
</tr>
<tr>
<td><code>orderby:time_desc</code></td>
<td>Sort by time descending</td>
<td><code>football orderby:time_desc</code></td>
</tr>
</tbody></table>
<h2>Popular Searches Endpoint</h2>
<p>Display popular search terms to help users discover content before they start typing.</p>
<pre><code>GET https://api.opti-x.optimove.net/search/v1/popular
</code></pre>
<h3>Headers</h3>
<table>
<thead>
<tr>
<th>Header</th>
<th>Description</th>
<th>Required</th>
</tr>
</thead>
<tbody><tr>
<td><code>x-api-key</code></td>
<td>Your API key</td>
<td>Yes</td>
</tr>
<tr>
<td><code>x-brand-key</code></td>
<td>Your brand identifier</td>
<td>Yes</td>
</tr>
</tbody></table>
<h3>Response</h3>
<pre><code class="language-json">{
  &quot;result&quot;: {
    &quot;execution_time&quot;: 1.2,
    &quot;popular_searches&quot;: [
      &quot;premier league&quot;,
      &quot;champions league&quot;,
      &quot;horse racing&quot;,
      &quot;tennis&quot;,
      &quot;rainbow riches&quot;
    ]
  }
}
</code></pre>
<p>Display these as search suggestions when the search box is focused but empty.</p>
<h2>Click Tracking</h2>
<p>To enable the self-learning features, send a click event whenever a user selects a search result.</p>
<pre><code>POST https://api.opti-x.optimove.net/search/v1/click
</code></pre>
<h3>Headers</h3>
<table>
<thead>
<tr>
<th>Header</th>
<th>Description</th>
<th>Required</th>
</tr>
</thead>
<tbody><tr>
<td><code>x-api-key</code></td>
<td>Your API key</td>
<td>Yes</td>
</tr>
<tr>
<td><code>x-brand-key</code></td>
<td>Your brand identifier</td>
<td>Yes</td>
</tr>
<tr>
<td><code>content-type</code></td>
<td>Must be <code>application/json</code></td>
<td>Yes</td>
</tr>
</tbody></table>
<h3>Request Body</h3>
<pre><code class="language-json">{
  &quot;type&quot;: &quot;track&quot;,
  &quot;userId&quot;: &quot;user_12345&quot;,
  &quot;properties&quot;: {
    &quot;event_type&quot;: &quot;search&quot;,
    &quot;event_name&quot;: &quot;SEARCH_CLICK&quot;,
    &quot;event_value&quot;: 1,
    &quot;event_info_1&quot;: &quot;manchester&quot;,
    &quot;event_info_2&quot;: &quot;search-a1b2c3d4-e5f6-7890-abcd-ef1234567890&quot;,
    &quot;event_ref_id&quot;: &quot;sel_111111&quot;,
    &quot;event_ref_type&quot;: &quot;selection&quot;
  },
  &quot;timestamp&quot;: &quot;2025-01-15T14:35:00.000Z&quot;,
  &quot;sentAt&quot;: &quot;2025-01-15T14:35:00.000Z&quot;,
  &quot;writeKey&quot;: &quot;&quot;,
  &quot;messageId&quot;: &quot;&quot;
}
</code></pre>
<h3>Click Tracking Parameters</h3>
<table>
<thead>
<tr>
<th>Parameter</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td><code>userId</code></td>
<td>Same user ID used in the search request</td>
</tr>
<tr>
<td><code>event_value</code></td>
<td>Rank position of the clicked result (1 = first)</td>
</tr>
<tr>
<td><code>event_info_1</code></td>
<td>The original search query</td>
</tr>
<tr>
<td><code>event_info_2</code></td>
<td>The <code>searchId</code> from the search response</td>
</tr>
<tr>
<td><code>event_ref_id</code></td>
<td>Identifier of the clicked item (selection key, game code, etc.)</td>
</tr>
<tr>
<td><code>event_ref_type</code></td>
<td>Type of item: <code>&quot;selection&quot;</code>, <code>&quot;market&quot;</code>, <code>&quot;event&quot;</code>, <code>&quot;game&quot;</code></td>
</tr>
</tbody></table>
<h2>Implementation Best Practices</h2>
<h3>Debouncing</h3>
<p>Implement debouncing to avoid making requests on every keystroke. We recommend waiting 250ms after the last keystroke before sending a request:</p>
<pre><code class="language-javascript">let debounceTimer;

function handleSearchInput(query) {
  clearTimeout(debounceTimer);
  debounceTimer = setTimeout(() =&gt; {
    if (query.length &gt;= 2) {
      performSearch(query);
    }
  }, 250);
}
</code></pre>
<h3>Minimum Query Length</h3>
<p>The API requires at least 2 characters before returning results. Do not call the API until the user has typed at least 2 characters.</p>
<h3>Response Compression</h3>
<p>Search responses can be large. The API returns gzip-compressed responses by default. Most HTTP client libraries handle decompression automatically.</p>
<h3>CORS</h3>
<p>When calling the API directly from frontend JavaScript, browsers send a preflight OPTIONS request. These are cached for at least 10 minutes, so subsequent requests skip the preflight check.</p>
<h2>Error Handling</h2>
<table>
<thead>
<tr>
<th>Status Code</th>
<th>Meaning</th>
<th>Action</th>
</tr>
</thead>
<tbody><tr>
<td>400</td>
<td>Invalid query (too short or malformed)</td>
<td>Check query length is at least 2 characters</td>
</tr>
<tr>
<td>401</td>
<td>Authentication failed</td>
<td>Verify your API keys</td>
</tr>
<tr>
<td>429</td>
<td>Rate limited</td>
<td>Implement backoff; check debouncing</td>
</tr>
<tr>
<td>500</td>
<td>Server error</td>
<td>Retry with exponential backoff</td>
</tr>
</tbody></table>
<hr>
<h2>Related Topics</h2>
<ul>
<li><a href="#api-reference-overview">API Overview</a></li>
<li><a href="#authentication">Authentication Guide</a></li>
<li><a href="#recommend-api">Recommend API</a></li>
<li><a href="#error-handling">Error Handling</a></li>
</ul>

</section>
<section id="intelligent-layouts-api" class="doc-section">
<h1>Intelligent Layouts API</h1>
<p>The Intelligent Layouts API returns complete page layouts with multiple placements in a single request, enabling full-page personalization.</p>
<h2>When to Use Intelligent Layouts</h2>
<p>Use the <strong>Intelligent Layouts API</strong> when you need to:</p>
<ul>
<li>Populate an entire page with multiple recommendation sections</li>
<li>Let Opti-X decide which placements to show and in what order</li>
<li>Implement dynamic page structures that adapt to each user</li>
</ul>
<p>Use the <strong>Recommend API</strong> when you need to:</p>
<ul>
<li>Fetch recommendations for a single, specific location</li>
<li>Have full control over which placements appear where</li>
<li>Make independent calls for different page sections</li>
</ul>
<h3>Example Scenario</h3>
<p>Imagine a casino homepage with several personalized sections:</p>
<ul>
<li>&quot;Recommended for You&quot; carousel</li>
<li>&quot;New Games&quot; section</li>
<li>&quot;Most Popular&quot; section</li>
<li>&quot;Because You Played [Game]&quot; section</li>
</ul>
<p>With the Recommend API, you would make 4 separate API calls. With Intelligent Layouts, you make 1 call and receive all sections in the optimal order for that user.</p>
<h2>Key Concepts</h2>
<h3>Areas</h3>
<p>An <strong>area</strong> is a logical grouping of placements on your page. Think of it as a container that can hold one or more placements. Areas have:</p>
<ul>
<li>A name (e.g., &quot;hero_section&quot;, &quot;main_content&quot;)</li>
<li>Minimum and maximum placement counts</li>
<li>An index determining display order</li>
</ul>
<h3>Placements</h3>
<p>A <strong>placement</strong> within a layout represents a specific recommendation slot, just like in the Recommend API. Each placement has:</p>
<ul>
<li>A unique <code>placementKey</code></li>
<li>A title for display</li>
<li>Configuration for what items to recommend</li>
<li>Optionally, a <code>dummy</code> flag for placeholder slots</li>
</ul>
<h2>Why This Matters</h2>
<p>Intelligent Layouts simplify complex personalized pages by:</p>
<ul>
<li>Reducing multiple API calls to one</li>
<li>Letting Opti-X optimize the page structure per user</li>
<li>Ensuring consistent deduplication across sections</li>
<li>Enabling A/B testing of different page layouts</li>
</ul>
<h2>Endpoint</h2>
<pre><code>POST https://api.opti-x.optimove.net/intelligentlayouts/v1/layouts/{layoutKey}/layout
</code></pre>
<p>Replace <code>{layoutKey}</code> with your layout&#39;s unique key from the Admin panel.</p>
<h2>Headers</h2>
<table>
<thead>
<tr>
<th>Header</th>
<th>Description</th>
<th>Required</th>
</tr>
</thead>
<tbody><tr>
<td><code>x-api-key</code></td>
<td>Your API key</td>
<td>Yes</td>
</tr>
<tr>
<td><code>x-brand-key</code></td>
<td>Your brand identifier</td>
<td>Yes</td>
</tr>
<tr>
<td><code>content-type</code></td>
<td>Must be <code>application/json</code></td>
<td>Yes</td>
</tr>
</tbody></table>
<h2>Request Parameters</h2>
<p>The request body is similar to the Recommend API, but with <code>type</code> set to <code>&quot;layout&quot;</code>:</p>
<table>
<thead>
<tr>
<th>Parameter</th>
<th>Type</th>
<th>Required</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td><code>userId</code></td>
<td>String</td>
<td>Yes</td>
<td>Unique identifier for the user</td>
</tr>
<tr>
<td><code>type</code></td>
<td>String</td>
<td>Yes</td>
<td>Must be <code>&quot;layout&quot;</code></td>
</tr>
<tr>
<td><code>context</code></td>
<td>Object</td>
<td>Yes</td>
<td>Current page and user context</td>
</tr>
<tr>
<td><code>context.product</code></td>
<td>String</td>
<td>No</td>
<td>Product vertical: <code>&quot;Gaming&quot;</code>, <code>&quot;Sports&quot;</code>, or <code>&quot;Ecommerce&quot;</code></td>
</tr>
<tr>
<td><code>context.category</code></td>
<td>String</td>
<td>No</td>
<td>Current category</td>
</tr>
<tr>
<td><code>context.page</code></td>
<td>Object</td>
<td>No</td>
<td>Page details</td>
</tr>
<tr>
<td><code>context.channel</code></td>
<td>String</td>
<td>No</td>
<td>Device type</td>
</tr>
<tr>
<td><code>traits</code></td>
<td>Object</td>
<td>No</td>
<td>Additional context attributes</td>
</tr>
</tbody></table>
<h2>Example Request</h2>
<pre><code class="language-bash">curl -X POST &quot;https://api.opti-x.optimove.net/intelligentlayouts/v1/layouts/casino-homepage/layout&quot; \
  -H &quot;x-api-key: your-api-key&quot; \
  -H &quot;x-brand-key: your-brand-key&quot; \
  -H &quot;Content-Type: application/json&quot; \
  -d &#39;{
    &quot;userId&quot;: &quot;user_12345&quot;,
    &quot;type&quot;: &quot;layout&quot;,
    &quot;context&quot;: {
      &quot;product&quot;: &quot;Gaming&quot;,
      &quot;category&quot;: &quot;Slots&quot;,
      &quot;page&quot;: {
        &quot;url&quot;: &quot;https://casino.example.com/&quot;,
        &quot;title&quot;: &quot;Casino Homepage&quot;
      },
      &quot;channel&quot;: &quot;Mobile&quot;
    }
  }&#39;
</code></pre>
<h2>Example Response</h2>
<pre><code class="language-json">{
  &quot;layout&quot;: {
    &quot;layoutId&quot;: &quot;layout-a1b2c3d4-e5f6-7890-abcd-ef1234567890&quot;,
    &quot;layoutDateTime&quot;: &quot;2025-01-15T14:30:00.000Z&quot;,
    &quot;result&quot;: [
      {
        &quot;area&quot;: {
          &quot;index&quot;: 0,
          &quot;name&quot;: &quot;hero_recommendations&quot;,
          &quot;placement&quot;: {
            &quot;title&quot;: &quot;Recommended for You&quot;,
            &quot;placementKey&quot;: &quot;placement-hero-rec&quot;,
            &quot;result&quot;: [
              {
                &quot;game&quot;: {
                  &quot;game_code&quot;: &quot;megaways_fortune&quot;,
                  &quot;name&quot;: &quot;Megaways Fortune&quot;,
                  &quot;score&quot;: 0.89,
                  &quot;rank&quot;: 1,
                  &quot;formFactors&quot;: [&quot;mobile&quot;, &quot;desktop&quot;, &quot;tablet&quot;],
                  &quot;gameType&quot;: &quot;Slots&quot;
                }
              },
              {
                &quot;game&quot;: {
                  &quot;game_code&quot;: &quot;rainbow_jackpot&quot;,
                  &quot;name&quot;: &quot;Rainbow Jackpot&quot;,
                  &quot;score&quot;: 0.82,
                  &quot;rank&quot;: 2,
                  &quot;formFactors&quot;: [&quot;mobile&quot;, &quot;desktop&quot;],
                  &quot;gameType&quot;: &quot;Slots&quot;
                }
              }
            ],
            &quot;explanation&quot;: {
              &quot;item&quot;: &quot;game&quot;,
              &quot;reason&quot;: &quot;personalized&quot;
            }
          }
        }
      },
      {
        &quot;area&quot;: {
          &quot;index&quot;: 1,
          &quot;name&quot;: &quot;popular_games&quot;,
          &quot;placement&quot;: {
            &quot;title&quot;: &quot;Most Popular&quot;,
            &quot;placementKey&quot;: &quot;placement-popular&quot;,
            &quot;result&quot;: [
              {
                &quot;game&quot;: {
                  &quot;game_code&quot;: &quot;starburst_classic&quot;,
                  &quot;name&quot;: &quot;Starburst Classic&quot;,
                  &quot;score&quot;: 0.95,
                  &quot;rank&quot;: 1,
                  &quot;formFactors&quot;: [&quot;mobile&quot;, &quot;desktop&quot;, &quot;tablet&quot;],
                  &quot;gameType&quot;: &quot;Slots&quot;
                }
              }
            ],
            &quot;explanation&quot;: {
              &quot;item&quot;: &quot;game&quot;,
              &quot;reason&quot;: &quot;most_popular&quot;
            }
          }
        }
      },
      {
        &quot;area&quot;: {
          &quot;index&quot;: 2,
          &quot;name&quot;: &quot;external_content&quot;,
          &quot;placement&quot;: {
            &quot;title&quot;: &quot;Bingo Schedule&quot;,
            &quot;placementKey&quot;: &quot;placement-bingo-schedule&quot;,
            &quot;dummy&quot;: true,
            &quot;result&quot;: []
          }
        }
      }
    ]
  }
}
</code></pre>
<h2>Response Structure</h2>
<h3>Layout Object</h3>
<table>
<thead>
<tr>
<th>Field</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td><code>layoutId</code></td>
<td>Unique identifier for this layout response</td>
</tr>
<tr>
<td><code>layoutDateTime</code></td>
<td>When the layout was generated</td>
</tr>
<tr>
<td><code>result</code></td>
<td>Array of area objects in display order</td>
</tr>
</tbody></table>
<h3>Area Object</h3>
<table>
<thead>
<tr>
<th>Field</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td><code>area.index</code></td>
<td>Display order (0 = first)</td>
</tr>
<tr>
<td><code>area.name</code></td>
<td>Area identifier</td>
</tr>
<tr>
<td><code>area.placement</code></td>
<td>The placement for this area</td>
</tr>
</tbody></table>
<h3>Placement Object</h3>
<table>
<thead>
<tr>
<th>Field</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td><code>placement.title</code></td>
<td>Display title for this section</td>
</tr>
<tr>
<td><code>placement.placementKey</code></td>
<td>Unique placement identifier</td>
</tr>
<tr>
<td><code>placement.result</code></td>
<td>Array of recommended items</td>
</tr>
<tr>
<td><code>placement.dummy</code></td>
<td>If <code>true</code>, this is a placeholder (no content from Opti-X)</td>
</tr>
<tr>
<td><code>placement.explanation</code></td>
<td>Why these items were recommended</td>
</tr>
</tbody></table>
<h2>Dummy Placements</h2>
<p>A placement with <code>&quot;dummy&quot;: true</code> indicates a slot in the page order without Opti-X content. Use dummy placements for:</p>
<ul>
<li>External content (e.g., bingo schedules, promotional banners)</li>
<li>Sections populated by other systems</li>
<li>Maintaining consistent page structure</li>
</ul>
<p>When you receive a dummy placement, render your own content at that position while maintaining the layout order.</p>
<h2>Managing Layouts</h2>
<p>You can create and manage layouts programmatically using the Layout Management API.</p>
<h3>Create a Layout</h3>
<pre><code>POST https://api.opti-x.optimove.net/intelligentlayouts/v1/layouts
</code></pre>
<h3>Read a Layout Configuration</h3>
<pre><code>GET https://api.opti-x.optimove.net/intelligentlayouts/v1/layouts/{layoutKey}
</code></pre>
<h3>Update a Layout</h3>
<pre><code>POST https://api.opti-x.optimove.net/intelligentlayouts/v1/layouts/{layoutKey}
</code></pre>
<h3>Delete a Layout</h3>
<pre><code>DELETE https://api.opti-x.optimove.net/intelligentlayouts/v1/layouts/{layoutKey}
</code></pre>
<p><strong>Note:</strong> Layout management requires a User or Service API key. Public keys cannot modify layouts.</p>
<h2>Layout Configuration Model</h2>
<p>When creating or updating layouts, use this structure:</p>
<h3>Layout Properties</h3>
<table>
<thead>
<tr>
<th>Field</th>
<th>Type</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td><code>layoutName</code></td>
<td>String</td>
<td>Display name for the layout</td>
</tr>
<tr>
<td><code>product</code></td>
<td>String</td>
<td><code>&quot;Gaming&quot;</code>, <code>&quot;Sports&quot;</code>, or <code>&quot;eCommerce&quot;</code></td>
</tr>
<tr>
<td><code>areas</code></td>
<td>Array</td>
<td>Ordered list of areas</td>
</tr>
<tr>
<td><code>cacheTime</code></td>
<td>Integer</td>
<td>Seconds to cache placement order (e.g., 86400 for 1 day)</td>
</tr>
<tr>
<td><code>safe_mode</code></td>
<td>Boolean</td>
<td>Return best-effort results even if rules are not fully met</td>
</tr>
<tr>
<td><code>dedupe</code></td>
<td>Object</td>
<td>Deduplication settings</td>
</tr>
</tbody></table>
<h3>Area Properties</h3>
<table>
<thead>
<tr>
<th>Field</th>
<th>Type</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td><code>name</code></td>
<td>String</td>
<td>Area identifier</td>
</tr>
<tr>
<td><code>min_placements</code></td>
<td>Integer</td>
<td>Minimum placements to return</td>
</tr>
<tr>
<td><code>max_placements</code></td>
<td>Integer</td>
<td>Maximum placements to return</td>
</tr>
</tbody></table>
<h3>Placement Properties (within areas)</h3>
<table>
<thead>
<tr>
<th>Field</th>
<th>Type</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td><code>placementKey</code></td>
<td>String</td>
<td>Reference to an existing placement</td>
</tr>
<tr>
<td><code>placementTitle</code></td>
<td>String</td>
<td>Display name in layout editor</td>
</tr>
<tr>
<td><code>title</code></td>
<td>String</td>
<td>Title returned in API response</td>
</tr>
<tr>
<td><code>dummy</code></td>
<td>Boolean</td>
<td>Mark as placeholder slot</td>
</tr>
<tr>
<td><code>extra</code></td>
<td>Object</td>
<td>Additional data (e.g., translations)</td>
</tr>
</tbody></table>
<h3>Deduplication</h3>
<p>Prevent the same item from appearing in multiple placements:</p>
<pre><code class="language-json">{
  &quot;dedupe&quot;: {
    &quot;dedupeLogic&quot;: &quot;topN&quot;,
    &quot;N&quot;: 6
  }
}
</code></pre>
<p>This ensures the top 6 items in the first placement will not appear in subsequent placements.</p>
<h2>Error Handling</h2>
<table>
<thead>
<tr>
<th>Status Code</th>
<th>Meaning</th>
<th>Action</th>
</tr>
</thead>
<tbody><tr>
<td>400</td>
<td>Invalid request</td>
<td>Check your JSON structure</td>
</tr>
<tr>
<td>401</td>
<td>Authentication failed</td>
<td>Verify your API keys</td>
</tr>
<tr>
<td>403</td>
<td>Insufficient permissions</td>
<td>Use User/Service key for layout management</td>
</tr>
<tr>
<td>404</td>
<td>Layout not found</td>
<td>Check the layoutKey exists</td>
</tr>
<tr>
<td>500</td>
<td>Server error</td>
<td>Retry with exponential backoff</td>
</tr>
</tbody></table>
<hr>
<h2>Related Topics</h2>
<ul>
<li><a href="#api-reference-overview">API Overview</a></li>
<li><a href="#recommend-api">Recommend API</a> - For single placement requests</li>
<li><a href="#authentication">Authentication Guide</a></li>
<li><a href="#error-handling">Error Handling</a></li>
</ul>

</section>
<section id="momentum-api" class="doc-section">
<h1>Momentum API</h1>
<p>The Momentum API provides access to Popular and Trending data through the Recommend API infrastructure. This gives you a unified approach to accessing all recommendation data, including real-time popularity signals.</p>
<h2>What is Momentum?</h2>
<p>Momentum refers to the velocity of user interest in items over time. Opti-X tracks two key momentum signals:</p>
<h3>Popular</h3>
<p><strong>Popular</strong> items have the highest overall engagement volume. These are the items that the most users interact with, measured across a longer time window (typically days or weeks).</p>
<p><strong>Example:</strong> A game that has been consistently played by thousands of users over the past week ranks high in Popular.</p>
<p><strong>Use for:</strong></p>
<ul>
<li>&quot;Most Popular Games&quot; sections</li>
<li>&quot;Top Picks&quot; carousels</li>
<li>Default recommendations for new users</li>
</ul>
<h3>Trending</h3>
<p><strong>Trending</strong> items show the fastest growth in engagement. These items may not have the highest total volume, but their engagement is increasing rapidly compared to their baseline.</p>
<p><strong>Example:</strong> A newly released game that saw a 300% increase in plays today compared to yesterday ranks high in Trending, even if its total plays are lower than established popular games.</p>
<p><strong>Use for:</strong></p>
<ul>
<li>&quot;Trending Now&quot; sections</li>
<li>&quot;Hot This Week&quot; widgets</li>
<li>Highlighting emerging content</li>
</ul>
<h2>Why This Matters</h2>
<p>Popular and Trending data helps you:</p>
<ul>
<li>Surface content that resonates with your audience</li>
<li>Highlight new or seasonal content gaining traction</li>
<li>Provide meaningful recommendations for users without history</li>
<li>Create dynamic, engaging page sections that change with user behavior</li>
</ul>
<h2>How to Access Momentum Data</h2>
<p>Momentum data is accessed through the standard Recommend API. This unified approach means:</p>
<ul>
<li>One API integration for all recommendation types</li>
<li>Consistent request and response formats</li>
<li>Full access to sports rules and constraints</li>
<li>Seamless switching between recommendation strategies</li>
</ul>
<h3>Setup Process</h3>
<ol>
<li><strong>Create a placement</strong> in the Opti-X Admin panel using the Recommend product</li>
<li><strong>Select the method</strong> as &quot;Popular&quot; or &quot;Trending&quot; when configuring the placement</li>
<li><strong>Configure rules</strong> such as item type, category filters, or time windows</li>
<li><strong>Use the Recommend API</strong> with your placement key</li>
</ol>
<h2>Example: Fetching Popular Games</h2>
<h3>Create the Placement</h3>
<p>In the Opti-X Admin panel:</p>
<ol>
<li>Navigate to <strong>Recommend &gt; Placements</strong></li>
<li>Create a new placement named &quot;Homepage Popular Games&quot;</li>
<li>Set the method to <strong>Popular</strong></li>
<li>Configure filters (e.g., product = Gaming, category = Slots)</li>
<li>Save and note the <code>placementKey</code></li>
</ol>
<h3>Make the API Request</h3>
<pre><code class="language-bash">curl -X POST &quot;https://api.opti-x.optimove.net/recommend/v1/placements/homepage-popular-games/recommendations&quot; \
  -H &quot;x-api-key: your-api-key&quot; \
  -H &quot;x-brand-key: your-brand-key&quot; \
  -H &quot;Content-Type: application/json&quot; \
  -d &#39;{
    &quot;userId&quot;: &quot;user_12345&quot;,
    &quot;type&quot;: &quot;recommendation&quot;,
    &quot;context&quot;: {
      &quot;product&quot;: &quot;Gaming&quot;,
      &quot;category&quot;: &quot;Slots&quot;,
      &quot;channel&quot;: &quot;Mobile&quot;
    }
  }&#39;
</code></pre>
<h3>Response</h3>
<pre><code class="language-json">{
  &quot;recommendation&quot;: {
    &quot;result&quot;: [
      {
        &quot;game&quot;: {
          &quot;game_code&quot;: &quot;starburst_classic&quot;,
          &quot;name&quot;: &quot;Starburst Classic&quot;,
          &quot;score&quot;: 0.98,
          &quot;rank&quot;: 1
        }
      },
      {
        &quot;game&quot;: {
          &quot;game_code&quot;: &quot;book_of_dead&quot;,
          &quot;name&quot;: &quot;Book of Dead&quot;,
          &quot;score&quot;: 0.95,
          &quot;rank&quot;: 2
        }
      },
      {
        &quot;game&quot;: {
          &quot;game_code&quot;: &quot;gonzo_quest&quot;,
          &quot;name&quot;: &quot;Gonzo&#39;s Quest&quot;,
          &quot;score&quot;: 0.92,
          &quot;rank&quot;: 3
        }
      }
    ],
    &quot;recId&quot;: &quot;rec-popular-a1b2c3d4&quot;,
    &quot;recDateTime&quot;: &quot;2025-01-15T14:30:00Z&quot;,
    &quot;explanation&quot;: {
      &quot;reason&quot;: &quot;most_popular&quot;,
      &quot;tag_type&quot;: &quot;portlet&quot;,
      &quot;tag&quot;: &quot;Most Popular&quot;
    }
  }
}
</code></pre>
<h2>Example: Fetching Trending Sports Bets</h2>
<h3>Create the Placement</h3>
<p>In the Opti-X Admin panel:</p>
<ol>
<li>Create a placement named &quot;Trending Bets Widget&quot;</li>
<li>Set the method to <strong>Trending</strong></li>
<li>Configure filters (e.g., product = Sports, category = Football)</li>
<li>Set the time window (e.g., trending in the last 24 hours)</li>
</ol>
<h3>Make the API Request</h3>
<pre><code class="language-bash">curl -X POST &quot;https://api.opti-x.optimove.net/recommend/v1/placements/trending-bets-widget/recommendations&quot; \
  -H &quot;x-api-key: your-api-key&quot; \
  -H &quot;x-brand-key: your-brand-key&quot; \
  -H &quot;Content-Type: application/json&quot; \
  -d &#39;{
    &quot;userId&quot;: &quot;user_67890&quot;,
    &quot;type&quot;: &quot;recommendation&quot;,
    &quot;context&quot;: {
      &quot;product&quot;: &quot;Sports&quot;,
      &quot;category&quot;: &quot;Football&quot;
    }
  }&#39;
</code></pre>
<h3>Response</h3>
<pre><code class="language-json">{
  &quot;recommendation&quot;: {
    &quot;result&quot;: [
      {
        &quot;selection&quot;: {
          &quot;selectionKey&quot;: 1196055705,
          &quot;selectionName&quot;: &quot;Both Teams to Score - Yes&quot;,
          &quot;marketName&quot;: &quot;Both Teams to Score&quot;,
          &quot;eventName&quot;: &quot;Arsenal vs Chelsea&quot;,
          &quot;score&quot;: 0.89,
          &quot;rank&quot;: 1
        }
      },
      {
        &quot;selection&quot;: {
          &quot;selectionKey&quot;: 1196055712,
          &quot;selectionName&quot;: &quot;Over 2.5 Goals&quot;,
          &quot;marketName&quot;: &quot;Total Goals&quot;,
          &quot;eventName&quot;: &quot;Liverpool vs Man City&quot;,
          &quot;score&quot;: 0.85,
          &quot;rank&quot;: 2
        }
      }
    ],
    &quot;recId&quot;: &quot;rec-trending-e5f6g7h8&quot;,
    &quot;recDateTime&quot;: &quot;2025-01-15T14:35:00Z&quot;,
    &quot;explanation&quot;: {
      &quot;reason&quot;: &quot;trending&quot;,
      &quot;tag_type&quot;: &quot;portlet&quot;,
      &quot;tag&quot;: &quot;Trending Now&quot;
    }
  }
}
</code></pre>
<h2>Combining Popular and Trending</h2>
<p>You can create multiple placements with different methods and display them together:</p>
<pre><code>[Homepage]
├── &quot;Recommended for You&quot; (Personalized method)
├── &quot;Trending Now&quot; (Trending method)
└── &quot;All-Time Favorites&quot; (Popular method)
</code></pre>
<p>Each section uses the same Recommend API with different placement keys, giving you a consistent integration pattern.</p>
<h2>Configuration Options</h2>
<p>When creating Popular or Trending placements in the Admin panel, you can configure:</p>
<table>
<thead>
<tr>
<th>Option</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>Time Window</td>
<td>Period to calculate popularity/trending (e.g., 24 hours, 7 days)</td>
</tr>
<tr>
<td>Category Filter</td>
<td>Limit to specific categories</td>
</tr>
<tr>
<td>Item Count</td>
<td>Number of items to return</td>
</tr>
<tr>
<td>Deduplication</td>
<td>Prevent items from appearing in multiple placements</td>
</tr>
</tbody></table>
<h2>Best Practices</h2>
<h3>Use Both Popular and Trending</h3>
<p>Popular shows proven winners; Trending shows emerging content. Using both gives users a complete picture of what is happening on your platform.</p>
<h3>Update Trending Frequently</h3>
<p>Trending data changes rapidly. Consider refreshing Trending sections more frequently than Popular sections to keep content fresh.</p>
<h3>Provide Context for New Users</h3>
<p>Popular items work well as fallback recommendations for users without history, ensuring everyone sees engaging content.</p>
<h3>Combine with Personalization</h3>
<p>Use Momentum data alongside personalized recommendations. A page might show &quot;Recommended for You&quot; (personalized), &quot;Trending Now&quot; (trending), and &quot;Most Popular&quot; (popular) sections together.</p>
<hr>
<h2>Related Topics</h2>
<ul>
<li><a href="#api-reference-overview">API Overview</a></li>
<li><a href="#recommend-api">Recommend API</a> - Full API documentation</li>
<li><a href="#intelligent-layouts-api">Intelligent Layouts API</a> - Combine multiple placements</li>
<li><a href="#authentication">Authentication Guide</a></li>
</ul>

</section>
<section id="gaming-inventory-api" class="doc-section">
<h1>Gaming Inventory API</h1>
<p>The Gaming Inventory API enables you to upload and manage your gaming catalog within Opti-X. This inventory data powers recommendations, search, and personalization features.</p>
<h2>Why This Matters</h2>
<p>Opti-X needs to know what items exist in your catalog to recommend them. By uploading your gaming inventory, you enable:</p>
<ul>
<li>Personalized game recommendations</li>
<li>Accurate search results</li>
<li>Filtering by game attributes (category, provider, RTP)</li>
<li>Real-time availability updates</li>
</ul>
<h2>Prerequisites</h2>
<p>Before using this API, ensure you have:</p>
<ol>
<li><strong>API Keys</strong> - Valid <code>x-api-key</code> and <code>x-brand-key</code> from the Opti-X Admin panel (Developer Tools &gt; API Keys)</li>
<li><strong>Service or User Key</strong> - Inventory upload requires elevated permissions (not a Public key)</li>
<li><strong>Inventory Data</strong> - Your game catalog in the required JSON format</li>
</ol>
<h2>Inventory Schema</h2>
<p>Your gaming inventory must be a JSON object where each key is a game code and each value contains the game&#39;s attributes.</p>
<h3>Required Fields</h3>
<table>
<thead>
<tr>
<th>Field</th>
<th>Type</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td><code>game_code</code></td>
<td>String</td>
<td>Unique identifier for the game</td>
</tr>
<tr>
<td><code>game_name</code></td>
<td>String</td>
<td>Display name of the game</td>
</tr>
</tbody></table>
<h3>Recommended Fields</h3>
<table>
<thead>
<tr>
<th>Field</th>
<th>Type</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td><code>game_category</code></td>
<td>String</td>
<td>Primary category (e.g., &quot;Slots&quot;, &quot;Table Games&quot;, &quot;Live Casino&quot;)</td>
</tr>
<tr>
<td><code>game_class</code></td>
<td>String</td>
<td>Classification (e.g., &quot;premium&quot;, &quot;standard&quot;)</td>
</tr>
<tr>
<td><code>game_type</code></td>
<td>String</td>
<td>Game type (e.g., &quot;3D&quot;, &quot;Classic&quot;, &quot;Megaways&quot;)</td>
</tr>
<tr>
<td><code>supplier</code></td>
<td>String</td>
<td>Game provider/supplier name</td>
</tr>
<tr>
<td><code>rtp</code></td>
<td>Float</td>
<td>Return to player percentage (e.g., 0.96 for 96%)</td>
</tr>
<tr>
<td><code>desktop</code></td>
<td>Integer</td>
<td>Available on desktop (1 = yes, 0 = no)</td>
</tr>
<tr>
<td><code>mobile</code></td>
<td>Integer</td>
<td>Available on mobile (1 = yes, 0 = no)</td>
</tr>
<tr>
<td><code>tablet</code></td>
<td>Integer</td>
<td>Available on tablet (1 = yes, 0 = no)</td>
</tr>
</tbody></table>
<h3>Optional Fields</h3>
<table>
<thead>
<tr>
<th>Field</th>
<th>Type</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td><code>description</code></td>
<td>String</td>
<td>Full game description</td>
</tr>
<tr>
<td><code>themes</code></td>
<td>Array</td>
<td>Theme tags (e.g., [&quot;Adventure&quot;, &quot;Egyptian&quot;])</td>
</tr>
<tr>
<td><code>launch_date</code></td>
<td>String</td>
<td>Release date (DD/MM/YYYY format)</td>
</tr>
<tr>
<td><code>new</code></td>
<td>Boolean</td>
<td>Flag for new games</td>
</tr>
<tr>
<td><code>default_order</code></td>
<td>Integer</td>
<td>Default sort order</td>
</tr>
<tr>
<td><code>jackpot_type</code></td>
<td>String</td>
<td>Jackpot type if applicable (e.g., &quot;progressive&quot;, &quot;fixed&quot;)</td>
</tr>
<tr>
<td><code>image_url</code></td>
<td>String</td>
<td>URL to game thumbnail</td>
</tr>
<tr>
<td><code>tags</code></td>
<td>Array</td>
<td>Custom tags for filtering</td>
</tr>
<tr>
<td><code>regulation</code></td>
<td>Array</td>
<td>Regulatory licenses (e.g., [&quot;UKGC&quot;, &quot;MGA&quot;])</td>
</tr>
<tr>
<td><code>inclusions</code></td>
<td>Object</td>
<td>Markets where game is available</td>
</tr>
<tr>
<td><code>exclusions</code></td>
<td>Object</td>
<td>Markets where game is not available</td>
</tr>
<tr>
<td><code>extra</code></td>
<td>Object</td>
<td>Additional custom attributes</td>
</tr>
</tbody></table>
<h3>Example Inventory Item</h3>
<pre><code class="language-json">{
  &quot;rainbow_riches_megaways&quot;: {
    &quot;game_code&quot;: &quot;rainbow_riches_megaways&quot;,
    &quot;game_name&quot;: &quot;Rainbow Riches Megaways&quot;,
    &quot;game_category&quot;: &quot;Slots&quot;,
    &quot;game_class&quot;: &quot;premium&quot;,
    &quot;game_type&quot;: &quot;Megaways&quot;,
    &quot;description&quot;: &quot;The classic Irish-themed slot with Megaways mechanics.&quot;,
    &quot;desktop&quot;: 1,
    &quot;mobile&quot;: 1,
    &quot;tablet&quot;: 1,
    &quot;rtp&quot;: 0.96,
    &quot;themes&quot;: [&quot;Irish&quot;, &quot;Fantasy&quot;],
    &quot;launch_date&quot;: &quot;15/03/2023&quot;,
    &quot;new&quot;: false,
    &quot;supplier&quot;: &quot;Barcrest&quot;,
    &quot;default_order&quot;: 5,
    &quot;jackpot_type&quot;: &quot;none&quot;,
    &quot;image_url&quot;: &quot;https://cdn.example.com/games/rainbow_riches_megaways.jpg&quot;,
    &quot;tags&quot;: [
      {&quot;featured&quot;: &quot;true&quot;},
      {&quot;lobby_position&quot;: &quot;top&quot;}
    ],
    &quot;regulation&quot;: [&quot;UKGC&quot;, &quot;MGA&quot;, &quot;DGA&quot;],
    &quot;inclusions&quot;: {
      &quot;country&quot;: [&quot;UK&quot;, &quot;DE&quot;, &quot;SE&quot;]
    },
    &quot;exclusions&quot;: {
      &quot;currency&quot;: [&quot;USD&quot;]
    },
    &quot;extra&quot;: {
      &quot;min_bet&quot;: 0.10,
      &quot;max_bet&quot;: 100.00
    }
  }
}
</code></pre>
<h2>Upload Process</h2>
<p>Uploading inventory is a two-step process:</p>
<ol>
<li><strong>Get a presigned URL</strong> from Opti-X</li>
<li><strong>Upload your file</strong> directly to cloud storage using that URL</li>
</ol>
<p>This approach allows for large file uploads without timeout issues.</p>
<h3>Step 1: Get Presigned URL</h3>
<pre><code>GET https://api.opti-x.optimove.net/inventory/v1/upload
</code></pre>
<h4>Headers</h4>
<table>
<thead>
<tr>
<th>Header</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td><code>x-api-key</code></td>
<td>Your API key (User or Service level)</td>
</tr>
<tr>
<td><code>x-brand-key</code></td>
<td>Your brand identifier</td>
</tr>
</tbody></table>
<h4>Example Request</h4>
<pre><code class="language-bash">curl -X GET &quot;https://api.opti-x.optimove.net/inventory/v1/upload&quot; \
  -H &quot;x-api-key: your-api-key&quot; \
  -H &quot;x-brand-key: your-brand-key&quot;
</code></pre>
<h4>Response</h4>
<pre><code class="language-json">{
  &quot;url&quot;: &quot;https://s3.amazonaws.com/opti-x-inventory-bucket&quot;,
  &quot;fields&quot;: {
    &quot;key&quot;: &quot;uploads/your-brand/inventory-20250115.json&quot;,
    &quot;AWSAccessKeyId&quot;: &quot;AKIA...&quot;,
    &quot;policy&quot;: &quot;eyJ...&quot;,
    &quot;signature&quot;: &quot;abc123...&quot;
  }
}
</code></pre>
<h3>Step 2: Upload File</h3>
<p>Use the presigned URL and fields to upload your inventory file:</p>
<pre><code class="language-bash">curl -X POST &quot;https://s3.amazonaws.com/opti-x-inventory-bucket&quot; \
  -F &quot;key=uploads/your-brand/inventory-20250115.json&quot; \
  -F &quot;AWSAccessKeyId=AKIA...&quot; \
  -F &quot;policy=eyJ...&quot; \
  -F &quot;signature=abc123...&quot; \
  -F &quot;file=@games.json&quot;
</code></pre>
<h3>Python Example</h3>
<pre><code class="language-python">import requests
import json

def upload_inventory(api_key: str, brand_key: str, inventory_file: str) -&gt; None:
    &quot;&quot;&quot;Upload gaming inventory to Opti-X.&quot;&quot;&quot;

    # Step 1: Get presigned URL
    presigned_response = requests.get(
        url=&quot;https://api.opti-x.optimove.net/inventory/v1/upload&quot;,
        headers={
            &quot;x-api-key&quot;: api_key,
            &quot;x-brand-key&quot;: brand_key
        }
    )
    presigned_data = presigned_response.json()

    # Step 2: Upload file
    with open(inventory_file, &#39;rb&#39;) as f:
        files = {&#39;file&#39;: (inventory_file, f)}
        upload_response = requests.post(
            presigned_data[&#39;url&#39;],
            data=presigned_data[&#39;fields&#39;],
            files=files
        )

    if upload_response.status_code == 204:
        print(&quot;Upload successful&quot;)
    else:
        print(f&quot;Upload failed: {upload_response.status_code}&quot;)

# Usage
upload_inventory(
    api_key=&quot;your-api-key&quot;,
    brand_key=&quot;your-brand-key&quot;,
    inventory_file=&quot;games.json&quot;
)
</code></pre>
<h3>Processing</h3>
<p>After upload, Opti-X processes your inventory asynchronously. Processing typically completes within a few minutes. Once processed, your inventory data appears in the Admin panel under <strong>Data &gt; Datasets</strong>.</p>
<h2>Validation Endpoint</h2>
<p>Before uploading a full inventory, validate a sample to catch formatting errors.</p>
<pre><code>POST https://api.opti-x.optimove.net/inventory/v1/validate
</code></pre>
<h3>Headers</h3>
<table>
<thead>
<tr>
<th>Header</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td><code>x-api-key</code></td>
<td>Your API key</td>
</tr>
<tr>
<td><code>x-brand-key</code></td>
<td>Your brand identifier</td>
</tr>
<tr>
<td><code>content-type</code></td>
<td><code>multipart/form-data</code></td>
</tr>
</tbody></table>
<h3>Request</h3>
<p>Attach your JSON file (recommend validating a sample of ~100 games due to 5MB size limit):</p>
<pre><code class="language-bash">curl -X POST &quot;https://api.opti-x.optimove.net/inventory/v1/validate&quot; \
  -H &quot;x-api-key: your-api-key&quot; \
  -H &quot;x-brand-key: your-brand-key&quot; \
  -F &quot;file=@games_sample.json&quot;
</code></pre>
<h3>Success Response</h3>
<pre><code class="language-json">{
  &quot;validation_errors&quot;: []
}
</code></pre>
<h3>Error Response</h3>
<pre><code class="language-json">{
  &quot;validation_errors&quot;: [
    {
      &quot;rainbow_riches_megaways&quot;: [
        {
          &quot;loc&quot;: [&quot;desktop&quot;],
          &quot;msg&quot;: &quot;value is not a valid integer&quot;,
          &quot;type&quot;: &quot;type_error.integer&quot;
        }
      ]
    },
    {
      &quot;book_of_dead&quot;: [
        {
          &quot;loc&quot;: [&quot;supplier&quot;],
          &quot;msg&quot;: &quot;str type expected&quot;,
          &quot;type&quot;: &quot;type_error.str&quot;
        }
      ]
    },
    {
      &quot;mystery_game&quot;: [
        {
          &quot;loc&quot;: [&quot;game_code&quot;],
          &quot;msg&quot;: &quot;none is not an allowed value&quot;,
          &quot;type&quot;: &quot;type_error.none.not_allowed&quot;
        }
      ]
    }
  ]
}
</code></pre>
<h3>Common Validation Errors</h3>
<table>
<thead>
<tr>
<th>Error</th>
<th>Cause</th>
<th>Fix</th>
</tr>
</thead>
<tbody><tr>
<td><code>value is not a valid integer</code></td>
<td>Field expects integer, received string</td>
<td>Use <code>1</code> instead of <code>&quot;1&quot;</code></td>
</tr>
<tr>
<td><code>str type expected</code></td>
<td>Field expects string, received number</td>
<td>Use <code>&quot;Barcrest&quot;</code> instead of <code>123</code></td>
</tr>
<tr>
<td><code>none is not an allowed value</code></td>
<td>Required field is null</td>
<td>Provide a value for the field</td>
</tr>
</tbody></table>
<h2>Error Handling</h2>
<h3>Upload Errors</h3>
<table>
<thead>
<tr>
<th>Status Code</th>
<th>Meaning</th>
<th>Action</th>
</tr>
</thead>
<tbody><tr>
<td>401</td>
<td>Invalid API key</td>
<td>Verify your credentials</td>
</tr>
<tr>
<td>403</td>
<td>Insufficient permissions</td>
<td>Use a User or Service key</td>
</tr>
<tr>
<td>413</td>
<td>File too large</td>
<td>Split inventory into smaller batches</td>
</tr>
<tr>
<td>500</td>
<td>Server error</td>
<td>Retry with exponential backoff</td>
</tr>
</tbody></table>
<h3>Validation Errors</h3>
<p>The validation endpoint returns 200 even when validation errors exist. Always check the <code>validation_errors</code> array in the response.</p>
<h2>Best Practices</h2>
<h3>Validate Before Upload</h3>
<p>Always run validation on a sample before uploading your full inventory. This catches data type issues early.</p>
<h3>Include All Attributes</h3>
<p>The more attributes you provide, the better Opti-X can:</p>
<ul>
<li>Filter recommendations by device type</li>
<li>Apply regulatory restrictions</li>
<li>Power search facets</li>
</ul>
<h3>Update Regularly</h3>
<p>Keep your inventory synchronized:</p>
<ul>
<li>Upload full inventory daily (or when catalog changes significantly)</li>
<li>Include availability/stock status for real-time accuracy</li>
</ul>
<h3>Use Consistent Game Codes</h3>
<p>Game codes must be consistent across:</p>
<ul>
<li>Your inventory uploads</li>
<li>Event tracking (gameplay events)</li>
<li>Any other integrations</li>
</ul>
<hr>
<h2>Related Topics</h2>
<ul>
<li><a href="#api-reference-overview">API Overview</a></li>
<li><a href="#authentication">Authentication Guide</a></li>
<li><a href="#recommend-api">Recommend API</a> - Uses inventory data</li>
<li><a href="#smart-search-api">Smart Search API</a> - Uses inventory data</li>
<li><a href="#error-handling">Error Handling</a></li>
</ul>

</section>
<section id="rate-limits" class="doc-section">
<h1>Rate Limits</h1>
<p>Opti-X APIs enforce rate limits to ensure system stability and fair usage across all clients. This guide explains the limits and how to work within them.</p>
<h2>Why This Matters</h2>
<p>Rate limits protect the platform from:</p>
<ul>
<li>Accidental runaway loops in your code</li>
<li>Denial of service (intentional or accidental)</li>
<li>Ensuring fair resource allocation across all customers</li>
</ul>
<p>Understanding rate limits helps you design integrations that work reliably at scale.</p>
<h2>Rate Limits by API</h2>
<table>
<thead>
<tr>
<th>API</th>
<th>Limit</th>
<th>Window</th>
<th>Notes</th>
</tr>
</thead>
<tbody><tr>
<td>Recommend API</td>
<td>1,000 requests</td>
<td>Per minute</td>
<td>Per API key</td>
</tr>
<tr>
<td>Intelligent Layouts API</td>
<td>1,000 requests</td>
<td>Per minute</td>
<td>Per API key</td>
</tr>
<tr>
<td>Smart Search API</td>
<td>500 requests</td>
<td>Per minute</td>
<td>Per API key</td>
</tr>
<tr>
<td>Gaming Inventory Upload</td>
<td>10 requests</td>
<td>Per hour</td>
<td>Per brand</td>
</tr>
<tr>
<td>Inventory Validation</td>
<td>100 requests</td>
<td>Per hour</td>
<td>Per brand</td>
</tr>
<tr>
<td>Sports Inventory</td>
<td>50 requests</td>
<td>Per 10 seconds</td>
<td>Per API key</td>
</tr>
</tbody></table>
<h2>Rate Limit Headers</h2>
<p>Responses include headers to help you track your usage:</p>
<table>
<thead>
<tr>
<th>Header</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td><code>X-RateLimit-Limit</code></td>
<td>Maximum requests allowed in the window</td>
</tr>
<tr>
<td><code>X-RateLimit-Remaining</code></td>
<td>Requests remaining in current window</td>
</tr>
<tr>
<td><code>X-RateLimit-Reset</code></td>
<td>Unix timestamp when the window resets</td>
</tr>
</tbody></table>
<h3>Example Response Headers</h3>
<pre><code class="language-http">HTTP/1.1 200 OK
X-RateLimit-Limit: 1000
X-RateLimit-Remaining: 847
X-RateLimit-Reset: 1705330800
Content-Type: application/json
</code></pre>
<h2>Handling 429 Responses</h2>
<p>When you exceed the rate limit, you receive a 429 status code:</p>
<pre><code class="language-json">{
  &quot;error&quot;: {
    &quot;code&quot;: &quot;RATE_LIMIT_EXCEEDED&quot;,
    &quot;message&quot;: &quot;Too many requests. Please retry after 10 seconds.&quot;,
    &quot;details&quot;: {
      &quot;retryAfter&quot;: 10,
      &quot;limit&quot;: 1000,
      &quot;window&quot;: &quot;1 minute&quot;
    }
  }
}
</code></pre>
<h3>Response Headers for 429</h3>
<pre><code class="language-http">HTTP/1.1 429 Too Many Requests
Retry-After: 10
X-RateLimit-Limit: 1000
X-RateLimit-Remaining: 0
X-RateLimit-Reset: 1705330800
</code></pre>
<h3>Retry Strategy</h3>
<ol>
<li><strong>Read the Retry-After header</strong> to know how long to wait</li>
<li><strong>Wait the specified time</strong> before retrying</li>
<li><strong>Implement exponential backoff</strong> for repeated 429s</li>
</ol>
<pre><code class="language-javascript">async function handleRateLimitedRequest(url, options) {
  const response = await fetch(url, options);

  if (response.status === 429) {
    const retryAfter = parseInt(response.headers.get(&#39;Retry-After&#39;) || &#39;10&#39;, 10);
    console.log(`Rate limited. Waiting ${retryAfter} seconds...`);

    await new Promise(resolve =&gt; setTimeout(resolve, retryAfter * 1000));

    // Retry the request
    return fetch(url, options);
  }

  return response;
}
</code></pre>
<h2>Best Practices for High-Volume Integrations</h2>
<h3>1. Implement Client-Side Rate Limiting</h3>
<p>Track your own request rate and slow down before hitting limits:</p>
<pre><code class="language-javascript">class RateLimiter {
  constructor(maxRequests, windowMs) {
    this.maxRequests = maxRequests;
    this.windowMs = windowMs;
    this.requests = [];
  }

  async throttle() {
    const now = Date.now();

    // Remove requests outside the window
    this.requests = this.requests.filter(time =&gt; now - time &lt; this.windowMs);

    if (this.requests.length &gt;= this.maxRequests) {
      // Wait until oldest request exits the window
      const oldestRequest = this.requests[0];
      const waitTime = this.windowMs - (now - oldestRequest);
      await new Promise(resolve =&gt; setTimeout(resolve, waitTime));
    }

    this.requests.push(Date.now());
  }
}

// Usage
const limiter = new RateLimiter(900, 60000); // 900 requests per minute (buffer)

async function makeRequest() {
  await limiter.throttle();
  return fetch(&#39;https://api.opti-x.optimove.net/...&#39;);
}
</code></pre>
<h3>2. Batch Requests When Possible</h3>
<p>Instead of making individual requests for each item, use the Intelligent Layouts API to fetch multiple placements in one request.</p>
<p><strong>Instead of:</strong></p>
<pre><code class="language-javascript">// 4 separate requests
const rec1 = await fetchPlacement(&#39;homepage-hero&#39;);
const rec2 = await fetchPlacement(&#39;homepage-popular&#39;);
const rec3 = await fetchPlacement(&#39;homepage-new&#39;);
const rec4 = await fetchPlacement(&#39;homepage-trending&#39;);
</code></pre>
<p><strong>Use:</strong></p>
<pre><code class="language-javascript">// 1 request for all placements
const layout = await fetchLayout(&#39;homepage-layout&#39;);
</code></pre>
<h3>3. Cache Responses Appropriately</h3>
<p>Implement caching to reduce redundant requests:</p>
<pre><code class="language-javascript">const cache = new Map();
const CACHE_TTL = 60000; // 1 minute

async function getRecommendationsWithCache(placementKey, userId) {
  const cacheKey = `${placementKey}:${userId}`;
  const cached = cache.get(cacheKey);

  if (cached &amp;&amp; Date.now() - cached.timestamp &lt; CACHE_TTL) {
    return cached.data;
  }

  const data = await fetchRecommendations(placementKey, userId);

  cache.set(cacheKey, {
    data,
    timestamp: Date.now()
  });

  return data;
}
</code></pre>
<h3>4. Use Debouncing for User-Triggered Requests</h3>
<p>For search and other user-initiated requests, implement debouncing:</p>
<pre><code class="language-javascript">let searchTimeout;

function handleSearchInput(query) {
  clearTimeout(searchTimeout);

  searchTimeout = setTimeout(() =&gt; {
    if (query.length &gt;= 2) {
      performSearch(query);
    }
  }, 250); // Wait 250ms after last keystroke
}
</code></pre>
<h3>5. Monitor Rate Limit Headers</h3>
<p>Track your usage proactively by monitoring the rate limit headers:</p>
<pre><code class="language-javascript">async function monitoredRequest(url, options) {
  const response = await fetch(url, options);

  const remaining = response.headers.get(&#39;X-RateLimit-Remaining&#39;);
  const limit = response.headers.get(&#39;X-RateLimit-Limit&#39;);

  // Log warning when approaching limit
  if (remaining &amp;&amp; limit &amp;&amp; parseInt(remaining) &lt; parseInt(limit) * 0.1) {
    console.warn(`Rate limit warning: ${remaining}/${limit} requests remaining`);
  }

  return response;
}
</code></pre>
<h3>6. Distribute Requests Over Time</h3>
<p>For batch operations, spread requests over time rather than sending all at once:</p>
<pre><code class="language-javascript">async function processItemsWithDelay(items, delayMs = 100) {
  const results = [];

  for (const item of items) {
    const result = await processItem(item);
    results.push(result);

    // Wait between requests
    await new Promise(resolve =&gt; setTimeout(resolve, delayMs));
  }

  return results;
}
</code></pre>
<h2>Sports Inventory Rate Limits</h2>
<p>The Sports Inventory API has stricter rate limits (50 requests per 10 seconds) due to its real-time nature. For high-frequency sports integrations:</p>
<h3>Use Webhooks</h3>
<p>Instead of polling for updates, configure webhooks to receive push notifications when data changes.</p>
<h3>Implement Efficient Polling</h3>
<p>If you must poll, use conditional requests:</p>
<pre><code class="language-javascript">let lastEtag = null;

async function pollSportsInventory() {
  const headers = {
    &#39;x-api-key&#39;: apiKey,
    &#39;x-brand-key&#39;: brandKey
  };

  if (lastEtag) {
    headers[&#39;If-None-Match&#39;] = lastEtag;
  }

  const response = await fetch(url, { headers });

  if (response.status === 304) {
    // No changes - no need to process
    return null;
  }

  lastEtag = response.headers.get(&#39;ETag&#39;);
  return response.json();
}
</code></pre>
<h2>Requesting Higher Limits</h2>
<p>If your use case requires higher rate limits:</p>
<ol>
<li><strong>Document your use case</strong> - Explain why current limits are insufficient</li>
<li><strong>Show your optimization efforts</strong> - Demonstrate you have implemented best practices</li>
<li><strong>Contact your account manager</strong> - Rate limit increases are evaluated case-by-case</li>
</ol>
<h2>Monitoring and Alerts</h2>
<p>Set up monitoring to track:</p>
<ul>
<li>Request volume over time</li>
<li>429 error frequency</li>
<li>Average response times</li>
</ul>
<p>Alert thresholds to consider:</p>
<ul>
<li>Usage exceeds 80% of rate limit</li>
<li>More than 5 rate limit errors in 5 minutes</li>
<li>Sudden spike in request volume</li>
</ul>
<hr>
<h2>Related Topics</h2>
<ul>
<li><a href="#api-reference-overview">API Overview</a></li>
<li><a href="#error-handling">Error Handling</a></li>
<li><a href="#authentication">Authentication Guide</a></li>
</ul>

</section>
<section id="error-handling" class="doc-section">
<h1>Error Handling</h1>
<p>This guide covers how to handle errors when integrating with Opti-X APIs, including common error codes, response formats, and retry strategies.</p>
<h2>Why This Matters</h2>
<p>Robust error handling ensures your application degrades gracefully when issues occur. Users should never see a broken experience because of an API error. Instead, your application should handle errors silently or show appropriate fallback content.</p>
<h2>HTTP Status Codes</h2>
<p>Opti-X APIs use standard HTTP status codes to indicate success or failure.</p>
<h3>Success Codes</h3>
<table>
<thead>
<tr>
<th>Code</th>
<th>Meaning</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>200</td>
<td>OK</td>
<td>Request succeeded</td>
</tr>
<tr>
<td>201</td>
<td>Created</td>
<td>Resource created successfully</td>
</tr>
<tr>
<td>204</td>
<td>No Content</td>
<td>Request succeeded, no content returned (common for uploads)</td>
</tr>
</tbody></table>
<h3>Client Error Codes</h3>
<table>
<thead>
<tr>
<th>Code</th>
<th>Meaning</th>
<th>Common Causes</th>
</tr>
</thead>
<tbody><tr>
<td>400</td>
<td>Bad Request</td>
<td>Invalid JSON, missing required fields, malformed parameters</td>
</tr>
<tr>
<td>401</td>
<td>Unauthorized</td>
<td>Missing or invalid API key</td>
</tr>
<tr>
<td>403</td>
<td>Forbidden</td>
<td>Valid key but insufficient permissions for this operation</td>
</tr>
<tr>
<td>404</td>
<td>Not Found</td>
<td>Placement, layout, or resource does not exist</td>
</tr>
<tr>
<td>422</td>
<td>Unprocessable Entity</td>
<td>Request is valid but cannot be processed (e.g., validation failed)</td>
</tr>
<tr>
<td>429</td>
<td>Too Many Requests</td>
<td>Rate limit exceeded</td>
</tr>
</tbody></table>
<h3>Server Error Codes</h3>
<table>
<thead>
<tr>
<th>Code</th>
<th>Meaning</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>500</td>
<td>Internal Server Error</td>
<td>Unexpected server error</td>
</tr>
<tr>
<td>502</td>
<td>Bad Gateway</td>
<td>Upstream service unavailable</td>
</tr>
<tr>
<td>503</td>
<td>Service Unavailable</td>
<td>Service temporarily unavailable</td>
</tr>
<tr>
<td>504</td>
<td>Gateway Timeout</td>
<td>Request timed out</td>
</tr>
</tbody></table>
<h2>Error Response Format</h2>
<p>When an error occurs, the API returns a JSON response with error details:</p>
<pre><code class="language-json">{
  &quot;error&quot;: {
    &quot;code&quot;: &quot;INVALID_REQUEST&quot;,
    &quot;message&quot;: &quot;Missing required field: userId&quot;,
    &quot;details&quot;: &quot;The userId field is required for all recommendation requests&quot;,
    &quot;requestId&quot;: &quot;req-a1b2c3d4-e5f6-7890&quot;
  }
}
</code></pre>
<h3>Error Response Fields</h3>
<table>
<thead>
<tr>
<th>Field</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td><code>error.code</code></td>
<td>Machine-readable error code</td>
</tr>
<tr>
<td><code>error.message</code></td>
<td>Human-readable error description</td>
</tr>
<tr>
<td><code>error.details</code></td>
<td>Additional context (when available)</td>
</tr>
<tr>
<td><code>error.requestId</code></td>
<td>Unique request identifier for support</td>
</tr>
</tbody></table>
<h2>Common Error Codes</h2>
<h3>Authentication Errors</h3>
<pre><code class="language-json">{
  &quot;error&quot;: {
    &quot;code&quot;: &quot;UNAUTHORIZED&quot;,
    &quot;message&quot;: &quot;Invalid API key provided&quot;
  }
}
</code></pre>
<p><strong>Causes:</strong></p>
<ul>
<li>Missing <code>x-api-key</code> header</li>
<li>Invalid or expired API key</li>
<li>Missing <code>x-brand-key</code> header</li>
</ul>
<p><strong>Resolution:</strong></p>
<ul>
<li>Verify your API keys in the Admin panel</li>
<li>Check that both headers are included in the request</li>
<li>Ensure keys are correctly copied without extra whitespace</li>
</ul>
<h3>Permission Errors</h3>
<pre><code class="language-json">{
  &quot;error&quot;: {
    &quot;code&quot;: &quot;FORBIDDEN&quot;,
    &quot;message&quot;: &quot;Insufficient permissions for this operation&quot;
  }
}
</code></pre>
<p><strong>Causes:</strong></p>
<ul>
<li>Using a Public key for an operation requiring User/Service key</li>
<li>Attempting to access a resource outside your brand</li>
</ul>
<p><strong>Resolution:</strong></p>
<ul>
<li>Use the appropriate key type for the operation</li>
<li>Verify the brand key matches the resource</li>
</ul>
<h3>Validation Errors</h3>
<pre><code class="language-json">{
  &quot;error&quot;: {
    &quot;code&quot;: &quot;VALIDATION_ERROR&quot;,
    &quot;message&quot;: &quot;Request validation failed&quot;,
    &quot;details&quot;: {
      &quot;fields&quot;: [
        {
          &quot;field&quot;: &quot;userId&quot;,
          &quot;error&quot;: &quot;Field is required&quot;
        },
        {
          &quot;field&quot;: &quot;context.product&quot;,
          &quot;error&quot;: &quot;Must be one of: Gaming, Sports, Ecommerce&quot;
        }
      ]
    }
  }
}
</code></pre>
<p><strong>Resolution:</strong></p>
<ul>
<li>Review the fields listed in the error</li>
<li>Check required fields are present</li>
<li>Verify field values match expected formats</li>
</ul>
<h3>Resource Not Found</h3>
<pre><code class="language-json">{
  &quot;error&quot;: {
    &quot;code&quot;: &quot;NOT_FOUND&quot;,
    &quot;message&quot;: &quot;Placement not found: invalid-placement-key&quot;
  }
}
</code></pre>
<p><strong>Causes:</strong></p>
<ul>
<li>Incorrect placement or layout key</li>
<li>Resource deleted from Admin panel</li>
<li>Typo in the resource identifier</li>
</ul>
<p><strong>Resolution:</strong></p>
<ul>
<li>Verify the key in the Admin panel</li>
<li>Check for typos in your request URL</li>
</ul>
<h3>Rate Limit Errors</h3>
<pre><code class="language-json">{
  &quot;error&quot;: {
    &quot;code&quot;: &quot;RATE_LIMIT_EXCEEDED&quot;,
    &quot;message&quot;: &quot;Too many requests&quot;,
    &quot;details&quot;: {
      &quot;retryAfter&quot;: 10
    }
  }
}
</code></pre>
<p><strong>Resolution:</strong></p>
<ul>
<li>Implement exponential backoff</li>
<li>Review your request patterns</li>
<li>See the <a href="#rate-limits">Rate Limits Guide</a></li>
</ul>
<h2>Retry Strategy</h2>
<p>For transient errors (5xx codes, network issues, rate limits), implement a retry strategy with exponential backoff.</p>
<h3>Exponential Backoff Algorithm</h3>
<ol>
<li>Make the initial request</li>
<li>If it fails with a retryable error, wait and retry</li>
<li>Double the wait time for each subsequent retry</li>
<li>Stop after a maximum number of retries</li>
</ol>
<h3>Retryable Errors</h3>
<table>
<thead>
<tr>
<th>Code</th>
<th>Retryable</th>
<th>Strategy</th>
</tr>
</thead>
<tbody><tr>
<td>429</td>
<td>Yes</td>
<td>Wait for <code>retryAfter</code> seconds, then retry</td>
</tr>
<tr>
<td>500</td>
<td>Yes</td>
<td>Exponential backoff</td>
</tr>
<tr>
<td>502</td>
<td>Yes</td>
<td>Exponential backoff</td>
</tr>
<tr>
<td>503</td>
<td>Yes</td>
<td>Exponential backoff</td>
</tr>
<tr>
<td>504</td>
<td>Yes</td>
<td>Exponential backoff</td>
</tr>
<tr>
<td>400</td>
<td>No</td>
<td>Fix the request</td>
</tr>
<tr>
<td>401</td>
<td>No</td>
<td>Fix authentication</td>
</tr>
<tr>
<td>403</td>
<td>No</td>
<td>Fix permissions</td>
</tr>
<tr>
<td>404</td>
<td>No</td>
<td>Fix the resource identifier</td>
</tr>
</tbody></table>
<h3>JavaScript Example</h3>
<pre><code class="language-javascript">async function fetchWithRetry(url, options, maxRetries = 3) {
  let lastError;

  for (let attempt = 0; attempt &lt; maxRetries; attempt++) {
    try {
      const response = await fetch(url, options);

      if (response.ok) {
        return await response.json();
      }

      // Don&#39;t retry client errors (except 429)
      if (response.status &gt;= 400 &amp;&amp; response.status &lt; 500 &amp;&amp; response.status !== 429) {
        const error = await response.json();
        throw new Error(`API Error: ${error.error.message}`);
      }

      // Handle rate limiting
      if (response.status === 429) {
        const errorData = await response.json();
        const retryAfter = errorData.error?.details?.retryAfter || 10;
        await sleep(retryAfter * 1000);
        continue;
      }

      // Server error - retry with backoff
      lastError = new Error(`Server error: ${response.status}`);

    } catch (networkError) {
      lastError = networkError;
    }

    // Exponential backoff: 1s, 2s, 4s
    const backoffMs = Math.pow(2, attempt) * 1000;
    await sleep(backoffMs);
  }

  throw lastError;
}

function sleep(ms) {
  return new Promise(resolve =&gt; setTimeout(resolve, ms));
}
</code></pre>
<h3>Python Example</h3>
<pre><code class="language-python">import time
import requests
from typing import Optional

def fetch_with_retry(
    url: str,
    headers: dict,
    data: Optional[dict] = None,
    max_retries: int = 3
) -&gt; dict:
    &quot;&quot;&quot;Make API request with exponential backoff retry.&quot;&quot;&quot;

    last_error = None

    for attempt in range(max_retries):
        try:
            if data:
                response = requests.post(url, headers=headers, json=data)
            else:
                response = requests.get(url, headers=headers)

            if response.ok:
                return response.json()

            # Don&#39;t retry client errors (except 429)
            if 400 &lt;= response.status_code &lt; 500 and response.status_code != 429:
                error_data = response.json()
                raise Exception(f&quot;API Error: {error_data[&#39;error&#39;][&#39;message&#39;]}&quot;)

            # Handle rate limiting
            if response.status_code == 429:
                error_data = response.json()
                retry_after = error_data.get(&#39;error&#39;, {}).get(&#39;details&#39;, {}).get(&#39;retryAfter&#39;, 10)
                time.sleep(retry_after)
                continue

            # Server error - retry with backoff
            last_error = Exception(f&quot;Server error: {response.status_code}&quot;)

        except requests.RequestException as e:
            last_error = e

        # Exponential backoff: 1s, 2s, 4s
        backoff_seconds = (2 ** attempt)
        time.sleep(backoff_seconds)

    raise last_error
</code></pre>
<h2>Graceful Degradation</h2>
<p>When API errors occur, your application should degrade gracefully rather than breaking entirely.</p>
<h3>Recommendation Fallbacks</h3>
<pre><code class="language-javascript">async function getRecommendations(userId, context) {
  try {
    const recommendations = await fetchRecommendations(userId, context);
    return recommendations;
  } catch (error) {
    console.error(&#39;Recommendation API error:&#39;, error);

    // Return cached recommendations if available
    const cached = getCachedRecommendations(userId);
    if (cached) {
      return cached;
    }

    // Return empty array - UI should handle gracefully
    return [];
  }
}
</code></pre>
<h3>UI Handling</h3>
<pre><code class="language-javascript">function renderRecommendations(recommendations) {
  if (!recommendations || recommendations.length === 0) {
    // Hide the recommendation section entirely
    document.getElementById(&#39;recommendations&#39;).style.display = &#39;none&#39;;
    return;
  }

  // Render recommendations normally
  // ...
}
</code></pre>
<h2>Logging and Monitoring</h2>
<h3>Include Request IDs</h3>
<p>Always log the <code>requestId</code> from error responses. This helps Opti-X support diagnose issues:</p>
<pre><code class="language-javascript">catch (error) {
  console.error(&#39;API Error&#39;, {
    message: error.message,
    requestId: error.requestId,
    timestamp: new Date().toISOString()
  });
}
</code></pre>
<h3>Monitor Error Rates</h3>
<p>Track error rates by:</p>
<ul>
<li>Endpoint</li>
<li>Error code</li>
<li>Time period</li>
</ul>
<p>Alert when error rates exceed thresholds to catch issues early.</p>
<h2>Getting Help</h2>
<p>When contacting Opti-X support about an error:</p>
<ol>
<li><strong>Include the requestId</strong> from the error response</li>
<li><strong>Provide the full request</strong> (URL, headers minus the API key, body)</li>
<li><strong>Note the timestamp</strong> when the error occurred</li>
<li><strong>Describe the frequency</strong> (one-time, intermittent, constant)</li>
</ol>
<hr>
<h2>Related Topics</h2>
<ul>
<li><a href="#api-reference-overview">API Overview</a></li>
<li><a href="#authentication">Authentication Guide</a></li>
<li><a href="#rate-limits">Rate Limits</a></li>
</ul>

</section>
<section id="events-overview" class="doc-section">
<h1>Events Overview</h1>
<p>Events are the foundation of Opti-X&#39;s personalization engine. They capture user actions and behaviors in real-time, enabling the system to deliver relevant recommendations and trigger timely campaigns.</p>
<h2>What Are Events?</h2>
<p>Events represent discrete user actions on your platform. Each event contains:</p>
<ul>
<li><strong>User identifier</strong>: Links the action to a specific user</li>
<li><strong>Event type</strong>: Categorizes the action (e.g., page view, purchase, game launch)</li>
<li><strong>Timestamp</strong>: Records when the action occurred</li>
<li><strong>Context data</strong>: Provides additional details about the action</li>
</ul>
<p>When users interact with your platform, these events flow into Opti-X and build a comprehensive picture of user behavior over time.</p>
<h2>Why Events Matter</h2>
<p>Events power two core capabilities:</p>
<ol>
<li><p><strong>Personalized Recommendations</strong>: Opti-X analyzes event patterns to understand user preferences and predict what content or products they want to see next.</p>
</li>
<li><p><strong>Smart Campaigns</strong>: Events trigger automated campaigns at the right moment, such as sending a notification when a user&#39;s favorite team is about to play or alerting them when a previously viewed item drops in price.</p>
</li>
</ol>
<h2>Event Ingestion Methods</h2>
<p>Opti-X supports two primary methods for ingesting events:</p>
<h3>Real-Time Ingestion</h3>
<p>Real-time events stream directly to Opti-X as they occur. This method is ideal for:</p>
<ul>
<li>Page views and browsing behavior</li>
<li>Game launches and session activity</li>
<li>Bet placements and cart additions</li>
<li>Any action requiring immediate response</li>
</ul>
<p>Real-time ingestion uses the Opti-X SDK or direct API calls. For high-volume scenarios, AWS Kinesis integration provides scalable streaming.</p>
<h3>Batch Ingestion</h3>
<p>Batch ingestion processes events in scheduled intervals. This method suits:</p>
<ul>
<li>Historical data imports</li>
<li>Transactional data from backend systems</li>
<li>Data warehouse synchronization</li>
<li>Regulatory or compliance-related data</li>
</ul>
<p>Batch files are typically uploaded via SFTP or cloud storage integration.</p>
<h2>Event Types by Vertical</h2>
<p>Different industries require different event types. Opti-X supports specialized events for each vertical:</p>
<h3>Gaming Events</h3>
<ul>
<li><strong>Game Launch</strong>: User starts playing a game</li>
<li><strong>Game Session</strong>: Tracks gameplay duration and outcomes</li>
<li><strong>Game Close</strong>: User ends a gaming session</li>
<li><strong>Page View</strong>: User views a game detail page</li>
</ul>
<h3>Sports Betting Events</h3>
<ul>
<li><strong>Bet Placement</strong>: User places a bet</li>
<li><strong>Add to Betslip</strong>: User adds a selection to their betslip</li>
<li><strong>Bet Settlement</strong>: Bet outcome is determined</li>
</ul>
<h3>E-commerce Events</h3>
<ul>
<li><strong>Product View</strong>: User views a product page</li>
<li><strong>Add to Cart</strong>: User adds an item to their cart</li>
<li><strong>Remove from Cart</strong>: User removes an item from their cart</li>
<li><strong>Online Order</strong>: User completes a purchase</li>
</ul>
<h3>Standard Events</h3>
<p>These events apply across all verticals:</p>
<ul>
<li><strong>Page Visit</strong>: User views any page</li>
<li><strong>Registration</strong>: User creates an account</li>
<li><strong>Login</strong>: User signs into their account</li>
<li><strong>Deposit</strong>: User adds funds to their account</li>
<li><strong>Withdrawal</strong>: User removes funds from their account</li>
</ul>
<h2>How Events Power Recommendations</h2>
<p>The recommendation engine uses events to:</p>
<ol>
<li><strong>Build user profiles</strong>: Aggregate behavior patterns over time</li>
<li><strong>Identify similar users</strong>: Find users with comparable interests</li>
<li><strong>Detect trends</strong>: Recognize popular and trending content</li>
<li><strong>Predict preferences</strong>: Anticipate what users want to see next</li>
</ol>
<p>Different recommendation methods rely on different event combinations. For example:</p>
<ul>
<li>The &quot;Recently Played&quot; method uses Game Launch events</li>
<li>The &quot;Similar Users&quot; method combines Game Launch and Page View events</li>
<li>The &quot;Hybrid&quot; method synthesizes multiple event types for comprehensive personalization</li>
</ul>
<h2>How Events Trigger Campaigns</h2>
<p>Smart Campaigns use events to:</p>
<ol>
<li><strong>Identify trigger conditions</strong>: Detect when a user meets campaign criteria</li>
<li><strong>Personalize content</strong>: Select relevant offers or messages</li>
<li><strong>Time delivery</strong>: Send communications at optimal moments</li>
<li><strong>Track outcomes</strong>: Measure campaign effectiveness</li>
</ol>
<p>For example, a &quot;Favorite Team Alert&quot; campaign monitors Bet Placement events to identify a user&#39;s preferred teams, then sends notifications before those teams play.</p>
<h2>Best Practices</h2>
<p><strong>Send events as they occur</strong>: Real-time data enables real-time personalization. Delays reduce recommendation accuracy and campaign timeliness.</p>
<p><strong>Include all available context</strong>: Rich event data improves personalization quality. Include optional parameters when available.</p>
<p><strong>Maintain consistent user identifiers</strong>: Use the same user ID across all events to build complete user profiles.</p>
<p><strong>Validate event data</strong>: Ensure events contain required fields and valid values before sending.</p>
<p><strong>Monitor event flow</strong>: Track event volumes and latency to catch integration issues early.</p>
<hr>
<h2>Related Topics</h2>
<ul>
<li><a href="#standard-events">Standard Events</a> - Common events across all verticals</li>
<li><a href="#gaming-events">Gaming Events</a> - Events for casino and gaming platforms</li>
<li><a href="#sports-events">Sports Events</a> - Events for sports betting platforms</li>
<li><a href="#ecommerce-events">E-commerce Events</a> - Events for retail and e-commerce</li>
<li><a href="#kinesis-integration">AWS Kinesis Integration</a> - High-volume event streaming</li>
</ul>

</section>
<section id="standard-events" class="doc-section">
<h1>Standard User Events</h1>
<p>Standard events capture fundamental user activities that apply across all verticals. These events track account-related actions such as registrations, logins, deposits, and withdrawals, as well as basic browsing behavior.</p>
<p>Implementing standard events enables core Opti-X functionality and provides the foundation for vertical-specific features.</p>
<h2>Page Visit</h2>
<p>The Page Visit event records when a user views a specific page on your platform. This is the most fundamental event type and is <strong>mandatory</strong> for Opti-X integration.</p>
<p>Page Visit events enable:</p>
<ul>
<li>Browsing behavior analysis</li>
<li>Content popularity tracking</li>
<li>User journey mapping</li>
<li>Recommendation personalization based on viewing history</li>
</ul>
<h3>Why This Matters</h3>
<p>Without Page Visit events, Opti-X cannot understand how users navigate your platform. This event forms the basis for &quot;Similar Users&quot; recommendations and contributes to nearly every personalization method.</p>
<h3>Event Setup</h3>
<table>
<thead>
<tr>
<th>Event Key</th>
<th>Event Name</th>
<th>Type</th>
</tr>
</thead>
<tbody><tr>
<td>set_page_visit</td>
<td>Page Visit</td>
<td>Simple event</td>
</tr>
</tbody></table>
<h3>Event Parameters</h3>
<table>
<thead>
<tr>
<th>Parameter Key</th>
<th>Parameter Name</th>
<th>Type</th>
<th>Required</th>
</tr>
</thead>
<tbody><tr>
<td>customURL</td>
<td>Custom URL</td>
<td>String</td>
<td>Yes</td>
</tr>
<tr>
<td>pageTitle</td>
<td>Page Title</td>
<td>String</td>
<td>Yes</td>
</tr>
<tr>
<td>category</td>
<td>Page Category</td>
<td>String</td>
<td>Optional</td>
</tr>
</tbody></table>
<h3>Example</h3>
<pre><code class="language-json">{
  &quot;event_key&quot;: &quot;set_page_visit&quot;,
  &quot;user_id&quot;: &quot;user_12345&quot;,
  &quot;params&quot;: {
    &quot;customURL&quot;: &quot;/games/slots/starburst&quot;,
    &quot;pageTitle&quot;: &quot;Starburst Slot Game&quot;,
    &quot;category&quot;: &quot;slots&quot;
  }
}
</code></pre>
<hr>
<h2>Registration</h2>
<p>The Registration event captures when users create new accounts on your platform. This event is essential for tracking user acquisition and enabling welcome campaigns.</p>
<p>Registration events enable:</p>
<ul>
<li>New user identification</li>
<li>Welcome campaign triggers</li>
<li>Registration funnel analysis</li>
<li>Email collection for communications</li>
</ul>
<h3>Why This Matters</h3>
<p>Registration marks the beginning of a user&#39;s journey. Capturing this event allows Opti-X to trigger onboarding campaigns and begin building a personalization profile from day one.</p>
<h3>Event Setup</h3>
<table>
<thead>
<tr>
<th>Event Key</th>
<th>Event Name</th>
<th>Type</th>
</tr>
</thead>
<tbody><tr>
<td>core_registration</td>
<td>Core Registration</td>
<td>Simple event</td>
</tr>
</tbody></table>
<h3>Recommended Parameters</h3>
<table>
<thead>
<tr>
<th>Parameter Key</th>
<th>Parameter Name</th>
<th>Type</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>email</td>
<td>Email</td>
<td>String</td>
<td>Required for email campaigns after registration</td>
</tr>
<tr>
<td>first_name</td>
<td>First Name</td>
<td>String</td>
<td>Enables personalization tags in communications</td>
</tr>
</tbody></table>
<h3>Example</h3>
<pre><code class="language-json">{
  &quot;event_key&quot;: &quot;core_registration&quot;,
  &quot;user_id&quot;: &quot;user_12345&quot;,
  &quot;params&quot;: {
    &quot;email&quot;: &quot;user@example.com&quot;,
    &quot;first_name&quot;: &quot;Alex&quot;
  }
}
</code></pre>
<hr>
<h2>Login</h2>
<p>The Login event tracks when users sign into their accounts. This event helps identify active users and enables session-based personalization.</p>
<p>Login events enable:</p>
<ul>
<li>Active user identification</li>
<li>Session start tracking</li>
<li>Login frequency analysis</li>
<li>Re-engagement campaign targeting</li>
</ul>
<h3>Why This Matters</h3>
<p>Login events help distinguish active users from dormant ones. Combined with other events, login data enables campaigns that target users based on their engagement patterns.</p>
<h3>Event Setup</h3>
<table>
<thead>
<tr>
<th>Event Key</th>
<th>Event Name</th>
<th>Type</th>
</tr>
</thead>
<tbody><tr>
<td>core_login</td>
<td>Core Login</td>
<td>Simple event</td>
</tr>
</tbody></table>
<h3>Recommended Parameters</h3>
<table>
<thead>
<tr>
<th>Parameter Key</th>
<th>Parameter Name</th>
<th>Type</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>login_timestamp</td>
<td>Login Timestamp</td>
<td>String</td>
<td>ISO 8601 datetime of login</td>
</tr>
<tr>
<td>balance</td>
<td>Balance</td>
<td>Number</td>
<td>User&#39;s account balance at login</td>
</tr>
<tr>
<td>is_first_login</td>
<td>Is First Login</td>
<td>Boolean</td>
<td>Indicates first-time login</td>
</tr>
<tr>
<td>session_ref</td>
<td>Session Reference</td>
<td>String</td>
<td>Unique session identifier</td>
</tr>
<tr>
<td>ccy_code</td>
<td>Currency Code</td>
<td>String</td>
<td>User&#39;s currency (e.g., &quot;GBP&quot;, &quot;USD&quot;)</td>
</tr>
<tr>
<td>language</td>
<td>Language</td>
<td>String</td>
<td>User&#39;s language preference (e.g., &quot;en&quot;)</td>
</tr>
<tr>
<td>country</td>
<td>Country</td>
<td>String</td>
<td>User&#39;s country code (e.g., &quot;GB&quot;)</td>
</tr>
<tr>
<td>platform</td>
<td>Platform</td>
<td>String</td>
<td>Device platform (e.g., &quot;iOS&quot;, &quot;Android&quot;, &quot;Web&quot;)</td>
</tr>
<tr>
<td>channel</td>
<td>Channel</td>
<td>String</td>
<td>Access channel (e.g., &quot;Mobile App&quot;, &quot;Desktop&quot;)</td>
</tr>
<tr>
<td>skinid</td>
<td>Skin ID</td>
<td>String</td>
<td>Brand or skin identifier</td>
</tr>
<tr>
<td>license</td>
<td>License</td>
<td>String</td>
<td>Regulatory license (e.g., &quot;UKGC&quot;, &quot;MGA&quot;)</td>
</tr>
</tbody></table>
<h3>Example</h3>
<pre><code class="language-json">{
  &quot;event_key&quot;: &quot;core_login&quot;,
  &quot;user_id&quot;: &quot;user_12345&quot;,
  &quot;params&quot;: {
    &quot;login_timestamp&quot;: &quot;2024-01-15T14:30:00Z&quot;,
    &quot;balance&quot;: 150.00,
    &quot;is_first_login&quot;: false,
    &quot;ccy_code&quot;: &quot;GBP&quot;,
    &quot;language&quot;: &quot;en&quot;,
    &quot;country&quot;: &quot;GB&quot;,
    &quot;platform&quot;: &quot;iOS&quot;,
    &quot;channel&quot;: &quot;Mobile App&quot;,
    &quot;license&quot;: &quot;UKGC&quot;
  }
}
</code></pre>
<hr>
<h2>Deposit</h2>
<p>The Deposit event records when a user adds funds to their account. This event is critical for financial tracking and enables deposit-related campaigns.</p>
<p>Deposit events enable:</p>
<ul>
<li>Financial activity tracking</li>
<li>Deposit confirmation campaigns</li>
<li>VIP tier calculations</li>
<li>Spending pattern analysis</li>
</ul>
<h3>Why This Matters</h3>
<p>Deposit events indicate user commitment and enable campaigns that encourage continued engagement. They also help identify high-value users for VIP treatment.</p>
<h3>Event Setup</h3>
<table>
<thead>
<tr>
<th>Event Key</th>
<th>Event Name</th>
<th>Type</th>
</tr>
</thead>
<tbody><tr>
<td>core_deposit</td>
<td>Core Deposit</td>
<td>Simple event</td>
</tr>
</tbody></table>
<h3>Recommended Parameters</h3>
<table>
<thead>
<tr>
<th>Parameter Key</th>
<th>Parameter Name</th>
<th>Type</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>deposit_timestamp</td>
<td>Deposit Timestamp</td>
<td>String</td>
<td>ISO 8601 datetime of deposit</td>
</tr>
<tr>
<td>start_balance</td>
<td>Start Balance</td>
<td>Number</td>
<td>Balance before deposit</td>
</tr>
<tr>
<td>deposit_amount</td>
<td>Deposit Amount</td>
<td>Number</td>
<td>Amount deposited</td>
</tr>
<tr>
<td>deposit_method</td>
<td>Deposit Method</td>
<td>String</td>
<td>Payment method (e.g., &quot;Credit Card&quot;, &quot;PayPal&quot;)</td>
</tr>
<tr>
<td>deposit_status</td>
<td>Deposit Status</td>
<td>String</td>
<td>Transaction status (e.g., &quot;completed&quot;, &quot;pending&quot;)</td>
</tr>
<tr>
<td>ccy_code</td>
<td>Currency Code</td>
<td>String</td>
<td>Transaction currency</td>
</tr>
<tr>
<td>language</td>
<td>Language</td>
<td>String</td>
<td>User&#39;s language preference</td>
</tr>
<tr>
<td>country</td>
<td>Country</td>
<td>String</td>
<td>User&#39;s country code</td>
</tr>
<tr>
<td>platform</td>
<td>Platform</td>
<td>String</td>
<td>Device platform</td>
</tr>
<tr>
<td>channel</td>
<td>Channel</td>
<td>String</td>
<td>Access channel</td>
</tr>
<tr>
<td>skinid</td>
<td>Skin ID</td>
<td>String</td>
<td>Brand or skin identifier</td>
</tr>
<tr>
<td>license</td>
<td>License</td>
<td>String</td>
<td>Regulatory license</td>
</tr>
</tbody></table>
<h3>Example</h3>
<pre><code class="language-json">{
  &quot;event_key&quot;: &quot;core_deposit&quot;,
  &quot;user_id&quot;: &quot;user_12345&quot;,
  &quot;params&quot;: {
    &quot;deposit_timestamp&quot;: &quot;2024-01-15T14:35:00Z&quot;,
    &quot;start_balance&quot;: 50.00,
    &quot;deposit_amount&quot;: 100.00,
    &quot;deposit_method&quot;: &quot;Credit Card&quot;,
    &quot;deposit_status&quot;: &quot;completed&quot;,
    &quot;ccy_code&quot;: &quot;GBP&quot;,
    &quot;country&quot;: &quot;GB&quot;,
    &quot;platform&quot;: &quot;iOS&quot;,
    &quot;license&quot;: &quot;UKGC&quot;
  }
}
</code></pre>
<hr>
<h2>Withdrawal</h2>
<p>The Withdrawal event records when a user removes funds from their account. This event helps track cash-out behavior and enables retention campaigns.</p>
<p>Withdrawal events enable:</p>
<ul>
<li>Cash-out pattern analysis</li>
<li>Withdrawal confirmation communications</li>
<li>Retention campaign triggers</li>
<li>Financial reporting</li>
</ul>
<h3>Why This Matters</h3>
<p>Withdrawal events can signal user intent to reduce engagement. Capturing this data enables timely retention campaigns and helps identify users who might benefit from re-engagement offers.</p>
<h3>Event Setup</h3>
<table>
<thead>
<tr>
<th>Event Key</th>
<th>Event Name</th>
<th>Type</th>
</tr>
</thead>
<tbody><tr>
<td>core_withdrawal</td>
<td>Core Withdrawal</td>
<td>Simple event</td>
</tr>
</tbody></table>
<h3>Recommended Parameters</h3>
<table>
<thead>
<tr>
<th>Parameter Key</th>
<th>Parameter Name</th>
<th>Type</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>withdrawal_timestamp</td>
<td>Withdrawal Timestamp</td>
<td>String</td>
<td>ISO 8601 datetime of withdrawal request</td>
</tr>
<tr>
<td>start_balance</td>
<td>Start Balance</td>
<td>Number</td>
<td>Balance before withdrawal</td>
</tr>
<tr>
<td>withdrawal_amount</td>
<td>Withdrawal Amount</td>
<td>Number</td>
<td>Amount withdrawn</td>
</tr>
<tr>
<td>withdrawal_method</td>
<td>Withdrawal Method</td>
<td>String</td>
<td>Payout method (e.g., &quot;Bank Transfer&quot;)</td>
</tr>
<tr>
<td>withdrawal_status</td>
<td>Withdrawal Status</td>
<td>String</td>
<td>Transaction status (Optional)</td>
</tr>
<tr>
<td>ccy_code</td>
<td>Currency Code</td>
<td>String</td>
<td>Transaction currency</td>
</tr>
<tr>
<td>language</td>
<td>Language</td>
<td>String</td>
<td>User&#39;s language preference</td>
</tr>
<tr>
<td>country</td>
<td>Country</td>
<td>String</td>
<td>User&#39;s country code</td>
</tr>
<tr>
<td>platform</td>
<td>Platform</td>
<td>String</td>
<td>Device platform</td>
</tr>
<tr>
<td>channel</td>
<td>Channel</td>
<td>String</td>
<td>Access channel</td>
</tr>
<tr>
<td>skinid</td>
<td>Skin ID</td>
<td>String</td>
<td>Brand or skin identifier</td>
</tr>
<tr>
<td>license</td>
<td>License</td>
<td>String</td>
<td>Regulatory license</td>
</tr>
</tbody></table>
<h3>Example</h3>
<pre><code class="language-json">{
  &quot;event_key&quot;: &quot;core_withdrawal&quot;,
  &quot;user_id&quot;: &quot;user_12345&quot;,
  &quot;params&quot;: {
    &quot;withdrawal_timestamp&quot;: &quot;2024-01-15T16:00:00Z&quot;,
    &quot;start_balance&quot;: 250.00,
    &quot;withdrawal_amount&quot;: 100.00,
    &quot;withdrawal_method&quot;: &quot;Bank Transfer&quot;,
    &quot;withdrawal_status&quot;: &quot;pending&quot;,
    &quot;ccy_code&quot;: &quot;GBP&quot;,
    &quot;country&quot;: &quot;GB&quot;,
    &quot;platform&quot;: &quot;Web&quot;
  }
}
</code></pre>
<hr>
<h2>Withdrawal Cancellation</h2>
<p>The Withdrawal Cancellation event captures when a user cancels a pending withdrawal. This event indicates renewed engagement intent.</p>
<p>Withdrawal cancellation events enable:</p>
<ul>
<li>Cancellation pattern tracking</li>
<li>Balance update notifications</li>
<li>Engagement opportunity identification</li>
</ul>
<h3>Why This Matters</h3>
<p>When users cancel withdrawals, they often intend to continue playing. This event creates opportunities for targeted content recommendations and personalized offers.</p>
<h3>Event Setup</h3>
<table>
<thead>
<tr>
<th>Event Key</th>
<th>Event Name</th>
<th>Type</th>
</tr>
</thead>
<tbody><tr>
<td>core_withdrawal_cancellation</td>
<td>Core Withdrawal Cancellation</td>
<td>Simple event</td>
</tr>
</tbody></table>
<h3>Recommended Parameters</h3>
<table>
<thead>
<tr>
<th>Parameter Key</th>
<th>Parameter Name</th>
<th>Type</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>event_name</td>
<td>Event Name</td>
<td>String</td>
<td>core_withdrawal_cancellation</td>
</tr>
<tr>
<td>withdrawal_cancel_timestamp</td>
<td>Cancellation Timestamp</td>
<td>String</td>
<td>ISO 8601 datetime of cancellation</td>
</tr>
<tr>
<td>end_balance</td>
<td>End Balance</td>
<td>Number</td>
<td>Balance after cancellation</td>
</tr>
<tr>
<td>withdrawal_amount</td>
<td>Withdrawal Amount</td>
<td>Number</td>
<td>Originally requested amount</td>
</tr>
<tr>
<td>withdrawal_method</td>
<td>Withdrawal Method</td>
<td>String</td>
<td>Original payout method</td>
</tr>
<tr>
<td>withdrawal_status</td>
<td>Withdrawal Status</td>
<td>String</td>
<td>Status (Optional)</td>
</tr>
<tr>
<td>ccy_code</td>
<td>Currency Code</td>
<td>String</td>
<td>Transaction currency</td>
</tr>
<tr>
<td>language</td>
<td>Language</td>
<td>String</td>
<td>User&#39;s language preference</td>
</tr>
<tr>
<td>country</td>
<td>Country</td>
<td>String</td>
<td>User&#39;s country code</td>
</tr>
<tr>
<td>platform</td>
<td>Platform</td>
<td>String</td>
<td>Device platform</td>
</tr>
<tr>
<td>channel</td>
<td>Channel</td>
<td>String</td>
<td>Access channel</td>
</tr>
<tr>
<td>skinid</td>
<td>Skin ID</td>
<td>String</td>
<td>Brand or skin identifier</td>
</tr>
<tr>
<td>license</td>
<td>License</td>
<td>String</td>
<td>Regulatory license</td>
</tr>
</tbody></table>
<h3>Example</h3>
<pre><code class="language-json">{
  &quot;event_key&quot;: &quot;core_withdrawal_cancellation&quot;,
  &quot;user_id&quot;: &quot;user_12345&quot;,
  &quot;params&quot;: {
    &quot;event_name&quot;: &quot;core_withdrawal_cancellation&quot;,
    &quot;withdrawal_cancel_timestamp&quot;: &quot;2024-01-15T16:30:00Z&quot;,
    &quot;end_balance&quot;: 250.00,
    &quot;withdrawal_amount&quot;: 100.00,
    &quot;withdrawal_method&quot;: &quot;Bank Transfer&quot;,
    &quot;ccy_code&quot;: &quot;GBP&quot;,
    &quot;country&quot;: &quot;GB&quot;
  }
}
</code></pre>
<hr>
<h2>Related Topics</h2>
<ul>
<li><a href="#events-overview">Events Overview</a> - Understanding the event system</li>
<li><a href="#gaming-events">Gaming Events</a> - Gaming-specific events</li>
<li><a href="#sports-events">Sports Events</a> - Sports betting events</li>
<li><a href="#ecommerce-events">E-commerce Events</a> - Retail and e-commerce events</li>
<li><a href="#kinesis-integration">AWS Kinesis Integration</a> - High-volume event streaming</li>
</ul>

</section>
<section id="gaming-events" class="doc-section">
<h1>Gaming Events</h1>
<p>This page explains how event data powers Opti-X Recommend and Smart Campaigns for gaming platforms. Understanding which events drive each feature helps you prioritize your integration and maximize personalization effectiveness.</p>
<blockquote>
<p><strong>Note</strong>: Event requirements may evolve as Opti-X adds new capabilities. To future-proof your integration, send as many relevant events as possible.</p>
</blockquote>
<blockquote>
<p><strong>Important</strong>: Both Recommend and Smart Campaigns require inventory data alongside events. Without a gaming inventory feed, recommendation and targeting logic cannot function. See <a href="#gaming-inventory">Gaming Inventory</a> for setup instructions.</p>
</blockquote>
<h2>Core Gaming Events</h2>
<p>Gaming platforms typically send these event types:</p>
<table>
<thead>
<tr>
<th>Event</th>
<th>Description</th>
<th>Primary Use</th>
</tr>
</thead>
<tbody><tr>
<td><strong>Game Launch</strong></td>
<td>User starts playing a game</td>
<td>Powers most recommendation methods</td>
</tr>
<tr>
<td><strong>Game Close</strong></td>
<td>User ends a gaming session</td>
<td>Session duration tracking</td>
</tr>
<tr>
<td><strong>Game Session</strong></td>
<td>Tracks gameplay metrics (duration, wins, bets)</td>
<td>Win-based recommendations, financial methods</td>
</tr>
<tr>
<td><strong>Page View</strong></td>
<td>User views a game detail page</td>
<td>Similar Users, browsing-based recommendations</td>
</tr>
<tr>
<td><strong>Registration</strong></td>
<td>User creates an account</td>
<td>Campaign targeting, new user journeys</td>
</tr>
<tr>
<td><strong>Deposit</strong></td>
<td>User adds funds to account</td>
<td>Financial segmentation</td>
</tr>
</tbody></table>
<h2>Why This Matters</h2>
<p>Gaming events form the foundation of personalized game discovery. When a user launches games, Opti-X learns their preferences and can recommend similar titles. When combined with session data showing wins and gameplay duration, the system identifies patterns that drive engagement.</p>
<p>For example:</p>
<ul>
<li>A user who frequently launches slot games with Irish themes will see more Irish-themed slots in their recommendations</li>
<li>A user who recently won on a specific game type may receive &quot;Previous Win&quot; recommendations featuring similar games</li>
<li>Popular games among users with similar behavior patterns surface through &quot;Similar Users&quot; methods</li>
</ul>
<h2>Recommend Methods</h2>
<p>Each recommendation method relies on specific events to generate personalized results:</p>
<table>
<thead>
<tr>
<th>Method</th>
<th>Events Used</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>Similar Users</td>
<td>Game Launch, Page View</td>
<td>Recommends games popular among users with similar behavior</td>
</tr>
<tr>
<td>Release Date</td>
<td>Inventory data only</td>
<td>Surfaces newly released games</td>
</tr>
<tr>
<td>Behavioural</td>
<td>Game Launch</td>
<td>Analyzes play patterns to predict preferences</td>
</tr>
<tr>
<td>New Games</td>
<td>Game Launch</td>
<td>Highlights new games based on user&#39;s genre preferences</td>
</tr>
<tr>
<td>Similar Items</td>
<td>Game Launch</td>
<td>Finds games similar to those the user has played</td>
</tr>
<tr>
<td>New Games Boost</td>
<td>Game Launch, Page View</td>
<td>Promotes new releases to likely interested users</td>
</tr>
<tr>
<td>Recently Played</td>
<td>Game Launch</td>
<td>Shows games the user played recently</td>
</tr>
<tr>
<td>Previously Played</td>
<td>Game Launch</td>
<td>Resurfaces games from the user&#39;s history</td>
</tr>
<tr>
<td>Remember This?</td>
<td>Game Launch</td>
<td>Re-engages users with games they haven&#39;t played in a while</td>
</tr>
<tr>
<td>Favourite Game</td>
<td>Game Launch, Game Session</td>
<td>Identifies and promotes the user&#39;s most-played games</td>
</tr>
<tr>
<td>Previous Win</td>
<td>Game Session</td>
<td>Recommends games where the user has won before</td>
</tr>
<tr>
<td>Hybrid</td>
<td>Game Launch, Game Session, Page View</td>
<td>Combines multiple signals for comprehensive personalization</td>
</tr>
<tr>
<td>Themed Content</td>
<td>Game Launch, Game Session, Page View</td>
<td>Matches games to user&#39;s preferred themes</td>
</tr>
<tr>
<td>Popular</td>
<td>Game Launch</td>
<td>Shows globally popular games</td>
</tr>
<tr>
<td>Trending</td>
<td>Game Launch</td>
<td>Highlights games gaining popularity</td>
</tr>
<tr>
<td>Multi-Brand Popular</td>
<td>Game Launch</td>
<td>Surfaces popular games across multiple brands</td>
</tr>
<tr>
<td>Popular Near You</td>
<td>Game Launch</td>
<td>Shows games popular in the user&#39;s region</td>
</tr>
<tr>
<td>Financials</td>
<td>Game Launch, Game Session</td>
<td>Considers betting patterns and financial behavior</td>
</tr>
<tr>
<td>Sequential Model</td>
<td>Game Launch</td>
<td>Predicts the next game based on play sequences</td>
</tr>
</tbody></table>
<h2>Smart Campaign Use Cases</h2>
<p>Smart Campaigns use gaming events to trigger automated, personalized communications:</p>
<table>
<thead>
<tr>
<th>Use Case</th>
<th>Events Required</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>Least Active Day</td>
<td>Game Launch</td>
<td>Targets users on days they typically don&#39;t play</td>
</tr>
<tr>
<td>Simple Gaming Recommendations</td>
<td>Game Launch, Registration</td>
<td>Sends game suggestions to new users</td>
</tr>
<tr>
<td>General Gaming Recommendations</td>
<td>Game Launch, Registration</td>
<td>Delivers personalized game recommendations via campaigns</td>
</tr>
</tbody></table>
<h2>Integration Priority</h2>
<p>When implementing gaming events, prioritize in this order:</p>
<ol>
<li><strong>Game Launch</strong> (Critical) - Powers the majority of recommendation methods</li>
<li><strong>Page View</strong> (High) - Enables browsing-based personalization</li>
<li><strong>Game Session</strong> (High) - Unlocks win-based and financial recommendations</li>
<li><strong>Registration</strong> (Medium) - Required for new user campaigns</li>
<li><strong>Game Close</strong> (Medium) - Completes session tracking</li>
<li><strong>Deposit</strong> (Medium) - Enables financial segmentation</li>
</ol>
<h2>Filtering Considerations</h2>
<p>Gaming recommendations support filtering to ensure users see only relevant, compliant content. Common filters include:</p>
<ul>
<li><strong>License-based filtering</strong>: Show only games available under the user&#39;s regulatory license</li>
<li><strong>Currency filtering</strong>: Display games supporting the user&#39;s currency</li>
<li><strong>Region-based filtering</strong>: Surface games popular or available in the user&#39;s location</li>
<li><strong>Supplier filtering</strong>: Include or exclude games from specific providers</li>
</ul>
<p>See <a href="#gaming-filtering">Gaming Filtering</a> for implementation details.</p>
<hr>
<h2>Related Topics</h2>
<ul>
<li><a href="#events-overview">Events Overview</a> - Understanding the event system</li>
<li><a href="#standard-events">Standard Events</a> - Common events across verticals</li>
<li><a href="#gaming-inventory">Gaming Inventory</a> - Setting up game catalog data</li>
<li><a href="#gaming-filtering">Gaming Filtering</a> - Filtering recommendations by tags and regions</li>
<li><a href="#kinesis-integration">AWS Kinesis Integration</a> - High-volume event streaming</li>
</ul>

</section>
<section id="sports-events" class="doc-section">
<h1>Sports Events</h1>
<p>This page explains how event data powers Opti-X Recommend and Smart Campaigns for sports betting platforms. Understanding which events drive each feature helps you prioritize your integration and deliver relevant betting recommendations.</p>
<blockquote>
<p><strong>Note</strong>: Event requirements may evolve as Opti-X adds new capabilities. To future-proof your integration, send as many relevant events as possible.</p>
</blockquote>
<blockquote>
<p><strong>Important</strong>: Both Recommend and Smart Campaigns require inventory data alongside events. Without a sports inventory feed, recommendation and targeting logic cannot function. See <a href="#sports-inventory">Sports Inventory</a> for setup instructions.</p>
</blockquote>
<h2>Core Sports Events</h2>
<p>Sports betting platforms typically send these event types:</p>
<table>
<thead>
<tr>
<th>Event</th>
<th>Description</th>
<th>Primary Use</th>
</tr>
</thead>
<tbody><tr>
<td><strong>Bet Placement</strong></td>
<td>User places a bet</td>
<td>Powers most recommendation methods and campaigns</td>
</tr>
<tr>
<td><strong>Add to Betslip</strong></td>
<td>User adds a selection to their betslip</td>
<td>Intent tracking, betslip optimization</td>
</tr>
<tr>
<td><strong>Bet Settlement</strong></td>
<td>Bet outcome is determined (win/loss)</td>
<td>Prior Win recommendations, outcome-based targeting</td>
</tr>
</tbody></table>
<h2>Why This Matters</h2>
<p>Sports betting events capture user intent and preferences at multiple stages. When a user adds a selection to their betslip, they signal interest even before committing money. When they place a bet, they demonstrate strong preference. And when bets settle, outcomes inform future recommendations.</p>
<p>For example:</p>
<ul>
<li>A user who frequently bets on Premier League football will see more Premier League markets</li>
<li>A user who adds tennis selections to their betslip but doesn&#39;t always bet may receive prompts about tennis events</li>
<li>A user who recently won on horse racing may see &quot;Prior Win&quot; recommendations for upcoming races</li>
</ul>
<h2>Recommend Methods</h2>
<p>Each recommendation method relies on specific events to generate personalized betting suggestions:</p>
<table>
<thead>
<tr>
<th>Method</th>
<th>Events Used</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>Similar Pre-event Category</td>
<td>Bet Placement</td>
<td>Recommends pre-match bets based on user&#39;s category preferences</td>
</tr>
<tr>
<td>Similar In-play Category</td>
<td>Bet Placement</td>
<td>Suggests live betting options matching user interests</td>
</tr>
<tr>
<td>Bet Builder</td>
<td>Bet Placement, Add to Betslip, Bet Settlement</td>
<td>Creates personalized multi-selection bet suggestions</td>
</tr>
<tr>
<td>Bet Builder Market</td>
<td>Bet Placement</td>
<td>Suggests markets for bet builder combinations</td>
</tr>
<tr>
<td>Trending</td>
<td>Bet Placement, Add to Betslip, Bet Settlement</td>
<td>Highlights markets gaining popularity</td>
</tr>
<tr>
<td>BetSlip</td>
<td>Bet Placement</td>
<td>Optimizes betslip with complementary selections</td>
</tr>
<tr>
<td>Popular</td>
<td>Bet Placement, Add to Betslip, Bet Settlement</td>
<td>Shows globally popular betting markets</td>
</tr>
<tr>
<td>Hybrid</td>
<td>Bet Placement, Add to Betslip, Bet Settlement</td>
<td>Combines multiple signals for comprehensive personalization</td>
</tr>
<tr>
<td>Behavioural 2.0</td>
<td>Bet Placement, Add to Betslip, Bet Settlement</td>
<td>Advanced behavior-based recommendations</td>
</tr>
<tr>
<td>Categories, Classes, Types</td>
<td>Bet Placement</td>
<td>Recommends based on betting category preferences</td>
</tr>
<tr>
<td>Personalised Popular</td>
<td>Bet Placement</td>
<td>Blends popularity with individual preferences</td>
</tr>
<tr>
<td>In-Play</td>
<td>Bet Placement</td>
<td>Focuses on live betting opportunities</td>
</tr>
<tr>
<td>Extra Leg</td>
<td>Bet Placement</td>
<td>Suggests additional selections for existing bets</td>
</tr>
<tr>
<td>Favourite Team</td>
<td>Bet Placement</td>
<td>Identifies and promotes bets on user&#39;s preferred teams</td>
</tr>
<tr>
<td>Explicit Popular</td>
<td>Bet Placement</td>
<td>Surfaces explicitly popular markets</td>
</tr>
<tr>
<td>Prior Win</td>
<td>Bet Settlement</td>
<td>Recommends markets similar to recent winning bets</td>
</tr>
</tbody></table>
<h2>Smart Campaign Use Cases</h2>
<p>Smart Campaigns use sports events to trigger automated, personalized communications:</p>
<table>
<thead>
<tr>
<th>Use Case</th>
<th>Events Required</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>Bet of the Day</td>
<td>Bet Placement</td>
<td>Sends daily personalized bet suggestions</td>
</tr>
<tr>
<td>In-Play Event Alerts</td>
<td>Bet Placement</td>
<td>Notifies users when relevant live events start</td>
</tr>
<tr>
<td>Pre-Match Alerts - Favorite Team</td>
<td>Bet Placement</td>
<td>Alerts users before their favorite team plays</td>
</tr>
<tr>
<td>Pre-Match Alerts - Favorite Market</td>
<td>Bet Placement</td>
<td>Notifies about upcoming events in preferred markets</td>
</tr>
<tr>
<td>Pre-Match Alerts - Favorite Type</td>
<td>Bet Placement</td>
<td>Alerts for preferred bet types (e.g., over/under)</td>
</tr>
<tr>
<td>Pre-Match Alerts Similar Users</td>
<td>Bet Placement</td>
<td>Recommends events popular among similar users</td>
</tr>
<tr>
<td>Prior Win - Horse Racing</td>
<td>Bet Placement</td>
<td>Suggests horse racing bets after wins</td>
</tr>
<tr>
<td>Prior Win - Team Version</td>
<td>Bet Settlement</td>
<td>Recommends team bets after winning on similar teams</td>
</tr>
<tr>
<td>Optilive</td>
<td>Bet Placement</td>
<td>Real-time live betting recommendations</td>
</tr>
</tbody></table>
<h2>Integration Priority</h2>
<p>When implementing sports events, prioritize in this order:</p>
<ol>
<li><strong>Bet Placement</strong> (Critical) - Powers nearly all recommendation methods and campaigns</li>
<li><strong>Add to Betslip</strong> (High) - Captures user intent and improves trending/popular methods</li>
<li><strong>Bet Settlement</strong> (High) - Enables Prior Win recommendations and outcome-based campaigns</li>
</ol>
<h2>Filtering Considerations</h2>
<p>Sports recommendations support filtering to refine results:</p>
<ul>
<li><strong>Price-based filtering</strong>: Filter by odds ranges (favorites, odds-on, specific price ranges)</li>
<li><strong>Time-based filtering</strong>: Filter by event timing (today, tomorrow, live, specific times)</li>
<li><strong>Category filtering</strong>: Focus on specific sports, leagues, or event types</li>
</ul>
<p>See <a href="#sports-filtering">Sports Filtering</a> for implementation details.</p>
<hr>
<h2>Related Topics</h2>
<ul>
<li><a href="#events-overview">Events Overview</a> - Understanding the event system</li>
<li><a href="#standard-events">Standard Events</a> - Common events across verticals</li>
<li><a href="#sports-inventory">Sports Inventory</a> - Setting up sports catalog data</li>
<li><a href="#sports-filtering">Sports Filtering</a> - Filtering by price, time, and categories</li>
<li><a href="#kinesis-integration">AWS Kinesis Integration</a> - High-volume event streaming</li>
</ul>

</section>
<section id="ecommerce-events" class="doc-section">
<h1>E-commerce Events</h1>
<p>This page explains how event data powers Opti-X Recommend and Smart Campaigns for e-commerce and retail platforms. Understanding which events drive each feature helps you prioritize your integration and maximize conversion through personalization.</p>
<blockquote>
<p><strong>Note</strong>: Event requirements may evolve as Opti-X adds new capabilities. To future-proof your integration, send as many relevant events as possible.</p>
</blockquote>
<blockquote>
<p><strong>Important</strong>: Both Recommend and Smart Campaigns require inventory data alongside events. Without a product inventory feed, recommendation and targeting logic cannot function. See <a href="#ecommerce-inventory">E-commerce Inventory</a> for setup instructions.</p>
</blockquote>
<h2>Core E-commerce Events</h2>
<p>E-commerce platforms typically send these event types:</p>
<table>
<thead>
<tr>
<th>Event</th>
<th>Description</th>
<th>Primary Use</th>
</tr>
</thead>
<tbody><tr>
<td><strong>Product View</strong></td>
<td>User views a product page</td>
<td>Browsing behavior, interest signals</td>
</tr>
<tr>
<td><strong>Add to Cart</strong></td>
<td>User adds an item to their cart</td>
<td>Purchase intent, cart-based recommendations</td>
</tr>
<tr>
<td><strong>Remove from Cart</strong></td>
<td>User removes an item from their cart</td>
<td>Abandonment tracking, preference refinement</td>
</tr>
<tr>
<td><strong>Online Order</strong></td>
<td>User completes a purchase</td>
<td>Transaction history, purchase-based recommendations</td>
</tr>
</tbody></table>
<h2>Why This Matters</h2>
<p>E-commerce events capture the complete shopping journey from browsing to purchase. Each event type provides different insights:</p>
<ul>
<li><strong>Product Views</strong> reveal browsing interests, even for items users don&#39;t purchase</li>
<li><strong>Add to Cart</strong> signals strong purchase intent</li>
<li><strong>Remove from Cart</strong> indicates price sensitivity or changed preferences</li>
<li><strong>Online Order</strong> confirms actual purchasing behavior</li>
</ul>
<p>For example:</p>
<ul>
<li>A user who views multiple running shoes will see more athletic footwear recommendations</li>
<li>A user who adds items to cart but doesn&#39;t purchase may receive cart abandonment campaigns</li>
<li>A user who previously purchased coffee beans will see complementary products like grinders or mugs</li>
</ul>
<h2>Recommend Methods</h2>
<p>Each recommendation method relies on specific events to generate personalized product suggestions:</p>
<table>
<thead>
<tr>
<th>Method</th>
<th>Events Used</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>Similar Users (Views)</td>
<td>Online Order, Add to Cart, Remove from Cart, Product View</td>
<td>Recommends products popular among users with similar viewing patterns</td>
</tr>
<tr>
<td>Similar Users (Abandons)</td>
<td>Online Order, Add to Cart, Remove from Cart, Product View</td>
<td>Targets users who showed interest but didn&#39;t purchase</td>
</tr>
<tr>
<td>Similar Users</td>
<td>Online Order, Add to Cart, Remove from Cart, Product View</td>
<td>Comprehensive similar-user recommendations</td>
</tr>
<tr>
<td>Recently Viewed</td>
<td>Product View</td>
<td>Shows products the user has viewed recently</td>
</tr>
<tr>
<td>Previously Purchased</td>
<td>Online Order</td>
<td>Resurfaces products for repeat purchase</td>
</tr>
<tr>
<td>Hybrid</td>
<td>Online Order, Add to Cart, Remove from Cart, Product View</td>
<td>Combines multiple signals for comprehensive personalization</td>
</tr>
<tr>
<td>Popular (Views)</td>
<td>Online Order, Add to Cart, Remove from Cart, Product View</td>
<td>Surfaces products with high view counts</td>
</tr>
<tr>
<td>Popular (Abandons)</td>
<td>Online Order, Add to Cart, Remove from Cart, Product View</td>
<td>Highlights frequently abandoned items (often indicates price sensitivity)</td>
</tr>
<tr>
<td>Popular (Recent Activity)</td>
<td>Online Order, Add to Cart, Remove from Cart, Product View</td>
<td>Shows products with recent engagement spikes</td>
</tr>
<tr>
<td>Popular</td>
<td>Online Order, Add to Cart, Remove from Cart, Product View</td>
<td>Overall popularity-based recommendations</td>
</tr>
</tbody></table>
<h2>Smart Campaign Use Cases</h2>
<p>Smart Campaigns use e-commerce events to trigger automated, personalized communications:</p>
<table>
<thead>
<tr>
<th>Use Case</th>
<th>Events Required</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>Back in Stock</td>
<td>Product View, Online Order</td>
<td>Notifies users when a previously viewed out-of-stock item returns</td>
</tr>
<tr>
<td>Price Drop</td>
<td>Product View, Online Order</td>
<td>Alerts users when items they viewed or purchased drop in price</td>
</tr>
<tr>
<td>Low in Stock</td>
<td>Product View, Online Order</td>
<td>Creates urgency by notifying users about low inventory on viewed items</td>
</tr>
</tbody></table>
<h2>Integration Priority</h2>
<p>When implementing e-commerce events, prioritize in this order:</p>
<ol>
<li><strong>Product View</strong> (Critical) - Foundation for browsing-based personalization</li>
<li><strong>Online Order</strong> (Critical) - Powers purchase-based recommendations and essential campaigns</li>
<li><strong>Add to Cart</strong> (High) - Captures purchase intent, enables cart abandonment campaigns</li>
<li><strong>Remove from Cart</strong> (Medium) - Refines preference understanding</li>
</ol>
<h2>Event Flow Example</h2>
<p>A typical e-commerce session generates events in this sequence:</p>
<pre><code>1. Product View: User browses &quot;Blue Running Shoes&quot;
   → Opti-X learns interest in running shoes

2. Product View: User browses &quot;Red Running Shoes&quot;
   → Interest pattern strengthens

3. Add to Cart: User adds &quot;Blue Running Shoes&quot;
   → Strong purchase intent signal

4. Product View: User browses &quot;Running Socks&quot;
   → Cross-category interest captured

5. Remove from Cart: User removes &quot;Blue Running Shoes&quot;
   → Possible price sensitivity or preference change

6. Add to Cart: User adds &quot;Red Running Shoes&quot;
   → Refined preference captured

7. Online Order: User purchases &quot;Red Running Shoes&quot;
   → Transaction completed, future recommendations influenced
</code></pre>
<p>This sequence enables:</p>
<ul>
<li>Similar Users recommendations based on the browsing-to-purchase pattern</li>
<li>Price Drop campaigns if the user views but doesn&#39;t purchase items</li>
<li>Complementary product recommendations (socks with shoes)</li>
<li>Previously Purchased suggestions for shoe-related items in future visits</li>
</ul>
<h2>Filtering Considerations</h2>
<p>E-commerce recommendations often require filtering:</p>
<ul>
<li><strong>Category filtering</strong>: Show only products from specific categories</li>
<li><strong>Price range filtering</strong>: Match recommendations to user&#39;s typical price range</li>
<li><strong>Availability filtering</strong>: Exclude out-of-stock items</li>
<li><strong>Brand filtering</strong>: Include or exclude specific brands</li>
</ul>
<p>Consult your Integration Manager for filtering implementation specific to your e-commerce setup.</p>
<hr>
<h2>Related Topics</h2>
<ul>
<li><a href="#events-overview">Events Overview</a> - Understanding the event system</li>
<li><a href="#standard-events">Standard Events</a> - Common events across verticals</li>
<li><a href="#ecommerce-inventory">E-commerce Inventory</a> - Setting up product catalog data</li>
<li><a href="#kinesis-integration">AWS Kinesis Integration</a> - High-volume event streaming</li>
</ul>

</section>
<section id="kinesis-integration" class="doc-section">
<h1>AWS Kinesis Integration</h1>
<p>This guide describes how to set up and test AWS Kinesis for streaming events to Opti-X. Kinesis integration is ideal for high-volume event ingestion scenarios where you need scalable, real-time data streaming.</p>
<h2>When to Use Kinesis</h2>
<p>Consider AWS Kinesis integration when:</p>
<ul>
<li>Your platform generates high event volumes (thousands of events per second)</li>
<li>You need guaranteed delivery and ordering of events</li>
<li>Your infrastructure already uses AWS services</li>
<li>You want to decouple event production from Opti-X API calls</li>
</ul>
<p>For lower-volume scenarios or simpler integrations, direct API calls to Opti-X may be sufficient. Consult your Integration Manager to determine the best approach for your use case.</p>
<h2>Installation and Configuration</h2>
<ol>
<li><p>Install AWS CLI if not already installed. Follow the official guide: <a href="https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2.html">https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2.html</a></p>
</li>
<li><p>Configure the AWS CLI with your Opti-X credentials:</p>
</li>
</ol>
<pre><code class="language-bash">aws configure --profile opti-x-events
</code></pre>
<p>You will be prompted for:</p>
<ul>
<li><strong>AWS Access Key ID</strong>: Provided by your Integration Manager</li>
<li><strong>AWS Secret Access Key</strong>: Provided by your Integration Manager</li>
<li><strong>Default region name</strong>: <code>eu-west-1</code> (or the region specified by your Integration Manager)</li>
</ul>
<h2>Understanding Kinesis Concepts</h2>
<p>AWS Kinesis uses Streams and Shards to manage data flows and scaling. This architecture is comparable to Kafka Topics and Partitions:</p>
<pre><code>┌─────────────────────────────────────────────────┐
│              Kinesis Stream                      │
│  (Your event stream, e.g., &quot;user-events&quot;)       │
└─────────────────┬───────────────────────────────┘
                  │
     ┌────────────┼────────────┐
     │            │            │
     ▼            ▼            ▼
┌─────────┐  ┌─────────┐  ┌─────────┐
│ Shard 1 │  │ Shard 2 │  │ Shard N │
│         │  │         │  │         │
│ Records │  │ Records │  │ Records │
└─────────┘  └─────────┘  └─────────┘
</code></pre>
<ul>
<li><strong>Stream</strong>: A named resource representing your event flow</li>
<li><strong>Shards</strong>: Parallel processing units that provide throughput capacity</li>
<li><strong>Records</strong>: Individual event data items within shards</li>
</ul>
<h2>Verifying Your Integration</h2>
<h3>Step 1: List Shards</h3>
<p>Request your stream name from your Integration Manager. Use it in subsequent commands. For example, for a stream named <code>my-brand-events</code>:</p>
<pre><code class="language-bash">aws kinesis list-shards \
  --stream-name my-brand-events \
  --profile opti-x-events
</code></pre>
<h3>Expected Output</h3>
<pre><code class="language-json">{
  &quot;Shards&quot;: [
    {
      &quot;ShardId&quot;: &quot;shardId-000000000000&quot;,
      &quot;HashKeyRange&quot;: {
        &quot;StartingHashKey&quot;: &quot;0&quot;,
        &quot;EndingHashKey&quot;: &quot;340282366920938463463374607431768211455&quot;
      },
      &quot;SequenceNumberRange&quot;: {
        &quot;StartingSequenceNumber&quot;: &quot;49614023790783601483728905336480125602121137113222086658&quot;
      }
    }
  ]
}
</code></pre>
<h2>Reading Data from Kinesis</h2>
<p>To verify events are flowing correctly, you can read data from the stream.</p>
<h3>Step 2: Understand Shard Iterator Types</h3>
<p>Before reading records, you need a shard iterator. The iterator type determines where reading begins:</p>
<table>
<thead>
<tr>
<th>Type</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>TRIM_HORIZON</td>
<td>Start from the beginning of retained data (up to 24 hours)</td>
</tr>
<tr>
<td>LATEST</td>
<td>Start from the most recent record</td>
</tr>
</tbody></table>
<p>For more details, see the AWS documentation: <a href="https://docs.aws.amazon.com/cli/latest/reference/kinesis/get-shard-iterator.html">https://docs.aws.amazon.com/cli/latest/reference/kinesis/get-shard-iterator.html</a></p>
<h3>Step 3: Get Shard Iterator and Read Records</h3>
<p>Use the shard ID from the previous step (e.g., <code>shardId-000000000000</code>):</p>
<pre><code class="language-bash">SHARD_ITERATOR=$(aws kinesis get-shard-iterator \
  --shard-id shardId-000000000000 \
  --shard-iterator-type TRIM_HORIZON \
  --stream-name my-brand-events \
  --query &#39;ShardIterator&#39; \
  --profile opti-x-events)

aws kinesis get-records \
  --shard-iterator $SHARD_ITERATOR \
  --profile opti-x-events
</code></pre>
<h3>Expected Response</h3>
<pre><code class="language-json">{
  &quot;Records&quot;: [],
  &quot;NextShardIterator&quot;: &quot;AAAAAAAAAAEROtFEiWoVdkmoa62xtMBG0LHYJVnQ24V5f2AgVR0dKTz021+VN2DZsDOM0zkKNra0ObvMV83s+e3xzxJ057eS+ESfxUtnd9megbDLlb7pJIP5r2NxsMgEr1LbAZRBozHt6HkNP0Gv94rSTVhoelmuvrCQ&quot;,
  &quot;MillisBehindLatest&quot;: 85128000
}
</code></pre>
<h3>Understanding the Response</h3>
<table>
<thead>
<tr>
<th>Field</th>
<th>Meaning</th>
</tr>
</thead>
<tbody><tr>
<td><code>Records: []</code></td>
<td>No data currently in the stream (or at this position)</td>
</tr>
<tr>
<td><code>Records: [...]</code></td>
<td>Contains event data (base64 encoded)</td>
</tr>
<tr>
<td><code>NextShardIterator</code></td>
<td>Use this iterator to fetch the next batch of records</td>
</tr>
<tr>
<td><code>MillisBehindLatest</code></td>
<td>How far behind real-time the current position is (in milliseconds)</td>
</tr>
</tbody></table>
<h3>Step 4: Read Subsequent Batches</h3>
<p>To continue reading, use the <code>NextShardIterator</code> from the previous response:</p>
<pre><code class="language-bash">aws kinesis get-records \
  --shard-iterator &quot;AAAAAAAAAAEROtFEiWoVdkmoa62...&quot; \
  --profile opti-x-events
</code></pre>
<h2>Decoding Records</h2>
<p>Records in Kinesis are base64 encoded. To view the actual event data:</p>
<pre><code class="language-bash"># Using jq to decode a single record
echo &quot;BASE64_ENCODED_DATA&quot; | base64 --decode | jq .
</code></pre>
<p>Or in Python:</p>
<pre><code class="language-python">import base64
import json

encoded_data = &quot;BASE64_ENCODED_DATA&quot;
decoded = base64.b64decode(encoded_data)
event = json.loads(decoded)
print(json.dumps(event, indent=2))
</code></pre>
<h2>Troubleshooting</h2>
<table>
<thead>
<tr>
<th>Issue</th>
<th>Possible Cause</th>
<th>Solution</th>
</tr>
</thead>
<tbody><tr>
<td>Empty Records array</td>
<td>No events sent yet</td>
<td>Send test events and wait a few seconds</td>
</tr>
<tr>
<td>Access denied</td>
<td>Invalid credentials</td>
<td>Verify AWS keys with Integration Manager</td>
</tr>
<tr>
<td>Stream not found</td>
<td>Incorrect stream name</td>
<td>Confirm stream name with Integration Manager</td>
</tr>
<tr>
<td>Expired iterator</td>
<td>Iterator timed out (5 minutes)</td>
<td>Get a new shard iterator</td>
</tr>
</tbody></table>
<hr>
<h2>Related Topics</h2>
<ul>
<li><a href="#events-overview">Events Overview</a> - Understanding the event system</li>
<li><a href="#standard-events">Standard Events</a> - Common events across verticals</li>
<li><a href="#gaming-events">Gaming Events</a> - Gaming-specific events</li>
<li><a href="#sports-events">Sports Events</a> - Sports betting events</li>
<li><a href="#ecommerce-events">E-commerce Events</a> - Retail and e-commerce events</li>
</ul>

</section>
<section id="filtering-overview" class="doc-section">
<h1>Filtering Overview</h1>
<p>Filtering enables you to refine Opti-X recommendations and search results based on specific criteria. By applying filters, you ensure users see only relevant, compliant, and contextually appropriate content.</p>
<h2>What Is Filtering?</h2>
<p>Filtering narrows down recommendation and search results based on rules you define. When a user requests recommendations, Opti-X generates personalized results, then applies your filters to remove items that don&#39;t match the specified criteria.</p>
<p>Common filtering scenarios include:</p>
<ul>
<li>Showing only games available under a user&#39;s regulatory license</li>
<li>Displaying products within a specific price range</li>
<li>Surfacing sports events happening today or currently live</li>
<li>Excluding specific suppliers or categories</li>
</ul>
<h2>Why Filtering Matters</h2>
<p>Filtering serves several critical purposes:</p>
<h3>Regulatory Compliance</h3>
<p>Many markets require content restrictions based on licensing. A user in the UK should only see games approved by the UKGC. A user in Malta should see MGA-licensed content. Filtering ensures compliance without requiring separate recommendation models for each region.</p>
<h3>User Experience</h3>
<p>Showing irrelevant content degrades the user experience. If a user browses football betting, showing them darts events dilutes the page. Filters keep content contextually relevant.</p>
<h3>Business Rules</h3>
<p>You may want to promote certain suppliers, exclude clearance items from premium placements, or limit results to specific categories. Filtering implements these business rules at the API level.</p>
<h2>Filter Types</h2>
<p>Opti-X supports several filtering approaches:</p>
<h3>Tag-Based Filtering</h3>
<p>Tag-based filters use metadata attached to inventory items. Games, products, and events can have tags like supplier, category, theme, or custom attributes.</p>
<p><strong>Example use cases:</strong></p>
<ul>
<li>Show only games from a specific supplier</li>
<li>Exclude &quot;jackpot&quot; themed games</li>
<li>Display only &quot;premium&quot; tier products</li>
</ul>
<p>Tag filters use rule types:</p>
<ul>
<li><code>IS_IN</code>: Include only items with specified tags</li>
<li><code>NOT_IN</code>: Exclude items with specified tags</li>
</ul>
<p>See <a href="#gaming-filtering">Gaming Filtering</a> for implementation details.</p>
<h3>Region-Based Filtering</h3>
<p>Region-based filters use the user&#39;s location to return geographically relevant results. This applies to both recommendations and popular/trending data.</p>
<p><strong>Example use cases:</strong></p>
<ul>
<li>Show games popular in the user&#39;s country</li>
<li>Surface region-specific promotions</li>
<li>Return localized popular searches</li>
</ul>
<p>See <a href="#gaming-filtering">Gaming Filtering</a> for region filter implementation.</p>
<h3>Price-Based Filtering</h3>
<p>Price-based filters refine results based on numerical price values. This is particularly useful for sports betting where odds matter.</p>
<p><strong>Example use cases:</strong></p>
<ul>
<li>Show only favorites (lowest price selections)</li>
<li>Filter to odds-on selections (price &lt; 2.0)</li>
<li>Display selections within a specific price range</li>
</ul>
<p>See <a href="#sports-filtering">Sports Filtering</a> for price filter syntax.</p>
<h3>Time-Based Filtering</h3>
<p>Time-based filters restrict results based on when events occur. Sports betting commonly uses these filters.</p>
<p><strong>Example use cases:</strong></p>
<ul>
<li>Show only events happening today</li>
<li>Display currently live events</li>
<li>Filter to events starting at a specific time</li>
</ul>
<p>See <a href="#sports-filtering">Sports Filtering</a> for time filter syntax.</p>
<h2>How Filtering Works</h2>
<p>Filtering applies at the API request level. You include filter parameters in your recommendation or search request, and Opti-X applies them before returning results.</p>
<p>The typical flow:</p>
<ol>
<li><strong>User makes a request</strong>: Your application calls the Opti-X API with user context</li>
<li><strong>Include filter parameters</strong>: Add tags, location, or query modifiers to the request</li>
<li><strong>Opti-X generates results</strong>: The recommendation engine produces personalized results</li>
<li><strong>Filters apply</strong>: Results that don&#39;t match filter criteria are removed</li>
<li><strong>Filtered results return</strong>: Your application receives only compliant, relevant items</li>
</ol>
<h2>Filter Placement in Requests</h2>
<p>Filters are included in the request body. Location varies by filter type:</p>
<pre><code class="language-json">{
  &quot;userId&quot;: &quot;user_12345&quot;,
  &quot;traits&quot;: {
    &quot;license&quot;: &quot;UKGC&quot;,
    &quot;currency&quot;: &quot;GBP&quot;,
    &quot;language&quot;: &quot;en&quot;
  },
  &quot;location&quot;: {
    &quot;country&quot;: &quot;GB&quot;
  },
  &quot;tag_rules&quot;: [
    {
      &quot;rule&quot;: {
        &quot;tags&quot;: [
          {&quot;tag&quot;: &quot;NetEnt&quot;, &quot;tag_type&quot;: &quot;supplier&quot;}
        ]
      },
      &quot;rule_type&quot;: &quot;IS_IN&quot;
    }
  ],
  &quot;query&quot;: &quot;slots today&quot;
}
</code></pre>
<p>In this example:</p>
<ul>
<li><code>traits</code> provide license and currency for compliance filtering</li>
<li><code>location</code> enables region-based result ranking</li>
<li><code>tag_rules</code> explicitly filter to a specific supplier</li>
<li><code>query</code> includes a time modifier (&quot;today&quot;) for time-based filtering</li>
</ul>
<h2>Combining Filters</h2>
<p>Multiple filter types can be combined in a single request. Opti-X applies them in sequence, creating an AND relationship between different filter types.</p>
<p>For example, a request might:</p>
<ol>
<li>Filter to UKGC-licensed games (trait-based)</li>
<li>Show only games popular in GB (region-based)</li>
<li>Include only Blueprint Gaming supplier (tag-based)</li>
</ol>
<p>All three conditions must be satisfied for an item to appear in results.</p>
<h2>Filter Behavior</h2>
<h3>Empty Results</h3>
<p>If filters are too restrictive, results may be empty. Consider:</p>
<ul>
<li>Broadening filter criteria</li>
<li>Implementing fallback logic to relax filters if initial results are empty</li>
<li>Validating filter combinations during development</li>
</ul>
<h3>Performance</h3>
<p>Filters are applied server-side and don&#39;t significantly impact response time. However, very complex tag rules with many conditions may have minor performance implications for large inventories.</p>
<h3>Case Sensitivity</h3>
<ul>
<li><strong>Country codes</strong>: Case-insensitive (&quot;GB&quot; and &quot;gb&quot; are equivalent)</li>
<li><strong>Tag values</strong>: Case-sensitive (match exactly as defined in inventory)</li>
<li><strong>Query modifiers</strong>: Case-insensitive (&quot;TODAY&quot; and &quot;today&quot; work the same)</li>
</ul>
<h2>Vertical-Specific Guides</h2>
<p>Each vertical has specific filtering capabilities:</p>
<ul>
<li><strong><a href="#gaming-filtering">Gaming Filtering</a></strong>: Tag-based and region-based filtering for casino games</li>
<li><strong><a href="#sports-filtering">Sports Filtering</a></strong>: Price-based and time-based filtering for sports betting</li>
</ul>
<hr>
<h2>Related Topics</h2>
<ul>
<li><a href="#gaming-filtering">Gaming Filtering</a> - Filter games by tags and regions</li>
<li><a href="#sports-filtering">Sports Filtering</a> - Filter sports by price and time</li>
<li><a href="#gaming-events">Gaming Events</a> - Events that power gaming recommendations</li>
<li><a href="#sports-events">Sports Events</a> - Events that power sports recommendations</li>
</ul>

</section>
<section id="gaming-filtering" class="doc-section">
<h1>Gaming Filtering</h1>
<p>This guide covers filtering options for gaming recommendations and Smart Search. Gaming platforms use tag-based filtering to control which games appear and region-based filtering to serve geographically relevant content.</p>
<h2>Tag-Based Filtering</h2>
<p>Tag-based filtering enables explicit data filtering through tags in conjunction with search queries. Use tag filters to implement features like supplier buttons, category filters, or compliance rules in your front-end interface.</p>
<h3>How Tag Filtering Works</h3>
<p>Every game in your inventory can have tags (supplier, category, theme, etc.). Tag rules tell Opti-X which games to include or exclude based on these tags.</p>
<p><strong>Common use cases:</strong></p>
<ul>
<li>Filter to games from a specific supplier (e.g., &quot;Show only NetEnt games&quot;)</li>
<li>Exclude certain categories (e.g., &quot;Hide jackpot games&quot;)</li>
<li>Implement regulatory filters (e.g., &quot;Show only games licensed for UK&quot;)</li>
</ul>
<h3>Request Body Structure</h3>
<p>The request body includes:</p>
<ul>
<li><strong>traits</strong>: User attributes like license, currency, and language for compliance filtering</li>
<li><strong>query</strong>: The search term (can be empty string to list all matching games)</li>
<li><strong>tag_rules</strong>: Array of rules defining which tags to include or exclude</li>
<li><strong>location</strong>: User&#39;s country for regional relevance</li>
</ul>
<blockquote>
<p><strong>Tip</strong>: Set the query parameter to an empty string (<code>&quot;&quot;</code>) to return a list of games that match your tag rules without searching for specific terms. This is useful for category landing pages.</p>
</blockquote>
<h3>Tag Rule Structure</h3>
<p>Each tag rule contains:</p>
<ul>
<li><strong>rule.tags</strong>: Array of tag objects with <code>tag</code> (value) and <code>tag_type</code> (category)</li>
<li><strong>rule_type</strong>: Either <code>IS_IN</code> (include) or <code>NOT_IN</code> (exclude)</li>
</ul>
<h3>Example: Filter by Supplier</h3>
<p>This example filters search results to show only games from the &quot;Blueprint Gaming&quot; supplier:</p>
<p><strong>Python:</strong></p>
<pre><code class="language-python">import requests
import json

url = &quot;https://api.opti-x.optimove.net/search/v1/query&quot;

headers = {
    &quot;accept&quot;: &quot;application/json&quot;,
    &quot;x-api-key&quot;: &quot;your_api_key&quot;,
    &quot;x-brand-key&quot;: &quot;your_brand_key&quot;,
    &quot;Content-Type&quot;: &quot;application/json&quot;
}

tag_rules = [
    {
        &quot;rule&quot;: {
            &quot;tags&quot;: [
                {
                    &quot;tag&quot;: &quot;Blueprint Gaming&quot;,
                    &quot;tag_type&quot;: &quot;supplier&quot;
                }
            ],
        },
        &quot;rule_type&quot;: &quot;IS_IN&quot;
    }
]

payload = {
    &quot;traits&quot;: {
        &quot;license&quot;: &quot;UKGC&quot;,
        &quot;currency&quot;: &quot;GBP&quot;,
        &quot;language&quot;: &quot;en&quot;
    },
    &quot;query&quot;: &quot;irish&quot;,
    &quot;context&quot;: {},
    &quot;skinId&quot;: &quot;main&quot;,
    &quot;location&quot;: {
        &quot;country&quot;: &quot;GB&quot;
    },
    &quot;tag_rules&quot;: tag_rules,
    &quot;type&quot;: &quot;search&quot;,
    &quot;userId&quot;: &quot;user_12345&quot;
}

response = requests.post(url, headers=headers, data=json.dumps(payload))

print(&quot;Status Code:&quot;, response.status_code)
print(&quot;Response:&quot;, response.json())
</code></pre>
<p><strong>cURL:</strong></p>
<pre><code class="language-bash">curl -X POST &quot;https://api.opti-x.optimove.net/search/v1/query&quot; \
-H &quot;accept: application/json&quot; \
-H &quot;x-api-key: your_api_key&quot; \
-H &quot;x-brand-key: your_brand_key&quot; \
-H &quot;Content-Type: application/json&quot; \
-d &#39;{
  &quot;traits&quot;: {
    &quot;license&quot;: &quot;UKGC&quot;,
    &quot;currency&quot;: &quot;GBP&quot;,
    &quot;language&quot;: &quot;en&quot;
  },
  &quot;query&quot;: &quot;irish&quot;,
  &quot;context&quot;: {},
  &quot;skinId&quot;: &quot;main&quot;,
  &quot;location&quot;: {
    &quot;country&quot;: &quot;GB&quot;
  },
  &quot;tag_rules&quot;: [
    {
      &quot;rule&quot;: {
        &quot;tags&quot;: [
          {
            &quot;tag&quot;: &quot;Blueprint Gaming&quot;,
            &quot;tag_type&quot;: &quot;supplier&quot;
          }
        ]
      },
      &quot;rule_type&quot;: &quot;IS_IN&quot;
    }
  ],
  &quot;type&quot;: &quot;search&quot;,
  &quot;userId&quot;: &quot;user_12345&quot;
}&#39;
</code></pre>
<h3>Expected Results</h3>
<ul>
<li><strong>Without tag rules</strong>: A search for &quot;irish&quot; might return 49 results from all suppliers</li>
<li><strong>With tag rules</strong>: Applying the Blueprint Gaming filter reduces results to only 5 games</li>
</ul>
<h3>Verifying Filtered Results</h3>
<p>Inspect the response to confirm filtering worked correctly:</p>
<pre><code class="language-python"># Check supplier tags in results
suppliers = [item[&quot;provider&quot;] for item in response.json()[&#39;result&#39;][&#39;search_results&#39;]]
print(suppliers)
# Output: [&#39;Blueprint Gaming&#39;, &#39;Blueprint Gaming&#39;, &#39;Blueprint Gaming&#39;, ...]

# Check all tags
tags = [item[&quot;tags&quot;] for item in response.json()[&#39;result&#39;][&#39;search_results&#39;]]
print(tags)
</code></pre>
<h3>Advanced Tag Rules</h3>
<p>Tag rules support complex logic:</p>
<p><strong>Multiple tags (OR within a rule):</strong></p>
<pre><code class="language-json">{
  &quot;rule&quot;: {
    &quot;tags&quot;: [
      {&quot;tag&quot;: &quot;Blueprint Gaming&quot;, &quot;tag_type&quot;: &quot;supplier&quot;},
      {&quot;tag&quot;: &quot;NetEnt&quot;, &quot;tag_type&quot;: &quot;supplier&quot;}
    ]
  },
  &quot;rule_type&quot;: &quot;IS_IN&quot;
}
</code></pre>
<p>This returns games from Blueprint Gaming OR NetEnt.</p>
<p><strong>Multiple rules (AND between rules):</strong></p>
<pre><code class="language-json">{
  &quot;tag_rules&quot;: [
    {
      &quot;rule&quot;: {
        &quot;tags&quot;: [{&quot;tag&quot;: &quot;Blueprint Gaming&quot;, &quot;tag_type&quot;: &quot;supplier&quot;}]
      },
      &quot;rule_type&quot;: &quot;IS_IN&quot;
    },
    {
      &quot;rule&quot;: {
        &quot;tags&quot;: [{&quot;tag&quot;: &quot;jackpot&quot;, &quot;tag_type&quot;: &quot;category&quot;}]
      },
      &quot;rule_type&quot;: &quot;NOT_IN&quot;
    }
  ]
}
</code></pre>
<p>This returns Blueprint Gaming games that are NOT in the jackpot category.</p>
<hr>
<h2>Region-Based Filtering</h2>
<p>Region-based filtering returns results relevant to the user&#39;s location. When you provide a country code, Opti-X returns region-specific popular searches and rankings.</p>
<h3>How Region Filtering Works</h3>
<p>Include the <code>location</code> field in your request with the user&#39;s country code. Opti-X uses this to:</p>
<ul>
<li>Return popular games specific to that country</li>
<li>Rank search results based on regional popularity</li>
<li>Surface region-specific trending content</li>
</ul>
<p>If no regional data exists for the specified country, Opti-X falls back to global data automatically.</p>
<h3>Example: Region-Specific Popular Games</h3>
<p>This example retrieves popular games for users in Great Britain:</p>
<p><strong>Python:</strong></p>
<pre><code class="language-python">import requests
import json

url = &quot;https://api.opti-x.optimove.net/search/v1/popular&quot;

headers = {
    &quot;accept&quot;: &quot;application/json&quot;,
    &quot;x-api-key&quot;: &quot;your_api_key&quot;,
    &quot;x-brand-key&quot;: &quot;your_brand_key&quot;,
    &quot;Content-Type&quot;: &quot;application/json&quot;
}

payload = {
    &quot;location&quot;: {
        &quot;country&quot;: &quot;GB&quot;
    }
}

response = requests.post(url, headers=headers, data=json.dumps(payload))

print(&quot;Status Code:&quot;, response.status_code)
print(&quot;Response:&quot;, response.json())
</code></pre>
<p><strong>cURL:</strong></p>
<pre><code class="language-bash">curl -X POST &quot;https://api.opti-x.optimove.net/search/v1/popular&quot; \
-H &quot;accept: application/json&quot; \
-H &quot;x-api-key: your_api_key&quot; \
-H &quot;x-brand-key: your_brand_key&quot; \
-H &quot;Content-Type: application/json&quot; \
-d &#39;{
  &quot;location&quot;: {
    &quot;country&quot;: &quot;GB&quot;
  }
}&#39;
</code></pre>
<h3>Expected Results</h3>
<ul>
<li><strong>With <code>location.country</code> specified</strong>: Returns popular games and searches specific to Great Britain</li>
<li><strong>Without <code>location.country</code></strong>: Returns global popular games and searches</li>
</ul>
<h3>Country Code Reference</h3>
<p>Use standard ISO 3166-1 alpha-2 country codes:</p>
<table>
<thead>
<tr>
<th>Code</th>
<th>Country</th>
</tr>
</thead>
<tbody><tr>
<td>GB</td>
<td>Great Britain</td>
</tr>
<tr>
<td>US</td>
<td>United States</td>
</tr>
<tr>
<td>DE</td>
<td>Germany</td>
</tr>
<tr>
<td>AU</td>
<td>Australia</td>
</tr>
<tr>
<td>CA</td>
<td>Canada</td>
</tr>
<tr>
<td>SE</td>
<td>Sweden</td>
</tr>
</tbody></table>
<p>Country codes are case-insensitive (&quot;GB&quot; and &quot;gb&quot; both work).</p>
<h3>Fallback Behavior</h3>
<p>If regional data isn&#39;t available for the specified country, Opti-X automatically uses global data. This ensures users always receive results, even in markets with limited historical data.</p>
<hr>
<h2>Combining Tag and Region Filters</h2>
<p>You can use both filter types in a single request:</p>
<pre><code class="language-json">{
  &quot;traits&quot;: {
    &quot;license&quot;: &quot;UKGC&quot;,
    &quot;currency&quot;: &quot;GBP&quot;,
    &quot;language&quot;: &quot;en&quot;
  },
  &quot;query&quot;: &quot;slots&quot;,
  &quot;location&quot;: {
    &quot;country&quot;: &quot;GB&quot;
  },
  &quot;tag_rules&quot;: [
    {
      &quot;rule&quot;: {
        &quot;tags&quot;: [{&quot;tag&quot;: &quot;NetEnt&quot;, &quot;tag_type&quot;: &quot;supplier&quot;}]
      },
      &quot;rule_type&quot;: &quot;IS_IN&quot;
    }
  ],
  &quot;userId&quot;: &quot;user_12345&quot;,
  &quot;type&quot;: &quot;search&quot;
}
</code></pre>
<p>This request:</p>
<ol>
<li>Searches for &quot;slots&quot;</li>
<li>Filters to NetEnt supplier only</li>
<li>Ranks results based on GB popularity</li>
<li>Applies UKGC license compliance</li>
</ol>
<hr>
<h2>Related Topics</h2>
<ul>
<li><a href="#filtering-overview">Filtering Overview</a> - Understanding filtering concepts</li>
<li><a href="#sports-filtering">Sports Filtering</a> - Price and time filtering for sports</li>
<li><a href="#gaming-events">Gaming Events</a> - Events that power gaming recommendations</li>
<li><a href="#gaming-inventory">Gaming Inventory</a> - Setting up game catalog data</li>
</ul>

</section>
<section id="sports-filtering" class="doc-section">
<h1>Sports Filtering</h1>
<p>This guide covers filtering options for sports betting recommendations and Smart Search. Sports platforms use price-based filtering to narrow results by odds and time-based filtering to focus on specific event windows.</p>
<p>These filters are applied directly within the search query parameter, making them easy to integrate with front-end components like sliders, dropdowns, or dynamically generated queries.</p>
<h2>Price-Based Filtering</h2>
<p>Price-based filtering refines sports searches based on odds criteria. Use these filters to help users find selections at their preferred price points.</p>
<h3>How Price Filtering Works</h3>
<p>Price filters are added directly to the query string. Opti-X parses these modifiers and applies them to the selection odds in your sports inventory.</p>
<h3>Available Price Filters</h3>
<p>Combine any search term with these price modifiers. In the examples below, <code>{search}</code> represents your search term (e.g., &quot;football&quot;, &quot;liverpool&quot;, &quot;premier league&quot;):</p>
<table>
<thead>
<tr>
<th>Filter</th>
<th>Description</th>
<th>Example</th>
</tr>
</thead>
<tbody><tr>
<td><code>{search} favourites</code></td>
<td>Returns the lowest price selection for each market</td>
<td><code>football favourites</code></td>
</tr>
<tr>
<td><code>{search} odds on</code></td>
<td>Returns selections with decimal price &lt; 2.0</td>
<td><code>liverpool odds on</code></td>
</tr>
<tr>
<td><code>{search} odds against</code></td>
<td>Returns selections with decimal price &gt; 2.0</td>
<td><code>premier league odds against</code></td>
</tr>
<tr>
<td><code>{search} evens</code></td>
<td>Returns selections with decimal price equal to 2.0</td>
<td><code>tennis evens</code></td>
</tr>
<tr>
<td><code>{search} pr:X-Y</code></td>
<td>Returns selections with decimal price between X and Y</td>
<td><code>football pr:1.5-3.5</code></td>
</tr>
</tbody></table>
<h3>Price Range Syntax</h3>
<p>The <code>pr:</code> modifier accepts a price range in decimal format:</p>
<ul>
<li>Format: <code>pr:minimum-maximum</code></li>
<li>Both values must be decimal odds</li>
<li>The range is exclusive (greater than minimum, less than maximum)</li>
</ul>
<p><strong>Examples:</strong></p>
<ul>
<li><code>pr:1.5-3.5</code> - Prices between 1.5 and 3.5</li>
<li><code>pr:2.0-5.0</code> - Prices between 2.0 and 5.0</li>
<li><code>pr:1.01-2.0</code> - Short-priced selections (odds-on to evens)</li>
</ul>
<hr>
<h2>Time-Based Filtering</h2>
<p>Time-based filtering refines results based on when events are scheduled. Use these filters to show users events within relevant time windows.</p>
<h3>How Time Filtering Works</h3>
<p>Time filters are added directly to the query string, similar to price filters. Opti-X interprets these modifiers relative to the current time and returns matching events.</p>
<h3>Available Time Filters</h3>
<p>Combine any search term with these time modifiers:</p>
<table>
<thead>
<tr>
<th>Filter</th>
<th>Description</th>
<th>Example</th>
</tr>
</thead>
<tbody><tr>
<td><code>{search} today</code></td>
<td>Events happening today</td>
<td><code>football today</code></td>
</tr>
<tr>
<td><code>{search} tomorrow</code></td>
<td>Events happening tomorrow</td>
<td><code>horse racing tomorrow</code></td>
</tr>
<tr>
<td><code>{search} live</code></td>
<td>Events currently in-play</td>
<td><code>tennis live</code></td>
</tr>
<tr>
<td><code>{search} at {time}</code></td>
<td>Events starting at a specific time</td>
<td><code>football at 3pm</code> or <code>football at 15:00</code></td>
</tr>
<tr>
<td><code>{search} around {time}</code></td>
<td>Events within one hour of specified time</td>
<td><code>football around 3pm</code> (returns 2pm-4pm)</td>
</tr>
<tr>
<td><code>{search} tr:{start}-{end}</code></td>
<td>Events within a time range</td>
<td><code>football tr:19:00-21:00</code> or <code>football tr:7pm-9pm</code></td>
</tr>
</tbody></table>
<h3>Time Format Options</h3>
<p>Opti-X accepts multiple time formats:</p>
<ul>
<li>12-hour: <code>3pm</code>, <code>7:30am</code>, <code>11:45pm</code></li>
<li>24-hour: <code>15:00</code>, <code>19:30</code>, <code>23:45</code></li>
</ul>
<p>Both formats work in <code>at</code>, <code>around</code>, and <code>tr:</code> modifiers.</p>
<hr>
<h2>Combining Filters</h2>
<p>You can combine multiple filters in a single query:</p>
<pre><code>football favourites pr:1.5-3.5 today
</code></pre>
<p>This query:</p>
<ol>
<li>Searches for &quot;football&quot;</li>
<li>Returns only favorites (lowest price per market)</li>
<li>Filters to prices between 1.5 and 3.5</li>
<li>Shows only events happening today</li>
</ol>
<hr>
<h2>Usage Examples</h2>
<h3>Example: Search with Filters</h3>
<p>This example shows a complete search request with price and time filters:</p>
<pre><code class="language-json">{
  &quot;context&quot;: {
    &quot;product&quot;: &quot;Sports&quot;,
    &quot;category&quot;: &quot;Football&quot;,
    &quot;page&quot;: {
      &quot;url&quot;: &quot;sports.example.optix.com&quot;,
      &quot;title&quot;: &quot;Football Home&quot;
    },
    &quot;channel&quot;: &quot;Mobile&quot;
  },
  &quot;query&quot;: &quot;football favourites pr:1.5-3.5 today&quot;,
  &quot;userId&quot;: &quot;user_12345&quot;,
  &quot;type&quot;: &quot;search&quot;
}
</code></pre>
<h3>Example: Live Events Only</h3>
<pre><code class="language-json">{
  &quot;context&quot;: {
    &quot;product&quot;: &quot;Sports&quot;,
    &quot;category&quot;: &quot;Tennis&quot;,
    &quot;page&quot;: {
      &quot;url&quot;: &quot;sports.example.optix.com/tennis&quot;,
      &quot;title&quot;: &quot;Tennis Live&quot;
    },
    &quot;channel&quot;: &quot;Desktop&quot;
  },
  &quot;query&quot;: &quot;tennis live&quot;,
  &quot;userId&quot;: &quot;user_12345&quot;,
  &quot;type&quot;: &quot;search&quot;
}
</code></pre>
<h3>Example: Evening Events in Price Range</h3>
<pre><code class="language-json">{
  &quot;context&quot;: {
    &quot;product&quot;: &quot;Sports&quot;,
    &quot;category&quot;: &quot;Football&quot;,
    &quot;page&quot;: {
      &quot;url&quot;: &quot;sports.example.optix.com/football&quot;,
      &quot;title&quot;: &quot;Football Tonight&quot;
    },
    &quot;channel&quot;: &quot;Mobile&quot;
  },
  &quot;query&quot;: &quot;premier league tr:19:00-22:00 pr:2.0-4.0&quot;,
  &quot;userId&quot;: &quot;user_12345&quot;,
  &quot;type&quot;: &quot;search&quot;
}
</code></pre>
<hr>
<h2>Front-End Integration</h2>
<p>These filters integrate naturally with UI components:</p>
<h3>Price Slider</h3>
<p>Map a slider range to the <code>pr:</code> modifier:</p>
<pre><code class="language-javascript">const minPrice = priceSlider.min;  // e.g., 1.5
const maxPrice = priceSlider.max;  // e.g., 3.5
const query = `${searchTerm} pr:${minPrice}-${maxPrice}`;
</code></pre>
<h3>Quick Filter Buttons</h3>
<p>Create buttons that append modifiers:</p>
<pre><code class="language-javascript">const filters = {
  &#39;Favourites&#39;: &#39;favourites&#39;,
  &#39;Odds On&#39;: &#39;odds on&#39;,
  &#39;Odds Against&#39;: &#39;odds against&#39;,
  &#39;Live Now&#39;: &#39;live&#39;,
  &#39;Today&#39;: &#39;today&#39;,
  &#39;Tomorrow&#39;: &#39;tomorrow&#39;
};

function applyFilter(searchTerm, filterKey) {
  return `${searchTerm} ${filters[filterKey]}`;
}
</code></pre>
<h3>Time Range Dropdown</h3>
<p>Map dropdown selections to time modifiers:</p>
<pre><code class="language-javascript">const timeRanges = {
  &#39;Morning&#39;: &#39;tr:06:00-12:00&#39;,
  &#39;Afternoon&#39;: &#39;tr:12:00-18:00&#39;,
  &#39;Evening&#39;: &#39;tr:18:00-23:00&#39;
};
</code></pre>
<hr>
<h2>Filter Behavior Notes</h2>
<h3>Empty Results</h3>
<p>If filters are too restrictive, the search may return no results. Consider:</p>
<ul>
<li>Implementing fallback queries that relax filters</li>
<li>Showing &quot;No results&quot; messaging with suggestions to broaden criteria</li>
<li>Validating filter combinations in development</li>
</ul>
<h3>Filter Stacking</h3>
<p>Multiple filters create AND conditions. Each filter further restricts results:</p>
<ul>
<li><code>football</code> - All football events</li>
<li><code>football today</code> - Football events today</li>
<li><code>football today pr:1.5-2.5</code> - Football events today with odds 1.5-2.5</li>
<li><code>football today pr:1.5-2.5 favourites</code> - Favorites only from above</li>
</ul>
<h3>Time Zone Handling</h3>
<p>Time filters use the server&#39;s configured time zone. Consult your Integration Manager about time zone settings for your deployment.</p>
<hr>
<h2>Related Topics</h2>
<ul>
<li><a href="#filtering-overview">Filtering Overview</a> - Understanding filtering concepts</li>
<li><a href="#gaming-filtering">Gaming Filtering</a> - Tag and region filtering for gaming</li>
<li><a href="#sports-events">Sports Events</a> - Events that power sports recommendations</li>
<li><a href="#sports-inventory">Sports Inventory</a> - Setting up sports catalog data</li>
</ul>

</section>
<section id="banner-deployment" class="doc-section">
<h1>Banner Deployment Guide</h1>
<h2>Why This Matters</h2>
<p>Personalized banners transform static marketing into dynamic, relevant experiences. Instead of showing every user the same generic content, Opti-X Banners display product recommendations tailored to each individual based on their behavior, preferences, and context. This personalization typically increases click-through rates by 2-3x compared to static content, because users see products they actually want.</p>
<p>Banners work across channels: embed them in emails, display them on your website, or include them in push notifications. The same banner configuration adapts to show the right products to the right user at the right time.</p>
<h2>Deployment Options</h2>
<p>There are two primary ways to render Opti-X Banner content:</p>
<ol>
<li><strong>Image-based banners</strong> - Reference Opti-X banner image URLs that dynamically generate personalized content</li>
<li><strong>Code-based banners</strong> - Implement JavaScript code that builds the banner directly in your site</li>
</ol>
<p>Both approaches deliver personalized recommendations. Choose image-based for email and simple implementations. Choose code-based for richer website interactions.</p>
<h2>Making Banners Personalized</h2>
<p>The power of Opti-X Banners comes from generating personalized content for each user. To achieve this personalization, banner URLs require parameters that identify who is viewing the content and where.</p>
<h3>Required Parameters</h3>
<table>
<thead>
<tr>
<th>Parameter</th>
<th>Description</th>
<th>Example Value</th>
</tr>
</thead>
<tbody><tr>
<td><code>bannerKey</code></td>
<td>Unique identifier for the banner configuration. Found in the Opti-X Admin panel under Widget Manager.</td>
<td><code>f34a724d-c41e-4716-b6b4-77d3c8...</code></td>
</tr>
<tr>
<td><code>auth</code></td>
<td>Encrypted authentication string containing your API key and brand. Ensures secure access.</td>
<td><code>7f1e2c1d3fceb7dbf7cf50b9d6f2b5...</code></td>
</tr>
<tr>
<td><code>userId</code></td>
<td>Identifies the end user viewing the banner. Enables the AI model to return personalized recommendations.</td>
<td><code>CUSTOMER_123456</code></td>
</tr>
<tr>
<td><code>contextId</code></td>
<td>Ensures uniqueness across multiple banner placements and aligns click-through links with displayed products.</td>
<td><code>CUST123:1706745600:slot1</code></td>
</tr>
</tbody></table>
<h3>What Happens Without userId</h3>
<p>If <code>userId</code> is not supplied or is empty, Opti-X cannot identify the user. The banner displays generic or default recommendations instead of personalized content. These defaults are configured in your banner settings and typically show popular or featured items.</p>
<p><strong>Common causes of missing userId:</strong></p>
<ul>
<li>Template tag not replaced (shows literal <code>[%CUSTOMER_ID%]</code> instead of actual ID)</li>
<li>User not logged in on website</li>
<li>ESP merge field misconfigured</li>
</ul>
<h3>Understanding contextId</h3>
<p>The <code>contextId</code> parameter serves a critical function: it ensures each banner placement shows different recommendations.</p>
<p><strong>Without a unique contextId:</strong> All users might see the same default content instead of personalized recommendations. If you place multiple banners on one page with identical contextIds, they show duplicate products.</p>
<p><strong>With proper contextId:</strong> Each banner placement generates unique recommendations, even when using the same banner configuration multiple times.</p>
<h4>contextId Structure</h4>
<p>Build your contextId from three segments separated by colons:</p>
<table>
<thead>
<tr>
<th>Segment</th>
<th>Purpose</th>
<th>Example</th>
</tr>
</thead>
<tbody><tr>
<td>First</td>
<td>User or session identifier</td>
<td>Customer ID, session ID</td>
</tr>
<tr>
<td>Second</td>
<td>Time or deployment context</td>
<td>Timestamp, campaign ID</td>
</tr>
<tr>
<td>Third</td>
<td>Placement location</td>
<td><code>slot1</code>, <code>header</code>, <code>sidebar</code></td>
</tr>
</tbody></table>
<p><strong>Example contextId:</strong> <code>CUST123456:1706745600:hero_banner</code></p>
<p>This structure ensures:</p>
<ul>
<li>Same user sees different recommendations in different emails (timestamp varies)</li>
<li>Same email shows different products in different banner slots (placement varies)</li>
<li>Recommendations remain consistent if user views the same banner again (all segments match)</li>
</ul>
<h3>What Happens With Wrong or Duplicated contextId</h3>
<table>
<thead>
<tr>
<th>Issue</th>
<th>Result</th>
</tr>
</thead>
<tbody><tr>
<td>Same contextId for all users</td>
<td>All users see identical recommendations (defeats personalization)</td>
</tr>
<tr>
<td>Same contextId for multiple banners on one page</td>
<td>Duplicate products across banners</td>
</tr>
<tr>
<td>contextId changes on every page load</td>
<td>Recommendations change unexpectedly, poor user experience</td>
</tr>
<tr>
<td>Missing contextId entirely</td>
<td>Falls back to default recommendations, caching issues</td>
</tr>
</tbody></table>
<h2>Embedding Banners in Email</h2>
<h3>Optimail Integration</h3>
<p>If your contract includes both Opti-X Smart Content and Optimail, the Visual Editor provides an &quot;Opti-X Banner&quot; content block. Simply drag the block into your template and select a banner from your Opti-X library.</p>
<p>Optimail automatically manages all parameters:</p>
<ul>
<li><code>userId</code> maps to the recipient&#39;s customer ID</li>
<li><code>contextId</code> generates automatically from message metadata</li>
<li>Authentication handles seamlessly</li>
</ul>
<p>See the dedicated Optimail integration guide for detailed implementation steps.</p>
<h3>Other Email Service Providers (ESPs)</h3>
<p>For ESPs not managed by Optimove, collect the banner assets manually:</p>
<ol>
<li>Open the Opti-X Widget Manager gallery</li>
<li>Click &quot;Get Implementation Codes&quot; on your banner</li>
<li>Select the &quot;Image Link&quot; tab</li>
<li>Copy the provided URLs</li>
</ol>
<p>The URLs include placeholders for personalization parameters:</p>
<pre><code>https://api.opti-x.optimove.net/banner/image?bannerKey=YOUR_KEY&amp;auth=YOUR_AUTH&amp;userId=[USER_ID]&amp;contextId=[CONTEXT_ID]
</code></pre>
<p>Replace the placeholders with your ESP&#39;s merge tags:</p>
<table>
<thead>
<tr>
<th>Placeholder</th>
<th>ESP Merge Tag Example</th>
</tr>
</thead>
<tbody><tr>
<td><code>[USER_ID]</code></td>
<td><code>%%CUSTOMER_ID%%</code>, <code>{{contact.id}}</code>, <code>[%CID%]</code></td>
</tr>
<tr>
<td><code>[CONTEXT_ID]</code></td>
<td><code>%%CUSTOMER_ID%%:%%SEND_TIMESTAMP%%:slot1</code></td>
</tr>
</tbody></table>
<p><strong>Important:</strong> Test that merge tags render actual values before sending. A common mistake is deploying with unresolved tags like literal <code>%%CUSTOMER_ID%%</code> text.</p>
<h2>Embedding Banners on Websites</h2>
<p>For website personalization, use the HTML code implementation:</p>
<ol>
<li>Open the Opti-X Widget Manager gallery</li>
<li>Click &quot;Get Implementation Codes&quot; on your banner</li>
<li>Select the &quot;HTML Code&quot; tab</li>
<li>Copy the provided code snippet</li>
</ol>
<p>The code includes JavaScript that:</p>
<ul>
<li>Fetches personalized recommendations</li>
<li>Renders the banner in your page</li>
<li>Tracks impressions and clicks</li>
</ul>
<p><strong>Populate the parameters dynamically:</strong></p>
<pre><code class="language-javascript">// Example: Set userId from your authentication system
const userId = getCurrentUserId(); // Your function to get logged-in user ID

// Example: Build contextId for this page and placement
const contextId = `${userId}:${Date.now()}:homepage_hero`;
</code></pre>
<p>For anonymous users, use a consistent session identifier as <code>userId</code> to maintain recommendation consistency during their visit.</p>
<h2>Troubleshooting Banner Issues</h2>
<h3>Blank or Missing Banners</h3>
<table>
<thead>
<tr>
<th>Symptom</th>
<th>Likely Cause</th>
<th>Solution</th>
</tr>
</thead>
<tbody><tr>
<td>Banner doesn&#39;t appear at all</td>
<td>Invalid <code>bannerKey</code></td>
<td>Verify the key in Widget Manager</td>
</tr>
<tr>
<td>White/empty banner space</td>
<td>Missing <code>image_url</code> in inventory items</td>
<td>Add image URLs to your product data</td>
</tr>
<tr>
<td>Broken image icon</td>
<td>Image URL returns 404</td>
<td>Check that product images are accessible</td>
</tr>
<tr>
<td>&quot;Unauthorized&quot; error</td>
<td>Invalid <code>auth</code> parameter</td>
<td>Regenerate authentication string</td>
</tr>
</tbody></table>
<h3>Wrong or Unexpected Content</h3>
<table>
<thead>
<tr>
<th>Symptom</th>
<th>Likely Cause</th>
<th>Solution</th>
</tr>
</thead>
<tbody><tr>
<td>Same products for everyone</td>
<td>Missing or static <code>userId</code></td>
<td>Ensure userId is populated per-user</td>
</tr>
<tr>
<td>Duplicate products in multiple slots</td>
<td>Same <code>contextId</code> for all placements</td>
<td>Add unique placement identifier to contextId</td>
</tr>
<tr>
<td>Irrelevant products</td>
<td>Missing filtering context</td>
<td>Add category or page context parameters</td>
</tr>
<tr>
<td>Old/outdated products</td>
<td>Inventory not refreshed</td>
<td>Check inventory upload frequency</td>
</tr>
</tbody></table>
<h3>Performance Issues</h3>
<table>
<thead>
<tr>
<th>Symptom</th>
<th>Likely Cause</th>
<th>Solution</th>
</tr>
</thead>
<tbody><tr>
<td>Slow banner loading</td>
<td>Large image files</td>
<td>Optimize images before uploading</td>
</tr>
<tr>
<td>Banners flash/reload</td>
<td>contextId changes on re-render</td>
<td>Stabilize contextId calculation</td>
</tr>
<tr>
<td>High latency</td>
<td>Network issues</td>
<td>Check API endpoint connectivity</td>
</tr>
</tbody></table>
<h2>Related Topics</h2>
<ul>
<li><a href="#inventory-overview">Inventory Management</a> - Ensure products have required image URLs</li>
<li><a href="#api-reference-overview">API Reference</a> - Banner API endpoint details</li>
<li><a href="#common-issues">Common Issues</a> - General troubleshooting guide</li>
<li><a href="#getting-help">Getting Help</a> - Contact support for banner issues</li>
</ul>

</section>
<section id="common-issues" class="doc-section">
<h1>Common Issues and Solutions</h1>
<p>This guide covers frequently encountered issues when integrating with Opti-X. Each issue includes the symptom you observe, the underlying cause, and actionable steps to resolve it.</p>
<h2>Authentication Issues</h2>
<h3>401 Unauthorized</h3>
<p><strong>Symptom:</strong> API requests return HTTP 401 status with message &quot;Unauthorized&quot; or &quot;Invalid API key.&quot;</p>
<p><strong>Cause:</strong> The API key is missing, malformed, or has been revoked.</p>
<p><strong>Solution:</strong></p>
<ol>
<li>Verify your API key is included in the request header:<pre><code>x-api-key: your-api-key-here
</code></pre>
</li>
<li>Check for extra whitespace or hidden characters in the key</li>
<li>Confirm the key is active in your Opti-X Admin panel under API Keys</li>
<li>If the key was recently created, wait 2-3 minutes for propagation</li>
</ol>
<p><strong>Example of correct header:</strong></p>
<pre><code class="language-bash">curl -X GET &quot;https://api.opti-x.optimove.net/v3/recommend&quot; \
  -H &quot;x-api-key: abc123def456&quot; \
  -H &quot;Content-Type: application/json&quot;
</code></pre>
<hr>
<h3>403 Forbidden</h3>
<p><strong>Symptom:</strong> API requests return HTTP 403 status with message &quot;Forbidden&quot; or &quot;Insufficient permissions.&quot;</p>
<p><strong>Cause:</strong> The API key is valid but lacks permission for the requested operation or brand.</p>
<p><strong>Solution:</strong></p>
<ol>
<li>Verify the API key has access to the brand specified in your request</li>
<li>Check that the key has the required permission level (read vs. write)</li>
<li>For inventory uploads, confirm the key has write permissions</li>
<li>Contact your Integration Manager to adjust key permissions if needed</li>
</ol>
<hr>
<h2>Recommendation Issues</h2>
<h3>Empty Recommendations Array</h3>
<p><strong>Symptom:</strong> The API returns successfully (HTTP 200) but the <code>recommendations</code> array is empty: <code>{&quot;recommendations&quot;: []}</code></p>
<p><strong>Cause:</strong> Multiple factors can cause empty results:</p>
<table>
<thead>
<tr>
<th>Possible Cause</th>
<th>How to Verify</th>
<th>Solution</th>
</tr>
</thead>
<tbody><tr>
<td>Inventory not loaded</td>
<td>Check Admin panel inventory status</td>
<td>Upload inventory file</td>
</tr>
<tr>
<td>User not found</td>
<td>Try request with known test user</td>
<td>Verify userId format matches your data</td>
</tr>
<tr>
<td>All items filtered out</td>
<td>Remove filters and test again</td>
<td>Adjust availability or display filters</td>
</tr>
<tr>
<td>No items match context</td>
<td>Check category/placement configuration</td>
<td>Broaden matching criteria</td>
</tr>
</tbody></table>
<p><strong>Solution steps:</strong></p>
<ol>
<li>First, test without any filters to confirm inventory is loaded</li>
<li>Then add filters back one at a time to identify which filter causes empty results</li>
<li>Verify your inventory includes items matching the placement configuration</li>
</ol>
<hr>
<h3>Same Recommendations for All Users</h3>
<p><strong>Symptom:</strong> Every user receives identical product recommendations regardless of their history or preferences.</p>
<p><strong>Cause:</strong> The request is missing <code>userId</code> or using the same <code>userId</code> for all requests. Without user identification, Opti-X returns default/fallback recommendations.</p>
<p><strong>Solution:</strong></p>
<ol>
<li>Verify <code>userId</code> parameter is included in every request:<pre><code class="language-json">{
  &quot;userId&quot;: &quot;CUSTOMER_123&quot;,
  &quot;numRecs&quot;: 5
}
</code></pre>
</li>
<li>Confirm the userId value changes per user (not hardcoded)</li>
<li>Check that template merge tags are rendering actual values, not literal tags like <code>[%CUSTOMER_ID%]</code></li>
<li>For banners, also verify <code>contextId</code> is unique per user/placement</li>
</ol>
<p><strong>Test:</strong> Make two requests with different userIds and compare results. If results are identical, the personalization is not working.</p>
<hr>
<h3>Irrelevant Recommendations</h3>
<p><strong>Symptom:</strong> Recommendations are personalized (different per user) but seem unrelated to the page context or user intent.</p>
<p><strong>Cause:</strong> Missing or incorrect context parameters that help Opti-X understand what the user is currently viewing.</p>
<p><strong>Solution:</strong></p>
<ol>
<li>Add context parameters to your request:<pre><code class="language-json">{
  &quot;userId&quot;: &quot;CUSTOMER_123&quot;,
  &quot;numRecs&quot;: 5,
  &quot;context&quot;: {
    &quot;currentCategory&quot;: &quot;electronics&quot;,
    &quot;currentItemId&quot;: &quot;PROD_456&quot;
  }
}
</code></pre>
</li>
<li>For product pages, include the current product ID to get &quot;similar items&quot; or &quot;frequently bought together&quot;</li>
<li>For category pages, include the category to get relevant products</li>
<li>Verify placement configuration matches the page type</li>
</ol>
<hr>
<h2>Inventory Issues</h2>
<h3>Validation Errors on Upload</h3>
<p><strong>Symptom:</strong> Inventory upload fails with validation errors listing specific fields or records.</p>
<p><strong>Cause:</strong> The uploaded data does not match the expected schema for your inventory type.</p>
<p><strong>Common validation errors:</strong></p>
<table>
<thead>
<tr>
<th>Error Message</th>
<th>Cause</th>
<th>Solution</th>
</tr>
</thead>
<tbody><tr>
<td>&quot;Missing required field: item_id&quot;</td>
<td>Required field not present</td>
<td>Add the missing field to all records</td>
</tr>
<tr>
<td>&quot;Invalid data type for price&quot;</td>
<td>Field contains wrong type (string vs number)</td>
<td>Convert to correct type: <code>&quot;price&quot;: 29.99</code> not <code>&quot;price&quot;: &quot;29.99&quot;</code></td>
</tr>
<tr>
<td>&quot;Unknown field: product_name&quot;</td>
<td>Field name doesn&#39;t match schema</td>
<td>Use exact field names from schema: <code>title</code> not <code>product_name</code></td>
</tr>
<tr>
<td>&quot;Duplicate item_id: PROD_123&quot;</td>
<td>Same ID appears multiple times</td>
<td>Ensure each item_id is unique</td>
</tr>
</tbody></table>
<p><strong>Solution:</strong></p>
<ol>
<li>Review the validation error message for specific field names</li>
<li>Compare your data against the inventory schema documentation</li>
<li>Fix the identified issues and re-upload</li>
<li>Use the inventory validation endpoint to test before full upload</li>
</ol>
<hr>
<h3>Products Not Appearing in Recommendations</h3>
<p><strong>Symptom:</strong> Specific products exist in inventory but never appear in recommendations.</p>
<p><strong>Cause:</strong> Products may be filtered out by display status, availability, or other criteria.</p>
<p><strong>Checklist:</strong></p>
<table>
<thead>
<tr>
<th>Check</th>
<th>Expected Value</th>
<th>How to Fix</th>
</tr>
</thead>
<tbody><tr>
<td><code>display</code> field</td>
<td><code>true</code> or <code>1</code></td>
<td>Set to true to make item recommendable</td>
</tr>
<tr>
<td><code>availability</code> field</td>
<td><code>in_stock</code> or equivalent</td>
<td>Update stock status</td>
</tr>
<tr>
<td><code>start_date</code> / <code>end_date</code></td>
<td>Current date within range</td>
<td>Adjust date range or remove date restrictions</td>
</tr>
<tr>
<td>Category assignment</td>
<td>Matches placement configuration</td>
<td>Assign product to correct categories</td>
</tr>
</tbody></table>
<p><strong>Solution:</strong></p>
<ol>
<li>Query your inventory to check the product&#39;s current field values</li>
<li>Verify the product meets all filter criteria for your placement</li>
<li>Update the product data and re-upload inventory</li>
<li>Wait for inventory refresh (typically 15-30 minutes)</li>
</ol>
<hr>
<h3>Stale or Outdated Data</h3>
<p><strong>Symptom:</strong> Recommendations show old prices, out-of-stock items, or discontinued products.</p>
<p><strong>Cause:</strong> Inventory data has not been refreshed recently, or caching is serving old data.</p>
<p><strong>Solution:</strong></p>
<ol>
<li>Check when inventory was last uploaded in the Admin panel</li>
<li>Implement automated inventory uploads (recommended: at least daily, hourly for fast-changing inventory)</li>
<li>For real-time updates, use the incremental update API for price/stock changes</li>
<li>Clear recommendation cache if available in your configuration</li>
</ol>
<p><strong>Recommended upload frequency:</strong></p>
<table>
<thead>
<tr>
<th>Inventory Change Rate</th>
<th>Recommended Frequency</th>
</tr>
</thead>
<tbody><tr>
<td>Rarely changes</td>
<td>Weekly</td>
</tr>
<tr>
<td>Daily updates</td>
<td>Daily</td>
</tr>
<tr>
<td>Frequent stock changes</td>
<td>Every 4-6 hours</td>
</tr>
<tr>
<td>Real-time pricing</td>
<td>Incremental updates + daily full sync</td>
</tr>
</tbody></table>
<hr>
<h2>Search Issues</h2>
<h3>No Search Results</h3>
<p><strong>Symptom:</strong> Search API returns empty results even for terms that should match products.</p>
<p><strong>Cause:</strong> Query may be too specific, inventory not indexed for search, or search configuration issues.</p>
<p><strong>Solution:</strong></p>
<ol>
<li>Test with a broader query (single common word)</li>
<li>Verify search is enabled for your inventory type</li>
<li>Check that searchable fields (<code>title</code>, <code>description</code>) contain the query terms</li>
<li>Confirm products are not filtered out by availability or display status</li>
</ol>
<p><strong>Example progression:</strong></p>
<pre><code>&quot;blue cotton mens dress shirt size large&quot; → no results
&quot;blue shirt&quot; → no results
&quot;shirt&quot; → results found (query was too specific)
</code></pre>
<hr>
<h3>Slow Search Responses</h3>
<p><strong>Symptom:</strong> Search requests take several seconds to return, causing poor user experience.</p>
<p><strong>Cause:</strong> Missing debouncing in implementation, causing excessive API calls, or network latency.</p>
<p><strong>Solution:</strong></p>
<ol>
<li>Implement debouncing in your search input (wait 300-500ms after user stops typing):<pre><code class="language-javascript">// Debounce example
let searchTimeout;
searchInput.addEventListener(&#39;input&#39;, (e) =&gt; {
  clearTimeout(searchTimeout);
  searchTimeout = setTimeout(() =&gt; {
    callSearchAPI(e.target.value);
  }, 300);
});
</code></pre>
</li>
<li>Show loading state to users during search</li>
<li>Cache recent search results on the client side</li>
<li>Check network latency to <code>api.opti-x.optimove.net</code></li>
</ol>
<hr>
<h2>Banner Issues</h2>
<h3>Blank Banners</h3>
<p><strong>Symptom:</strong> Banner placeholder appears but shows no content or images.</p>
<p><strong>Cause:</strong> Products in recommendations are missing <code>image_url</code> field, or images are inaccessible.</p>
<p><strong>Solution:</strong></p>
<ol>
<li>Verify your inventory includes <code>image_url</code> for all products</li>
<li>Test that image URLs are publicly accessible (not behind authentication)</li>
<li>Check image URLs return valid images (not 404 or redirect loops)</li>
<li>Confirm image format is supported (JPG, PNG, WebP)</li>
</ol>
<p><strong>Test image accessibility:</strong></p>
<pre><code class="language-bash">curl -I &quot;https://your-cdn.com/product-image.jpg&quot;
# Should return HTTP 200 with image content-type
</code></pre>
<hr>
<h3>Same Banner Content for Everyone</h3>
<p><strong>Symptom:</strong> All users see identical banner content instead of personalized recommendations.</p>
<p><strong>Cause:</strong> Missing <code>userId</code> or <code>contextId</code> parameters in the banner URL.</p>
<p><strong>Solution:</strong></p>
<ol>
<li>Verify banner URL includes both parameters:<pre><code>...&amp;userId=CUSTOMER_123&amp;contextId=CUST123:1706745600:slot1
</code></pre>
</li>
<li>Confirm template merge tags are rendering (not showing literal <code>[%CUSTOMER_ID%]</code>)</li>
<li>Check that <code>contextId</code> includes user-specific segment</li>
<li>Test with two different userIds and compare rendered content</li>
</ol>
<hr>
<h3>Wrong Products in Banner</h3>
<p><strong>Symptom:</strong> Banner shows products, but they seem unrelated to the expected category or placement.</p>
<p><strong>Cause:</strong> Banner placement configuration does not match intended use, or filtering is misconfigured.</p>
<p><strong>Solution:</strong></p>
<ol>
<li>Review banner configuration in Widget Manager</li>
<li>Verify the correct <code>bannerKey</code> is being used</li>
<li>Check placement filters (category, tags, product types)</li>
<li>Confirm inventory items are assigned to correct categories</li>
</ol>
<hr>
<h2>Related Topics</h2>
<ul>
<li><a href="#banner-deployment">Banner Deployment Guide</a> - Detailed banner implementation</li>
<li><a href="#inventory-overview">Inventory Management</a> - Inventory upload and schema</li>
<li><a href="#api-reference-overview">API Reference</a> - Complete API documentation</li>
<li><a href="#getting-help">Getting Help</a> - Contact support for unresolved issues</li>
</ul>

</section>
<section id="getting-help" class="doc-section">
<h1>Getting Help</h1>
<p>When you encounter issues that this documentation does not resolve, Optimove provides multiple support channels. This guide explains how to get help efficiently and what information to provide for faster resolution.</p>
<h2>Self-Service Resources</h2>
<p>Before contacting support, check these resources:</p>
<h3>Documentation</h3>
<ul>
<li><strong>This developer documentation</strong> - Search for your specific issue or browse the troubleshooting section</li>
<li><strong><a href="#common-issues">Common Issues Guide</a></strong> - Solutions for frequently encountered problems</li>
</ul>
<h3>Opti-X Admin Panel</h3>
<p>Access at your configured Admin URL to:</p>
<ul>
<li>View inventory upload status and validation errors</li>
<li>Check API key status and permissions</li>
<li>Review banner configurations</li>
<li>Monitor system health and recent activity</li>
</ul>
<h3>API Response Messages</h3>
<p>Opti-X API responses include descriptive error messages. The <code>message</code> field often indicates exactly what went wrong:</p>
<pre><code class="language-json">{
  &quot;error&quot;: &quot;validation_error&quot;,
  &quot;message&quot;: &quot;Missing required field: item_id in record 47&quot;
}
</code></pre>
<hr>
<h2>Contact Your Integration Manager</h2>
<p><strong>For technical integration issues</strong>, contact your assigned Integration Manager. They handle:</p>
<ul>
<li>API integration questions</li>
<li>Inventory schema and upload issues</li>
<li>Recommendation algorithm configuration</li>
<li>Banner implementation troubleshooting</li>
<li>Performance optimization</li>
<li>Custom integration requirements</li>
</ul>
<p>Your Integration Manager has deep technical knowledge of Opti-X and direct access to engineering resources when needed.</p>
<hr>
<h2>Contact Your Customer Success Manager</h2>
<p><strong>For business and account questions</strong>, contact your Customer Success Manager. They handle:</p>
<ul>
<li>Contract and licensing questions</li>
<li>Feature requests and roadmap discussions</li>
<li>Best practices for your use case</li>
<li>Training and onboarding sessions</li>
<li>Escalation of critical issues</li>
<li>Strategic guidance on using Opti-X effectively</li>
</ul>
<hr>
<h2>Information to Provide When Requesting Help</h2>
<p>Providing complete information upfront significantly speeds up issue resolution. Include the following details in your support request:</p>
<h3>Always Include</h3>
<table>
<thead>
<tr>
<th>Information</th>
<th>Description</th>
<th>Example</th>
</tr>
</thead>
<tbody><tr>
<td><strong>Brand key</strong></td>
<td>Your Opti-X brand identifier</td>
<td><code>acme_retail_prod</code></td>
</tr>
<tr>
<td><strong>Environment</strong></td>
<td>Production, staging, or development</td>
<td><code>Production</code></td>
</tr>
<tr>
<td><strong>Timestamp</strong></td>
<td>When the issue occurred (include timezone)</td>
<td><code>2024-01-15 14:32:00 UTC</code></td>
</tr>
<tr>
<td><strong>Issue description</strong></td>
<td>Clear description of what happened</td>
<td>&quot;Recommendations returning empty for all users since 2pm&quot;</td>
</tr>
</tbody></table>
<h3>For API Issues</h3>
<table>
<thead>
<tr>
<th>Information</th>
<th>Description</th>
<th>Example</th>
</tr>
</thead>
<tbody><tr>
<td><strong>Endpoint</strong></td>
<td>Full API URL called</td>
<td><code>https://api.opti-x.optimove.net/v3/recommend</code></td>
</tr>
<tr>
<td><strong>HTTP method</strong></td>
<td>GET, POST, etc.</td>
<td><code>POST</code></td>
</tr>
<tr>
<td><strong>Request body</strong></td>
<td>Full request payload (redact sensitive data)</td>
<td>See example below</td>
</tr>
<tr>
<td><strong>Response</strong></td>
<td>Full response received</td>
<td>See example below</td>
</tr>
<tr>
<td><strong>HTTP status code</strong></td>
<td>Response status</td>
<td><code>400 Bad Request</code></td>
</tr>
</tbody></table>
<p><strong>Example request (with sensitive data redacted):</strong></p>
<pre><code class="language-json">{
  &quot;userId&quot;: &quot;USER_[REDACTED]&quot;,
  &quot;numRecs&quot;: 5,
  &quot;placement&quot;: &quot;homepage_hero&quot;,
  &quot;context&quot;: {
    &quot;category&quot;: &quot;electronics&quot;
  }
}
</code></pre>
<p><strong>Example response:</strong></p>
<pre><code class="language-json">{
  &quot;error&quot;: &quot;invalid_request&quot;,
  &quot;message&quot;: &quot;Unknown placement: homepage_hero&quot;,
  &quot;requestId&quot;: &quot;req_abc123def456&quot;
}
</code></pre>
<h3>For Banner Issues</h3>
<table>
<thead>
<tr>
<th>Information</th>
<th>Description</th>
<th>Example</th>
</tr>
</thead>
<tbody><tr>
<td><strong>Banner key</strong></td>
<td>The bannerKey from your implementation</td>
<td><code>f34a724d-c41e-4716-b6b4...</code></td>
</tr>
<tr>
<td><strong>Full banner URL</strong></td>
<td>Complete URL including all parameters</td>
<td>Include userId and contextId values used</td>
</tr>
<tr>
<td><strong>Screenshot</strong></td>
<td>Visual of what the banner displays</td>
<td>Attach image showing the issue</td>
</tr>
<tr>
<td><strong>Expected behavior</strong></td>
<td>What should happen</td>
<td>&quot;Should show 3 personalized products&quot;</td>
</tr>
<tr>
<td><strong>Actual behavior</strong></td>
<td>What actually happens</td>
<td>&quot;Shows blank white space&quot;</td>
</tr>
</tbody></table>
<h3>For Inventory Issues</h3>
<table>
<thead>
<tr>
<th>Information</th>
<th>Description</th>
<th>Example</th>
</tr>
</thead>
<tbody><tr>
<td><strong>Upload timestamp</strong></td>
<td>When the upload was attempted</td>
<td><code>2024-01-15 10:00:00 UTC</code></td>
</tr>
<tr>
<td><strong>File details</strong></td>
<td>File name, size, record count</td>
<td><code>products.json, 2.4MB, 15,000 records</code></td>
</tr>
<tr>
<td><strong>Validation errors</strong></td>
<td>Any error messages received</td>
<td>&quot;Invalid data type for field &#39;price&#39; in record 127&quot;</td>
</tr>
<tr>
<td><strong>Sample records</strong></td>
<td>Example of problematic data (redacted)</td>
<td>2-3 records showing the issue</td>
</tr>
</tbody></table>
<hr>
<h2>Tips for Faster Resolution</h2>
<h3>Do</h3>
<ul>
<li><strong>Be specific</strong> - &quot;Empty recommendations for userId ABC123 at 2pm UTC&quot; is better than &quot;recommendations broken&quot;</li>
<li><strong>Include request IDs</strong> - If the response includes a <code>requestId</code>, always provide it</li>
<li><strong>Test in isolation</strong> - Try to reproduce with minimal parameters before reporting</li>
<li><strong>Check recent changes</strong> - Note any changes made before the issue started</li>
</ul>
<h3>Do Not</h3>
<ul>
<li><strong>Share API keys</strong> - Redact or replace with <code>[REDACTED]</code></li>
<li><strong>Share customer PII</strong> - Replace real user IDs with anonymized examples</li>
<li><strong>Send production credentials</strong> - Use test environment examples when possible</li>
<li><strong>Wait to report critical issues</strong> - Escalate immediately if production is impacted</li>
</ul>
<hr>
<h2>Issue Severity Levels</h2>
<p>When reporting issues, indicate the severity to help prioritize response:</p>
<table>
<thead>
<tr>
<th>Severity</th>
<th>Definition</th>
<th>Example</th>
</tr>
</thead>
<tbody><tr>
<td><strong>Critical</strong></td>
<td>Production down, all users affected</td>
<td>API returning 500 errors for all requests</td>
</tr>
<tr>
<td><strong>High</strong></td>
<td>Major feature broken, significant user impact</td>
<td>Recommendations empty for 50% of users</td>
</tr>
<tr>
<td><strong>Medium</strong></td>
<td>Feature degraded, workaround available</td>
<td>Slow response times, but functional</td>
</tr>
<tr>
<td><strong>Low</strong></td>
<td>Minor issue, minimal impact</td>
<td>Cosmetic banner display issue</td>
</tr>
</tbody></table>
<hr>
<h2>Response Time Expectations</h2>
<p>Response times vary by severity and support tier. Your Integration Manager or Customer Success Manager can provide specific SLA details for your contract.</p>
<p>General guidelines:</p>
<ul>
<li><strong>Critical issues</strong> - Initial response within hours</li>
<li><strong>High severity</strong> - Initial response within 1 business day</li>
<li><strong>Medium/Low</strong> - Initial response within 2-3 business days</li>
</ul>
<p>For critical production issues outside business hours, use the emergency contact provided in your onboarding materials.</p>
<hr>
<h2>Related Topics</h2>
<ul>
<li><a href="#common-issues">Common Issues</a> - Self-service troubleshooting guide</li>
<li><a href="#api-reference-overview">API Reference</a> - Complete API documentation</li>
<li><a href="#banner-deployment">Banner Deployment</a> - Banner implementation details</li>
</ul>

</section>
    </main>
  </div>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/highlight.js/11.9.0/highlight.min.js"></script>
  <script>
    // Syntax highlighting
    hljs.highlightAll();

    // Sidebar section collapse/expand
    document.querySelectorAll('.section-toggle').forEach(btn => {
      btn.addEventListener('click', () => {
        const children = btn.nextElementSibling;
        const expanded = btn.getAttribute('aria-expanded') === 'true';
        btn.setAttribute('aria-expanded', String(!expanded));
        children.style.display = expanded ? 'none' : '';
        btn.querySelector('.toggle-icon').innerHTML = expanded ? '&#9656;' : '&#9662;';
      });
    });

    // Scroll-spy: highlight active nav link
    const observer = new IntersectionObserver(entries => {
      entries.forEach(entry => {
        if (entry.isIntersecting) {
          document.querySelectorAll('.nav-link').forEach(a => a.classList.remove('active'));
          const link = document.querySelector('.nav-link[href="#' + entry.target.id + '"]');
          if (link) {
            link.classList.add('active');
            link.scrollIntoView({ block: 'nearest', behavior: 'auto' });
          }
        }
      });
    }, { rootMargin: '-10% 0px -85% 0px' });

    document.querySelectorAll('.doc-section').forEach(sec => observer.observe(sec));

    // Smooth scroll for anchor links
    document.addEventListener('click', e => {
      const a = e.target.closest('a[href^="#"]');
      if (!a) return;
      e.preventDefault();
      const id = a.getAttribute('href').slice(1);
      const target = document.getElementById(id);
      if (target) {
        target.scrollIntoView({ behavior: 'smooth' });
        // On mobile, close sidebar after navigation
        document.getElementById('sidebar').classList.remove('open');
      }
    });

    // Mobile sidebar toggle
    document.getElementById('sidebar-toggle').addEventListener('click', () => {
      document.getElementById('sidebar').classList.toggle('open');
    });

    // Close sidebar when clicking outside on mobile
    document.getElementById('content').addEventListener('click', () => {
      document.getElementById('sidebar').classList.remove('open');
    });
  </script>
</body>
</html>
