# Engineering Blog Setup & Deployment

This repository holds the source code and configuration for my professional Engineering Blog, powered by [MkDocs](https://www.mkdocs.org/) and the [Material for MkDocs](https://squidfunk.github.io/mkdocs-material/) theme.

## 🚀 Setup Local Development

To run this blog locally, ensure you have Python installed, then follow these steps:

1. **Install Dependencies:**
   Run the following pip command to install the required static site generator and the Material theme.

   ```bash
   pip install -r requirements.txt
   # OR directly:
   # pip install mkdocs mkdocs-material mkdocs-mermaid2-plugin pymdown-extensions
   ```

2. **Serve the Blog Locally:**
   Start the local development server. This features hot-reloading, meaning any markdown changes will instantly appear in your browser.
   ```bash
   mkdocs serve
   ```
   Preview the blog at: `http://127.0.0.1:8000/`

---

## 🛠️ How to Add Content

The site is built entirely using simple Markdown (`.md`) files inside the `docs/` directory.

### 1. Create a Post

To add a new project deep-dive:

1. Create a new markdown file in `docs/projects/` (e.g., `docs/projects/new-app.md`).
2. Write your content using standard markdown. The Material theme supports code blocks, GitHub alerts, tables, and Mermaid graphs automatically!

### 2. Update Navigation

To make sure your new post appears in the sidebar and top navigation:

1. Open the `mkdocs.yml` file in the root directory.
2. Under the `nav:` section, link your new file under the appropriate category:
   ```yaml
   nav:
     - Home: index.md
     - Projects:
         - My New App: projects/new-app.md
         - Flux RAG Assistant: projects/flux-rag-assistant.md
   ```

---

## 🚀 Deployment to GitHub Pages

This blog is configured to deploy directly to GitHub Pages for free, performant static hosting.

### Understand GitHub Pages Hosting

When you run the deploy command, MkDocs will compile all your markdown into static HTML/CSS/JS files and push them to a hidden branch (usually `gh-pages` or `main` depending on your repo). GitHub reads this branch and hosts the HTML globally via its CDN.

### How to Deploy

Ensure your code is pushed to your GitHub repository first. Then run:

```bash
mkdocs gh-deploy
```

This command automatically builds your site and pushes the static files to the `gh-pages` branch. Wait 1-2 minutes, and your live URL will reflect the latest changes!
