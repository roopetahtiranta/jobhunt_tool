# Live web access: nimble-web-expert with fallback

1. Detect: check whether the `nimble-web-expert` skill is available/authenticated
   (e.g. it responds, or `nimble --version` succeeds).
2. If available: use it to search job boards (LinkedIn, Indeed, company pages) and
   to fetch individual posting pages. It is built to fetch these sites.
3. If unavailable: fall back to plain web search to discover postings, and ask the
   user to paste posting URLs or name boards to target.
4. Never hand-roll scraping of protected boards, and never block the pipeline —
   if discovery is thin, ask the user for URLs and proceed.
