# Tesla SOTP Dashboard — Morgan Stanley Valuation Model

Interactive Sum-of-the-Parts valuation of Tesla (TSLA), reproducing the framework used by **Andrew Percoco** (Morgan Stanley, took over Tesla coverage from Adam Jonas in Dec 2025) to arrive at a **$425/share** price target.

## What it does

Five business segments are modeled independently with their own DCF or multiple-based valuation, then summed to a per-share price target:

| Segment | Per Share | Approach |
|---|---:|---|
| Network Services (FSD + Supercharging) | $145 | Gordon-growth DCF |
| Robotaxi (Tesla Mobility) | $125 | Gordon-growth DCF |
| Optimus (Humanoids) | $60 | DCF × (1 − 50% probability haircut) |
| Core Auto | $55 | Blended P/E + terminal-growth |
| Energy Storage | $40 | EV/EBITDA × PV factor |
| **Total** | **$425** | |

Every parameter is a slider. Two global sliders (WACC, terminal growth `g`) apply to all DCFs. Each segment tab shows:

- The current per-share and total ($B) value
- Sliders for the segment's drivers, each with a badge comparing to today's reality
- The full derivation flow (formulas with live numbers plugged in)
- Major competitors with their actual market values for comparison

## Math

For long-duration segments (Network, Robotaxi, Optimus):

```
PV = Steady-state FCF × [1 / (WACC − g)] × [1 / (1 + WACC)^15]
```

Optimus additionally applies a probability haircut: `PV × (1 − haircut)`.

Auto uses a 5-year discount on a blended (exit P/E, Gordon terminal) average. Energy uses an EV/EBITDA multiple discounted back 5 years.

## Run locally

```bash
# Any static server works. Easiest options:
python3 -m http.server 8000
# then open http://localhost:8000

# or with Node:
npx serve .
```

Or just open `index.html` directly in a browser — no build step, no dependencies beyond the Chart.js CDN.

## Deploy on GitHub Pages

1. Push this repo to GitHub.
2. Repo → **Settings** → **Pages**.
3. **Source**: Deploy from a branch.
4. **Branch**: `main` (or `master`), folder `/ (root)`.
5. Save. The dashboard is live at `https://<your-username>.github.io/<repo-name>/` in ~1 minute.

## References

- [Parameter.io — Segment breakdown](https://parameter.io/tesla-tsla-stock-new-morgan-stanley-analyst-cuts-rating-on-rich-valuation/)
- [Investing.com — Percoco $425 PT note](https://www.investing.com/news/stock-market-news/morgan-stanley-moves-tesla-to-equal-weight-as-it-waits-for-a-better-entry-4395125)

## Disclaimer

This is a reconstruction of a public valuation framework for educational purposes. Morgan Stanley's full proprietary model is not public; defaults are calibrated to reproduce their published per-segment values. Not investment advice.
