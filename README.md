# Blue Team Colab Labs (Network + Endpoint)

Two beginner-friendly Blue Team investigation labs you can run in **Google Colab**:
- **Network-centric lab**: DNS / TLS / HTTP / connection patterns (SIEM-style pivots)
- **Endpoint-centric lab**: process chains / artifacts / persistence / outbound connections (EDR-style pivots)

These labs teach a repeatable investigation workflow:
**entity → pivots → timeline → decision → documentation**.

---

## What’s in this repo

- files/
- network_lab.ipynb
- endpoint_lab.ipynb
- network_events.csv
- endpoint_events.csv


### Lab outputs (what participants produce)
Each lab ends with:
- 8 investigation questions (host, indicators, timeline, containment, detection improvement)
- a 6–10 sentence incident summary

---

## Quick start (recommended): Run in Google Colab

### Option A: Open via direct Colab links
- **Network lab:**  
  https://colab.research.google.com/github/dadirad/blue-team-lab/blob/main/files/network_lab.ipynb

- **Endpoint lab:**  
  https://colab.research.google.com/github/dadirad/blue-team-lab/blob/main/files/endpoint_lab.ipynb

### Option B: Open via Colab’s GitHub browser
1. Go to https://colab.research.google.com
2. File → Open notebook
3. GitHub tab → search for: `dadirad/blue-team-lab`
4. Open the notebook from the `files/` folder

### What to do once the notebook opens
1. **File → Save a copy in Drive** (recommended so you can edit variables)
2. **Runtime → Run all**
3. Fill in the one “timeline” variable:
   - Network lab: set `HOST_IP = "..."` using the `src_ip` from the host summary output
   - Endpoint lab: set `HOST = "..."` using the `host` value from the suspicious chain output
4. Re-run the timeline cell
5. Complete the questions + incident summary at the end

---

## What these labs teach (beginner-friendly)

### Network lab (SIEM-style thinking)
You will learn how to:
- identify a suspicious internal host (`src_ip`)
- spot suspicious indicators:
  - rare DNS queries (`query`)
  - suspicious HTTP paths (`uri`) like downloads or payloads
  - repeated connection patterns (`CONN`) as a beaconing hint
- build a host timeline and optionally pivot by a domain

### Endpoint lab (EDR-style thinking)
You will learn how to:
- identify suspicious parent → child process chains (example: email client → PowerShell)
- spot risky command line patterns (encoded/hidden/no-profile flags)
- pivot to a single host timeline
- identify dropped artifacts (file writes) and persistence mechanisms
- summarize repeated outbound destinations as possible command and control

---

## Running with a class or group (facilitation tips)

**Recommended structure (pairs):**
- Driver: runs notebook cells
- Navigator: interprets outputs and chooses pivots
- Scribe: writes answers and incident summary

**Suggested pacing (60 minutes):**
- 0–10 min: background + setup
- 10–40 min: run lab + fill in timeline variable
- 40–55 min: write-up (8 questions + incident summary)
- 55–60 min: 2–3 share-outs

---

## Troubleshooting

### “EmptyDataError: No columns to parse”
This means the CSV loaded from the raw URL is empty or not valid CSV.
- Open the raw file URL in a browser and confirm it shows CSV text.
- Ensure the CSV has a header row.
- If editing CSV manually in GitHub, **fully-quoted CSV** is the safest format.

### Notebook runs but sections show no rows
That can be normal if the dataset is small or doesn’t contain that signal.
- Confirm earlier cells ran and `df` has rows.
- Check `df.columns`.
- Continue to the next section and use the evidence you do have.

### Timeline cell says to set HOST/HOST_IP
You must fill in the variable and rerun the cell:
- Endpoint lab: `HOST = "WS-023"` (example)
- Network lab: `HOST_IP = "10.0.5.23"` (example)

### Colab won’t let me edit
Use: **File → Save a copy in Drive** and edit your copy.

---

## Editing or extending the labs

### Swap in your own dataset
Replace the CSV files in `files/`:
- `files/network_events.csv`
- `files/endpoint_events.csv`

Keep the headers consistent with the notebooks, or update the notebook column references.

### Add more realism
Common extensions:
- add more hosts and background noise
- add additional attack stages (lateral movement, privilege escalation)
- add “prevalence” checks (how many hosts hit the same domain)
- add a detection-engineering section (write a simple rule from the evidence)

---

## License / Use
Use freely for training and education. If you redistribute modified versions, include a note describing your changes (dataset, questions, or logic).
