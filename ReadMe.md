# Matillion docs staging area

## Overview

This repo hosts the source code for a static site built using MkDocs. The site is hosted on GitHub Pages.

The Matillion docs team can use this site to host previews of its docs, e.g. to share with colleagues, preview updates to text, and so on.

---

## Run the site locally

1. [Make a GitHub account](https://docs.github.com/en/get-started/signing-up-for-github/signing-up-for-a-new-github-account) if you don't have one already.
1. Learn how to [fork a GitHub repo](https://docs.github.com/en/get-started/quickstart/fork-a-repo).
1. Now follow the [installation guide](https://www.mkdocs.org/user-guide/installation/) to check whether you have Python on your machine, and then pip, and once those are installed, scroll down to **Installing MkDocs**.
1. Once you've done all of the above, make sure in your CLI you're at the `docs-previews` directory.
1. Run `mkdocs serve`.
1. Open up `http://127.0.0.1:8000/` in your browser, and you'll see the default home page being displayed.

`http://127.0.0.1:8000/` is a local copy, and will update almost in real time when you save changes to files in this repo on your machine.

## Contribute

1. While in the `docs-previews` directory in your CLI, checkout a new branch while on master, e.g. `git checkout -b david-branch-1`
1. Add or modify some markdown files. You will also need to amend the `mkdocs.yml` file if you wish to situate your new markdown files in the site's nav. Read [_Writing your docs_](https://www.mkdocs.org/user-guide/writing-your-docs/) to learn about this.
1. Save, stage, and commit your changes.
1. Push your changes to remote if you wish to create a PR to be merged into `master`.