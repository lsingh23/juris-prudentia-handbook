# Juris Prudentia Handbook

An interactive study companion to **Paper I: Jurisprudence** (LL.B. 1st Year, First Semester, Lucknow University), built around Dr N.V. Paranjape, *Studies in Jurisprudence & Legal Theory*. Plain static HTML with inline CSS and JS: no build step, no dependencies beyond Google Fonts.

## Folder layout

```
index.html          Hub: all four units, topic links, exam kits, reading progress
.nojekyll           Tells GitHub Pages to serve files as-is (no Jekyll)
STYLE-NOTES.md      Conventions for building and editing pages
unit-1/ … unit-4/   One folder per unit
  index.html        Unit landing page
  <topic>.html      One lesson per syllabus topic
  exam.html         Exam kit for the unit
```

Units: I Introduction to Jurisprudence · II Schools of Legal Theory · III Basic Concepts of Law · IV Justice and Contemporary Issues.

Reading progress ("Mark chapter as read") is stored in the browser's localStorage only.

## Publish on GitHub Pages

1. Create a GitHub repository and push this folder to its `main` branch, with `index.html` at the repo root.
2. In the repository, open **Settings → Pages**.
3. Under **Build and deployment**, choose **Source: Deploy from a branch**, then **Branch: `main`**, folder **`/ (root)`**, and save.
4. After a minute the site is live at `https://<username>.github.io/<repo>/`.

All links are relative, so the site also works when opened locally from disk.
