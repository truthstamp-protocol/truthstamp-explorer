# truthstamp-explorer
Public explorer UI/backend.

# TruthStamp Explorer

The public explorer for the TruthStamp Protocol — browse, search, and 
verify permanent stamps on MegaETH.

🔍 **Live at:** https://truthstamp.io/explorer.html

---

## What It Does

The explorer is a public-facing interface that lets anyone:

- Browse all public stamps in real time
- Filter by type (text, file, URL), category, and feed (latest, reveals, upcoming)
- Search by keyword, creator, or proof ID
- View the reveal calendar for upcoming sealed stamps
- See top creators by stamp count
- Verify any stamp independently without an account

No login required. No TruthStamp account needed. Fully read-only.

---

## Stack

| Component       | Technology                  |
|-----------------|-----------------------------|
| Frontend        | Vanilla HTML / CSS / JS     |
| Database        | Supabase (read-only queries)|
| Blockchain      | MegaETH (Chain ID: 4326)    |
| Permanent storage | Arweave                   |
| Hosting         | GitHub Pages                |

The explorer queries Supabase directly from the browser using the 
public anon key. It never writes to the database — read-only throughout.

---

## Files

| File            | Description                                      |
|-----------------|--------------------------------------------------|
| `explorer.html` | Main explorer page — stamp feed, filters, search |
| `proof.html`    | Individual stamp proof page                      |
| `verify.html`   | Verify any content by hash                       |
| `js/config.js`  | Contract address, RPC, Supabase config           |

---

## Self-Hosting

You can run your own explorer instance against your own contract 
and Supabase database.

### 1. Fork this repo

```bash
git clone https://github.com/truthstamp-protocol/truthstamp-explorer
```

### 2. Configure

Edit `js/config.js`:

```js
const TRUTHSTAMP_CONFIG = {
  SUPABASE_URL:      'https://yourproject.supabase.co',
  SUPABASE_ANON_KEY: 'your-anon-key',
  CONTRACT_ADDRESS:  '0xYourContractAddress',
  CONTRACT_CHAIN_ID: 4326,
  CONTRACT_RPC_URL:  'https://mainnet.megaeth.com/rpc',
  CONTRACT_EXPLORER: 'https://mega.etherscan.io/',
};
```

### 3. Deploy

Push to GitHub and enable GitHub Pages — Settings → Pages → 
Source: `main` branch. Your explorer will be live in seconds.

Or deploy to any static host: Vercel, Netlify, Cloudflare Pages.

### 4. Prerequisites

Your self-hosted explorer needs:

- A deployed TruthStamp contract  
  → [truthstamp-contracts](https://github.com/truthstamp-protocol/truthstamp-contracts)
- A running indexer syncing on-chain events to Supabase  
  → [truthstamp-indexer](https://github.com/truthstamp-protocol/truthstamp-indexer)
- The `stamps_with_creator` view in your Supabase database  
  → SQL in [truthstamp-web](https://github.com/truthstamp-protocol/truthstamp-web)

---

## Key Features

### Stamp Feed
Real-time feed of public stamps with infinite scroll. Filterable by 
content type, category tag, and sort order.

### Reveal Calendar
Right panel shows upcoming sealed stamps grouped by reveal date — 
so anyone can follow predictions as they unlock.

### Independent Verification
Every stamp card links directly to:
- The on-chain transaction on MegaETH explorer
- The permanent content on Arweave (for revealed stamps)

Anyone can verify a stamp without TruthStamp — the proof lives 
on-chain forever.

### Search
Search across titles, content, creator identity, and proof ID. 
Typing a pure number (e.g. `42`) jumps directly to Proof #42.

---

## Privacy

The explorer only shows **public** and **revealed** stamps. 

- Hash-only stamps show only the hash — content is never exposed
- Sealed stamps show only the reveal countdown — content stays 
  hidden until on-chain reveal
- Sealed file/URL stamps never expose the actual content or URL 
  until the reveal date passes and the on-chain reveal is complete

---

## Related Repos

- [truthstamp-contracts](https://github.com/truthstamp-protocol/truthstamp-contracts) — Smart contract
- [truthstamp-indexer](https://github.com/truthstamp-protocol/truthstamp-indexer) — Indexer
- [truthstamp-web](https://github.com/truthstamp-protocol/truthstamp-web) — Full web app
- [tsp-spec](https://github.com/truthstamp-protocol/tsp-spec) — Protocol specification

---

## License

MIT
