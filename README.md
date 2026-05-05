# rngkll.github.io

[![Nikola](https://img.shields.io/badge/built%20with-Nikola-00BFFF)](https://getnikola.com/)
[![CC BY 4.0](https://img.shields.io/badge/License-CC%20BY%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by/4.0/)

Personal blog of Alvaro Segura Del Barco, featuring technical tutorials, recipes, and recommendations on technology, networking, blockchain, and food. Built with Nikola, a static site generator.

## Table of Contents
- [Description](#description)
- [Installation](#installation)
- [Usage](#usage)
- [Features](#features)
- [Contributing](#contributing)
- [License](#license)

## Description
This repository contains the source code for a multilingual (Spanish/English) static site blog. The content covers a mix of technical guides, open-source tool setups, Ethereum blockchain development, networking hacks, and personal interests like recipes and local food recommendations in Costa Rica.

Site URL: [http://rngkll.github.io/](http://rngkll.github.io/)

## Installation
See [AGENTS.md](AGENTS.md) for detailed setup instructions.

Prerequisites:
- Python 3
- Virtual environment

1. Create and activate virtual environment:
   ```bash
   python3 -m venv venv
   source venv/bin/activate
   ```

2. Install Nikola:
   ```bash
   pip install "Nikola[extras]"
   ```

## Usage
### Building the Site
```bash
nikola build
```

### Serving Locally
```bash
nikola serve -b
```

### Deployment
Deploy to GitHub Pages:
```bash
nikola github_deploy
```
Uses configuration from `conf.py`: source branch 'misitio', deploy branch 'master', remote 'origin'.

### Adding Content
- **Posts**: Add files to `posts/` (supports .md, .rst, .txt, .html)
- **Pages**: Add files to `pages/` (same formats)
- **Galleries**: Add to `galleries/`
- **Static files**: Add to `files/`

Include metadata in posts for title, date, tags, etc.

## Features
- **Multilingual Support**: Default language Spanish (`es`), with English (`en`) translations
- **Static Site Generation**: Fast, secure, and scalable with Nikola
- **Theme**: bootblog4
- **Content Types**: Markdown, reStructuredText, HTML
- **Categories and Tags**: Automatic taxonomy generation
- **RSS Feeds**: Available at `/rss.xml`
- **Sitemap**: Generated for SEO

## Contributing
1. Fork the repository
2. Create a new branch for your changes
3. Add posts or pages following the existing structure
4. Test locally with `nikola build` and `nikola serve -b`
5. Submit a pull request

For post metadata, include fields like `title`, `date`, `tags`, and `slug` in the file header or separate `.meta` file.

## License
This work is licensed under [Creative Commons Attribution 4.0 International](https://creativecommons.org/licenses/by/4.0/).

© 2026 Alvaro Segura Del Barco. Code snippets are included for documentation and educational purposes as part of the content.

To reuse, provide attribution as required by the license.

## Contact
- Author: Alvaro Segura Del Barco
- Email: alvarosb@gmail.com
- GitHub: [rngkll](https://github.com/rngkll)</content>
<parameter name="filePath">/Users/asegura/git/rngkll/rngkll.github.io/README.md