# Section 15: MCP External Tool Access in ServiceNow MCP Client

## What is MCP?

**MCP - Model Context Protocol** 
- A standard that enables AI agents to securely interact with enterprise systems where data resides, such as content repositories, business applications, development environments and databases. 
- This allows enterprise businesses to reduce the integration challenges of manual workflows, thereby delivering outcomes from models more quickly. Since then, MCP servers have become foundational for agentic applications, providing a consistent and secure mechanism for invoking tools and retrieving data.

**Why MCP ?**
- Open Standard introduced by Anthropic
- Enables AI Agents to access external tools, data and context
- Acts as universal connector for AI systems
- Standardizes communication between AI models and Enterprise systems
- Essential for scalable and interoperable AI Integrations


## ServiceNow as MCP Client

- Oauth support for connecting to external MCP Server
- Supports multiple OAuth grant types
    1. Authorization COde
    2. Client Credential
    3. JWT Bearer
- Ensure secure authentication and authorization
- Support dynamic client registration


## Dynamic Client Registration
- Automates OAuth client creation with MCP Servers
- Uses discovery endpoints for authorization metadata
- Eliminates need for manual client configuration
- Ensures up-to-date and secure integration

![MCP](screenshots/MCP1.png)

**Benefits:**
- Reduces manual errors and admin effort
- Enables plug-and-play integration with MCP Servers
- Aligns with secure OAuth best practices
- Accelerates AI adoption across enterprise workflows

## Before we get started with the lab, Below are the pre-requisites

Prerequisites:
1. Platform version: YP6+ / ZP1+
2. Application: Now Assist AI Agents 5.0.24+

Download and install Model Context Protocol Client
https://store.servicenow.com/store/app/5eeda18f1b996a10229141d1b24bcbfc

Login as maint role user, update MCP tool property, `sn_aia.enable_mcp_tool`, and set to `true`
Once done, logout!

Great! With this you now have everything that is needed for accessing external mcp server within ServiceNow.

Now login as admin, and Go to `All`, Search for `AI Agent Studio`, then go to `Settings`

![MCP](screenshots/mcp-add-server.png)

In Settings, select `Manage MCP Servers`, this is the place where we add new MCP connections and later use them as part of AI Agents as tools.

![MCP](screenshots/mcp-add-server1.png)

Now, as part of today's lab, we will be using MCP Server of `Prisma.io` which is a postgres database platform.
Before we move forward, i would request you to go to `prisma.io` and create your account. This would be essential step before we go ahead and start integration with the MCP server of `prisma.io`.

I hope everyone by now has created account with `prisma.io`, and created your workspace.
Great! let's proceed with our lab.

Click `New` to add a new mcp server connection.

Add `Name`, which in this case we are giving as `Prisma`
Provide `Authentication Type`, which will be `OAuth 2.0`
Provide `MCP Server URL`, which will be `https://mcp.prisma.io/mcp`

Click, `Next`

![MCP](screenshots/mcp-add-server2.png)

This is where we select the `Client Registration type`, which we will be `Dynamic Client Registration`
Keep everything same, i.e.,

- `Grant type` will be `Authorization Code`
- `Token authentication method` will be `Client Secret Basic`
- `Authorization URL` will be `https://mcp.prisma.io/authorize`
- `Token URL` will be `https://mcp.prisma.io/token`
- `Token Revokation URL` will be `https://mcp.prisma.io/token`

Click `Add`

Perfect! With this we have added our first MCP Server.

![MCP](screenshots/mcp-add-server3.png)

While we have added our first MCP Server, one critical piece that is pending is the authentication.
**Check out the pink bar on top**

Now, to authenticate, click the `Authenticate` button, this take you to prisma.io for authentication.

![MCP](screenshots/mcp-add-server4.png)

Now, as part of this, we need to authorize the API access to the `prisma.io` mcp server, by logging into the `prisma.io`.
Can be a google/email/SSO sign-in.

![MCP](screenshots/mcp-add-server5.png)

Once Authenticated, we will now see `Re-authenticate` and the pink bar on top will be gone.

Click `Save`

![MCP](screenshots/mcp-add-server6.png)

Perfect! with this we now have completed the connection setup of our first mcp server.

![MCP](screenshots/mcp-add-server7.png)

Next, we will now try build an AI Agent that leverages this MCP Server.

Go to `Create and Manage` from the bar, go to `AI Agents` and click `New`

Let's define the the AI Agent, starting with `Define the specialty`

- Give the AI Agent a `Name`, let's call it `Prisma AI Agent`
- Provide a `Description`, let's say `AI Agent to manage database workflows`

Let's define the role and required steps

- `AI Agent Role` : `You are an AI Agent that manages database workflows`
- `List of steps` : `Manage database workflows using the existing tools`

Click `Save and Continue` at bottom right.

![MCP](screenshots/mcp-add-server8.png)

Click on `Add Tools` and select `MCP Server Tool`

<img src="screenshots/mcp-add-server11.png" alt="MCP" height="600" width="900"/>

With this we add the MCP tool that we have defined. `Prisma`

<img src="screenshots/mcp-add-server10.png" alt="MCP" height="600" width="900"/>

Perfect! we now have added our first tool to our first AI Agent with MCP.

![MCP](screenshots/mcp-add-server9.png)

Click `Continue`

And then Click `Save and Test`
