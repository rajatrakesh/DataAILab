# Appendix A1: Now Creator Sample Prompts

This appendix provides sample prompts you can use with Now Assist for Creator to generate flows, code, and other ServiceNow artifacts.

## Text to Flow Prompts

### Incident Management Flows

```
Anytime an incident record is created. Wait 1 minute. If the incident priority equals high, then send a Teams message.
```

```
Whenever a change request is created or updated where the model is an unauthorized demo, do the following in parallel. Apply change approval policy. If approvals are approved or skipped, update change request record as approved. If not, update change request record as rejected. Evaluate the model once again. If rejected, send an email. Wait until active is false, disregard change request approvals, and evaluate the change model.
```

### HR and Expense Management

```
When an expense claim is submitted, email the user that the claim has been received. Then, ask their manager for approval. If the manager approves, change the status to approved and inform the user via email. If rejected, send an email.
```

## Text to Code Prompts

### Basic Utility Functions

```javascript
//write a function which takes an input in Celsius and returns the value in Fahrenheit
```

```javascript
//validate that the variable emails is a string and has allowed syntax
//if the syntax is allowed return true
```

### ServiceNow-Specific Queries

```javascript
//return all critical incidents created in the last 6 months
```

```javascript
// function to query the incident table to find the latest record created in the last quarter by the current user
```

```javascript
// If email is provided, ensure it is from my domain.
//If not, abort the action
```

```javascript
//Get all active incidents where the caller is a VIP
//If 90 percent of the SLA has been consumed, send an alert to the assignment group manager
```

```javascript
//Use glide aggregate to count number of P1 incidents closed between March 3 to April 13 of 2023 assigned to admin
```

### Email Scripts

```javascript
//Find all open incidents with an inactive assigned to the user and email the manager
```

```javascript
// write a glide record query to find all locked-out users and email their manager
```

### Script Include Functions

```javascript
// create a function with regular expression search of text to find social security numbers and mask them with *
```

## Advanced Flow Examples

### Multi-Step Approval Process

```
When a high-value purchase request is submitted:
1. Notify the requester of receipt
2. Route to department manager for initial approval
3. If approved and amount > $5000, route to finance team
4. If finance approves, create purchase order
5. Send final notification to all parties
6. If rejected at any stage, notify requester with reason
```

### Automated Incident Response

```
When a P1 incident is created:
1. Immediately notify the on-call engineer via SMS
2. Create a war room in Teams
3. Send email to management team
4. Start a 15-minute timer
5. If not acknowledged within 15 minutes, escalate to manager
6. Update incident with all notification timestamps
```

## Code Generation Best Practices

### Effective Prompt Structure

1. **Be Specific:** Include table names, field names, and exact requirements
2. **Use Comments:** Start with `//` to describe what you want
3. **Include Context:** Mention if it's for a script include, business rule, etc.
4. **Specify Data Types:** Mention expected inputs and outputs
5. **Add Error Handling:** Request validation and error handling when needed

### Example of Well-Structured Prompt

```javascript
// Create a script include function called 'getHighPriorityIncidents'
// Input: user sys_id (string)
// Output: array of incident objects
// Logic: Query incident table for P1 and P2 incidents assigned to the user
// Include error handling for invalid user sys_id
// Return empty array if no incidents found
```

## Integration Examples

### External System Integration

```
When a customer case is created in ServiceNow:
1. Call external CRM API to get customer details
2. Update case with customer tier information
3. If VIP customer, auto-assign to senior agent
4. Send Slack notification to customer success team
5. Create follow-up task for 24-hour check-in
```

### Multi-System Workflow

```
When an employee termination request is approved:
1. Disable Active Directory account
2. Remove from all distribution lists
3. Update HR system employment status
4. Create asset return task
5. Notify IT, Security, and Facilities teams
6. Schedule account deletion for 30 days
```

## Tips for Success

### Flow Generation Tips
- Use clear, sequential language
- Specify conditions and triggers explicitly
- Include timing requirements (wait, delay, schedule)
- Mention parallel vs sequential execution when needed

### Code Generation Tips
- Include specific ServiceNow APIs you want to use (GlideRecord, GlideAggregate, etc.)
- Mention security considerations
- Specify logging requirements
- Include performance considerations for large datasets

### Testing and Refinement
- Start with simple prompts and build complexity
- Test generated code in a development environment
- Refine prompts based on results
- Save successful prompt patterns for reuse

---

**Back to:** [Main README](README.md) | **Next:** [Appendix A2: Agent Ideas](appendix-a2-agent-ideas.md)