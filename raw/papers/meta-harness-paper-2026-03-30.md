# Raw Source: Meta-Harness Paper

- Original URL: https://arxiv.org/abs/2603.28052
- Retrieved via: https://r.jina.ai/http://arxiv.org/abs/2603.28052 + https://r.jina.ai/http://arxiv.org/html/2603.28052
- Retrieved on: 2026-04-25
- Authors: Yoonho Lee, Roshen Nair, Qizheng Zhang, Kangwook Lee, Omar Khattab, Chelsea Finn
- Institution: Stanford IRIS Lab
- Submitted: 2026-03-30
- arXiv ID: 2603.28052
- Type: Research paper
- Title: Meta-Harness: End-to-End Optimization of Model Harnesses

---

## Abstract

The performance of large language model (LLM) systems depends not only on model weights, but also on their harness: the code that determines what information to store, retrieve, and present to the model. Yet harnesses are still designed largely by hand, and existing text optimizers are poorly matched to this setting because they compress feedback too aggressively: they are memoryless, condition only on scalar scores, or restrict feedback to short templates or summaries.

We introduce **Meta-Harness**, an outer-loop system that searches over harness code for LLM applications. It uses an **agentic proposer** that accesses the source code, scores, and execution traces of all prior candidates through a **filesystem**. On online text classification, Meta-Harness improves over a state-of-the-art context management system by **7.7 points** while using **4× fewer context tokens**. On retrieval-augmented math reasoning, a single discovered harness improves accuracy on 200 IMO-level problems by **4.7 points** on average across five held-out models. On agentic coding, discovered harnesses surpass the best hand-engineered baselines on TerminalBench-2. Together, these results show that richer access to prior experience can enable automated harness engineering.

## Core Innovation

### Why Existing Text Optimizers Fail for Harness Optimization

Existing text optimizers (TTT-Discover, OpenEvolve) compress feedback too aggressively:
- **Memoryless**: don't retain history of prior attempts
- **Scalar-only**: condition only on scores, not execution traces
- **Template-restricted**: limit feedback to short summaries

Meta-Harness solves this by giving the proposer **full filesystem access** to:
- Source code of all prior candidate harnesses
- Execution traces (up to 10 million tokens of diagnostic info per evaluation)
- Scores and performance metrics
- The proposer uses `grep` and `cat` to read whatever it needs

### The Outer-Loop Architecture

1. **Initialize population** from strong baselines (e.g., Terminus-KIRA for coding, ACE for text classification)
2. **Proposer** (an agent with filesystem access) proposes new harness variants
3. **Evaluate** candidates on search set
4. **Select** best candidates based on Pareto dominance (accuracy vs context cost)
5. **Iterate** — proposer learns from all prior attempts via filesystem

### Key Design Choice: Minimum Necessary Structure

Meta-Harness intentionally imposes minimum structure on the outer loop:
- Proposer gets raw filesystem access, not pre-processed summaries
- Preserves full experience history
- Allows proposer to inspect anything necessary
- This is why it outperforms structure-heavy optimizers like OpenEvolve and TTT-Discover

## Three Experimental Domains

### 1. Online Text Classification
- **Result**: +7.7 points over ACE (state-of-the-art context management), 4× fewer context tokens
- **Speed**: Matches best prior text optimizer's final performance after just **4 evaluations** (vs 60 for competitors)
- **Ablation**: Full interface (scores + traces) reaches 50.0 median accuracy; scores-only reaches 34.6; scores+summary reaches 34.9
- **Conclusion**: Full access to execution traces is the most important component

### 2. Retrieval-Augmented Math Reasoning
- **200 IMO-level problems** from IMO-AnswerBench, IMO-ProofBench, ArXivMath
- **5 held-out models**: GPT-OSS-20B, GPT-5.4-nano, GPT-5.4-mini, Gemini-3.1-Flash-Lite, Gemini-3-Flash
- **Result**: +4.7 points average across all 5 models
- **Method**: Discovered retrieval harness operates in code space on BM25, no additional dense encoder needed

### 3. Agentic Coding on TerminalBench-2
- **Claude Opus 4.6**: **76.4%** pass rate
  - Surpasses Terminus-KIRA (74.7%)
  - Ranks **#2** among all Opus 4.6 agents (ForgeCode is #1 at 81.8% but unreproducible from published code)
- **Claude Haiku 4.5**: **37.6%** pass rate
  - Ranks **#1** among all Haiku 4.5 agents
  - Outperforms next-best (Goose, 35.5%) by 2.1 points
- **Discovered harness**: Environment bootstrapping (see below)

## The Discovered TerminalBench-2 Harness

### Environment Bootstrapping (the key discovery)

Before the agent loop begins, the harness runs a compound shell command to gather a snapshot of the sandbox environment and injects it into the initial prompt.

**Snapshot includes:**
- Working directory
- Listing of /app (truncated to 20 entries for large directories)
- Available programming languages and versions (Python, GCC, G++, Node, Java, Rust, Go)
- Installed package managers (pip, apt-get)
- Available memory

**Effect**: Eliminates 2–4 exploratory turns that agents typically spend discovering what tools and files are available, allowing the model to begin productive work immediately.

**Implementation details:**
- Bootstrapping command guarded by 15-second timeout
- Fails silently (doesn't break agent in unusual environments)
- Adds roughly 80 lines on top of Terminus-KIRA
- Inherits Terminus-KIRA's native tool calling, 30KB output cap, multi-perspective completion checklist

### Search Process Narrative

The paper includes a fascinating narrative arc from the search log:
1. Early candidates failed due to over-aggressive environment assumptions
2. Proposer formed explicit diagnosis of failures
3. Shifted toward safer design pattern (environment bootstrapping with timeout + silent failure)
4. Final harness is robust and generalizable

### Proposer File Access Statistics

From the TerminalBench-2 search run (10 iterations, Claude Opus 4.6):
- Proposer reads extensively from filesystem
- Roughly equal attention to prior source code and execution traces
- Uses `grep` and `cat` to navigate diagnostic information

## Key Comparisons

### vs Hand-Engineered Harnesses
| Method | Accuracy | Context Tokens |
|--------|----------|---------------|
| Meta-Harness | 48.6% | 11.4K |
| ACE (hand-designed) | 40.9% | 50.8K |
| MCE (hand-designed) | 40.0% | 28.5K |

### vs Text Optimizers (Online Text Classification)
| Method | Evaluations to Match Final | Final Accuracy |
|--------|--------------------------|----------------|
| Meta-Harness | 4 | ~56.7 |
| OpenEvolve | ~40 | ~46 |
| TTT-Discover | ~60 | ~46 |

### TerminalBench-2 Leaderboard (Opus 4.6)
| Rank | Agent | Score |
|------|-------|-------|
| 1 | ForgeCode | 81.8% (unreproducible) |
| **2** | **Meta-Harness** | **76.4%** |
| 3 | Capy | 75.3% |
| 4 | Terminus-KIRA | 74.7% |

## Generalization

### Out-of-Distribution (OOD) Text Classification
- Evaluated on **9 diverse datasets** unseen during search
- Meta-Harness achieves **73.1%** average accuracy
- Outperforms ACE (70.2%) and all few-shot baselines
- Highest performance on 6/9 datasets
- Suggests discovered harness captures generally effective strategies, not overfitting

## Links

- Paper: https://arxiv.org/abs/2603.28052
- PDF: http://arxiv.org/pdf/2603.28052
- HTML: https://arxiv.org/html/2603.28052v1
- Main repo (framework): https://github.com/stanford-iris-lab/meta-harness
- TerminalBench-2 artifact: https://github.com/stanford-iris-lab/meta-harness-tbench2-artifact
- TerminalBench: https://tbench.ai
