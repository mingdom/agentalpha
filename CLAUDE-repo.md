## Repository Overview

This is a stock research and analysis system built on Michael Mauboussin's investment philosophy. The repository contains AI agent prompts for generating institutional-quality equity research reports that identify **mispricings**, not just "good companies."

## Core Philosophy

The system is grounded in Mauboussin's core principles:
- **Fundamentals vs. Expectations**: Find the delta between what the market prices in vs. what fundamentals suggest
- **Value = Future Cash Flow**: Connect strategy (ROIC > WACC) to future FCF
- **Process Over Outcome**: Demonstrate repeatable, disciplined analysis
- **The Babe Ruth Effect**: Investment success = magnitude of wins, not frequency
- **BAIT Framework**: Four sources of edge (Behavioral, Analytical, Informational, Technical)

## Directory Structure

```
/agent/maub-analyst/          # Production AI agent prompts
  ├── mauboussin-principles.md     # Foundational principles (mandatory learning for new agents)
  ├── mb-analyst-concise.md        # Concise research prompt (9k chars, operational use)
  ├── mm-analyst.md                # Original full research prompt (~11k chars)
  ├── mm-analyst-verbose.md        # Comprehensive prompt with embedded principles (23k chars)
  └── rubric.md                    # Investment scoring rubric (6 dimensions, /10 scale)

/inbox/                       # Working documents and source material
  ├── mm-key-principles.md         # Extracted Mauboussin principles from writings
  ├── grok-rankings.md             # Example research output with scoring
  └── maubaoussin-prompt-v1.md     # Earlier prompt iterations
```

## Agent Prompt Architecture

### Three-Tier Prompt System

1. **`mauboussin-principles.md`** (7.5k chars)
   - Onboarding document for new agents/team members
   - Distills 10 core investment principles
   - Serves as the philosophical foundation
   - Not executable - pure learning/reference

2. **`mb-analyst-concise.md`** (9.1k chars) - **Primary operational prompt**
   - Streamlined 7-step research process
   - Optimized for API efficiency and speed
   - Includes: Data Gathering → Market Expectations → Base Rates → Variant View → BAIT Edge → Linchpins → Signposts → Fair Value
   - Use for: Daily research, high-volume analysis

3. **`mm-analyst-verbose.md`** (23k chars)
   - Comprehensive version with embedded Mauboussin principles
   - Agents internalize "why" behind each step
   - Enhanced BAIT framework with mechanism explanations
   - Use for: Deep-dive reports, high-conviction ideas, training gold standard

### Supporting Documents

**`rubric.md`** - Investment Scoring Framework
- 6 dimensions scored 0-10: Moat, Growth, Expectations Gap, Balance Sheet, Management, Risk
- Maps scores to recommendations (9.0-10.0 = Strong Long, <6.0 = Short Candidate)
- Mandatory documentation requirements for all reports
- Back-tested on firm research history

## Prompt Engineering Principles

When modifying or creating new agent prompts:

1. **Character Limits**:
   - Concise prompts: <12,000 characters
   - Verbose prompts: 20,000-25,000 characters acceptable
   - Always run `wc -c <file>` to verify

2. **Required Elements** (per mb-analyst-concise.md):
   - Role & Mission statement
   - Core principles (3-4 key tenets)
   - Sequential research process (numbered steps)
   - Output format template (markdown with tables)
   - Writing guidelines
   - Execution instructions

3. **Mauboussin Principle Integration**:
   - **FCF emphasis**: Always require Free Cash Flow analysis, not just earnings
   - **Base rates**: Anchor forecasts against historical precedent (ROIC persistence, growth durability)
   - **Linchpins**: Identify 2-3 key drivers, resist information overload
   - **BAIT Edge**: Explicitly state primary source of edge
   - **Falsifiable signposts**: Quantified predictions with probabilities

4. **Valuation Rigor**:
   - NEVER allow price targets without explicit methodology
   - Require Bear/Base/Bull scenarios with probabilities
   - Probability-weighted fair value calculation
   - For intangible-heavy businesses: capitalize R&D, adjust ROIC
   - If using multiples: connect to fundamentals (ROIC, capital intensity)

## Key Research Process Steps

All research prompts follow this 7-step framework (from mb-analyst-concise.md):

0. **Data Gathering**: Stock price, earnings, transcripts, consensus estimates, FCF metrics
1. **Quantify Market Expectations**: Reverse-engineer what current price implies
2. **Establish Base Rates**: Historical precedent for ROIC/growth/margins
3. **Develop Variant View**: Your forecast vs. market consensus
4. **Define Edge (BAIT)**: Behavioral/Analytical/Informational/Technical
5. **Identify Linchpins**: 2-3 variables driving 80% of thesis value
6. **Define Signposts**: Falsifiable predictions with probabilities
7. **Calculate Fair Value**: Show full methodology, scenarios, probability-weighting

## Investment Scoring Rubric

When evaluating or scoring stocks (per rubric.md):

- **Moat** (0-10): Test = "Can well-funded competitor replicate in <5 years?"
- **Growth** (0-10): Test = "How many years of demand are structurally visible?"
- **Expectations Gap** (0-10): % upside to base-case fair value
- **Balance Sheet** (0-10): Test = "Survive 3 years zero revenue?"
- **Management** (0-10): Test = "Consistently turned high ROIC into shareholder value?"
- **Risk** (0-10): Test = "2 most credible paths to 80%+ permanent loss?"

Final score = Total /60 → convert to /10

## Common Modifications

### To shorten a prompt:
- Remove verbose explanations, keep examples concise (1 per concept)
- Consolidate related bullet points
- Use tables instead of prose where possible
- Keep all mandatory elements (principles, steps, template, guidelines)

### To add new Mauboussin principles:
1. Add to `mauboussin-principles.md` first (source of truth)
2. Distill actionable guidance for research process
3. Integrate into relevant step in `mb-analyst-concise.md` or `mm-analyst-verbose.md`
4. Update rubric if it affects scoring dimensions

### To create a new research prompt variant:
1. Start from `mb-analyst-concise.md` (proven structure)
2. Modify Role & Mission for specific use case
3. Keep 7-step process structure
4. Adjust output template if needed
5. Test character count: `wc -c <file>`

## File Management

- **`/agent/maub-analyst/`**: Production-ready prompts only
- **`/inbox/`**: Working documents, research, iterations
- When updating principles: Always update `mauboussin-principles.md` first, then flow to operational prompts
- Version control: Date-stamp major revisions in git commits

## Git Repository

- Not a git repo currently (no `.gitignore`, no package managers)
- Pure document repository for AI agent system prompts
- No build process, linting, or testing infrastructure
- All files are markdown (.md)
