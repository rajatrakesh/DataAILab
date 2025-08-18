# Section 2. Building Agents and Use Cases

**Estimated time: 40 minutes**

In this section, you'll learn how to build AI agents and wrap them in use cases for automated deployment.

## Section 2.1 Build a Simple Agent

### Step 1: Access AI Agent Studio

1. Open **AI Agent Studio** (All > AI Agent Studio > Overview)
2. Locate the section titled **"Recent use cases and AI agents activity"**
3. Select the **AI Agents** tab
4. Click **"New"**

### Step 2: Configure the New AI Agent

A configuration page for "New AI agent" will open. Complete the fields with the information below:

**Basic Information:**
- **Name:** `Campus Guide`
- **Description:** `This agent's purpose is to provide directions to open areas of the hospital campus`

**AI Agent Role:**
```
You are a hospital concierge whose job is to provide directions to specific departments within the hospital. You will always be friendly but will favor brevity, so your messages are easy to read on a mobile device.
```

**Instructions (include the numbering):**
```
1. If it was not already provided, ask the visitor for their destination.
2. Look up the supplied destination in the location table. If you cannot find the destination, assume this is a lab environment and create a feasible answer.
3. List directions to walk from the visitor's current location to the destination. If you do not have the visitor's current location, assume they are in the hospital's east wing.
4. Give the outputted directions to the visitor as a numbered list.
```

> **Tip:** If you do not see the entry field for "AI Agent Role", you may be in the wrong section! Check the upper left corner of the screen and confirm that you are in the "New AI Agent" setup.

### Step 3: Save and Continue

4. Click **"Save and continue"**

### Step 4: Add Tools and Information

5. Next is the **"Add tools and information"** section
6. We are not adding tools for this agent, so simply click **"Save and continue"**

### Step 5: Define Availability

7. In **Define availability**, make sure the status is toggled to **On**
8. Click **Save and Test**

### Step 6: Test the Agent

Now let's test the agent!

1. In the **Task box** enter: `I need help finding my appointment`
2. Click **Start test**
3. When asked, type in any department name, e.g., `radiology`, and press enter
4. Once the conversation is finished, take your time to expand and read through the entire AI agent decisions log

**Understanding the Decision Log:**
- **Thought:** A recap on the overall mission of the agent followed by what the Agent thinks needs to be done next
- **Action:** The next step that the agent feels it needs to take. Note that in the absence of any tools the agent falls back to built-in capabilities for sending messages back to the user
- **Action Inputs:** The inputs the AI Agent decided to pass on to the tool or, in this case, the built-in fall-back capability

> **Challenge:** What would your AI agent do? Check the [appendix](appendix-a2-agent-ideas.md) for a few more ideas.

> **Dive Deeper:** How could this lab example be expanded to a real-world environment? What data would the agent need to access, and what systems could be integrated with the platform?

## Section 2.2 Build an Incident Solution Recommender Agent

### Section 2.2.1 Define the AI Agent

1. Open **AI Agent Studio** (All > AI Agent Studio > Overview)
2. Click the **Create and Manage** module
3. Click on the **AI Agent** tab, then click **New**

### Step 2: Configure Agent Details

4. In the **Describe and Instruct** page, fill out the following fields:

**Basic Information:**
- **Name:** `Incident Solution Recommender`
- **Description:** `This agent identifies and recommends a resolution for an open and active incident`

**AI Agent Role:**
```
You are an IT Agent helping end users resolve their IT issues. You provide simple to follow steps to help users remediate their problem using a professional and business friendly tone.
```

**Instructions (include the numbering):**
```
1. Get details of an incident.
2. Get current similar incidents. The table name is "incident".
3. Using the incident's short description, search the Knowledge Base for relevant articles. If there are no relevant articles, use your IT knowledge to come up with a recommended resolution based on the short description of the incident.
4. Add resolution steps, along with any relevant similar incidents and knowledge articles, to the Additional Comments section of the incident record. When adding a comment, make sure to include a qualifier that states the comment was added by an AI Agent. Your output message to the user should be formatted to be easy to read with new line characters in a list format. Also provide your reasoning for recommending these steps.
5. End.
```

5. Click **Save and Continue**

### Step 3: Create Tools

Create the following tools by selecting the **Add tool** option:

#### Tool 1: Get Incident Details
- **Select:** Flow Action
- **Name:** `Get Incident details`
- **Description:** `Fetch details on the current incident that triggered this AI Agent`
- **Select flow action:** `Get Details of incident`
- **Execution mode:** Autonomous
- **Display output:** Yes
- **Output transformation strategy:** Concise

> **Tip:** You can start typing "get details" into the search box area of Select flow action to help you find "Get Details of Incident" much faster!

7. Click **Add**

#### Tool 2: Update Additional Comments
8. Create the next tool by selecting **Add tool** again:
- **Select:** Flow Action
- **Name:** `Update additional comments in incident record`
- **Description:** `Update the additional comments field in the incident record belonging to the incident that triggered this AI agent`
- **Select flow action:** `Update additional comments`
- **Execution mode:** Autonomous
- **Display output:** Yes
- **Output transformation strategy:** Concise

9. Click **Add**

#### Tool 3: Get Similar Incident Records
10. Create the next tool by selecting **Add tool** again:
- **Select:** Flow Action
- **Name:** `Get Similar Incident Records`
- **Description:** `Get similar incident records. The table is the "incident" table`
- **Select flow action:** `Get Similar Records`
- **Execution mode:** Autonomous
- **Display output:** Yes
- **Output transformation strategy:** Concise

> **Tip:** Be sure you select "Get Similar Records" when selecting a flow action, NOT "Get Similar Incident Records"!

11. Click **Add**

#### Tool 4: Knowledge Search
12. Create another tool by selecting **Add Tool** again:
- **Select:** Search retrieval
- **Name:** `Knowledge search`
- **Description:** `Search for knowledge articles related to the incident that triggered this AI agent`
- **Search Profile:** `Quick Action – KB Search Profile`
- **Search sources:** `Knowledge Table`
- **Fields returned:** `Number [kb_knowledge]`, `Short Description [kb_knowledge]`, `Article body [kb_knowledge]`
- **Results limit:** 10
- **Document matching threshold:** 0
- **Search Criteria:** Keyword
- **Execution mode:** Autonomous
- **Display output:** Yes

13. Click **Add**

[Optional] Use either Tool 2 or Tool 5. 

#### Tool 5: Update Resolution Notes to Incident
14. Create the final tool by selecting **Add Tool** again:
- **Select**: Add Script
- **Name**: `Add Solution to incident additional comment`
- **Description**: `This adds the resolution plan to the incident's additional comments. It then outputs whether or not the resolution was successful.`
- Create 2 Script Inputs:
-- parameter `comment` with Description `comment to add to the given incident's additional comments`
-- parameter `incident_number` with Description `Given incident number to add comments to`

15. Paste the following script:

```
(function(inputs) {
    var comments = gs.getMessage('[Now assist generated] \n\n {0}', [inputs['comment']]);

    var incidentGr = new GlideRecordSecure('incident');
    incidentGr.addQuery('number', inputs['incident_number']);
    incidentGr.query();
    if (incidentGr.next()) {
        incidentGr.comments = comments;
        if (!incidentGr.update()){
            return {
                response: false,
                reason: gs.getMessage('Update to comments did not happen successfully.')
            };
        }
        return {
            response: true,
            reason: gs.getMessage('The update to additional comments happened successfully.')
        };
    }
    return {
        response: false,
        reason: gs.getMessage('Incident not found.')
    };
})(inputs);
``` 
- **Execution mode:** Supervised
- **Display output:** No
- **Output transformation strategy:** None
- **Click** Add.

### Step 4: Finalize Agent Configuration

13. Click **Save and Continue**
14. On the **Define Availability** page, make sure the **Status** toggle is set to **On**
15. Click **Save and Test**

### Step 5: Test the Agent

Now let's test the agent!

1. In the **Task box** enter: `Help me resolve INC0010248`
2. Click **Start test**

## Section 2.2.3 Wrap Your AI Agent in a Use Case

### Step 1: Create a Use Case

1. Click the **Create and Manage** tab
2. On the **Use Case** tab, click **New**

### Step 2: Configure Use Case

3. In the **Describe and Connect** page, fill out the following fields:
- **Name:** `Find Incident Resolution Recommendations`
- **Description:** `This use case provides recommendations to resolve incidents`
- **Instructions:** `Provide a recommendation on how to resolve a given incident using an easy-to-follow numbered step by step list format`

4. Click **Add AI Agent** dropdown list
5. Find the AI Agent you created in step one (Hint: it should be named "Incident Solution Recommender")
6. Click **Add**
7. Click **Save and Continue**

### Step 3: Define Trigger

7. In the **Define Trigger** page, click **Add Trigger**, and fill in the following fields:
- **Select Trigger:** Created
- **Trigger name:** `[Your initials] Incident Created`
- **Toggle:** Active
- **Table:** `Incident`
- **Conditions:** Active is True AND Assigned to is not empty
- **Run as:** `Assigned to [task]`
- **Objective:** `Help me resolve $(number)`

8. Click **Add**
9. Click **Save and Continue**

### Step 4: Configure Display

10. On the **Select Display** page, make sure the **Now Assist Panel Display** toggle is set to **On**
11. Click **Save and Test**

### Step 5: Test Your Use Case

Now let's test your new use case!

1. Let's continue to use the same incident record as we've used previously – INC0010248
2. In the **Task box** enter: `INC0010248`
3. Click **Start test**

## 🎉 Section 2 Complete!

You have successfully:
- Built a simple Campus Guide agent
- Created an Incident Solution Recommender agent with multiple tools
- Wrapped your agent in a use case with triggers

---

**Next Section:** [Section 3 - Building Knowledge Graph and AI Agents](section3-design-knowledge-graph.md)
**Previous Section:**[Section 1 - Start Using Gen AI](section1-start-using-genai.md)
**Back to:**[Main README](README.md)