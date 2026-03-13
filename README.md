# bootstrap5-template

[bootstrap5-template](https://github.com/thecdil/bootstrap-template) is a basic template repository to create a [Bootstrap 5](https://getbootstrap.com/) site using Jekyll on GitHub Pages (or where every you want to host it). 
The layout is based on the [Bootstrap starter template example](https://getbootstrap.com/docs/5.3/examples/) with a navbar, search box (using lunr.js), and footer.
It is intended as a quick starting point for creating new web projects.

Demo: <https://thecdil.github.io/bootstrap5-template/>

*Please note: if you are looking for older bootstrap 4 version, see [bootstrap-template](https://github.com/thecdil/bootstrap-template).*

## Get Started 

- Click green "Use this template" button to make a copy of the code in your own repository (alternatively, use Import or manually copy files)
- Edit `_config.yml` with your site information
- In your new repository visit "Settings" > "Pages" to activate GitHub Pages
- Edit and create pages in the "pages" folder (probably in Markdown). Use each page's yaml front matter to populate the navbar:
    - `title` will appear as h1 at top of the page content.
    - `nav` if this option has a value, it will appear in the navbar as link to this page.
    - `nav_order` navbar items will be sorted using this number. 
- Use "includes" to simplify adding Bootstrap features to Markdown pages (see comments in the "_include/" files for instructions).

See [docs/create-website.md](https://github.com/thecdil/bootstrap5-template/blob/main/docs/create-website.md) for more details.

## Customize 

- Tweak base variables in `assets/css/main.scss` (text color, link color, container size)
- Tweak bootstrap theme colors using `_data/theme-colors.csv` (add a css color in the color column next to the BS color-class to override, or create a new class name. This will generate btn-, text-, and bg- classes.)
- Add custom CSS to `_sass/_custom.scss` (content of `_sass/_template.scss` relates to template components)
- Use Bootstrap to customize `_layouts/` and `_includes/template/`.

## Blog System

This site includes a built-in blog system powered by Jekyll. The blog can be accessed via the "Blog" link in the navigation menu.

### Adding New Blog Posts

To create a new blog post:

1. **Create a new file** in the `_posts/` directory following Jekyll's naming convention:
   ```
   YYYY-MM-DD-title-with-hyphens.md
   ```
   Example: `2024-12-15-my-new-blog-post.md`

2. **Add front matter** at the top of your file:
   ```yaml
   ---
   layout: post
   title: "Your Blog Post Title"
   date: 2024-12-15 10:30:00 +0530
   author: "Your Name"
   tags: [tag1, tag2, tag3]
   excerpt: "A brief description of your post that appears in the blog index."
   ---
   ```

3. **Write your content** in Markdown format below the front matter. You can use:
   - Headers (`# ## ###`)
   - Code blocks with syntax highlighting (```language)
   - Lists, links, images, and other Markdown features
   - HTML when needed for advanced formatting

4. **Preview your post** by running `bundle exec jekyll serve` locally and visiting `http://localhost:4000/blog/`

### Blog Features

- **Responsive design** with Bootstrap 5 styling
- **Syntax highlighting** for code blocks
- **Tag system** for categorizing posts
- **Post navigation** (Previous/Next links)
- **SEO-friendly** URLs and meta tags
- **RSS feed** automatically generated
- **Search functionality** (posts are included in site search)

### Example Blog Post Structure

```markdown
---
layout: post
title: "Getting Started with Azure DevOps"
date: 2024-12-15 14:20:00 +0530
author: "Jijith MS"
tags: [azure, devops, ci-cd, automation]
excerpt: "Learn how to set up CI/CD pipelines in Azure DevOps for automated deployments."
---

# Getting Started with Azure DevOps

Your content goes here...

## Code Example

```yaml
trigger:
- main

pool:
  vmImage: 'ubuntu-latest'

steps:
- task: DotNetCoreCLI@2
  inputs:
    command: 'build'
```

## Conclusion

Wrap up your thoughts here.
```

## Template Assets

Included in assets/lib folder:

- [Bootstrap](https://getbootstrap.com/docs/5.1/getting-started/introduction/) 5.3.2
- [Bootstrap Icons](https://icons.getbootstrap.com/) 1.11.2
- [lunr.js](https://lunrjs.com/) 2.3.9
- [lazysizes](https://github.com/aFarkas/lazysizes) 5.3.2
