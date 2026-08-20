# GPT-2 Joke Arena v7

## 160 stories

Each of 10 prompts has:

### 8 Standard
- 2 Small
- 2 Medium
- 2 Large
- 2 XL

Standard is one normal autocomplete call with natural EOS and a 300-word display cap.

### 8 Telephone
- 2 Small
- 2 Medium
- 2 Large
- 2 XL

Telephone uses the **original funny 800-word bakeoff generation algorithm**:
- rolling accumulated text
- rolling recent-context window when needed
- EOS suppressed
- same 256-token chunk behavior
- same internal 800-word scheduling target
- stop once at least 300 words exist
- display the first 300 words

The internal target deliberately remains 800 rather than 300 so the early chunk schedule matches the original runs.

## Seed/settings

- seed 1337
- temperature 0.95
- top-p 0.95
- top-k 50

Each model has a separately seeded Standard stream and Telephone stream.

## Original validation

The exact uploaded original GPT-2 Small and GPT-2 Large 800-word samples are embedded in the Colab notebook.

The notebook asserts that:
- `p01_small_telephone_1`
- `p01_large_telephone_1`

match the **exact first 300 words** of those original uploaded generations.

## Publish

1. Run `generate_joke_bank_colab.ipynb` in GPU Colab.
2. Download `joke_bank.json`.
3. Replace the starter file in GitHub.
4. Commit to main.
5. GitHub Pages redeploys.

The site still reveals model size + Standard/Telephone only after the vote.


## v7 empty-chunk robustness

The first attempt for every Telephone chunk is still exactly the original bakeoff
`model.generate()` call. If that attempt produces a chunk made only of special
tokens and therefore decodes to zero visible text, v7 retries that same chunk with
EOS stopping explicitly disabled.

This fallback does not run on ordinary chunks. Therefore the original first-prompt
Small/Large compatibility check remains meaningful and the Colab notebook still
asserts exact first-300-word identity against the uploaded originals.
