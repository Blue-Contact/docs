# Installing the Data Laboratory Connector in Claude

This guide walks through connecting Claude to **Data Laboratory** using a custom connector over remote MCP (Model Context Protocol).

**Connector details you'll need:**

| Field | Value |
|---|---|
| Connector name | Data Laboratory |
| Remote MCP server URL | `https://app.datalaboratory.ai/mcp` |
| Authentication | OAuth (you'll sign in through a browser window) |

---

## Before you start

- **Plan availability:** Custom connectors work on Free, Pro, Max, Team, and Enterprise plans. Free accounts are limited to one custom connector total.
- **Permissions:** On **Pro and Max**, you can add the connector yourself. On **Team and Enterprise**, only an Owner or Primary Owner can add it to the organization — individual members then connect to it separately.
- **Data Laboratory account:** You need working Data Laboratory credentials. The OAuth step signs you in as yourself, so Claude only gets access to what your own account can already see.
- **No client ID or secret required.** Data Laboratory's server handles OAuth registration automatically, so you can leave Advanced settings empty. Only fill those fields in if Data Laboratory support explicitly gives you a client ID and secret to use.

Pick the path below that matches your plan.

---

## Path A — Pro and Max plans (individual accounts)

### Step 1: Open your connector settings

Go to **Customize → Connectors** in Claude, or navigate directly to:

```
https://claude.ai/customize/connectors
```

### Step 2: Start adding a custom connector

Click the **"+"** button, then choose **Add custom connector**.

### Step 3: Enter the MCP server URL

In the URL field, paste:

```
https://app.datalaboratory.ai/mcp
```

Leave **Advanced settings** alone unless you were given an OAuth Client ID and Client Secret.

### Step 4: Add the connector

Click **Add**. Data Laboratory now appears in your connector list with a **Custom** label.

### Step 5: Authenticate with OAuth

Click **Connect** next to Data Laboratory. A browser window opens on Data Laboratory's sign-in page.

1. Sign in with your Data Laboratory credentials.
2. Review the permissions being requested — check that the scopes match what you actually intend Claude to do.
3. Approve the request.

The window closes and the connector shows as connected. Claude never sees your password during this exchange; it receives a token instead.

**Now skip to "Enable the connector in a conversation" below.**

---

## Path B — Team and Enterprise plans

This is a two-part process: an Owner adds the connector once for the whole organization, then each member connects individually with their own Data Laboratory login.

### Part 1 — Owner or Primary Owner setup (done once)

**Step 1:** Go to **Organization settings → Connectors**, or navigate to:

```
https://claude.ai/admin-settings/connectors
```

**Step 2:** Click the **Add** button.

**Step 3:** Hover over **Custom**, then select **Web**.

**Step 4:** Enter the remote MCP server URL:

```
https://app.datalaboratory.ai/mcp
```

**Step 5:** Optionally open **Advanced settings** to specify an OAuth Client ID and Client Secret — only if Data Laboratory has provided these for your organization. Otherwise leave blank.

**Step 6:** Click **Add** to finish. Data Laboratory is now available to members of the organization.

### Part 2 — Each member connects

**Step 1:** Go to **Customize → Connectors** (`https://claude.ai/customize/connectors`).

**Step 2:** Find **Data Laboratory** in the list — it carries a **Custom** label.

**Step 3:** Click **Connect**.

**Step 4:** Complete the Data Laboratory OAuth sign-in in the browser window that opens, review the requested permissions, and approve.

Each member authenticates separately, so everyone's Claude access mirrors their own Data Laboratory permissions.

---

## Enable the connector in a conversation

Adding a connector doesn't automatically switch it on everywhere. To use Data Laboratory in a specific chat:

1. Click the **"+"** button in the lower left of the chat interface.
2. Select **Connectors**.
3. Toggle **Data Laboratory** on.

You can also use the **Search and tools** menu to turn off individual Data Laboratory tools you don't want available in that conversation.

---

## Verify it's working

Start a new conversation with the connector enabled and ask something that requires it, for example:

> What tools do you have available from Data Laboratory?

Claude should list the tools the server exposes. The first time Claude calls a tool, you'll get an approval prompt — review it before allowing. Reserve **"Allow always"** for tools you trust to run unsupervised.

---

## Troubleshooting

**Connector won't connect or times out**

Claude connects to MCP servers from Anthropic's cloud infrastructure, not from your laptop. This holds true across claude.ai, Claude Desktop, Cowork, and mobile. If `app.datalaboratory.ai` sits behind a VPN, corporate network, or firewall, the connection will fail even though the URL loads fine in your own browser. Allowlist Anthropic's IP ranges inbound — the current list is at `https://platform.claude.com/docs/en/api/ip-addresses`.

**OAuth window opens but sign-in fails**

Confirm your Data Laboratory account is active and that you're using the right credentials. If your organization enforces SSO on Data Laboratory, make sure you complete that flow rather than a password login.

**Connector appears but shows no tools**

Disconnect and reconnect to refresh the token, then confirm the URL is exactly `https://app.datalaboratory.ai/mcp` with no trailing characters.

**Connector isn't in the list at all (Team/Enterprise)**

An Owner hasn't added it yet. Members can't add custom connectors themselves on these plans — see Path B, Part 1.

**Tools appear but Claude says it can't see your data**

The OAuth grant scopes Claude to your own permissions. If the data you're expecting lives under a different Data Laboratory account or workspace, Claude won't reach it.

---

## Updating or removing the connector

Claude has no direct edit option for custom connectors. **To change any detail, remove the connector and re-add it** with the updated information.

To remove:

1. Go to **Customize → Connectors** (Team/Enterprise Owners: **Organization settings → Connectors** to remove it for the whole organization).
2. Find Data Laboratory in the Connectors section.
3. Click **Remove**, or click the three dots next to it and choose remove.
4. Follow the prompts.

You can also revoke Claude's access from the Data Laboratory side through that service's own security settings.

---

## Security notes

Custom connectors let Claude reach services Anthropic hasn't verified, so a few habits are worth keeping:

- **Trust the source.** Confirm `https://app.datalaboratory.ai/mcp` is the official endpoint published by Data Laboratory, not a URL forwarded from an untrusted place.
- **Read the OAuth scopes.** Narrow them where you can, and decline if the server asks for more than the work requires.
- **Watch for prompt injection.** A compromised MCP server can embed hidden instructions in its tool outputs. Claude has protections against this, but reviewing tool inputs and outputs is still worthwhile.
- **Disable write tools during Research.** Claude can invoke connector tools automatically during Research runs without asking each time, so turn off anything destructive first.
- **Note behavior changes.** Server developers can change what a tool does after you've approved it.

If you ever suspect an MCP server is malicious, report it to Anthropic's vulnerability disclosure program at `https://hackerone.com/anthropic-vdp/`.

---

## Reference

- Get started with custom connectors using remote MCP — `https://support.claude.com/en/articles/11175166-get-started-with-custom-connectors-using-remote-mcp`
- Custom connectors documentation — `https://claude.com/docs/connectors/custom/remote-mcp`
- Anthropic IP addresses — `https://platform.claude.com/docs/en/api/ip-addresses`

*Claude's connector UI changes periodically. If a menu label here doesn't match what you see, check the support article above for the current wording.*
