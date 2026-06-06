# BASELINE — Training & Nutrition Protocol Generator

A single-file web app that asks a person a few questions and returns a personalized training & nutrition protocol.

**Free tier:** your daily **calories** — BMR and maintenance (TDEE) from sex, age, height, weight and lifestyle activity.

**Premium unlocks the rest:**

- **Goal & goal-weight targets** — set a target weight and the app picks the direction, sizes protein to your goal weight, and estimates a weekly rate + timeline
- **Macros** — daily protein / carbs / fat, with macro styles: Standard, **High protein (two variants: lower-carb/moderate-fat or moderate-carb/lower-fat)**, and Low carb. (Carb balance was retuned so it no longer over-weights carbs.)
- **Workout split** — auto-tailored to your equipment and training days, or switch it **off** (“nutrition only”) if you don’t need a plan
- **Cardio & sport** — log activities; their calorie burn is added to your target
- **Hydration & sleep** — water goal and recovery-sleep target with a wake→bedtime calculator
- **AI coach** — ask plan questions; uses a free, keyless AI service (see privacy note below)

**Always free:** dark/light theme and a **custom accent color switcher** (presets + any color you pick), plus an Auto mode that matches the selected sex.

> **Previewing Premium:** subscriptions are processed by the App Store / Google Play in the packaged app. To preview the full app on the web, open it with **`?premium=1`** in the URL.

> **AI privacy note:** the AI coach sends your question + a short plan summary (calorie/macro numbers, no personal identifiers) to a third-party service (Pollinations). The rest of the app runs entirely in your browser.

-----

## How to host it on GitHub (free, ~2 minutes)

1. Create a new GitHub repository (e.g. `baseline`).
1. Upload **`index.html`** to the root of the repo (drag-and-drop in the GitHub web UI works fine).
1. Go to **Settings → Pages**.
1. Under **Build and deployment → Source**, choose **Deploy from a branch**.
1. Pick branch **`main`** and folder **`/ (root)`**, then click **Save**.
1. Wait ~30–60 seconds. Your app is live at:
   `https://<your-username>.github.io/<repo-name>/`

That’s it. To update it, just edit/replace `index.html` and commit — Pages redeploys automatically.

> Want it at a custom domain? Add a `CNAME` file with your domain and point a DNS `CNAME` record at `<your-username>.github.io`.

### Run it locally

Just double-click `index.html` to open it in any browser. (Or `python3 -m http.server` in the folder and visit `http://localhost:8000`.)

-----

## How the numbers are calculated

|Step                        |Method                                                                                                                                        |
|----------------------------|----------------------------------------------------------------------------------------------------------------------------------------------|
|BMR (with lean body mass)   |**Katch-McArdle**: `370 + 21.6 × LBM(kg)`                                                                                                     |
|BMR (without LBM)           |**Mifflin-St Jeor** (sex-specific)                                                                                                            |
|Baseline burn               |`BMR × lifestyle multiplier` (1.2–1.6) — daily life **excluding** workouts                                                                    |
|Exercise burn (added on top)|MET-based estimate per session: `MET × 3.5 × kg ÷ 200 × minutes`, summed across your strength sessions + logged cardio/sport, averaged per day|
|Maintenance (TDEE)          |`baseline + exercise burn`                                                                                                                    |
|Fat-loss target             |TDEE − 20% (with a safe calorie floor)                                                                                                        |
|Muscle-gain target          |TDEE + 10%                                                                                                                                    |
|Protein                     |~2.6 g/kg of lean mass, or 1.8–2.2 g/kg bodyweight by goal                                                                                    |
|Fat                         |~25% of calories (with a hormonal minimum)                                                                                                    |
|Carbs                       |the remaining calories                                                                                                                        |

This **additive model** is why the activity question asks about your *baseline daily life only* — your training and sport are counted separately in the Cardio & Sport section (and from your strength training days), so nothing is double-counted.

The workout engine filters a built-in exercise library by the equipment you select, then assembles a 2–6 day split (full-body / upper-lower / push-pull-legs) with set, rep and rest schemes matched to your goal.

-----

## ⚠️ Disclaimer

This tool provides **general estimates from population-level formulas — not personalized medical or nutritional advice.** Individual needs vary. Anyone who is pregnant, under 18, managing a medical condition, or has a history of disordered eating should consult a doctor or registered dietitian before changing their diet or training. Adjust based on real-world results over 2–4 weeks rather than chasing the numbers exactly.

## License

Do whatever you like with it. Attribution appreciated but not required.