# Senior Data Scientist AI Guidance

Version 0.1.0

A small, versioned set of reusable guidance for using capable LLMs as senior-standard data-science collaborators. The project separates concise behavioural instructions from a fuller professional playbook so the model gets strong defaults without turning the instruction block into a textbook.

## Artefacts

- `senior-data-scientist-instructions.md` - concise operating instructions for the LLM. Use this as the reusable instruction layer in a notebook, project or equivalent context.
- `data-science-playbook.md` - deeper defaults, decision rules and checklists that the instructions explicitly require the LLM to consult when available.
- `CHANGELOG.md` - transparent record of the reasoning and scope decisions that produced the artefacts.

## How the pieces work together

The intended precedence is:

1. the current task and explicit user requirements;
2. project-specific requirements, data documentation and architecture decisions;
3. `senior-data-scientist-instructions.md`;
4. relevant guidance in `data-science-playbook.md`;
5. general professional defaults.

Project requirements should normally override generic defaults. The LLM should flag a conflict rather than silently following a project rule when that rule creates a material scientific, statistical, legal, security or operational problem.

The instructions and playbook are complementary. The instructions deliberately contain the behaviours that should stay active across most work. The playbook supplies the fuller reasoning needed for substantial analyses, reviews, designs and implementations. When the playbook is available, the instructions tell the LLM when and how to consult it rather than mentioning it only as optional background.

## Recommended use

### Microsoft Copilot notebooks or comparable project contexts

Add both the instructions and playbook to the working context when the interface allows it. Give the instructions higher prominence and make the playbook available as a reference artefact. Add project-specific material separately rather than editing generic guidance for every project.

### Other LLM project/workspace systems

Use the same separation: core instructions plus playbook plus project context. Adapt the packaging to the product, but keep the canonical content in this repository.

### Individual prompts

You normally should not need to repeat the playbook. A task can be as compact as:

> Mode: Review. Review this forecasting notebook. Apply the Senior Data Scientist Instructions and the relevant sections of the Data Science Playbook. Prioritise conclusions that could materially change the analysis.

## Working modes

The instructions define seven optional modes:

- Explore
- Analyse
- Design
- Engineer
- Review
- Reproduce
- Explain

Modes alter the working approach and quality criteria, not merely the writing style.

## Language scope

First-class analytical languages are Python, R and SQL. Julia is supported for scientific and numerical computing. JavaScript/TypeScript is included for interactive visualisation and analytical applications. Go is recognised at the operational engineering boundary. Other languages are not prohibited when project context requires them.

## Design principles

1. Work to a senior standard while adapting to the user.
2. Frame the problem before choosing the method.
3. Put scientific validity and data integrity before sophistication.
4. Think across the complete data-science lifecycle.
5. Apply rigour and engineering proportionately.
6. Choose technologies contextually rather than dogmatically.
7. Make evidence, assumptions and uncertainty explicit.
8. Make important work reproducible and verifiable.
9. Challenge material weaknesses without performative criticism.
10. Exploit LLM strengths while checking characteristic LLM failure modes.

## Versioning and improvement

Treat these artefacts as maintained engineering assets. Evaluate changes against representative tasks, record material changes in `CHANGELOG.md`, and prefer changes that correct recurring or consequential model behaviour rather than accumulating stylistic preferences.

The long-term aim is not a perfect prompt. It is a compact, testable and maintainable standard for LLM-assisted data science.
