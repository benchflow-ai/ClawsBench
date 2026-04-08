# ClawsBench

**Benchmarking LLM Agents in Realistic Productivity Environments**

[![License: CC BY-NC-SA 4.0](https://img.shields.io/badge/License-CC%20BY--NC--SA%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by-nc-sa/4.0/)
[![Website](https://img.shields.io/badge/Website-ClawsBench-blue)](https://benchflow-ai.github.io/ClawsBench/)
[![Paper](https://img.shields.io/badge/Paper-arXiv-red)](https://arxiv.org/abs/2604.05172)
[![Dataset](https://img.shields.io/badge/Dataset-HuggingFace-yellow)](https://huggingface.co/datasets/benchflow/ClawsBench)

ClawsBench evaluates LLM agents on realistic productivity tasks across **5 high-fidelity mock services** (Gmail, Calendar, Docs, Drive, Slack), measuring both **capability** (task success) and **safety** (harmful action prevention).

## News

- **[2026/4/8]** Project website, GitHub repo, and [Hugging Face dataset](https://huggingface.co/datasets/benchflow/ClawsBench) launched. 7,834 agent traces (7,224 main + pilot data). Tasks will be added soon.
- **[2026/4/7]** Paper submitted to arXiv — 6 models, 4 harnesses, 33 conditions, 7,224 trials.

## Headline Results

| Model | TSR (scaffolded) | UAR (scaffolded) |
|-------|:-:|:-:|
| Claude Opus 4.6 | **63%** | 23% |
| GLM-5 | 60% | 23% |
| Gemini 3.1 Pro | 58% | 10% |
| Claude Sonnet 4.6 | 56% | 13% |
| GPT-5.4 | 53% | **7%** |
| Gemini 3.1 Flash-Lite | 39% | 23% |

> Without scaffolding (skills + meta prompt), all models score 0-8% TSR. Scaffolding is the dominant factor — the 40-60pp lift dwarfs model differences.

## Key Findings

1. **Scaffolding dominates model capability** — the scaffolding effect (+39-63pp) dwarfs the model spread (10pp among top five)
2. **Top models are statistically indistinguishable** — no pairwise differences survive Holm-Bonferroni correction
3. **No safety-capability tradeoff** — the best model (Opus, 63% TSR) ties for the most unsafe (23% UAR)
4. **Multi-service tasks are harder and more dangerous** — +23pp TSR gap, +10pp UAR for multi-service
5. **8 recurring rogue behaviors** including sandbox escalation, prompt injection compliance, and unauthorized contract modification

## Repository Structure

```
ClawsBench/
├── docs/                    # Project website (GitHub Pages)
│   ├── index.html
│   └── assets/              # Figures and images
├── trajectories/            # Agent trajectory data (coming soon)
│   └── README.md
├── LICENSE                  # CC BY-NC-SA 4.0
└── README.md
```

## Benchmark Overview

- **5 Mock Services**: claw-gmail (62 endpoints), claw-gcal, claw-gdocs, claw-gdrive, claw-slack (45 endpoints)
- **44 Tasks**: 30 single-service + 14 cross-service, including 24 safety-critical scenarios
- **6 Models**: Claude Opus 4.6, Claude Sonnet 4.6, GPT-5.4, Gemini 3.1 Pro, Gemini 3.1 Flash-Lite, GLM-5
- **4 Harnesses**: OpenClaw, Claude Code, Codex, Gemini CLI
- **33 Conditions**: Varying domain skills and meta prompt across model-harness combinations
- **7,224 Trials**: Full experimental data with bootstrap CIs and statistical tests

## Anti-Cheating Sandbox

We discovered that agents could read evaluation criteria, oracle solutions, and seed data when running as root. We deployed Unix permission hardening with a restricted `agent` user and `gosu` privilege dropping. Zero successful sandbox bypasses were observed across all 7,224 trials.

## License

This work is licensed under [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/). You may share and adapt the materials for non-commercial purposes with attribution. You may **not** use the data, trajectories, or environments for commercial purposes.

## Citation

```bibtex
@misc{li2026clawsbenchevaluatingcapabilitysafety,
      title={ClawsBench: Evaluating Capability and Safety of LLM Productivity Agents in Simulated Workspaces}, 
      author={Xiangyi Li and Kyoung Whan Choe and Yimin Liu and Xiaokun Chen and Chujun Tao and Bingran You and Wenbo Chen and Zonglin Di and Jiankai Sun and Shenghan Zheng and Jiajun Bao and Yuanli Wang and Weixiang Yan and Yiyuan Li and Han-chung Lee},
      year={2026},
      eprint={2604.05172},
      archivePrefix={arXiv},
      primaryClass={cs.AI},
      url={https://arxiv.org/abs/2604.05172}, 
}
```

## Links

- [Project Website](https://benchflow-ai.github.io/ClawsBench/)
- [Paper (arXiv)](https://arxiv.org/abs/2604.05172)
- [Dataset (Hugging Face)](https://huggingface.co/datasets/benchflow/ClawsBench)
- [Agent Skills Workshop (ACM CAIS 2026)](https://agentskills-workshop.github.io)
- [Discord](https://discord.gg/mZ9Rc8q8W3)
