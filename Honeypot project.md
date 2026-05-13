# Final Locked System Architecture

```
[Kali VM / Internet]
        |
        ↓ HTTP Requests
[Flask Honeypot App]  ←——— deployable locally or to cloud
        |
        ↓ Writes to
[SQLite Database]
   ├── honeypot_logs table
   ├── predictions table
   ├── model_metrics table
   └── retraining_events table
        |
        ↓ Read by
[Feature Extractor]  →  [Unified Feature Vector]
                                |
                    ┌———————————┴———————————┐
                    ↓                       ↓
            [Training Pipeline]    [Inference Engine]
            CICIDS2017 +           Loads current model
            UNSW-NB15 +            Classifies new logs
            Honeypot logs          Writes to predictions
                    |
                    ↓
            [Stacking Ensemble]
            RF + XGBoost + LR meta-learner
                    |
                    ↓
            [Retraining Pipeline]
            Triggered at N=200 new samples
            Validates before replacing model
            Logs version + metrics to DB
                    |
                    ↓
[Flask API]  →  [Plotly Dash Dashboard]
            /api/logs          Live attack feed
            /api/predictions   IDS decisions
            /api/metrics       Performance charts
            /api/retraining    Retraining history
```

---

## Revised 3-Month Sprint Plan (Solo, Starting Now)

### Month 1 — Foundation (Weeks 1–4)

**Week 1 — Honeypot + Environment**

- Set up VirtualBox with Ubuntu (target) and Kali (attacker) VMs on host-only network
- Build the Flask honeypot with 4 vulnerable endpoints
- Verify SQLite logging is working end-to-end
- Run first Nikto scan and confirm logs are captured correctly

**Week 2 — Attack Simulation + Data Collection**

- Run SQLMap, Nikto, OWASP ZAP in structured sessions from Kali
- Simulate benign traffic using Python `requests` scripts
- Simultaneously deploy honeypot to Oracle Cloud free tier — let it run passively collecting real traffic in background for 2 weeks while you work on other things

**Week 3 — Dataset Download + Feature Schema Design**

- Download CICIDS2017 Web Attacks subset and UNSW-NB15 Exploits/Fuzzers subsets
- Define the unified 25-feature schema that works across all three sources
- Write the feature extraction script that maps honeypot logs → feature vectors

**Week 4 — Dataset Harmonization + Training CSV**

- Harmonize CICIDS2017 and UNSW-NB15 to the unified schema
- Merge all three sources into one clean labeled CSV
- Apply SMOTE for class imbalance
- Pull down cloud honeypot logs and incorporate them

---

### Month 2 — ML + Pipeline (Weeks 5–8)

**Week 5 — Baseline Models**

- Train Logistic Regression and Random Forest on the training CSV
- Run 5-fold stratified cross-validation
- Record baseline metrics — this becomes your static IDS benchmark

**Week 6 — Stacking Ensemble**

- Build RF + XGBoost stacking ensemble with Logistic Regression meta-learner
- Validate improvement over baseline
- Save initial model with joblib, versioned with timestamp

**Week 7 — Retraining Pipeline**

- Build threshold-triggered retraining pipeline (N=200 new honeypot rows)
- Run in background thread using APScheduler
- Validate-before-deploy logic — new model only replaces old if F1 holds or improves

**Week 8 — Flask API**

- Build four Flask API endpoints that serve data from SQLite to the dashboard
- Test all endpoints return correct JSON with Postman or curl

---

### Month 3 — Dashboard + Evaluation + Demo (Weeks 9–12)

**Week 9 — Plotly Dash Dashboard**

- Build four dashboard panels wired to Flask API
- Set up `dcc.Interval` auto-refresh every 10 seconds
- Polish layout and charts

**Week 10 — Evaluation Experiment**

- Phase 1: train on SQLi + Nikto data, freeze static IDS
- Phase 2: introduce XSS attacks, measure both models across 3 retraining cycles
- Run 5 times with different seeds, record mean ± std

**Week 11 — Buffer + Integration Testing**

- Full end-to-end system run: attack simulation → honeypot → IDS → dashboard
- Fix any pipeline breaks, edge cases, or dashboard refresh issues
- Prepare demo script

**Week 12 — Report + Demo Preparation**

- Write results and evaluation chapters (data already collected)
- Record backup demo video in case of live demo technical failures
- Final submission

---

## What You Build This Week (Week 1)

Three concrete tasks, in order:

1. Install VirtualBox, create Ubuntu VM and Kali VM, configure host-only network adapter on both — verify they can ping each other
2. Build the Flask honeypot (I'll generate the full code for this right now if you want)
3. Confirm SQLite is logging every request with the right fieldshttps://www.youtube.com/redirect?event=video_description&redir_token=QUFFLUhqblhSTnVUY1FIUHlPSVVScHh2Rm1uN00zaWIwQXxBQ3Jtc0tuZVNaMnN1b2pPcUZUOVV4WkJZRWpEN0VGNUh4ZXBWUTZrWVpkVUM4TUFodWJ0TkFnZjFhTkxZeDFBQUUtM1l2ZnlFYzRFbDBJZjlvUHNpZy03Snp1YUNiMDNSZ2h1T2FqWE96bkZaZ0pETWRuNk1JQQ&q=https%3A%2F%2Fgithub.com%2Fvercel-labs%2Fopensrc&v=KYOg81dfac8

Say **"build the honeypot"** and I'll generate the complete Flask honeypot code with all four vulnerable endpoints, SQLite logging, and a schema designed to feed directly into your feature extraction pipeline.

