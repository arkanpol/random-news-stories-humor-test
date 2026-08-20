# GPT-2 Joke Arena

A static GitHub Pages experiment with **10 prompts × 8 GPT-2 answers** and local Elo-style matchmaking.

## Bank design

Each prompt has exactly 8 continuations:

- 2 × GPT-2 Small
- 2 × GPT-2 Medium
- 2 × GPT-2 Large
- 2 × GPT-2 XL

The model identity is **not shown in the voting interface**. It is retained in the data for analysis.

## Setup

1. Open `generate_joke_bank_colab.ipynb` in Google Colab.
2. Use a GPU runtime.
3. Run all cells.
4. Download the generated `joke_bank.json`.
5. Replace the starter `joke_bank.json` in this folder with the generated one.
6. Commit/push the folder contents to a GitHub repository.
7. In GitHub: **Settings → Pages → Deploy from a branch → main / root**.

You can also test before publishing: open `index.html` through a simple local web server, or use the site's **Load joke_bank.json** button.

## Elo matchmaking

- Initial rating: 1500
- K-factor: 32
- Comparisons are only between answers to the **same prompt**
- Scheduler prioritizes:
  1. prompts with fewer battles,
  2. unseen/less-seen answer pairs,
  3. pairs with similar Elo
- Choices: A wins / tie / B wins
- Left/right position is randomized independently of model identity

This gives broad matchup coverage early and increasingly close Elo matches later.

## Persistence

GitHub Pages is static, so ratings and votes are saved in the participant's browser via `localStorage`.

The site can export:

- `joke_arena_votes.csv`
- `joke_arena_state.json`

That is suitable for collecting files from multiple participants and merging them later. A shared live/global Elo would require a backend/database rather than plain GitHub Pages.

## Files

- `index.html` — GitHub Pages experiment
- `joke_bank.json` — starter schema; replace with the real generated bank
- `generate_joke_bank_colab.ipynb` — real GPT-2 bank generator
- `.nojekyll` — tells GitHub Pages to serve files directly
