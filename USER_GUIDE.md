# User Guide

This guide is for anyone who wants to update and rebuild this resume without already knowing how the repository is organized.

## What You Edit

The only file you should edit for resume content is [`resume.yaml`](./resume.yaml).

That file is the single source of truth for:

- personal details
- work experience
- projects
- education
- achievements
- PDF metadata
- embedded `resume.json`
- embedded `schema.json`

Do not manually edit these generated files:

- [`sections/header.tex`](./sections/header.tex)
- [`sections/experience.tex`](./sections/experience.tex)
- [`sections/skills.tex`](./sections/skills.tex)
- [`sections/projects.tex`](./sections/projects.tex)
- [`sections/achievements.tex`](./sections/achievements.tex)
- [`sections/education.tex`](./sections/education.tex)
- [`generated/metadata.tex`](./generated/metadata.tex)
- [`resume.json`](./resume.json)
- [`schema.json`](./schema.json)

## Prerequisites

Install these tools first:

- [Docker](https://docs.docker.com/)
- [Git](https://git-scm.com/)
- [yq](https://github.com/mikefarah/yq)
- `python3`
- optionally: `exiftool`
- optionally: `pdfdetach`

Check that the required tools are available:

```sh
python3 --version
yq --version
docker --version
make --version
```

## Editing Resume Content

Open [`resume.yaml`](./resume.yaml) and update the data you want.

Common sections:

- `basics`: name, email, links, location
- `pdf`: title/keywords/metadata fields
- `skills`: grouped skills
- `experience`: jobs and bullets
- `projects`: project entries and bullets
- `education`: education entries
- `achievements`: certifications, awards, coding profiles

### Supported Inline Formatting

Inside prose fields such as experience bullets, project bullets, and achievements, you can use:

- `**bold**`
- `_italic_`
- `[label](https://example.com)`

Example:

```yaml
bullets:
  - "Built an **internal platform** for _faster onboarding_."
  - "Published the project at [example.com](https://example.com)."
```

Do not put raw LaTeX like `\textbf{}` or `\href{}` into `resume.yaml`.

## Build Commands

### Recommended command

After editing [`resume.yaml`](./resume.yaml), run:

```sh
make compile
```

This will:

1. regenerate all derived TeX and JSON files
2. compile the final PDF

### Other useful commands

Generate derived files only:

```sh
make generate
```

Build the Docker image:

```sh
make docker
```

Build Docker image and compile:

```sh
make build
```

Remove generated PDF and LaTeX aux files:

```sh
make clean
```

Clean and recompile:

```sh
make dev
```

Show all available make targets:

```sh
make help
```

## Output

The generated PDF file is:

```sh
Aditya_SWE_Resume_2YOE.pdf
```

## Verifying the Output

Check embedded attachments:

```sh
pdfdetach -list Aditya_SWE_Resume_2YOE.pdf
```

Expected files:

- `resume.json`
- `schema.json`

Inspect XMP metadata:

```sh
exiftool -xmp:all Aditya_SWE_Resume_2YOE.pdf
```

## Troubleshooting

If `make compile` fails:

- ensure `yq` is installed and available in `PATH`
- ensure Docker is running
- ensure the Docker image builds successfully with `make docker`
- check for YAML syntax mistakes in [`resume.yaml`](./resume.yaml)

If you changed [`resume.yaml`](./resume.yaml) and the PDF did not update:

- rerun `make compile`
- check whether the generated section files changed
- confirm the edited field is actually used by the generator

## Repository Structure

Useful files:

- [`resume.yaml`](./resume.yaml): source of truth
- [`scripts/generate_resume.py`](./scripts/generate_resume.py): generator
- [`main.tex`](./main.tex): LaTeX entry point and PDF embedding
- [`formatting.sty`](./formatting.sty): visual styling
- [`README.md`](./README.md): project overview
