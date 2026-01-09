# GitHub Heartbeat Setup Guide

This workflow keeps your Supabase free tier database active by pinging it every 3 days.

## 🎯 What It Does

- ✅ Runs automatically every 3 days
- ✅ Pings your Supabase database (queries 1 story)
- ✅ Prevents Supabase from pausing due to inactivity
- ✅ Can be triggered manually from GitHub Actions tab
- ✅ Shows success/failure status

---

## 📋 Setup Steps

### Step 1: Get Your Supabase Credentials

1. Go to your Supabase project dashboard: https://app.supabase.com
2. Click on your project
3. Go to **Settings** → **API**
4. Copy these values:
   - **Project URL** (looks like: `https://xxxxx.supabase.co`)
   - **Anon/Public Key** (starts with `eyJ...`)

### Step 2: Add Secrets to GitHub

1. Go to your GitHub repository: https://github.com/Syded74/app-library
2. Click **Settings** (top right)
3. In left sidebar, click **Secrets and variables** → **Actions**
4. Click **New repository secret**

Add these two secrets:

**Secret 1:**
- Name: `SUPABASE_URL`
- Value: `https://your-project.supabase.co` (your Project URL)

**Secret 2:**
- Name: `SUPABASE_ANON_KEY`
- Value: `eyJhbGci...` (your Anon/Public key)

### Step 3: Commit & Push the Workflow

```bash
cd /Users/m2/Downloads/story/library_files

# Add the workflow file
git add .github/workflows/heartbeat.yml

# Commit
git commit -m "Add Supabase heartbeat workflow"

# Push to GitHub
git push origin main
```

### Step 4: Verify It's Working

1. Go to your GitHub repo
2. Click **Actions** tab
3. You should see "Supabase Heartbeat" workflow
4. Click **Run workflow** to test manually
5. Check that it succeeds (green checkmark)

---

## 📅 Schedule

- **Automatic**: Every 3 days at midnight UTC
- **Manual**: Click "Run workflow" button anytime
- **First run**: Will trigger on next scheduled time or when you run manually

---

## 🔍 Monitoring

### View Workflow Runs:
1. Go to GitHub repo → **Actions** tab
2. Click "Supabase Heartbeat"
3. See all past runs with timestamps

### Check Logs:
1. Click any run
2. Click "ping" job
3. Expand steps to see detailed output

### Expected Output:
```
🔄 Pinging Supabase to keep it alive...
✅ Supabase heartbeat successful!
Response: [{"id":"story_0"}]
⏰ Last heartbeat: 2026-01-09 00:00:00 UTC
```

---

## ⚠️ Troubleshooting

### Error: "Heartbeat failed with status: 401"
**Fix:** Check your `SUPABASE_ANON_KEY` secret is correct

### Error: "Heartbeat failed with status: 404"
**Fix:** Verify your `SUPABASE_URL` is correct and includes `https://`

### Error: "Heartbeat failed with status: 500"
**Fix:** Check your Supabase database is running and `stories` table exists

### Workflow doesn't appear in Actions tab
**Fix:** Make sure the file is in `.github/workflows/heartbeat.yml` (exact path)

---

## 🎛️ Customization

### Change Frequency

Edit the cron schedule in `heartbeat.yml`:

```yaml
# Every day:
- cron: '0 0 * * *'

# Every 7 days:
- cron: '0 0 */7 * *'

# Twice a week (Mon & Thu):
- cron: '0 0 * * 1,4'
```

### Add Email Notifications

GitHub can email you if the workflow fails:
1. Go to repo **Settings** → **Notifications**
2. Enable "Actions" notifications

---

## 📊 Why This is Important

| Without Heartbeat | With Heartbeat |
|-------------------|----------------|
| Database pauses after 7 days | ✅ Always active |
| Apps break | ✅ Reliable |
| Need manual wake-up | ✅ Automated |
| Poor user experience | ✅ Seamless |

---

## ✅ Checklist

- [ ] Got Supabase URL and Anon Key
- [ ] Added `SUPABASE_URL` secret to GitHub
- [ ] Added `SUPABASE_ANON_KEY` secret to GitHub
- [ ] Created `.github/workflows/heartbeat.yml` file
- [ ] Committed and pushed to GitHub
- [ ] Tested workflow manually
- [ ] Verified it succeeded

---

## 🚀 You're Done!

Your Supabase database will now stay active automatically. The workflow will:
- Run every 3 days
- Keep your free tier database awake
- Ensure your WildInk app stays fast and reliable

Check the Actions tab periodically to ensure it's running successfully!
