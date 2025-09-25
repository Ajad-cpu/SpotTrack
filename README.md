# Fix README screenshot links — commands & patch

Use these commands from your repo root (Git Bash). They rename screenshots (if they exist with spaces), update `README.md`, commit and push.

---

## Quick diagnosis

```bash
ls -la MOT16_eval
git ls-files MOT16_eval
git status -- MOT16_eval README.md
git lfs ls-files || true
grep -n "Screenshot 2025-08-19" README.md || true
```

---

## Recommended: rename files and update README (Option A)

```bash
# 1) check files
ls -la MOT16_eval
git ls-files MOT16_eval
git status -- MOT16_eval README.md

# 2) if files with spaces exist locally, rename them
git mv "MOT16_eval/Screenshot 2025-08-19 193426.png" MOT16_eval/Screenshot-2025-08-19-193426.png || true
git mv "MOT16_eval/Screenshot 2025-08-19 193451.png" MOT16_eval/Screenshot-2025-08-19-193451.png || true
git mv "MOT16_eval/Screenshot 2025-08-19 193531.png" MOT16_eval/Screenshot-2025-08-19-193531.png || true

# 3) update README in-place
perl -0777 -pe 's/MOT16_eval\/Screenshot 2025-08-19 193426.png/MOT16_eval\/Screenshot-2025-08-19-193426.png/g;
                s/MOT16_eval\/Screenshot 2025-08-19 193451.png/MOT16_eval\/Screenshot-2025-08-19-193451.png/g;
                s/MOT16_eval\/Screenshot 2025-08-19 193531.png/MOT16_eval\/Screenshot-2025-08-19-193531.png/g' -i README.md

# 4) add, commit, push
git add MOT16_eval/*.png README.md
git commit -m "Fix README image links; rename screenshots to remove spaces"
git push
```

**If the image files are not present locally**, copy them into `MOT16_eval/` first, then run the `git add` step:

```bash
cp "/path/to/Screenshot 2025-08-19 193426.png" MOT16_eval/
cp "/path/to/Screenshot 2025-08-19 193451.png" MOT16_eval/
cp "/path/to/Screenshot 2025-08-19 193531.png" MOT16_eval/
# then add, commit, push
git add MOT16_eval/*.png README.md
git commit -m "Add demo screenshots"
git push
```

---

## Alternative: apply patch to README only (Option B)

Save the block below as `fix-screenshots.patch` and run:

```bash
git apply fix-screenshots.patch
git add README.md
git commit -m "Fix README image links"
git push
```

Patch content (save as `fix-screenshots.patch`):

```diff
*** Begin Patch
*** Update File: README.md
@@
-Demo 1 - ![Alt Text](MOT16_eval/Screenshot 2025-08-19 193426.png) Demo 2 - ![Alt Text](MOT16_eval/Screenshot 2025-08-19 193451.png)
-Demo 3 - ![Alt Text](MOT16_eval/Screenshot 2025-08-19 193531.png)
+Demo 1 - ![Demo 1](MOT16_eval/Screenshot-2025-08-19-193426.png)
+Demo 2 - ![Demo 2](MOT16_eval/Screenshot-2025-08-19-193451.png)
+Demo 3 - ![Demo 3](MOT16_eval/Screenshot-2025-08-19-193531.png)
*** End Patch
```

> Note: Option B only updates `README.md`. If your repo contains files with spaces, run the `git mv` commands from Option A first (or copy the correctly named files into `MOT16_eval/`).

---

## Git LFS

If the PNGs were committed with Git LFS but objects are missing, run:

```bash
git lfs pull
git lfs ls-files
```

---

If you want, I can also generate a combined patch that renames the files and updates README so you can `git apply` it. Reply `patch please` and I will produce it.
