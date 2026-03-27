---
name: docling
description: Local reference snapshot based on the Beagle Docling skill. Use when converting documents, exporting structured formats, running OCR, or chunking parsed content for RAG pipelines.
source_urls:
  - https://skills.sh/existential-birds/beagle/docling
  - https://github.com/existential-birds/beagle/tree/main/plugins/beagle-core/skills/docling
---

# Docling Skill Snapshot

This is a local consultation copy based on the upstream Beagle skill. Keep the upstream links above as the source of truth for future updates.

## When To Use

Use Docling when you need to:

- convert PDFs, DOCX, PPTX, HTML, images, and other formats into structured content
- export parsed documents to Markdown, HTML, JSON, plain text, or DocTags
- enable OCR or table extraction for scanned or layout-heavy documents
- process many files with `convert_all()`
- chunk parsed documents before sending them into a RAG pipeline

## Core Objects

- `DocumentConverter`: main entry point for parsing and conversion
- `ConversionResult`: conversion output with status, errors, and parsed document
- `DoclingDocument`: structured document representation
- `PdfPipelineOptions`: PDF-specific options such as OCR and table handling
- `HierarchicalChunker` and `HybridChunker`: chunking strategies for retrieval workflows

## Quick Start

```python
from docling.document_converter import DocumentConverter

source = "https://arxiv.org/pdf/2408.09869"
converter = DocumentConverter()
result = converter.convert(source)

markdown = result.document.export_to_markdown()
print(markdown[:500])
```

## Common Workflows

### Basic Conversion

```python
from docling.document_converter import DocumentConverter

converter = DocumentConverter()
result = converter.convert("document.pdf")

result.document.save_as_markdown("document.md")
result.document.save_as_json("document.json")
result.document.save_as_html("document.html")
```

### PDF With OCR And Table Structure

```python
from docling.datamodel.base_models import InputFormat
from docling.datamodel.pipeline_options import PdfPipelineOptions
from docling.document_converter import DocumentConverter, PdfFormatOption

pipeline_options = PdfPipelineOptions()
pipeline_options.do_ocr = True
pipeline_options.do_table_structure = True

converter = DocumentConverter(
    format_options={
        InputFormat.PDF: PdfFormatOption(pipeline_options=pipeline_options)
    }
)

result = converter.convert("scanned.pdf")
```

### Batch Processing

```python
from docling.document_converter import DocumentConverter
from docling.datamodel.base_models import ConversionStatus

converter = DocumentConverter()
results = converter.convert_all(
    ["a.pdf", "b.docx", "c.html"],
    raises_on_error=False,
)

for result in results:
    if result.status == ConversionStatus.SUCCESS:
        result.document.save_as_markdown(f"{result.input.file.stem}.md")
```

### Chunking For RAG

```python
from docling.chunking import HybridChunker
from docling.document_converter import DocumentConverter
from transformers import AutoTokenizer

converter = DocumentConverter()
result = converter.convert("document.pdf")

tokenizer = AutoTokenizer.from_pretrained("sentence-transformers/all-MiniLM-L6-v2")
chunker = HybridChunker(tokenizer=tokenizer, max_tokens=512)
chunks = list(chunker.chunk(result.document))
```

## Practical Guidance

- Start with `DocumentConverter()` and only add PDF options when OCR or tables are needed.
- Use `convert_all()` when processing folders or queues of files.
- Export Markdown for simple downstream LLM work.
- Export JSON when structure and provenance matter.
- Use `HybridChunker` when token limits are important.
- Use `HierarchicalChunker` when preserving document structure matters more than chunk size.

## Helpful Links

- Official docs: https://docling-project.github.io/docling/
- Supported formats: https://docling-project.github.io/docling/usage/supported_formats/
- Advanced usage: https://docling-project.github.io/docling/usage/advanced_options/
- MCP usage: https://docling-project.github.io/docling/usage/mcp/
