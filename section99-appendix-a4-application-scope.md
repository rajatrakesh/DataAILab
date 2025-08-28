# Appendix A4: Application Scope

This appendix provides guidance for situations where you cannot find the "Platform AI Agents and Skills" application scope during Section 2.3 of the lab.

## When to Use This Appendix

You need this appendix if:
- You cannot find **"Platform AI Agents and Skills"** in the application scope dropdown
- The scope selector doesn't show the expected AI-related scopes
- You encounter errors when trying to switch application scopes
- The scope appears but is not selectable

![Application Scope Not Found](screenshots/app-scope-not-found.png)

## Alternative Scope Solution

### Primary Alternative: UXC Generative AI

If you couldn't find the **"Platform AI Agents and Skills"** application scope, then please look for **"UXC Generative AI"** and create your script under it.

![UXC Generative AI Scope](screenshots/uxc-generative-ai-scope.png)

**Steps to use UXC Generative AI:**

1. Click the **Application Scope** icon at the top of the page
2. Select **Application scope: Global**
3. In the filter/search box, type **"UXC"**
4. Select **"UXC Generative AI"** from the filtered results
5. Continue with the lab instructions using this scope instead

### Scope Selection Process

1. **Access Scope Selector**
   - Click the gear/settings icon in the top navigation
   - Or click the current scope name if visible

![Access Scope Selector](screenshots/access-scope-selector.png)

2. **Search for Available Scopes**
   - Type "Platform" to find Platform-related scopes
   - Type "UXC" to find UXC-related scopes
   - Type "AI" to find AI-related scopes

![Search Scopes](screenshots/search-scopes.png)

3. **Select Appropriate Scope**
   - Choose the closest match to the required scope
   - Ensure you have sufficient permissions for the scope

## Understanding Application Scopes

### What Are Application Scopes?

Application scopes in ServiceNow provide:
- **Namespace isolation** for custom development
- **Permission boundaries** for security
- **Organizational structure** for applications
- **Deployment packaging** for change management

### AI-Related Scopes

Common AI and ML related scopes you might encounter:

- **Platform AI Agents and Skills** - Primary AI agent development scope
- **UXC Generative AI** - Alternative AI development scope  
- **Machine Learning Framework** - Core ML functionality
- **AI Search** - Search and indexing capabilities
- **Natural Language Understanding** - NLU processing

### Scope Hierarchy

```
Global (System)
├── Platform AI Agents and Skills
├── UXC Generative AI
├── Machine Learning Framework
├── AI Search
└── Custom AI Applications
```

## Troubleshooting Scope Issues

### Issue: No AI Scopes Visible

**Possible Causes:**
- Insufficient user permissions
- AI plugins not activated
- Instance configuration incomplete

**Solutions:**
1. Verify you're logged in as admin
2. Check plugin activation status
3. Use Global scope as fallback

### Issue: Scope Selection Grayed Out

**Possible Causes:**
- Active development session
- Insufficient privileges
- Scope restrictions in place

**Solutions:**
1. Complete current development work
2. Switch to admin user
3. Clear browser cache and retry

### Issue: Scripts Don't Save in Selected Scope

**Possible Causes:**
- Read-only scope permissions
- Scope compatibility issues
- Missing dependencies

**Solutions:**
1. Verify write permissions
2. Try alternative scope (UXC Generative AI)
3. Create in Global scope if needed

## Working with Alternative Scopes

### Adapting Lab Instructions

When using **UXC Generative AI** instead of **Platform AI Agents and Skills**:

1. **Flow Action Names:** May have different prefixes
2. **Available Templates:** Might be slightly different
3. **Permission Levels:** Could vary between scopes
4. **Integration Points:** May require scope adjustments

### Best Practices

**During Development:**
- Always note which scope you're working in
- Document any scope-specific configurations
- Test functionality across scope boundaries
- Keep track of custom vs. out-of-box components

**For Production:**
- Plan scope strategy before implementation
- Consider upgrade and maintenance implications
- Document scope dependencies
- Test deployment across environments

## Verification Steps

After selecting an alternative scope:

### Confirm Scope Selection

1. **Check Current Scope Display**
   - Look for scope name in top navigation
   - Verify you're in the correct application context

![Current Scope Display](screenshots/current-scope-display.png)

2. **Test Basic Functionality**
   - Try creating a simple script or flow action
   - Verify save/update operations work
   - Check that objects appear in correct scope

### Validate Permissions

1. **Script Creation:** Can you create new script includes?
2. **Flow Actions:** Can you copy and modify flow actions?
3. **Publishing:** Can you publish changes?
4. **Testing:** Can you execute test operations?

## Recovery Options

### If Nothing Works

**Fallback to Global Scope:**
1. Select **Global** as the application scope
2. Continue with lab exercises
3. Note that some features may be limited
4. Document differences for future reference

**Alternative Lab Path:**
1. Skip the advanced flow modification section
2. Focus on agent creation and testing
3. Use out-of-box flow actions when possible
4. Complete other lab sections normally

**Instance Reset:**
1. Contact lab administrator
2. Request fresh instance or scope reset
3. Restart from Section 2.3 preparation steps
4. Document issues for improvement

## Scope Reference Guide

### Quick Scope Finder

| Looking For | Try These Scopes |
|-------------|------------------|
| AI Agent Development | Platform AI Agents and Skills |
| Alternative AI Dev | UXC Generative AI |
| Flow Designer | Global or specific app scope |
| Script Development | Global or app-specific |
| Testing/Prototyping | Global |

### Permission Requirements

Different scopes require different permission levels:

- **Global:** System Administrator
- **Platform AI:** AI Administrator or higher
- **UXC Generative AI:** Developer or higher
- **Custom Scopes:** Varies by configuration

## Support and Resources

### When to Contact Support

- Multiple scope alternatives don't work
- Permissions seem correct but access denied
- Instance appears to be missing AI components
- Scope selector is completely missing

### Information to Provide

When reporting scope issues:
- Current user role and permissions
- Instance URL and version
- Steps attempted
- Error messages (exact text)
- Screenshots of scope selector
- Browser and system information

### Self-Help Resources

- ServiceNow Documentation on Application Scopes
- Community forums for scope-related questions
- Lab facilitator or workshop support
- ServiceNow Developer Portal resources

---

**Back to:** [Section 2.3](section2-building-agents.md#section-23-extra---build-an-ai-agent-that-checks-outages) | **Main Menu:** [README](README.md) | **Previous:** [Appendix A3](appendix-a3-ai-search-setup.md)