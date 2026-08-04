# Running Analytics Dashboard

A single-file, browser-based dashboard for exploring running data — built to track training load and pacing consistency. I designed this specifically for my marathon training. But you can use it for any exported run-data from strava.

**[Live demo](#)** — enable GitHub Pages on this repo, then link it here (see setup notes below).

---

## Why I built this

Strava's built-in charts show pace and heart rate, but not the things that actually matter for training decisions: is my pacing controlled, is my heart rate drifting up within a run (a fatigue signal), and am I getting more speed per heartbeat over time. I built this to answer those questions from my own training data, using ChatGPT as a coding partner — the same "AI co-developer, human owns the decisions" approach I use professionally.

## What it does

- Loads a CSV export of running records directly in the browser. No install, no server, no account — the data never leaves your machine.
- **Individual run view**: pace/speed and heart rate over time or distance, with split sections (e.g. marathon-pace intervals inside a long run) highlighted automatically.
- **Aggregated view**: progression across all runs of a given type (easy, tempo, long, marathon pace) as box, violin, or average-point plots, so you can see whether a training block is actually working.
- Computed training metrics per run: **aerobic efficiency** (speed produced per heartbeat), **HR drift** (first half vs. second half of the run — a fatigue/pacing signal), and **pace variability** (how controlled the pacing was).
- Per-run distance bars with stacked splits, cadence, and average speed markers across an entire training block.
- Adjustable axis ranges on every chart, and a toggle between pace and speed display.

## Try it

1. Open `index.html` in any browser — or use the live demo link above once GitHub Pages is enabled.
2. Click "Load your master_records.csv file" and select `sample_data.csv` from this repo (synthetic data, two sample runs) to see it working immediately.
3. To use your own data, export your runs to a CSV with these columns:

   | Column | Required | Notes |
   |---|---|---|
   | `run_id` | yes | unique per run |
   | `main_run_type` | yes | e.g. `easy`, `long`, `tempo`, `mp` |
   | `segment_type` | no | set only on split sections, e.g. `long_MP` |
   | `timestamp` | yes | ISO datetime |
   | `distance_km` | yes | cumulative distance |
   | `pace_min_km` or `speed_m_s` | yes | one of the two |
   | `elapsed_sec` | yes | cumulative elapsed time |
   | `heart_rate_bpm` | no | enables HR charts and metrics |
   | `power_w`, `altitude_m` | no | shown in hover tooltips if present |
   | `cadence_label`, `cadence_spm` | no | cadence tracking |
   | `source_file` | no | cosmetic, shown in run header |

## Tech stack

Vanilla JavaScript, [Plotly.js](https://plotly.com/javascript/) for charts, [PapaParse](https://www.papaparse.com/) for CSV parsing. No backend, no build step, no framework — one HTML file.

## Status

Personal training tool, actively used during marathon prep. Shared here as an example of fast prototyping and turning raw sensor data into decision-useful metrics for a non-technical audience — the same instinct behind [Vis4Cat](https://github.com/khatamirad/vis4cat), applied to my own training instead of catalysis data.

