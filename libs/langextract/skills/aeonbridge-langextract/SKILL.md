---
name: langextract
description: Local reference snapshot based on the Aeonbridge LangExtract skill. Use when extracting structured, source-grounded data from unstructured text with Gemini, OpenAI, or local models.
source_urls:
  - https://skills.sh/aeonbridge/ab-anthropic-claude-skills/langextract
  - https://github.com/aeonbridge/ab-anthropic-claude-skills/tree/main/output/langextract
  - https://github.com/google/langextract
---

# LangExtract Skill Snapshot

This is a local consultation copy adapted from the upstream skill and the official project README. Keep the upstream links above as the source of truth for future updates.

## When To Use

Use LangExtract when you need to:

- extract structured entities from unstructured text
- keep every extraction tied to the exact source span
- process long documents that exceed normal prompt sizes
- build few-shot extraction pipelines without fine-tuning
- generate JSONL outputs and HTML visualizations for human review

## Strengths

- source grounding for traceability and validation
- structured outputs driven by prompt instructions and examples
- long-document handling with chunking, parallel workers, and extraction passes
- support for Gemini, OpenAI, Vertex AI, and Ollama-style local setups
- practical review flow with saved annotations and HTML visualization

## Recommended Workflow

1. Write a precise `prompt_description` describing what to extract.
2. Add a few high-quality `ExampleData` examples with grounded `Extraction` items.
3. Run `lx.extract(...)` on the target text or documents.
4. Review the extracted spans and attributes.
5. Save results to JSONL and visualize them in HTML when manual review matters.

## Quick Start

```python
import langextract as lx
import textwrap

prompt = textwrap.dedent("""\
    Extract all medications mentioned in the text.
    Include name, dosage, and frequency.
    Use exact text from the source.""")

examples = [
    lx.data.ExampleData(
        text="Patient prescribed Lisinopril 10mg daily.",
        extractions=[
            lx.data.Extraction(
                extraction_class="medication",
                extraction_text="Lisinopril 10mg daily",
                attributes={
                    "name": "Lisinopril",
                    "dosage": "10mg",
                    "frequency": "daily",
                },
            )
        ],
    )
]

result = lx.extract(
    text_or_documents="Patient continues Metformin 500mg twice daily.",
    prompt_description=prompt,
    examples=examples,
    model_id="gemini-2.5-flash",
)

for extraction in result.extractions:
    print(extraction.extraction_text, extraction.attributes)
```

## Common Patterns

### Save JSONL And Visualize

```python
import langextract as lx

lx.io.save_annotated_documents(
    [result],
    output_name="extractions.jsonl",
    output_dir=".",
)

html = lx.visualize("extractions.jsonl")
with open("extractions.html", "w") as f:
    if hasattr(html, "data"):
        f.write(html.data)
    else:
        f.write(html)
```

### Long Documents

```python
result = lx.extract(
    text_or_documents=long_text,
    prompt_description=prompt,
    examples=examples,
    model_id="gemini-2.5-flash",
    extraction_passes=3,
    max_workers=20,
    max_char_buffer=1000,
)
```

### OpenAI Models

```python
result = lx.extract(
    text_or_documents=text,
    prompt_description=prompt,
    examples=examples,
    model_id="gpt-4o",
    use_schema_constraints=False,
    fence_output=True,
)
```

### Local Models Through Ollama

```python
result = lx.extract(
    text_or_documents=text,
    prompt_description=prompt,
    examples=examples,
    model_id="gemma2:2b",
    model_url="http://localhost:11434",
    use_schema_constraints=False,
)
```

## Practical Guidance

- Keep examples small, realistic, and consistent with the output you want.
- Prefer grounded `extraction_text` values copied directly from the source text.
- Start with one simple example before scaling to many classes or attributes.
- Increase `extraction_passes` when recall matters more than speed.
- Use visualization whenever the extraction pipeline needs auditing.
- Filter out ungrounded results if your workflow requires strict traceability.

## Key Parameters

- `model_id`: target model, such as `gemini-2.5-flash` or `gpt-4o`
- `examples`: few-shot examples that define the extraction style and schema
- `extraction_passes`: extra passes to improve recall on long text
- `max_workers`: parallel worker count for larger workloads
- `max_char_buffer`: overlap and context sizing for long-document chunking
- `use_schema_constraints`: disable when using providers that do not support the same constraints
- `fence_output`: often useful with OpenAI models

## Helpful Links

- Official repository: https://github.com/google/langextract
- Examples: https://github.com/google/langextract/tree/main/examples
- Docs examples: https://github.com/google/langextract/tree/main/docs/examples
- Gemini API docs: https://ai.google.dev/
