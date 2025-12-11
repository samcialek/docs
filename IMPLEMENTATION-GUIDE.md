# Abisko Docs Restructure: Implementation Guide

## What's Included

**65 files total:**
- 1 `docs.json` (navigation configuration)
- 64 MDX content files

**7 top-level tabs:**
1. Getting Started (4 pages)
2. Properties & Meters (12 pages)
3. Data Quality (6 pages)
4. Performance (14 pages)
5. GRESB (12 pages)
6. Compliance (10 pages)
7. ESPM (5 pages)

---

## Option A: Full Replace (Recommended)

This replaces your entire docs repo with the new structure.

### Step 1: Backup Current Repo
```bash
# In your local machine
cd ~/repos
git clone https://github.com/samcialek/docs docs-backup
```

### Step 2: Clear Existing Content
```bash
cd ~/repos/docs

# Keep git history but remove content
rm -rf glossary/
rm docs.json
```

### Step 3: Extract New Files
```bash
# Download the zip from Claude's output
# Then extract to your docs folder
unzip abisko-docs-restructure.zip -d ~/repos/docs/
```

### Step 4: Push to GitHub
```bash
cd ~/repos/docs
git add .
git commit -m "Restructure docs: 7 tabs, 64 pages, new navigation"
git push origin main
```

### Step 5: Verify Deployment
- Wait 2-3 minutes for Mintlify to rebuild
- Check https://abisko-d076937d.mintlify.app
- All 7 tabs should appear in top navigation

---

## Option B: Manual Upload via GitHub Web

If you prefer not to use git locally:

### Step 1: Delete Old Folders
In GitHub (github.com/samcialek/docs):
1. Navigate to `glossary/` folder
2. Click "..." → Delete directory
3. Commit the deletion

### Step 2: Upload New Structure
1. Go to repo root
2. Click "Add file" → "Upload files"
3. Drag the entire unzipped folder contents
4. Commit

**Note:** GitHub web upload has a 100-file limit per commit. You may need to upload in batches:
- Batch 1: `getting-started/`, `data-quality/`, `espm/`
- Batch 2: `properties-meters/`, `performance/`
- Batch 3: `gresb/`, `compliance/`
- Batch 4: `docs.json`

---

## Option C: Trigger Rebuild Only (If Files Already Exist)

If you've already uploaded files but they haven't deployed:

1. Open `docs.json` in GitHub
2. Click edit (pencil icon)
3. Add a blank line at the end
4. Commit the change

This triggers Mintlify to rebuild all files.

---

## Verification Checklist

After deployment, verify:

- [ ] Top navigation shows 7 tabs
- [ ] Each tab has left sidebar with subsections
- [ ] All 64 pages load without 404 errors
- [ ] No MDX syntax errors in build logs
- [ ] Links between pages work correctly

---

## Troubleshooting

### 404 Errors on Pages
- Check that folder names match `docs.json` paths exactly
- Ensure no spaces in folder/file names
- Verify `.mdx` extension on all content files

### Build Failures
- Check Mintlify dashboard for error logs
- Common issue: `<` symbols in content (must be escaped)
- All files in this package have been sanitized

### Navigation Not Updating
- Clear browser cache
- Wait full 5 minutes for CDN propagation
- Check `docs.json` was committed to main branch

---

## File Structure Reference

```
docs/
├── docs.json                          # Navigation config
├── getting-started/
│   ├── index.mdx
│   ├── portfolio-manager-sync.mdx
│   ├── primary-performance-meters.mdx
│   └── data-completeness.mdx
├── properties-meters/
│   ├── properties/
│   │   ├── index.mdx
│   │   ├── gross-floor-area.mdx
│   │   ├── ownership-periods.mdx
│   │   ├── property-use-details.mdx
│   │   ├── space-types.mdx
│   │   └── base-building.mdx
│   └── meters/
│       ├── index.mdx
│       ├── meter-status.mdx
│       ├── master-submeter.mdx
│       ├── meter-space-assignments.mdx
│       ├── meter-types.mdx
│       └── estimated-bills.mdx
├── data-quality/
│   ├── index.mdx
│   ├── data-completeness.mdx
│   ├── data-coverage.mdx
│   ├── gaps.mdx
│   ├── overlaps.mdx
│   └── jumps.mdx
├── performance/
│   ├── index.mdx
│   ├── eui.mdx
│   ├── source-site-eui.mdx
│   ├── benchmark-comparison.mdx
│   ├── performance-tiers.mdx
│   ├── spaces/
│   │   ├── index.mdx
│   │   └── landlord-tenant-control.mdx
│   ├── emissions/
│   │   ├── index.mdx
│   │   ├── scope-123.mdx
│   │   ├── emissions-factor.mdx
│   │   └── location-market-based.mdx
│   └── green-power/
│       ├── index.mdx
│       ├── recs.mdx
│       ├── onsite.mdx
│       └── offsite.mdx
├── gresb/
│   ├── index.mdx
│   ├── reporting-season.mdx
│   ├── workflows.mdx
│   ├── asset-spreadsheet.mdx
│   ├── gap-filling.mdx
│   ├── data-availability.mdx
│   ├── data-coverages.mdx
│   ├── like-for-like.mdx
│   └── decarbonization/
│       ├── index.mdx
│       ├── crrem.mdx
│       ├── stranding-risk.mdx
│       └── bps-vs-crrem.mdx
├── compliance/
│   ├── index.mdx
│   ├── building-performance-standard.mdx
│   ├── submissions.mdx
│   ├── exposure.mdx
│   ├── penalties.mdx
│   └── benchmarks/
│       ├── index.mdx
│       ├── ashrae-100.mdx
│       ├── cbecs.mdx
│       ├── epa.mdx
│       └── bpd.mdx
└── espm/
    ├── index.mdx
    ├── imports.mdx
    ├── properties-meters.mdx
    ├── property-uses.mdx
    └── metrics.mdx
```

---

## What Changed from Original Glossary

| Before | After |
|--------|-------|
| 27 terms in flat glossary | 64 pages in hierarchical sections |
| 6 categories | 7 top-level tabs |
| Single sidebar | Tabs + sidebar + page TOC |
| GIF placeholders | No placeholders (clean text) |
| Some MDX syntax errors | All files validated |

---

## Next Steps After Deployment

1. **Content Review:** Have Julio B. review each page for accuracy
2. **Add Screenshots:** Identify 5-10 pages that need visuals
3. **Scribe How-Tos:** Export Scribe guides as MDX and add to relevant sections
4. **Connect to Abisko GitHub:** Eventually move docs into main monorepo
