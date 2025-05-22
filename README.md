# Tech Forward Blog - A Jamstack Blog with Hugo and GitHub Pages

Welcome to your Tech Forward Blog! This project provides a modern, deployable template for a technical blog focusing on cutting-edge topics such as Artificial Intelligence, advanced programming techniques, Vector Databases, Large Language Models (LLMs), DevOps methodologies, and Cloud-Native architectures. 

Built with [Hugo](https://gohugo.io/) and the [PaperMod](https://github.com/adityatelange/hugo-PaperMod) theme, this blog is designed for fast performance, easy content creation using Markdown, and seamless automated deployment via GitHub Actions to GitHub Pages. The visual style is a "future tech/AI vibe" with a dark theme and syntax highlighting.

## Project Structure

```
.
├── archetypes/         # Content templates (default.md for new posts)
├── assets/             # For Hugo Pipes processed assets (like custom CSS)
│   └── css/extended/
│       └── custom.css  # Your custom CSS overrides
├── content/
│   └── blog/           # Your Markdown blog posts reside here
├── data/               # Data files for Hugo
├── .github/
│   └── workflows/
│       └── deploy.yml  # GitHub Actions workflow for auto-deployment
├── layouts/            # Custom layouts (if any, currently relying on theme)
├── static/             # Static assets (images, favicons, etc.)
│   └── assets/         # User-added static files (e.g., images go here)
├── themes/             # Hugo themes (PaperMod is added via Hugo Modules in CI)
├── go.mod              # Hugo Modules file (defines theme dependency)
├── go.sum              # Hugo Modules checksums
├── hugo.yaml           # Main Hugo configuration file
└── README.md           # This file
```

## Local Development

To run and develop this blog locally:

1.  **Install Hugo:**
    Follow the official Hugo installation guide: [https://gohugo.io/installation/](https://gohugo.io/installation/)
    Make sure to install the **extended version** as PaperMod requires it. The CI workflow currently uses Hugo `latest`.

2.  **Install Go (Golang):**
    Hugo Modules require Go. Install Go from [https://go.dev/doc/install](https://go.dev/doc/install). Version 1.19+ is recommended (CI uses 1.21).

3.  **Clone the Repository:**
    ```bash
    git clone https://github.com/clarencechien/staticsite.git # Replace with your repo if forked
    cd staticsite
    ```

4.  **Download Theme & Dependencies:**
    Hugo uses Go Modules to manage themes. Run the following command in the project root:
    ```bash
    hugo mod tidy
    # You might also run `hugo mod get -u` if you want to ensure all modules are up-to-date
    ```
    This will download the theme (PaperMod) and other dependencies into your local Hugo module cache and update `go.mod` and `go.sum`.

5.  **Run the Hugo Development Server:**
    ```bash
    hugo server
    ```
    This will start a local server, usually at `http://localhost:1313/`. The site will automatically rebuild when you make changes.
    To include draft posts, run `hugo server -D`.

## Writing a New Blog Post

1.  **Create a New Markdown File:**
    You can manually create a new `.md` file in the `content/blog/` directory.
    Or, use the Hugo CLI (from the root of your project):
    ```bash
    hugo new content blog/my-new-post.md 
    ```
    This uses `archetypes/default.md` to pre-populate front matter.

2.  **Edit Front Matter:**
    Open the new Markdown file (e.g., `content/blog/my-new-post.md`) and update the front matter:
    ```yaml
    ---
    title: "Your Awesome Post Title"
    date: YYYY-MM-DD # Set the publication date, e.g., 2024-05-22
    tags: ["tag1", "tag2", "relevant-tech"]
    description: "A brief summary of your post for SEO and previews."
    draft: false # Set to false when ready to publish
    ---
    ```

3.  **Write Content:**
    Use Markdown for your post.

    **Code Blocks:**
    ````markdown
    ```python
    def hello_world():
        print("Hello from your tech blog!")
    ```
    ````

    **Images:**
    Place images in `static/assets/images/` (create the `images` subfolder if needed).
    Reference them like this:
    ```markdown
    ![Alt text for image](/assets/images/your-image-name.png) 
    ```
    (Note: The path starts with `/assets/` because files in `static/assets/` are served from `/assets/` at the site root).

## Deployment

Deployment is automated via GitHub Actions using `.github/workflows/deploy.yml`.

1.  **Commit and Push Changes:**
    Push changes to the `main` branch:
    ```bash
    git add .
    git commit -m "Add new blog post: Your Title"
    git push origin main
    ```

2.  **Automatic Build and Deploy:**
    The push triggers the GitHub Action, which builds the Hugo site and deploys it to the `gh-pages` branch.

## GitHub Pages Configuration

For the deployed site to be accessible at `https://clarencechien.github.io/staticsite/`:

1.  **Go to Repository Settings:** On GitHub, navigate to your `clarencechien/staticsite` repository. Go to "Settings" > "Pages".
2.  **Source:** Under "Build and deployment", ensure the "Source" is set to **"Deploy from a branch"**.
3.  **Branch:**
    *   Select `gh-pages` as the branch.
    *   Select `/ (root)` as the folder.
    *   Click "Save".

It might take a few minutes for GitHub Pages to update and for your site to become live after a deployment or after changing these settings. If you see a 404 error after a successful deployment, double-check these settings and allow some time.

## Customization

*   **Configuration:** Modify `hugo.yaml` for site-wide settings, menus, and PaperMod theme parameters. The `baseURL` is already set for your GitHub Pages site.
*   **Styling:** Add custom CSS to `assets/css/extended/custom.css`. PaperMod automatically includes this.
*   **Favicons:** Update favicon links in `hugo.yaml` (`params.assets`) and place your favicon files in the `static/` directory (e.g., `static/favicon.ico`).

Happy blogging!
