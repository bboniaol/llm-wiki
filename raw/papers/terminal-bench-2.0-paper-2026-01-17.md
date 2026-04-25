# Raw Source: Terminal-Bench 2.0 Paper

- Original URL: https://arxiv.org/abs/2601.11868
- Retrieved via: https://r.jina.ai/http://arxiv.org/abs/2601.11868
- Retrieved on: 2026-04-25
- Authors: Mike A. Merrill, Alexander G. Shaw, Nicholas Carlini, Boxuan Li, Harsh Raj, Ivan Bercovich, Lin Shi, Jeong Yeon Shin, Thomas Walshe, E. Kelly Buchanan, Junhong Shen, Guanghao Ye, Haowei Lin, Jason Poulos, Maoyu Wang, Marianna Nezhurina, Jenia Jitsev, Di Lu, Orfeas Menis Mastromichalakis, Zhiwei Xu, Zizhao Chen, Yue Liu, Robert Zhang, Leon Liangyu Chen, Anurag Kashyap, Jan-Lucas Uslu, Jeffrey Li, Jianbo Wu, Minghao Yan, Song Bian, Vedang Sharma, Ke Sun, Steven Dillmann, Akshay Anand, Andrew Lanpouthakoun, Bardia Koopah, Changran Hu, Etash Guha, Gabriel H.S. Dreiman, Jiacheng Zhu, Karl Krauth, Li Zhong, Niklas Muennighoff, Robert Amanfu, Shangyin Tan, Shreyas Pimpalgaonkar, Tushar Aggarwal, Xiangning Lin, Xin Lan, Xuandong Zhao, Yiqing Liang, Yuanli Wang, Zilong Wang, Changzhi Zhou, David Heineman, Hange Liu, Harsh Trivedi, John Yang, Junhong Lin, Manish Shetty, Michael Yang, Nabil Omi, Negin Raoof, Shanda Li, Terry Yue Zhuo, Wuwei Lin, Yiwei Dai, Yuxin Wang, Wenhao Chai, Shang Zhou, Dariush Wahdany, Ziyu She, Jiaming Hu, Zhikang Dong, Yuxuan Zhu, Sasha Cui, Ahson Saiyed, Arinbjörn Kolbeinsson, Jesse Hu, Christopher Michael Rytting, Ryan Marten, Yixin Wang, Alex Dimakis, Andy Konwinski, Ludwig Schmidt
- Institution: Multiple (including Stanford, Google, KRAFTON AI, etc.)
- Submitted: 2026-01-17
- arXiv ID: 2601.11868
- Type: Benchmark paper

---

## Abstract

AI agents may soon become capable of autonomously completing valuable, long-horizon tasks in diverse domains. Current benchmarks either do not measure real-world tasks, or are not sufficiently difficult to meaningfully measure frontier models. To this end, we present Terminal-Bench 2.0: a carefully curated hard benchmark composed of **89 tasks** in computer terminal environments inspired by problems from real workflows. Each task features a unique environment, human-written solution, and comprehensive tests for verification. We show that **frontier models and agents score less than 65%** on the benchmark and conduct an error analysis to identify areas for model and agent improvement. We publish the dataset and evaluation harness to assist developers and researchers in future work at https://www.tbench.ai/.

## Key Facts

- **89 tasks** in computer terminal environments
- Tasks inspired by **real workflows**
- Each task has: unique environment, human-written solution, comprehensive tests
- **Frontier models/agents score < 65%** — benchmark is hard enough to differentiate
- Uses **Harbor harness** — supports Claude Code, Codex CLI, OpenHands, Mini-SWE-Agent, and Terminus 2
- Harbor task format + adapters for diverse agent configurations
- Premature termination detection: agent declares completion before meeting explicit objectives

## Benchmark Design

- Terminal-based tasks (command line interfaces)
- Real-world inspired problems
- Docker container environments
- Tool use required: editing files, running Bash commands
- Verification via comprehensive tests

## Supported Agents

The Harbor harness supports:
- Claude Code
- Codex CLI
- OpenHands
- Mini-SWE-Agent
- Terminus 2 (neutral testbed for comparing model performance)

## Key Numbers from Leaderboard (via search)

| Rank | Agent/Model | Score |
|------|-------------|-------|
| ~5 | LangChain Deep Agents (after harness optimization) | ~66.5% |
| - | OpenAI GPT-5.3 Codex | 77.3% |
| - | OpenAI GPT-5.2 Codex | 64.0% |
| - | Anthropic Claude Opus 4.5 | 59.3% |
| - | Anthropic Claude Sonnet 4.6 | 59.1% |
| **1** | **Stanford Meta-Harness (Claude Opus 4.6)** | **76.4%** |

Note: The 76.4% Meta-Harness result is from a separate research project (Stanford IRIS Lab), not the original paper.

## Error Analysis

The paper conducts error analysis to identify areas for model and agent improvement. Specific error categories are detailed in the full paper.

## Links

- Paper: https://arxiv.org/abs/2601.11868
- Dataset & harness: https://www.tbench.ai/
- PDF: http://arxiv.org/pdf/2601.11868
- HTML: https://arxiv.org/html/2601.11868v1
