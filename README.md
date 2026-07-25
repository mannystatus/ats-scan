# ATS Scan

**Live site:** https://mannystatus.github.io/ats-scan/

A resume ↔ job posting compatibility checker. Everything runs client-side in the browser:

- **Local Mode** (default, no AI account needed) — formatting/parseability checks (length, contact info detection, standard section headers, bullet points, layout artifacts, special characters) plus a keyword-overlap score: the most frequent meaningful terms from the pasted job posting, checked against which ones literally appear in the resume. If the posting has a "Nice to have"/"Preferred" section, terms above it are weighted double toward the score — modeled on Greenhouse's own recruiter keyword-search feature, which lets recruiters mark search terms "Required" (all must match) vs "Preferred" (any one matches). See [support.greenhouse.io — Search resumes for keywords](https://support.greenhouse.io/hc/en-us/articles/115004600186-Search-resumes-for-keywords). This is a plain word-match heuristic, not an AI judgment of fit and not a simulation of any specific ATS — no data ever leaves the browser, no API key, no backend, no cost. The in-app "How real ATS scoring actually works" card explains, with sources, why most real ATS platforms (Greenhouse included) don't auto-score or auto-reject resumes the way this kind of tool's score might imply.
- **"Use your own AI" (optional)** — for a deeper AI-generated score (relevance, keyword gaps, a tailored summary, bullet rewrites), the tool builds a prompt the user copies into any AI they already have — ChatGPT, Claude, Gemini, a local model, anything with a chat box — then pastes the reply back in. We never call any AI ourselves: no API key, no CORS dependency, no per-provider integration to maintain, and the data only goes to whichever AI service the user chooses to paste it into.

## Running it

It's a single static HTML file — there's nothing to build or install.

- **Locally:** open `index.html` directly in a browser, or serve the folder with any static file server (e.g. `npx serve .`).
- **Publicly:** deploy `index.html` as-is to any static host — GitHub Pages, Netlify, Vercel, Cloudflare Pages, S3, etc. No environment variables, no server process, no ongoing cost regardless of traffic.

## Notes

- The "Fetch" button next to the job posting URL box attempts a direct browser fetch of that page. It only succeeds on sites that allow cross-origin requests (most job boards don't) — when it fails, paste the posting text in manually.
- Because there's no AI involved, the keyword list is a straightforward frequency count with common stopwords filtered out, not a semantic understanding of the role. Treat the score as a rough signal, not a verdict.
