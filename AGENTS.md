# AGENTS.md

## Setup
- Activate virtual environment before running Nikola commands: `source venv/bin/activate`
- Install Nikola with extras: `pip install "Nikola[extras]"`

## Building and Serving
- Build site: `nikola build`
- Serve locally: `nikola serve -b`

## Deployment
- Deploy to GitHub Pages: `nikola github_deploy`
- Uses config from conf.py: source branch 'misitio', deploy branch 'master', remote 'origin'

## Content Structure
- Posts in `posts/` (supports .rst, .txt, .html, .md)
- Pages in `pages/` (same formats)
- Galleries in `galleries/`
- Static files in `files/`
- Output to `output/`

## Quirks
- Multilingual site: default 'es', also 'en'
- Theme: 'monospace'
- Pretty URLs disabled, strip indexes disabled