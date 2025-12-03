# Presidio: PII Detection & Anonymization

A 2-minute technical overview of Microsoft's Presidio framework for PII detection and anonymization.

## About Presidio

Presidio is an open-source framework that helps organizations identify and remove sensitive information (PII) from text and images through automated detection and anonymization.

## Setup & Usage

### Prerequisites
- Node.js 18+ and npm

### First Time Setup

```bash
cd tech-radar-2025/presidio
npm install
```

### Running the Presentation

```bash
# Development mode with hot reload
npm run dev
```

This will open the slides at http://localhost:3030

### Keyboard Shortcuts
- `Space` / `→` - Next slide
- `←` - Previous slide
- `o` - Slides overview
- `f` - Toggle fullscreen
- `d` - Toggle dark mode
- `c` - Enable camera view
- `g` - Show goto dialog

### Exporting

```bash
# Export to PDF
npm run export-pdf

# Export to PNG images
npm run export

# Build static SPA
npm run build
```

## Presentation Structure

1. **Title** - Introduction
2. **The Privacy Challenge** - Problem statement
3. **What is Presidio** - Overview with code example
4. **Detection Capabilities** - Built-in features
5. **Deployment Flexibility** - How to deploy
6. **Key Use Cases** - When to use it
7. **The Important Caveat** - Limitations warning
8. **Benefits** - Why consider it
9. **Challenges** - What to watch out for
10. **Tech Radar Rating** - Final assessment

**Target Duration:** 2 minutes

## Learn More

- [Presidio GitHub](https://github.com/microsoft/presidio)
- [Slidev Documentation](https://sli.dev/)

## Version Control

All presentation content is in `slides.md` - pure Markdown with YAML frontmatter. Changes are easily tracked in Git with meaningful diffs.
