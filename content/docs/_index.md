---
title: "Documentation"
date: 2024-05-22T10:45:51+05:30
draft: false
---

## Introduction

HI,Welcome to the Enhancing Disaster Resilience in Eastern Africa (E4DRR) project website! This platform is dedicated to improving disaster management and resilience in Eastern Africa through advanced climate storylines and impact-based forecasting. Our goal is to empower communities with the knowledge and tools they need to better understand and prepare for potential hazards, ultimately benefiting over 200 million people by 2026.

The E4DRR project leverages innovative technology and data-driven approaches to provide timely and accurate information for disaster response efforts. By implementing impact-based forecasting methodologies and offering capacity development programs, we aim to enhance the skills and knowledge of stakeholders involved in disaster management, enabling more efficient and coordinated response strategies.

## Documentation Overview

This documentation page provides comprehensive guidance on how to navigate, contribute to, and maintain the E4DRR project. Whether you are adding new content, editing existing files, or setting up the project locally, this documentation will help you through the process.

### Project Files and Directories

Here’s an overview of the main files and directories in the E4DRR project:

- Archetypes/: Contains the default archetypes for content creation.
- assets/: Houses custom CSS and media files.
- content/: Contains all the Markdown files for the website content, including blogs and homepage content.
- layouts/: Holds the HTML templates and partials used to render the site.

* static/: Stores static assets such as images and fonts.
* config.yaml: The main configuration file for the Hugo site.
* .github/: Contains GitHub Actions workflows for continuous deployment.
* README.md: Provides a brief overview of the project and setup instructions.

### Key Sections of the Documentation

- Adding New Blogs: Instructions on how to create and publish new blog posts.
- Editing Files: Guidelines for editing content and configuration files.
- Running a Local Test Setup: Steps to set up and run the project locally using Hugo.
- Deployment: Information on how the site is deployed using GitHub Actions.
- Troubleshooting: Common issues and their solutions.
- Contributing: How to contribute to the project, including forking the repository and submitting pull requests.

  We hope this documentation makes it easy for you to contribute to the E4DRR project and helps ensure the successful deployment and maintenance of the site. If you have any questions or need further assistance, please refer to the [Hugo Documentation](https://gohugo.io/documentation/) or reach out to the hugo support team.

## Adding New Blogs

To add a new blog post, follow these steps:

1. Navigate to the `content/blog/` directory.
2. Create a new Markdown file with a descriptive name, e.g., `new-blog-post.md`.
3. Add the following front matter at the top of the file:

```
---
title: "Your Blog Title"
date: YYYY-MM-DD
draft: false
---

```

4. Write your blog content in Markdown format, including any images or code snippets.

```
    ## Introduction

    This is the introduction to your new blog post.

    ## Main Content

    Here is where you write the main content of your blog post.


```

5. Save the file. Your new blog post will be included in the site build.

### Editing Files

To edit existing files, navigate to the relevant directory and open the file in your preferred text editor. Common files you might need to edit include:

- `content/_index.md`: Edit the homepage content.
- `config.yaml`: Update site configuration settings.

## Running a Local Test Setup

To run a test setup locally, ensure you have [Hugo](https://gohugo.io/getting-started/installing/) installed on your machine. Then, follow these steps:

1. Open your terminal or command prompt.
2. Navigate to the project directory:

```
   cd path/to/E4DRR.github.io

```

3. Start the Hugo server:

```
    hugo server
```

4. Open your web browser and navigate to the local server address displayed in the terminal to view the site.

## Deployment

The project is configured to deploy using GitHub Actions. Follow these steps to ensure successful deployment:

1. Ensure GitHub Pages is enabled in your repository settings and configured to use the `gh-pages` branch.
2. Push your changes to the `main` branch. GitHub Actions will automatically build and deploy the site.

The GitHub Actions workflow file `.github/workflows/gh-pages.yml` is configured as follows:

```
name: Deploy website to GitHub Pages

env:
  WC_HUGO_VERSION: "0.125.2"

on:
  # Trigger the workflow every time you push to the `main` branch
  push:
    branches: ["main"]
  # Allows you to run this workflow manually from the Actions tab on GitHub.
  workflow_dispatch:

# Provide permission to clone the repo and deploy it to GitHub Pages
permissions:
  contents: read
  pages: write
  id-token: write

concurrency:
  group: "pages"
  cancel-in-progress: false

jobs:
  # Build website
  build:
    if: github.repository_owner != 'HugoBlox'
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4
        with:
          # Fetch history for Hugo's .GitInfo and .Lastmod
          fetch-depth: 0
      - name: Setup Hugo
        uses: peaceiris/actions-hugo@v3
        with:
          hugo-version: ${{ env.WC_HUGO_VERSION }}
          extended: true
      - uses: actions/cache@v4
        with:
          path: /tmp/hugo_cache_runner/
          key: ${{ runner.os }}-hugomod-${{ hashFiles('**/go.mod') }}
          restore-keys: |
            ${{ runner.os }}-hugomod-
      - name: Setup Pages
        id: pages
        uses: actions/configure-pages@v5
      - name: Build with Hugo
        env:
          HUGO_ENVIRONMENT: production
        run: |
          echo "Hugo Cache Dir: $(hugo config | grep cachedir)"
          hugo --minify --baseURL "${{ steps.pages.outputs.base_url }}/"
      - name: Generate Pagefind search index
        run: npx pagefind --source "public"
      - name: Upload artifact
        uses: actions/upload-pages-artifact@v3
        with:
          path: ./public

  # Deploy website to GitHub Pages hosting
  deploy:
    if: github.repository_owner != 'HugoBlox'
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    needs: build
    steps:
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v4

```

3. Monitor the GitHub Actions workflow under the "Actions" tab in your repository to ensure the build and deployment processes complete successfully.

4. Once the workflow completes, your site should be live on GitHub Pages. You can verify this by visiting the URL specified in your repository's GitHub Pages settings.

## Troubleshooting

### Common Issues and Solutions

#### Error: nil pointer evaluating resource.Resource.Process

- **Cause:** This error typically occurs when an image or resource is not correctly referenced in the template or content files. Hugo is trying to process a resource that doesn't exist or is incorrectly specified, leading to a nil pointer evaluation.
- **Solution:**
  1. **Check References:** Ensure that all images and resources are correctly referenced in your content files. Verify that the paths are accurate and relative to the site's root or the specific page.
  2. **File Existence:** Confirm that the referenced files actually exist in the specified directories.
  3. **Debugging:** Add debug statements or logs in your templates to trace where the nil pointer is occurring. This can help identify the exact reference causing the issue.
  4. **Example Fix:**
     ```markdown
     ![Alt text](/images/example.jpg)
     ```
     Ensure `/images/example.jpg` exists in the `static` directory of your Hugo project.

#### Error: No such file or directory @ dir_chdir

- **Cause:** This error indicates that the specified directory does not exist or the path is incorrect in your configuration or script. It often happens when the deployment or build scripts are looking for a directory that hasn't been created or is misnamed.
- **Solution:**
  1. **Verify Paths:** Double-check all directory paths specified in your configuration files (e.g., `config.toml`, `config.yaml`) and deployment scripts.
  2. **Create Missing Directories:** Ensure that all required directories are created before running the build or deployment process. For example, if a directory is dynamically created during the build process, make sure the script includes steps to create it.
  3. **Correct Directory Names:** Ensure there are no typos or case sensitivity issues in the directory names.
  4. **Example Fix:**
     ```yaml
     destination: /github/workspace/docs/_site
     ```
     Ensure `/github/workspace/docs` exists and is correctly named.

#### GitHub Pages build failure

- **Cause:** Build failures on GitHub Pages can be due to several issues, including misconfigurations in the GitHub Actions workflow file, incorrect repository settings, or issues with the Hugo site configuration.
- **Solution:**

  1. **Workflow Configuration:**

     - Ensure that your GitHub Actions workflow file (`.github/workflows/gh-pages.yml`) is correctly set up. Check for syntax errors and ensure all necessary steps are included.
     - Example snippet:

       ```yaml
       name: Deploy Hugo site to Pages

       on:
         push:
           branches:
             - main # Set to the branch you want to deploy from

       jobs:
         build:
           runs-on: ubuntu-latest

           steps:
             - name: Checkout repository
               uses: actions/checkout@v2

             - name: Setup Hugo
               uses: peaceiris/actions-hugo@v2
               with:
                 hugo-version: "0.125.5"
                 extended: true

             - name: Build the site
               run: hugo --minify

             - name: Deploy to GitHub Pages
               uses: peaceiris/actions-gh-pages@v3
               with:
                 github_token: ${{ secrets.GITHUB_TOKEN }}
                 publish_dir: ./public
       ```

  2. **GitHub Pages Settings:**
     - Ensure GitHub Pages is enabled in your repository settings. Navigate to the repository's settings, find the "Pages" section, and make sure it is set to build from the `gh-pages` branch or any other branch you specified.
  3. **Check Repository Configuration:**
     - Verify that the branch specified in the workflow (`main` in the example) is correct and matches the branch from which you are pushing changes.
     - Ensure the `publish_dir` specified in the workflow matches the output directory of your Hugo build.
  4. **Debug Logs:**
     - Enable debug logs in your GitHub Actions workflow to get more detailed error messages. This can help identify specific issues during the build or deployment process.

## Frequently Asked Questions (FAQs)

### Q: How do I change the site’s theme?

**A:** To change the site’s theme, follow these steps:

1. **Update the Configuration File:**

   - Open the `config.yaml` (or `config.toml`) file in your project.
   - Update the `theme` field to the name of the new theme. For example:
     ```yaml
     theme: new-theme-name
     ```

2. **Include Theme Files:**

   - Ensure that the new theme’s files are included in the project. You can download the theme from the [Hugo themes repository](https://themes.gohugo.io/) and place it in the `themes/` directory of your project.

3. **Check Theme Documentation:**
   - Refer to the new theme’s documentation for any additional setup steps or configuration options.

### Q: How can I add images to my blog posts?

**A:** To add images to your blog posts, follow these steps:

1. **Place Images in Static Directory:**

   - Save your images in the `static/images/` directory of your project.

2. **Reference Images in Markdown:**
   - In your Markdown files, reference the images using relative paths. For example:
     ```markdown
     ![Alt text](images/your-image.jpg)
     ```

### Q: How do I customize the site's navigation menu?

**A:** To customize the navigation menu, follow these steps:

1. **Edit the Configuration File:**

   - Open the `config.yaml` (or `config.toml`) file.
   - Locate the `menu` section and add or modify menu items. For example:
     ```yaml
     menu:
       main:
         - identifier: about
           name: About
           url: /about/
           weight: 1
         - identifier: blog
           name: Blog
           url: /blog/
           weight: 2
     ```

2. **Save and Preview:**
   - Save your changes and preview the site to ensure the navigation menu is updated as expected .

We hope this documentation makes it easy for you to contribute to the E4DRR project and helps ensure the successful deployment and maintenance of the site. If you have any questions or need further assistance, please refer to the [Hugo Documentation](https://gohugo.io/documentation/) or reach out to our support team.
