---
inclusion: fileMatch
fileMatchPattern: 'images/**'
---

# Image Optimization SOP

## Purpose

Keep image file sizes reasonable for a git repository. Presentation memes and slides don't need full-resolution originals.

## Tool

Use macOS built-in `sips` (scriptable image processing system). No extra dependencies required.

## Rules

When adding or modifying images in the `images/` directory:

1. **Check dimensions** before staging:
   ```bash
   sips -g pixelWidth -g pixelHeight images/<file>
   ```

2. **Resize if too large** — if the longest side exceeds 1920px:
   ```bash
   sips --resampleHeightWidthMax 1920 images/<file>
   ```

3. **Convert PNG to JPEG** when the image is a photo/meme (not a diagram with transparency needs) and the PNG exceeds 500KB:
   ```bash
   sips -s format jpeg -s formatOptions 80 images/<file>.png --out images/<file>.jpeg
   rm images/<file>.png
   ```

4. **Compress existing JPEGs** that exceed 500KB by re-saving at quality 80:
   ```bash
   sips -s formatOptions 80 images/<file>.jpeg
   ```

5. **Batch check** all images in the directory:
   ```bash
   for f in images/*.{png,jpg,jpeg}; do echo "$f"; sips -g pixelWidth -g pixelHeight -g format "$f" 2>/dev/null; ls -lh "$f" | awk '{print "  Size:", $5}'; echo; done
   ```

## Thresholds

| Metric | Maximum | Action |
|--------|---------|--------|
| Longest side | 1920px | `--resampleHeightWidthMax 1920` |
| File size (JPEG) | 500KB | Re-save at quality 80 |
| File size (PNG, photo) | 500KB | Convert to JPEG at quality 80 |
| File size (PNG, diagram) | 1MB | Resize to max 1920px |

## When to Apply

- Before any `git add` of image files
- When the user adds new images to `images/`
- When asked to optimize or compress images
- Proactively suggest optimization if images look oversized during any task involving the `images/` folder
