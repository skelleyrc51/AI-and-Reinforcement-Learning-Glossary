# AI & RL Lexicon

A searchable glossary of **124 artificial intelligence and reinforcement learning terms**, written for people who need to hold a technical conversation with ML researchers without being one. It covers transformer basics through RL post-training, environments and graders, reward hacking, evaluation and safety, and the code-security vocabulary that shows up when RL targets vulnerability work.

- **Browse it:** open [`index.html`](index.html) (or the GitHub Pages site once Pages is enabled) for search, topic filters and cross-linked "See also" terms.
- **Read it on GitHub:** [`GLOSSARY.md`](GLOSSARY.md) has every term in plain Markdown.
- **Reuse it:** all content lives in [`data/terms.json`](data/terms.json).

## Topics

| Topic | What it covers |
|---|---|
| AI foundations | Transformers, tokens, attention, pretraining, scaling laws |
| RL core concepts | MDPs, policies, value functions, advantage, credit assignment |
| RL algorithms | Policy gradient, PPO, GRPO, DPO, MCTS, offline RL |
| LLM post-training | SFT, RLHF, RLVR, reward models, reasoning models |
| Environments & rewards | Tasks, graders, verifiers, reward hacking, pass@k, sandboxes |
| Evaluation & safety | Benchmarks, red teaming, frontier safety frameworks, agents |
| Security for AI training | Fuzzing, PoCs, exploits, sanitizers, ground truth |

Each entry has a definition and may also include an alias, the notation used in papers (for example `π_θ(a | s)`), an "In the room" note on how the idea comes up in practice, and related terms.

## Repository layout

```
.
├── index.html              # Searchable web version (loads data/*.json)
├── GLOSSARY.md             # Generated Markdown version. Do not edit by hand.
├── data/
│   ├── categories.json     # Topic list and order
│   └── terms.json          # All glossary entries (source of truth)
├── scripts/
│   └── build.py            # Validates data and regenerates GLOSSARY.md
└── .github/workflows/
    └── validate.yml        # CI: checks data and that GLOSSARY.md is current
```

## Adding or editing a term

1. Edit `data/terms.json`. Each entry looks like this:

   ```json
   {
     "term": "Advantage",
     "category": "core",
     "notation": "A(s,a) = Q(s,a) − V(s)",
     "definition": "How much better an action was than the policy's average in that state.",
     "note": "Optional: how this shows up in real conversations.",
     "see_also": ["GRPO", "PPO", "Baseline"]
   }
   ```

   `term`, `category` and `definition` are required. `aka`, `notation`, `note` and `see_also` are optional. Every `see_also` value must exactly match another entry's `term`.

2. Regenerate the Markdown and check your work:

   ```bash
   python3 scripts/build.py
   ```

3. Commit both `data/terms.json` and `GLOSSARY.md`. CI fails if they are out of sync.

## Viewing locally

`index.html` loads its data with `fetch`, so serve the folder instead of double-clicking the file:

```bash
python3 -m http.server 8000
# then open http://localhost:8000
```

## Publishing with GitHub Pages

In the repo, go to **Settings → Pages**, set **Source** to *Deploy from a branch*, choose `main` and `/ (root)`, and save. The site appears at `https://<your-username>.github.io/ai-rl-lexicon/`.

## License

Content is licensed under [Creative Commons Attribution 4.0 International (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/). See [LICENSE](LICENSE).
