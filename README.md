# Spotify Freemium Paywall — A/B Test Analysis

I built this project to explore a question that Spotify's product team has almost certainly debated internally: **what actually happens when you restrict free-tier skips?**

The assumption is that frustration = upgrades. But I wanted to test whether that holds across different types of users and the answer turns out to be more nuanced (and more interesting) than a simple yes or no.

---

## What this project does

It simulates a full A/B test where:
- **Control group** gets the current experience — unlimited skips
- **Treatment group** gets capped at 6 skips per hour

I split users into three segments based on how much they listen per day, ran two-proportion z-tests on each one (with Bonferroni correction since we're testing three groups simultaneously), modeled the revenue impact, and wrote up a recommendation based on the data.

The simulation parameters aren't made up they're calibrated to Spotify's actual Q2 2024 numbers: 626M monthly active users, ~39% Premium conversion, $11.99/month US pricing, and a 2.5hr average daily listening time.

---

## The finding that surprised me

Power users — the people listening 4+ hours a day don't upgrade when you limit their skips. **They leave.**

Churn spiked +17 percentage points in that segment, and conversion actually *dropped*. These are Spotify's most engaged free-tier users, and they have options. A hard paywall pushed them out the door rather than toward a subscription.

Regular users (2–4 hrs/day) responded exactly as the hypothesis predicted: statistically significant conversion lift, manageable churn, positive net revenue. The skip restriction works just not universally.

---

## Recommendation

Don't ship this globally. The right move is a segmented rollout:

- **Regular users** → roll it out, the data supports it
- **Casual listeners** → skip the hard paywall, try a free trial offer instead
- **Power users** → don't touch this group at all

A global launch looks profitable in month one. It goes negative by month six once Power User churn compounds.

---

## How to run it

```bash
pip install pandas numpy matplotlib scipy
jupyter notebook A_B_testing.ipynb
```

Run the cells in order. Cell 5 generates a 2×2 results dashboard and saves it as `spotify_ab_test_dashboard.png`.

---

## Stack

Python, pandas, NumPy, SciPy, Matplotlib

---

*Dhrumi Kansara — MS Business Analytics, Arizona State University*  
[LinkedIn](#) · [GitHub](#)
