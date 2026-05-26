# Poker Platform Analytics: Commercial Behavioral Insights from Gameplay Logs

This project analyzes PHH poker hand-history logs as a commercial analytics case study. The goal is not poker strategy or coaching. The goal is to show how messy gameplay event data can be transformed into business-readable metrics around participant behavior, street-level engagement, contest lifecycle depth, interaction intensity, resolution visibility, and outcome concentration.

The project is framed for gaming, sportsbook, fantasy, marketplace, and product analytics roles where analysts need to work with imperfect event logs and translate them into operational insight.

## Project Highlights

- Parsed and audited 10,088 single-hand PHH files for the main analysis.
- Identified 21,782 additional `.phhs` HandHQ multi-hand container files and documented why they are excluded from the main single-hand analysis.
- Built action-based KPIs for engagement depth, street survival, high-commitment action rate, resolution path, lifecycle progression, contested-chip intensity, and normalized outcome intensity.
- Separated Pluribus, WSOP, and reference-example hands instead of folding Pluribus into a generic "Other" source bucket.
- Added variant and game-structure checks for fields such as `blinds_or_straddles`, `antes`, `bring_in`, `small_bet`, and `big_bet`.
- Validated that private-card and terminal show/muck visibility are incomplete, preventing unsupported hand-strength or strategy claims.
- Demonstrated participant behavior profiling using anonymized event-log features.
- Reframed poker hand histories as a commercial/product analytics workflow rather than gambling hobby content.

## Key Findings

- Most hands follow a repeatable interaction pattern, with a median of roughly 16 actions per hand.
- About 46.8% of hands resolve before any board reveal, while about 27.5% reach the final board reveal.
- About 83.0% of hands resolve before show/muck-like activity; only about 17.0% reach a show/muck-like terminal state.
- High-action hands are much more likely to reach showdown-like resolution, making action depth useful as a product-experience segmentation metric.
- Street-level parsing creates a product-style engagement funnel that distinguishes public card reach from later-street decision activity.
- Winner-card visibility is extremely limited, so the analysis avoids strategy conclusions and focuses on observable behavior.
- Outcome intensity is concentrated: in the Pluribus subset, the top 10% of hands account for roughly 55.9% of normalized outcome intensity.

## Repository Structure

```text
.
|-- README.md
|-- requirements.txt
|-- .gitignore
|-- notebooks/
|   `-- PokerProject2_behavioral_analytics.ipynb
|-- reports/
|   |-- PokerProject2_Case_Study.pdf
|   |-- PokerProject2_Case_Study.html
|   `-- figures/
|       `-- *.png
`-- data/
    |-- README.md
    `-- .gitkeep
```

## Data Note

The raw PHH/PHHS data is not included in this GitHub-ready folder because the local dataset is over 16 GB, mostly from HandHQ `.phhs` multi-hand containers. The notebook is designed to run when the data is placed under a local `data/` folder.

Data source used for this project:

- Kim, Juho. **A Dataset of Poker Hand Histories**. Zenodo. Version **v2**. DOI: `10.5281/zenodo.13997158`
- Source URL: https://zenodo.org/records/13997158

This project is explicitly pinned to the Zenodo **v2** record above, not the newer v3 version. The PHH reference GitHub repository currently documents the newer v3 release, so this project uses that repository for format and schema context only. The logic around PHH loading, variants, `.phhs` containers, and structured fields still applies, but the file inventory and reported results here are from v2.

Expected local layout:

```text
data/
|-- pluribus/
|-- wsop/
|-- handhq/
|-- alice-carol-wikipedia.phh
|-- antonius-blom-2009.phh
|-- arieh-yockey-2019.phh
|-- dwan-ivey-2009.phh
`-- phua-xuan-2019.phh
```

The main analysis uses single-hand `.phh` files as the unit of observation. The `.phhs` files are audited as multi-hand containers readable with `HandHistory.load_all()`, but are not mixed into the main hand-level analysis. A separate HandHQ container analysis would be the right next step if the goal were session-depth or stake-level behavior.

## How To Run

1. Clone or download this repository.
2. Install dependencies:

```bash
pip install -r requirements.txt
```

3. Place the PHH data under `data/` using the layout above.
4. Open `notebooks/PokerProject2_behavioral_analytics.ipynb`.
5. Run the notebook from top to bottom.

If the `data/` folder is not found in the repository, the notebook falls back to the original local Downloads path used during development.

## Why This Matters Commercially

This project demonstrates how gameplay logs can be converted into metrics that product, commercial, or operations teams can use:

- engagement depth
- street-level survival and disengagement
- high-commitment interaction intensity
- lifecycle progression
- resolution clarity
- contested-chip concentration and outcome volatility
- participant behavior profiles
- data-quality and observability limits

The analysis is intentionally careful about incomplete visibility. Rather than pretending the dataset supports perfect strategy evaluation, it treats missingness and obfuscation as part of the analytical problem.

## Limitations

- Public PHH data is partially obfuscated.
- Terminal show/muck activity does not guarantee full card visibility.
- The main analysis excludes `.phhs` multi-hand containers to keep the unit of observation consistent.
- The public PHH GitHub repository is currently oriented around v3; this project uses v2 and treats the repository as schema context rather than as the exact analyzed file release.
- WSOP mixed-game hands can use bring-in or fixed-limit structure fields rather than no-limit blind fields, so the notebook audits those fields instead of assuming every hand has the same betting structure.
- Participant profiles are descriptive, not causal.
- Stronger commercial conclusions would require account-level features such as tenure, session frequency, contest type, acquisition channel, promotion exposure, and retention outcomes.
