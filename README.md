# flex-dl

[![PyPI version](https://img.shields.io/pypi/v/kino-flex-dl.svg)](https://pypi.org/project/kino-flex-dl/)
[![Downloads](https://static.pepy.tech/badge/kino-flex-dl)](https://pepy.tech/project/kino-flex-dl)
[![Python versions](https://img.shields.io/pypi/pyversions/kino-flex-dl.svg)](https://pypi.org/project/kino-flex-dl/)
[![License](https://img.shields.io/pypi/l/kino-flex-dl.svg)](https://github.com/ndenissov/flex-dl/blob/main/LICENSE)
[![GitHub stars](https://img.shields.io/github/stars/ndenissov/flex-dl)](https://github.com/ndenissov/flex-dl/stargazers)

CLI tool and Python library for downloading movies, series, and video content from flex-kino.com using `yt-dlp`.

---

## Features

- Flexible episode filtering for TV series (by season and episode ranges or custom lists)
- Custom output directory and file path formatting
- Support for `yt-dlp` stream selection, multi-thread downloading, and dry-run execution
- CLI interface and programmatic Python API

---

## Installation

Install using `pip`:

```bash
pip install kino-flex-dl
```

Or using `poetry`:

```bash
poetry add kino-flex-dl
```

---

## Quick Start

### Command Line Interface

Run using the `kino-flex-dl` entrypoint (or `flex-dl`) or via module execution:

```bash
kino-flex-dl <slug> [options]
```

Or:

```bash
python -m flex_dl <slug> [options]
```

### CLI Arguments

```text
positional arguments:
  slug                  flex-kino.com title slug

options:
  -h, --help            show help message and exit
  -f FORMAT, --format FORMAT
                        download format string passed to yt-dlp
  -s SERIES, --series SERIES
                        series filter ("*[start,[stop,step]]:..." for ranges or "s1,s2:e1,e2|...")
  -v STUDIO, --studio STUDIO
                        studio name, slug, #id or index
  -o OUT, --out OUT     output file path template
  -e EXE, --exe EXE     yt-dlp executable path (default: yt-dlp)
  -x                    multithread yt-dlp execution
  -l                    dry-run mode (print generated commands without running)
```

### Examples

Print yt-dlp download commands without executing them:

```bash
kino-flex-dl movie-slug -l
```

Download specific seasons and episodes:

```bash
kino-flex-dl series-slug -s "1,2:1,2,3" -f "best"
```

---

## Python API Usage

```python
from flex_dl import FlexClient

with FlexClient(print_only=False, executable="yt-dlp") as client:
    client.download(
        slug="series-slug",
        out="{f[original_name]}/{e[season]:0>2}/{e[series]:0>2}.%(ext)s",
        file_format="best",
        filter_episodes=lambda season, episode: season == 1,
        add=[],
    )
```

---

## Requirements

- Python >= 3.8
- `yt-dlp` installed and available in `PATH`

---

## License

Distributed under the MIT License. See [LICENSE](file:///home/nikita/dev/ndenissov/flex-dl/LICENSE) for details.
