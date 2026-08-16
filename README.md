# Eval Skills

Skills that guide AI coding agents to help you build [product-specific](https://hamel.dev/notes/llm/evals/) AI evals (not foundation model benchmarks).

These skills guard against common mistakes we've seen helping 50+ companies and teaching thousands of students in our [AI Evals course](https://maven.com/parlance-labs/evals?promoCode=evals-info-url). In the course you build a support agent and use evals to find and fix its failures. If you're new to evals, see [Hamel's evals notes](https://hamel.dev/notes/llm/evals/) for free resources on the fundamentals.

## New to evals? Start here

Start with the `eval-audit` skill. Give your coding agent these instructions:

> Install the eval skills with `npx skills add https://github.com/ai-evals-course/error-discovery-skill`, then run the eval-audit skill on my eval pipeline. Investigate each diagnostic area using a separate subagent in parallel, then synthesize the findings into a single report. Use other skills from this set as recommended by the audit.

The audit isn't a complete solution, but it catches common problems and recommends other skills to fix them.

## Installation

Install with [npx skills](https://github.com/vercel-labs/skills):

```bash
npx skills add https://github.com/ai-evals-course/error-discovery-skill
```

Install one skill only:

```bash
npx skills add https://github.com/ai-evals-course/error-discovery-skill --skill error-discovery
```

Check for updates:

```bash
npx skills check
npx skills update
```

## Available skills

| Skill | What it does |
|-------|-------------|
| eval-audit | Audit an eval pipeline and surface problems with prioritized severity |
| error-analysis | Entry point for error analysis requests. Routes to the skill that matches your situation |
| error-discovery | Build a review app, select diverse samples, and organize your notes into failure modes |
| generate-synthetic-data | Create diverse synthetic test inputs using dimension-based tuple generation |
| write-judge-prompt | Design LLM-as-Judge evaluators for subjective quality criteria |
| validate-evaluator | Calibrate LLM judges against human labels using data splits, TPR/TNR, and bias correction |
| evaluate-rag | Evaluate retrieval and generation quality in RAG pipelines |
| build-review-interface | Build custom annotation interfaces for human trace review |

## The error-discovery skill

This skill makes an AI agent run error analysis on a dataset. Point it at a
JSONL/CSV/JSON file of LLM outputs or traces, and it:

1. Reads the dataset and figures out the content type (articles, agent traces,
   code, structured output, etc.).
2. Designs visual encoding based on what varies in the data. Uses Gestalt
   principles (color for categories, spacing for hierarchy, opacity for
   importance).
3. Builds a single-file HTML review app served by a Python stdlib server. No
   dependencies.
4. Clusters the data and picks a diverse initial sample (cluster reps + random
   picks).
5. Runs an interactive loop: monitors annotations, categorizes failure modes,
   proposes new samples to increase coverage.

![Error Discovery Skill Workflow](workflow.png)

You read and leave free-text notes. The agent sorts them into failure modes,
tracks coverage, and picks new samples to fill gaps.

Once installed, point the agent at a dataset:

```
Can you help me do error analysis on traces.jsonl?
```

## Write your own skills

These skills encode common mistakes that generalize across projects. Skills grounded in your own data and domain will outperform them. Start here, then write your own. Matt Pocock's [writing-for-agents](https://github.com/mattpocock/skills/tree/main/skills/productivity/writing-for-agents) skill teaches an agent to write good skills.

## Beyond these skills

These skills cover the parts of eval work that generalize across projects. Much of the process doesn't, such as production monitoring, CI/CD regression suites, and cost optimization. The [AI Evals course](https://maven.com/parlance-labs/evals?promoCode=evals-info-url) covers the full process.
