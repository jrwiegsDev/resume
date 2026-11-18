# Resume

My resume, kept as code. The content lives in one YAML file, [RenderCV](https://github.com/rendercv/rendercv) turns it into a PDF, and GitHub Actions publishes a fresh PDF on every push to `main`.

**Latest PDF:** [jrwportfolio.com/resume](https://www.jrwportfolio.com/resume)

## Why

My resume used to live in a Word document. Every change meant editing it, exporting a PDF and uploading that PDF everywhere it was linked. Now there is one source file with its full history in git, and one link that always serves the newest build.

## How it works

| Piece | What it does |
|---|---|
| `Joe_Wiegert_CV.yaml` | All of the content (experience, projects, skills, education) plus the layout settings |
| `pyproject.toml`, `uv.lock` | Pin RenderCV 2.8 so every build uses exactly the same version |
| `.github/workflows/build.yml` | On every push to `main`: install RenderCV with uv, render the PDF, save it as a workflow artifact, and publish it to a new GitHub Release marked latest |

Each release attaches the PDF as `Joe_Wiegert_Resume.pdf`, so this URL always downloads the newest build:

```
https://github.com/jrwiegsDev/resume/releases/latest/download/Joe_Wiegert_Resume.pdf
```

`jrwportfolio.com/resume` redirects to it.

## Building it locally

Requires [uv](https://docs.astral.sh/uv/).

```
uv run rendercv render Joe_Wiegert_CV.yaml
```

The PDF lands in `rendercv_output/`, which git ignores. Add `--watch` to rebuild every time the YAML is saved.

## License

The build setup is under the [MIT License](LICENSE). The resume content itself is mine.
