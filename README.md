# Video AI Analyzer API — Hook Score, Shot List & Summary — Python, Node.js & cURL examples

Send **video files you own** (direct links, Google Drive, Dropbox, OneDrive, S3) and get back one structured JSON row per video: the **opening hook with a 1-10 score**, the **structure in labelled sections**, a **shot-by-shot list with keyframe images and on-screen text**, the **call to action**, brands and products, **measured pacing** (cuts, cuts per minute, average shot length — measured with FFmpeg, not guessed), a **summary or chapters**, the **answer to any question** you ask and the **timestamped transcript**. Built for ad creative reviews, UGC checks, course libraries and AI agents. From $0.025 per video; failed videos are free.

Hosted on Apify: **[Video AI Analyzer API — Hook Score, Shot List & Summary](https://apify.com/tidydata/video-ai-analyzer?fpr=wtg6qt)**. These examples show how to call it from your code; the Actor runs in the cloud, no API key for the source site, no proxies to manage.

## Python

```bash
pip install apify-client
export APIFY_TOKEN=...   # free account at apify.com → Settings → API & Integrations
```

```python
import os
from apify_client import ApifyClient

client = ApifyClient(os.environ["APIFY_TOKEN"])
run = client.actor("tidydata/video-ai-analyzer").call(run_input={
    "videoUrls": [
        "https://example.com/ads/summer-ad-v2.mp4"
    ],
    "analysis": "creative",
    "question": "Write 3 alternative opening hooks",
    "outputLanguage": "English"
})
for item in client.dataset(run["defaultDatasetId"]).iterate_items():
    print({k: item.get(k) for k in ['fileName', 'hook', 'callToAction', 'pacing', 'summary', 'answer']})
```

## Node.js

```javascript
import { ApifyClient } from 'apify-client';

const client = new ApifyClient({ token: process.env.APIFY_TOKEN });
const run = await client.actor('tidydata/video-ai-analyzer').call({"videoUrls": ["https://example.com/ads/summer-ad-v2.mp4"], "analysis": "summary"});
const { items } = await client.dataset(run.defaultDatasetId).listItems();
console.log(items.length, items[0]);
```

## cURL (one call, results as JSON)

```bash
curl -s -X POST "https://api.apify.com/v2/acts/tidydata~video-ai-analyzer/run-sync-get-dataset-items?token=$APIFY_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"videoUrls": ["https://example.com/ads/summer-ad-v2.mp4"], "analysis": "summary"}'
```

## More TidyData Actors

[YouTube Transcript](https://apify.com/tidydata/youtube-transcript-scraper?fpr=wtg6qt) · [YouTube Comments](https://apify.com/tidydata/youtube-comments-scraper?fpr=wtg6qt) · [YouTube Scraper](https://apify.com/tidydata/youtube-channel-scraper?fpr=wtg6qt) · [Website Contacts](https://apify.com/tidydata/website-contact-extractor?fpr=wtg6qt) · [Google News](https://apify.com/tidydata/google-news-scraper?fpr=wtg6qt) · [App Reviews](https://apify.com/tidydata/app-reviews-scraper?fpr=wtg6qt) · [Merge & Dedupe](https://apify.com/tidydata/merge-dedupe-datasets?fpr=wtg6qt) · [all of them](https://github.com/tidydata-dev)

Examples are MIT-licensed.

---
<sub>Links to apify.com include our affiliate ID: if you start a paid Apify plan through them, Apify pays TidyData a commission at no extra cost to you.</sub>
