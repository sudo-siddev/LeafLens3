# Quick Fix for Render Deployment

## The Problem
Render can't find the `App` directory because your repository structure has `App/` as a subdirectory.

## Solution: Update Render Settings

### Step 1: Change Root Directory Setting

1. Go to [Render Dashboard](https://dashboard.render.com)
2. Click on your **leaflens** service
3. Go to **Settings** tab
4. Scroll to **"Root Directory"**
5. **DELETE** the value `App` (make it empty/blank)
6. Click **Save Changes**

### Step 2: Update Build & Start Commands

**Build Command:**
```bash
pip install -r requirements.txt
```

**Start Command:**
```bash
cd App && gunicorn app:app
```

OR leave Start Command blank - the Procfile I created will handle it.

### Step 3: Commit and Push

The files I created at the root level need to be committed:

```bash
git add Procfile requirements.txt runtime.txt render.yaml
git commit -m "Add root-level deployment files for Render"
git push origin main
```

### Step 4: Redeploy

Render will automatically redeploy when you push. Or manually trigger a deploy from the dashboard.

## Alternative: If Above Doesn't Work

If the `cd App &&` approach doesn't work, try this Start Command instead:

```bash
PYTHONPATH=/opt/render/project/src/App:$PYTHONPATH gunicorn app:app --chdir App
```

## Verify Your Repository Structure

Make sure your GitHub repo has this structure:
```
leaflens-2/
├── App/
│   ├── app.py
│   ├── templates/
│   ├── static/
│   ├── trained_model.pth
│   └── ...
├── Procfile          ← NEW (at root)
├── requirements.txt  ← NEW (at root)
├── runtime.txt       ← NEW (at root)
└── render.yaml       ← NEW (at root)
```

## Summary

**Root Directory in Render:** Leave EMPTY (not "App")

**Start Command:** `cd App && gunicorn app:app` OR use Procfile

This tells Render to:
1. Build from root directory
2. Install dependencies from root `requirements.txt`
3. Change to `App/` directory
4. Run gunicorn from there

