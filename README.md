# RTT vs. Speed-of-Light
### Networks Assignment — Measurement & Geography

## Setup
```bash
pip install requests matplotlib numpy
python rtt_speedoflight.py
```

## Submission
1. Fork this repo to your own GitHub account
2. Complete the tasks in `rtt_speedoflight.py`
3. Run the script and take a screenshot of your full terminal output
4. Commit everything to your fork:
   - `rtt_speedoflight.py`
   - `figures/fig1_rtt_comparison.png`
   - `figures/fig2_distance_scatter.png`
   - `terminal_screenshot.png`
   - `analysis.md`
5. Submit your GitHub repo URL via the course portal

## Repo Structure
```
├── rtt_speedoflight.py       # starter code — fill in the TODOs
├── assignment.md             # full assignment spec and grading rubric
├── figures/                  # auto-created when you run the script
│   ├── fig1_rtt_comparison.png
│   └── fig2_distance_scatter.png
├── terminal_screenshot.png   # screenshot of your terminal output (required)
└── analysis.md               # your written answers
```

## Notes
- No `sudo` needed — the script uses HTTP requests, not raw sockets
- Your location is auto-detected from your IP when you run the script
- The terminal screenshot must show your detected location on the first line, e.g. `Your location: Boston (42.3601, -71.0589)`
