# 🚀 How to Create and Publish a Website Using GitHub Pages and Jekyll

## Overview
This tutorial walks beginners through creating and publishing a simple personal website using **GitHub Pages**, **Jekyll**, and **basic Git command-line workflows**.

By the end, you will have:
- A live website online  
- A repository that hosts your site  
- A Jekyll theme applied  
- Markdown content rendered into a styled webpage  

**Audience:** Beginners with basic computer skills, learning Git/GitHub and web documentation workflows.  
**Tools Used:** GitHub, Git, command line, Jekyll (GitHub Pages–hosted version), YAML, Markdown.

---

# 1. Prerequisites

Before starting, ensure you have:

### ✔ Git installed
Download from: https://git-scm.com/downloads

### ✔ A GitHub account
Sign up: https://github.com/

### ✔ A code/text editor  
Examples: Visual Studio Code, Sublime Text, Atom.

### ✔ Basic familiarity with the terminal  
You will run simple commands like:
```
git clone
git add
git commit
git push
```

---

# 2. Create Your GitHub Pages Repository

1. Log into GitHub.  
2. Click **New Repository**.  
   > **Screenshot Placeholder:** GitHub → "+" → "New repository"  

3. Name your repository:

```
yourusername.github.io
```

This naming format is required for GitHub Pages user sites.

4. Set visibility to **Public**.  
5. Do **not** initialize with a README (we’ll add files manually).  
6. Click **Create repository**.

> **Screenshot Placeholder:** New repo form with correct settings  

---

## 3. Clone the Repository (Terminal Only)

🖥 **Where this step happens:** Terminal / Command Prompt<br />

Run the following command in your terminal (replace with your actual username):

```bash
git clone https://github.com/YOUR_USERNAME/YOUR_USERNAME.github.io
```

This downloads your repository and creates a **new folder** on your computer with the same name as the repo.

Next, still in the terminal, move into that folder:

```bash
cd YOUR_USERNAME.github.io
```

> **Tip:** If `cd` doesn't work, run `ls` (Mac/Linux/Git Bash) or `dir` (Windows) to confirm the folder name.

---

## 4. Add the Jekyll Theme (Code Editor Only)

📝 **Where this step happens:** Your code editor (VS Code, Sublime Text, etc.)

1. Open your code editor.  
2. Open the cloned folder (`YOUR_USERNAME.github.io`).  
3. Create a new file named:

```
_config.yml
```

4. Paste the following YAML into the file:

```yaml
title: My Portfolio
description: A simple website built with GitHub Pages and Jekyll.
theme: minima
```

5. Save the file.

This file tells GitHub Pages which theme to apply to your site.


**Explanation:**
- `theme:` sets your site’s look and layout  
- `title:` appears in site header/title  
- `description:` appears in metadata  

> **Screenshot Placeholder:** Editor showing a `_config.yml` file  

---

# 5. Create Your Homepage Using `index.md`

📝 **Where this step happens:** Your code editor (VS Code, Sublime Text, etc.)  

Create a file named:

```
index.md
```

Add:

```markdown
---
layout: home
title: Welcome
---

# Welcome to My Portfolio

This site is powered by **GitHub Pages** and styled with the **Minima** Jekyll theme.

Here you'll find examples of my technical writing, tutorials, and documentation projects.
```

This Markdown file becomes your homepage.

> **Screenshot Placeholder:** Editor showing `index.md` with front matter  

---

# 6. Commit and Push Your Changes

In the terminal:

```
git add .
git commit -m "Initial site files"
git push origin main
```

If your default branch is `master`, replace `main` with `master`.

> **Screenshot Placeholder:** Terminal with `git add`, `git commit`, `git push`  

---

# 7. Enable GitHub Pages

1. Go to your repository on GitHub.  
2. Click **Settings** → **Pages**.  
   > **Screenshot Placeholder:** GitHub → Settings → Pages  

3. Under **Source**, choose:
- Branch: `main`
- Folder: `/ (root)`

4. Click **Save**.

GitHub will now build your site.

> **Screenshot Placeholder:** GitHub Pages configuration page  

---

# 8. View Your Live Website

After a few moments, your site will appear at:

```
https://yourusername.github.io
```

If it doesn’t load immediately:
- Wait 1–2 minutes  
- Refresh your browser  
- Verify the Pages settings  

> **Screenshot Placeholder:** Browser showing the published site  

---

# 9. Optional Enhancements

### Add an About Page
Create `about.md`:

```markdown
---
layout: page
title: About
---

# About Me
I’m a technical writer specializing in audio, web, and software documentation.
```

Link it from your homepage or navigation.

---

### Add navigation links (Minima theme)
Add this to `_config.yml`:

```yaml
header_pages:
  - index.md
  - about.md
```

---

### Add images
Create an `/assets` folder and reference images like:

```markdown
![My photo](/assets/profile.jpg)
```

---

### Customize theme colors (advanced)
You can override CSS by adding files under `/assets/css/`.

---

# 10. Troubleshooting

| Issue | Cause | Solution |
|------|--------|----------|
| Site shows 404 | Pages not enabled | Check Settings → Pages |
| YAML error | Incorrect spacing/indentation | Use spaces, not tabs |
| Theme not applying | Wrong theme name | Use only supported GitHub Pages themes |
| Changes not updating | Cached build or commit not pushed | Refresh / run `git push` |
| Build failed | Unsupported plugin | Remove plugins from `_config.yml` |

---

# Conclusion

You now have a **live GitHub Pages website** built using **Jekyll** and managed with **Git**. This setup is widely used in professional documentation teams, so completing this tutorial demonstrates:

- Git and GitHub command workflows  
- Use of Markdown  
- Use of YAML configuration  
- Ability to publish and maintain web documentation  
- Understanding of static site generators  

Perfect for showcasing in a technical writing portfolio.

---
