# Fix for Render Deployment Error

## Problem
```
Root directory "App" does not exist
```

## Solution

You have two options:

### Option 1: Change Render Settings (EASIEST) ✅

1. Go to your Render dashboard
2. Click on your service
3. Go to **Settings**
4. Find **"Root Directory"** setting
5. **Clear it** (leave it empty) or set it to `.` (root)
6. Update **Build Command** to:
   ```bash
   pip install -r requirements.txt
   ```
7. Update **Start Command** to:
   ```bash
   gunicorn App.app:app
   ```
   OR use the Procfile (which I've updated)

8. Save changes and redeploy

### Option 2: Move Files to Root (Alternative)

If Option 1 doesn't work, you can restructure:

1. Move `App/app.py` to root as `app.py`
2. Move `App/templates/` to root
3. Move `App/static/` to root
4. Update imports in `app.py` if needed

## Files Created at Root

I've created these files at the **root** of your repository:

✅ `Procfile` - Updated to use `App.app:app`
✅ `requirements.txt` - Copied from App/
✅ `runtime.txt` - Python version
✅ `render.yaml` - Configuration file

## Updated Render Settings

**Root Directory:** (Leave EMPTY or set to `.`)

**Build Command:**
```bash
pip install -r requirements.txt
```

**Start Command:**
```bash
gunicorn App.app:app
```

OR just use the Procfile (it's already configured)

## Next Steps

1. **Commit and push the new files:**
   ```bash
   git add Procfile requirements.txt runtime.txt render.yaml
   git commit -m "Fix Render deployment - add root level files"
   git push origin main
   ```

2. **Update Render settings:**
   - Root Directory: **Empty** (or `.`)
   - Build Command: `pip install -r requirements.txt`
   - Start Command: Leave blank (uses Procfile) OR `gunicorn App.app:app`

3. **Redeploy** - Render will automatically redeploy on push

## Verify

After deployment, check:
- ✅ Build completes successfully
- ✅ App starts without errors
- ✅ Homepage loads at your Render URL

## If Still Not Working

Check your GitHub repository structure:
- Does the `App/` folder exist in the repo?
- Are all files committed and pushed?

You can verify by:
```bash
git ls-files | grep App
```

This should show files in the App directory.

