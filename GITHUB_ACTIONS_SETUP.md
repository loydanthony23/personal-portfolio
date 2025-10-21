# GitHub Actions Configuration Guide for MyResume Website

## 🚀 Quick Setup Instructions

### Step 1: Enable GitHub Pages
1. Go to your repository on GitHub
2. Click on **Settings** tab
3. Scroll down to **Pages** section (left sidebar)
4. Under **Source**, select **"GitHub Actions"**
5. Save the changes

### Step 2: Configure Repository Permissions
1. In **Settings** → **Actions** → **General**
2. Under **Workflow permissions**, select:
   - ✅ **Read and write permissions**
   - ✅ **Allow GitHub Actions to create and approve pull requests**
3. Click **Save**

### Step 3: Push Your Workflows
The workflow files are already created in your `.github/workflows/` directory:
- `deploy.yml` - Main deployment workflow
- `pages.yml` - GitHub Pages deployment
- `pr-validation.yml` - Pull request validation
- `maintenance.yml` - Automated maintenance

Push these files to your repository:
```bash
git add .github/
git commit -m "Add GitHub Actions workflows for automated deployment"
git push origin main
```

### Step 4: Verify Workflows Are Running
1. Go to your repository on GitHub
2. Click on **Actions** tab
3. You should see your workflows listed
4. Click on any workflow to see its status

## 🔧 Detailed Configuration

### Workflow Triggers Explained

#### 1. Deploy Workflow (`deploy.yml`)
- **Triggers**: Every push to `main` branch + pull requests
- **What it does**: Validates code and deploys to GitHub Pages
- **Manual trigger**: Available in Actions tab

#### 2. Pages Workflow (`pages.yml`)
- **Triggers**: Push to `main` branch only
- **What it does**: Deploys your site to GitHub Pages
- **Environment**: Uses `github-pages` environment

#### 3. PR Validation (`pr-validation.yml`)
- **Triggers**: Pull requests affecting HTML/CSS/JS/PHP files
- **What it does**: Validates code quality and comments on PRs
- **Manual trigger**: Available in Actions tab

#### 4. Maintenance Workflow (`maintenance.yml`)
- **Triggers**: Every Monday at 9 AM UTC + manual trigger
- **What it does**: Checks for updates and creates maintenance issues
- **Manual trigger**: Available in Actions tab

### Customization Options

#### Add Custom Domain
Edit `pages.yml` and add your domain:
```yaml
- name: Deploy to GitHub Pages
  uses: actions/deploy-pages@v4
  with:
    cname: your-domain.com  # Add your custom domain here
```

#### Change Maintenance Schedule
Edit `maintenance.yml` cron schedule:
```yaml
on:
  schedule:
    # Run every day at 2 PM UTC
    - cron: '0 14 * * *'
```

#### Add Environment Variables
Create secrets in **Settings** → **Secrets and variables** → **Actions**:
- `CUSTOM_DOMAIN` - Your custom domain
- `ANALYTICS_ID` - Google Analytics ID
- `CONTACT_EMAIL` - Contact form email

## 🛠️ Troubleshooting

### Common Issues

#### 1. Workflows Not Running
- Check if GitHub Actions is enabled in repository settings
- Verify workflow files are in `.github/workflows/` directory
- Ensure YAML syntax is correct

#### 2. Deployment Fails
- Check GitHub Pages settings (must be set to "GitHub Actions")
- Verify repository permissions
- Look at workflow logs in Actions tab

#### 3. Validation Errors
- HTML validation errors: Fix HTML syntax issues
- CSS validation errors: Fix CSS syntax (warnings are usually OK)
- JavaScript validation errors: Fix JS syntax issues

### Debugging Steps

1. **Check Workflow Logs**:
   - Go to Actions tab
   - Click on failed workflow
   - Expand each step to see error details

2. **Test Locally**:
   ```bash
   # Install validators locally
   npm install -g html-validate csslint jshint
   
   # Test HTML validation
   html-validate index.html
   
   # Test CSS validation
   csslint assets/css/main.css
   
   # Test JavaScript validation
   jshint assets/js/main.js
   ```

3. **Manual Workflow Trigger**:
   - Go to Actions tab
   - Click on workflow name
   - Click "Run workflow" button
   - Select branch and click "Run workflow"

## 📊 Monitoring Your Workflows

### Workflow Status Badges
Add these badges to your README.md:
```markdown
![Deploy Status](https://github.com/yourusername/MyResume-1.0.0/workflows/Deploy%20Resume%20Website/badge.svg)
![Pages Status](https://github.com/yourusername/MyResume-1.0.0/workflows/GitHub%20Pages%20Deploy/badge.svg)
```

### Notifications
- GitHub will email you when workflows fail
- You can configure additional notifications in repository settings

## 🔒 Security Considerations

### Repository Secrets
Never commit sensitive information. Use GitHub Secrets for:
- API keys
- Database credentials
- Third-party service tokens

### Workflow Permissions
- Only grant necessary permissions
- Use `permissions` block in workflows to limit access
- Regularly review and update permissions

## 📈 Performance Optimization

### Workflow Optimization
- Use `actions/cache` for dependencies
- Run workflows in parallel when possible
- Use `if` conditions to skip unnecessary steps

### Website Optimization
- Compress images before committing
- Minify CSS and JavaScript
- Use CDN for external resources

## 🆘 Getting Help

### GitHub Actions Documentation
- [Official GitHub Actions Docs](https://docs.github.com/en/actions)
- [Workflow Syntax Reference](https://docs.github.com/en/actions/using-workflows/workflow-syntax-for-github-actions)

### Community Resources
- [GitHub Actions Marketplace](https://github.com/marketplace?type=actions)
- [GitHub Community Forum](https://github.community/c/github-actions)

---

## ✅ Checklist

- [ ] GitHub Pages enabled with "GitHub Actions" source
- [ ] Repository permissions configured
- [ ] Workflow files pushed to repository
- [ ] First workflow run successful
- [ ] Website deployed and accessible
- [ ] Pull request validation working
- [ ] Maintenance workflow scheduled

Your GitHub Actions setup is now complete! 🎉
