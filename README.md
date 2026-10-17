# EthStaker Docs

This is the source code for <https://docs.ethstaker.org>.



## Local Development

To execute/build locally:

1. Create virtual environment: `python3 -m venv venv/`
1. Start the local server: `. venv/bin/activate && pip install -r requirements.txt && zensical serve`
1. Or run each command individually:
    1. Start python virtual environment: `. venv/bin/activate`
    1. Install dependencies: `pip install -r requirements.txt`
    1. Run the script: `zensical serve`
1. Go to <http://127.0.0.1:8000/> to view changes
1. Close virtual environment: `deactivate`

To build the site use `zensical build`.

Resources:

- [MkDocs](https://www.mkdocs.org/user-guide/)
- [Material MkDocs](https://squidfunk.github.io/mkdocs-material/)


