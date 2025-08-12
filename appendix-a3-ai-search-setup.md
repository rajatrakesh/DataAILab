# Appendix A3: AI Search Set-Up

In this section, we will run a quick fix to ensure AI Search is running on your lab instance.

## When to Use This Appendix

Use this troubleshooting guide if:
- AI Search shows as **inactive** in the Lab Configuration section
- You see error messages related to AI Search functionality
- Now Assist features are not working properly
- The green checkmark is missing from AI Search Status

![AI Search Inactive](screenshots/ai-search-inactive.png)

## Repair Process

### Step 1: Log Out Safely

1. **Log out** of your lab instance completely
2. In your browser, edit the URL to remove the `/external_logout.do`
3. You will be presented with a fresh login page

![Fresh Login Page](screenshots/fresh-login-page.png)

### Step 2: Login with Service Account

3. Log into your instance again, this time with the following **service credentials**:
   - **User:** `aislab.admin`
   - **Password:** `aislab.admin`

![Service Account Login](screenshots/service-account-login.png)

> **Important:** These are special service account credentials specifically for AI Search repair. Do not use these for regular lab activities.

### Step 3: Access Repair Tool

4. Navigate to **All > Repair Machine Learning Settings Tool**

![Repair Tool Access](screenshots/repair-tool-access.png)

### Step 4: Execute Repair

5. In the pane on the right, you will see **"Repair/Reset Machine Learning Settings"**
6. Click **"Reset"**

![Reset ML Settings](screenshots/reset-ml-settings.png)

### Step 5: Wait for Completion

7. **Wait a few minutes** for your instance to be ready
8. You may see progress indicators or status messages during this process

![Repair Progress](screenshots/repair-progress.png)

### Step 6: Return to Admin Access

8. Use your **magic link** to log in again as admin
9. To return to the beginning of the lab, [click here](lab-configuration.md)

## Verification Steps

After completing the repair process, verify that AI Search is working:

### Check AI Search Status

1. Navigate to **AI Search > AI Search Status**
2. Confirm you see a **green check mark**
3. All AI Search components should show as "Active"

![AI Search Active](screenshots/ai-search-status-green.png)

### Test Basic Functionality

1. Try accessing **Now Assist Admin > Overview**
2. Verify that Now Assist features are available
3. Test a simple search in Employee Center (if accessible)

## Common Issues and Solutions

### Issue: Repair Tool Not Found

**Solution:**
- Ensure you're logged in with the `aislab.admin` account
- Clear browser cache and try again
- Check that you're on the correct instance URL

### Issue: Reset Button Grayed Out

**Solution:**
- Verify service account permissions
- Wait for any background processes to complete
- Refresh the page and try again

### Issue: Reset Doesn't Complete

**Solution:**
- Wait longer (process can take 5-10 minutes)
- Check browser console for error messages
- Try logging out and back in with magic link

### Issue: Still Showing Inactive After Repair

**Solution:**
- Perform the reset process again
- Contact lab administrator for instance-specific issues
- Check ServiceNow community for known issues

## Alternative Repair Methods

### Manual Service Restart

If the automated repair doesn't work:

1. Navigate to **System Definition > Scheduled Jobs**
2. Look for AI/ML related scheduled jobs
3. Run the jobs manually if they appear stopped

### Database Refresh

For persistent issues:

1. Check with lab administrator about instance refresh
2. Consider using a different lab instance
3. Verify browser compatibility and clear all cache

## Prevention Tips

### Maintaining AI Search Health

- Don't modify AI Search configurations during the lab
- Avoid running multiple AI operations simultaneously
- Clear browser cache between different lab sections
- Use incognito/private browsing mode if experiencing issues

### Best Practices

- Always verify AI Search status before starting lab sections
- Report persistent issues to lab administrators
- Keep the repair steps bookmarked for quick access
- Document any custom configurations that might interfere

## Instance Specifications

### Required Components

For AI Search to function properly, your instance needs:
- **Machine Learning Framework:** Active
- **AI Search Plugin:** Activated
- **Natural Language Understanding:** Enabled
- **Semantic Search:** Configured
- **Vector Database:** Operational

### Resource Requirements

- **Memory:** Sufficient for ML model loading
- **CPU:** Available for search processing
- **Storage:** Space for indexes and models
- **Network:** Connectivity to ServiceNow AI services

## Troubleshooting Checklist

Before using this repair process, verify:

- [ ] Correct instance URL
- [ ] Proper user permissions
- [ ] Browser compatibility (Chrome, Firefox, Safari latest versions)
- [ ] No VPN or proxy interference
- [ ] JavaScript enabled
- [ ] Pop-up blockers disabled for ServiceNow domain
- [ ] Sufficient system resources (not running too many browser tabs)

## Support Resources

If repair steps don't resolve the issue:

### ServiceNow Resources
- ServiceNow Community Forums
- ServiceNow Documentation Portal
- Now Support (if you have access)

### Lab-Specific Help
- Check with workshop facilitator
- Review lab instance documentation
- Contact lab technical support

### Browser and System
- Update to latest browser version
- Clear all browser data for ServiceNow domain
- Try different browser or incognito mode
- Restart browser completely

---

**Back to:** [Lab Configuration](lab-configuration.md) | **Main Menu:** [README](README.md) | **Next:** [Appendix A4](appendix-a4-application-scope.md)