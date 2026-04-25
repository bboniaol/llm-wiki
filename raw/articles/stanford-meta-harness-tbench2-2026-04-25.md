# Raw Source: Stanford Meta-Harness

- Original URL: https://github.com/stanford-iris-lab/meta-harness-tbench2-artifact
- Retrieved via: https://raw.githubusercontent.com/stanford-iris-lab/meta-harness-tbench2-artifact/main/README.md
- Retrieved on: 2026-04-25
- Author: Stanford IRIS Lab
- Type: Research artifact / agent harness
- License: Not specified (public repo)

---

# Meta-Harness

Agent scaffold for [Terminal-Bench 2.0](https://tbench.ai), built on top of [Terminus-KIRA](https://github.com/krafton-ai/KIRA) by KRAFTON AI and [Harbor](https://github.com/laude-institute/harbor)'s Terminus-2 framework.

## Results

**76.4% on Terminal-Bench 2.0** (89 tasks × 5 trials, Claude Opus 4.6).

| Split  | N  | Score |
|--------|---:|------:|
| Easy   |  4 | 100.0 |
| Medium | 55 |  81.1 |
| Hard   | 30 |  64.7 |
| **All**| 89 |**76.4**|

## Usage

```bash
pip install harbor

export ANTHROPIC_API_KEY=***

harbor run \
  --agent-import-path agent:AgentHarness \
  -d terminal-bench@2.0 \
  -m anthropic/claude-opus-4-6 \
  -e runloop \
  -n 20 \
  --n-attempts 5
```

## Method

Meta-Harness extends the [Terminus-KIRA](https://github.com/krafton-ai/KIRA) agent with **environment bootstrapping**: before the agent loop starts, it gathers a snapshot of the sandbox environment (working directory, file listing, available languages/tools, package managers, memory) and injects it into the initial prompt. This saves 2-5 early exploration turns that the agent normally spends on `ls`, `which python3`, etc.

The agent was **discovered through automated harness evolution**. More details coming soon.

## Key Insight

This is the "separate research project" referenced by Akshay Pachaar that hit 76.4% pass rate by having an LLM optimize the infrastructure itself, surpassing hand-designed systems.

The core innovation is **automated harness evolution**: the harness wasn't hand-designed by humans, but was discovered/evolved automatically. This validates the claim that "harness optimization" can be automated and can outperform human-designed harnesses.

## Acknowledgements

We thank KRAFTON AI for compute support.

## Links

- GitHub: https://github.com/stanford-iris-lab/meta-harness-tbench2-artifact
- Terminal-Bench: https://tbench.ai
- Terminus-KIRA: https://github.com/krafton-ai/KIRA
- Harbor: https://github.com/laude-institute/harbor
