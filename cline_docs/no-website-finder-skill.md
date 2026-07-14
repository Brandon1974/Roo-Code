# No Website Finder Skill

**Type:** Lead Generation Tool | **Author:** Tripp Digital  
**Status:** Production | **Last Updated:** 2026-07-14

---

## Overview

The **no-website-finder** is a lead generation skill designed to identify local businesses with strong online presence (Google Business Profiles, reviews) but **no website**. These are ideal prospects for web agency services.

This skill integrates with Roo Code as a custom mode, providing specialized functionality for lead prospecting and qualification.

## Use Cases

1. **Web Agency Lead Generation** — Find prospects for a web design / hosting service
2. **Market Research** — Identify gaps in website adoption by industry and location
3. **Sales Intelligence** — Qualify leads based on review count and business maturity
4. **Outreach Campaigns** — Build targeted lists for local business development

## How It Works

### 1. Search Businesses
The tool searches Google Places for businesses matching a location and industry keyword:
- **Input:** Location (city/state) + Industry (keyword)
- **Search Scope:** Up to 20 results per run

### 2. Check for Websites
For each business found, the tool fetches full details via the Google Places API Details endpoint:
- Retrieves the `website` field specifically
- Collects contact info, rating, review count, and Maps URL

### 3. Filter & Rank
Results are filtered to include **only** businesses without websites:
- **Sort Order:** By review count (descending)
- **Logic:** Established businesses (20+ reviews) + no website = hot lead
- These are prospects actively present on Google but never invested in their own site

### 4. Export Results
Results are saved in your chosen format:
- **JSON:** Structured data for integration and analysis
- **CSV:** Spreadsheet-friendly format for sales teams

## Installation & Setup

### Prerequisites
- Node.js 14+
- Google Places API key with these permissions:
  - Places API (Text Search)
  - Places API (Place Details)
- The key must have these specific permissions enabled in Google Cloud Console

### Installation

#### Option 1: Via Tripp Digital Repository
If you have access to the Tripp Digital repo (`brandon1974/trippdigital`):

```bash
git clone https://github.com/brandon1974/trippdigital
cd trippdigital
npm install
```

Then run:
```bash
npm run no-website-finder --location "Virginia Beach, VA" --industry "handyman"
```

#### Option 2: Standalone Setup
Copy the `bin/no-website-finder.js` and `package.json` to your project, then:

```bash
node bin/no-website-finder.js --location "City, State" --industry "niche"
```

## Usage

### Basic Command

```bash
no-website-finder --location "Virginia Beach, VA" --industry "handyman"
```

### With Output Format Specified

```bash
no-website-finder --location "Austin, TX" --industry "pressure washing" --format csv
```

### Command Options

| Option | Type | Required | Example |
|--------|------|----------|---------|
| `--location` | string | Yes | `"Virginia Beach, VA"` |
| `--industry` | string | Yes | `"landscaping"` |
| `--format` | string | No | `json` or `csv` (default: json) |

## Output Examples

### JSON Output

```json
[
  {
    "name": "Joe's Handyman Services",
    "phone": "(757) 555-0123",
    "address": "123 Main St, Virginia Beach, VA 23456",
    "rating": 4.8,
    "reviewCount": 47,
    "mapsUrl": "https://www.google.com/maps/search/..."
  },
  {
    "name": "Local Repairs LLC",
    "phone": "(757) 555-0456",
    "address": "456 Oak Ave, Virginia Beach, VA 23462",
    "rating": 4.5,
    "reviewCount": 23,
    "mapsUrl": "https://www.google.com/maps/search/..."
  }
]
```

### CSV Output

```csv
name,phone,address,rating,reviewCount,mapsUrl
"Joe's Handyman Services","(757) 555-0123","123 Main St, Virginia Beach, VA 23456",4.8,47,"https://www.google.com/maps/search/..."
"Local Repairs LLC","(757) 555-0456","456 Oak Ave, Virginia Beach, VA 23462",4.5,23,"https://www.google.com/maps/search/..."
```

## File Output

Results are automatically saved with a timestamp:
- **Naming Pattern:** `leads_[industry]_[date].json` or `.csv`
- **Example:** `leads_handyman_2026-07-14.json`
- **Location:** Current working directory

## Quality Indicators

When evaluating leads from this tool:

| Metric | Good | Excellent |
|--------|------|-----------|
| Review Count | 10+ | 30+ |
| Rating | 4.0+ | 4.5+ |
| Website Status | Missing | No website field |

**Hot Leads:** 25+ reviews, 4.5+ rating, no website = established business ready for a professional site.

## Workflow Integration

### Web Agency Pitch Workflow

```
1. Run tool → Get leads without websites
   ↓
2. Review results → Identify 4-5 hot prospects
   ↓
3. Call/Email → "I see your business on Google..."
   ↓
4. Send live link → Free spec site (photo gallery + contact)
   ↓
5. Pitch → $97/month hosting + updates
   ↓
6. Deploy → Live on Netlify
```

### Tripp Digital Integration

This tool supports Tripp Digital's core business model:
- **Find:** Businesses with no website (no-website-finder)
- **Build:** Free spec site (photo gallery, contact form)
- **Deploy:** Netlify hosting
- **Pitch:** $97/month recurring revenue

## API Configuration

### Google Cloud Console Setup

1. Go to [Google Cloud Console](https://console.cloud.google.com/)
2. Create or select your project
3. Enable these APIs:
   - **Places API** (legacy and/or new)
   - **Maps API**
4. Create an API key:
   - Navigate to Credentials
   - Create API Key
   - Restrict to your IP (if needed)
5. Copy the key and use it in this tool

### Troubleshooting

#### Error: "REQUEST_DENIED"
- The API key doesn't have Places API enabled
- **Fix:** Enable Places API in Google Cloud Console and wait 5 minutes for changes to propagate

#### Error: "No results found"
- Location + industry combination returned no results
- **Try:** Use broader search terms or different location (e.g., "VA" instead of specific city)

#### Error: "quota exceeded"
- Hit the API rate limit
- **Fix:** Wait 24 hours; adjust API tier in Google Cloud Console for higher limits

## Custom Mode Usage (Roo Code)

Once imported, you can switch to the **No Website Finder** mode in Roo Code:

```
/switch-mode no-website-finder
```

This mode will:
- Provide specialized prompts for lead generation
- Restrict edit permissions to lead files (JSON/CSV)
- Guide you through outreach workflows
- Help analyze and prioritize leads

## Best Practices

1. **Specificity Matters** — Use exact city + specific industry for best results
2. **Quality Over Quantity** — A few hot leads (25+ reviews) beats many cold leads
3. **Regular Searches** — Run monthly for new market entries or seasonal opportunities
4. **Territory Planning** — Cover one niche deeply before expanding to others
5. **Data Cleaning** — Remove duplicates and verify phone numbers before outreach
6. **Follow-up Tracking** — Track which leads convert to sales (for ROI calculation)

## Example Scenarios

### Scenario 1: Handyman Niche Expansion

```bash
no-website-finder --location "Virginia Beach, VA" --industry "handyman" --format csv
```

**Use:** Find 10-15 handymen without websites → Call top 5 by review count → Pitch free spec sites.

### Scenario 2: Multi-City Campaign

```bash
no-website-finder --location "Richmond, VA" --industry "landscaping"
no-website-finder --location "Norfolk, VA" --industry "landscaping"
no-website-finder --location "Charlottesville, VA" --industry "landscaping"
```

**Use:** Map out landscaping prospects across Virginia for a territory plan.

### Scenario 3: Market Verification

```bash
no-website-finder --location "Austin, TX" --industry "pressure washing"
```

**Use:** Test a new market before hiring a local partner or expanding the agency.

## Limitations

- **Geographic Focus:** Best for US-based searches (Google Places coverage)
- **Industry Keywords:** More specific keywords (e.g., "plumber") work better than generic ones (e.g., "services")
- **Review Accuracy:** Google reviews may be outdated; always verify
- **API Costs:** Each search uses API quota; monitor your Google Cloud billing

## Support & Feedback

For issues or improvements:
- **Bug Reports:** GitHub Issues (Roo Code repository)
- **Feature Requests:** Contact Tripp Digital
- **Community:** Join the Roo Code Discord for skill discussions

## See Also

- [Tripp Digital Repository](https://github.com/Brandon1974/trippdigital)
- [Google Places API Documentation](https://developers.google.com/maps/documentation/places)
- [Web Agency Workflow Guide](../trippdigital-web-agency.md)

---

**Last Updated:** 2026-07-14  
**Version:** 1.0  
**Status:** Production
