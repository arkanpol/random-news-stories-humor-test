# GPT-2 Joke Arena v3

The bank now contains **160 real GPT-2 stories**.

## Standard: 80
Every one of 10 prompts has:
- 2 GPT-2 Small
- 2 GPT-2 Medium
- 2 GPT-2 Large
- 2 GPT-2 XL

Settings:
- seed 1337
- temperature 0.95
- top-p 0.95
- top-k 50
- 300-word cap
- natural EOS allowed

## Telephone: 80
Every one of the same 10 prompts also has:
- 2 GPT-2 Small
- 2 GPT-2 Medium
- 2 GPT-2 Large
- 2 GPT-2 XL

Each telephone story is **300 words = 4 x 75-word hops**.

- hop 1 sees original prompt
- hop 2 sees only hop 1
- hop 3 sees only hop 2
- hop 4 sees only hop 3

The displayed answer concatenates all four hops.

After voting, the site reveals:
- GPT-2 model size
- Standard or Telephone

Then click Next matchup.

## Publish
1. Run `generate_joke_bank_colab.ipynb` in Google Colab with GPU.
2. Download `joke_bank.json`.
3. Replace the starter `joke_bank.json` in the GitHub repo.
4. Commit to `main`.
5. GitHub Pages redeploys.

Elo is otherwise unchanged: starting Elo 1500, K=32, same-prompt comparisons, unseen pairs prioritized, then similar-rated pairs, randomized A/B placement, localStorage persistence, CSV/JSON export.
