# Installing the Blue Contact plugin for Claude (Cowork)

This directory contains the Blue Contact plugin bundle for Cowork, the Claude desktop app.

**Download:** [claude-plugins.zip](https://github.com/Blue-Contact/docs/raw/refs/heads/main/plugin/claude-plugins.zip)

Plugins require a **paid plan** (Pro, Max, Team, or Enterprise) — the Free tier can't install plugins. There are two ways to install, depending on your account:

- **Individual users** (Pro or Max) — install the plugin for yourself. Jump to [Install for yourself](#install-for-yourself).
- **Teams / Enterprise owners & admins** — install for yourself first to verify, then push it to every member of the org so it's available by default. See [Roll out to your team](#roll-out-to-your-team-teams--enterprise).

Everyone should finish with [Run the setup command to get started](#run-the-setup-command-to-get-started).

## What you're installing

The `blue-contact` plugin adds:

- An MCP connection to Blue Contact's data platform at `query.bluecontact.com/mcp`
- 11 skills for audience building, market sizing, reporting, and data diagnostics
- Slash commands (e.g. `/blue-contact:getting-started`, `/blue-contact:audience-pull`)
- A `data-analyst` sub-agent for multi-step analysis
- Interactive React-based dashboards generated from your data

## Prerequisites

- A **paid** Claude plan (Pro, Max, Team, or Enterprise) — the Free tier cannot install plugins
- The Claude desktop app (Cowork) installed and signed in to your account
- The [`claude-plugins.zip`](https://github.com/Blue-Contact/docs/raw/refs/heads/main/plugin/claude-plugins.zip) bundle downloaded
- A Blue Contact account for the OAuth connection
- **For the team rollout only:** you must be the **owner** (or an admin with plugin management permission) on a Claude Teams or Enterprise account

---

## Install for yourself

This works on any **paid** Claude account — Pro, Max, or as an individual member of a Teams/Enterprise org. Teams/Enterprise owners should also do this first to verify the bundle before rolling it out.

1. Download [`claude-plugins.zip`](https://github.com/Blue-Contact/docs/raw/refs/heads/main/plugin/claude-plugins.zip).
2. Open the Claude desktop app.
3. Go to **Cowork → Customize → Plugins**.
4. Click the **+** button and choose **Upload plugin**.
5. Select the `claude-plugins.zip` you just downloaded.
6. Confirm the install. The `blue-contact` plugin should appear in your installed list.
7. Start a new Cowork session and run `/blue-contact:getting-started` to confirm it loads.

The plugin is distributed as a downloadable bundle only — it isn't published to a public plugin marketplace, so uploading the zip is the way to install it.

If you're an individual user, that's it — skip ahead to [Run the setup command to get started](#run-the-setup-command-to-get-started).

---

## Roll out to your team (Teams / Enterprise)

> This section requires a Claude **Teams or Enterprise** account and **owner/admin** permissions. Individual users don't have an admin console and can ignore this section — installing for yourself above is all you need.

Once you've confirmed the plugin works in your own Cowork, roll it out org-wide.

1. Open **Claude Admin settings** at [claude.ai/settings/admin](https://claude.ai/settings/admin) (you must be signed in as the Teams/Enterprise owner or an admin).
2. Navigate to **Capabilities → Plugins** (the plugin management panel may be labeled **Plugins & Connectors** in some admin console versions).
3. Click **Add plugin** and upload the [`claude-plugins.zip`](https://github.com/Blue-Contact/docs/raw/refs/heads/main/plugin/claude-plugins.zip) file.
4. When the upload completes, find `blue-contact` in the plugin list and open its settings.
5. Toggle **Install for all members** (sometimes labeled **Default for organization** or **Auto-install**) to **On**.
6. Optionally, toggle **Required** if you want to prevent members from uninstalling it.
7. Save.

New and existing members will see the plugin in Cowork automatically the next time their desktop app syncs — usually within a few minutes. They do not need to manually install anything.

### Verify the rollout

1. Ask a team member (or use a test account) to open the Cowork app.
2. Start a new Cowork session and type `/blue-contact:` — the slash command menu should show the Blue Contact commands.
3. Run `/blue-contact:setup` to confirm the MCP connection to `query.bluecontact.com/mcp` is authenticated.

If a member sees no Blue Contact commands, have them fully quit and reopen the Cowork app to force a plugin sync.

---

## Run the setup command to get started

Once the plugin is installed — whether you installed it for yourself or picked it up from an org rollout — the first thing to run is the setup command. It walks through connection verification and offers a guided tour of the data. Each user authenticates their own Blue Contact connection via OAuth, so every member does this once.

1. Open a new Cowork session.
2. Type:

   ```
   /blue-contact:setup
   ```

3. Claude will:
   - Verify the MCP connection to `https://query.bluecontact.com/mcp` and prompt you to authenticate via OAuth if needed.
   - Confirm the data catalogs available to your account.
   - Run a quick test query to confirm connectivity is live.
   - Load the schema so it knows what data you can query.
   - Ask if you'd like the guided tour — say **"Yes — give me the tour"** to hand off to `/blue-contact:getting-started`, which walks you through live examples tailored to your available data.

4. If you'd rather skip the tour, you can jump straight into common workflows:

   ```
   /blue-contact:audience-pull          # Build an audience from a one-line description
   /blue-contact:industry-playbooks     # Pre-built recipes for real estate, auto, insurance, etc.
   /blue-contact:data-health            # Diagnostic report on your data coverage and quality
   ```

5. Or just ask a question in natural language, for example:

   > "Build me an audience of homeowners in Austin, TX aged 30–45 with household income over $100K. I need name, address, phone, and email."

   The plugin's `data-querying` and `audience-building` skills activate automatically when you ask data questions — no slash command required.

### Troubleshooting setup

- **OAuth authentication fails:** Check that your Blue Contact credentials are active. Contact support@bluecontact.com if the login flow itself is broken.
- **"No data catalogs found":** The MCP is connected but the account has no catalog permissions. Reach out to Blue Contact support to confirm licensing.
- **Slow first query:** AWS Athena cold-starts can take 10–30 seconds for complex audience pulls. This is normal; subsequent queries are faster.

## Updating the plugin later

When a new version of `claude-plugins.zip` is released, re-download it and re-install:

- **Individual users:** Go to **Cowork → Customize → Plugins → `blue-contact`**, uninstall it, then upload the new zip.
- **Teams/Enterprise:** Go to Admin → Capabilities → Plugins → `blue-contact` → **Replace bundle**, upload the new zip, and save. All members pick up the new version on next Cowork sync.

## Removing the plugin

- **Individual users:** open **Cowork → Customize → Plugins → `blue-contact`** and click **Uninstall**. This removes it for you only.
- **Teams/Enterprise owners:** Admin → Capabilities → Plugins → `blue-contact` → **Remove from organization**. This uninstalls it for every member.

## Support

- Email: support@bluecontact.com
- GitHub Issues: https://github.com/Blue-Contact/docs/issues
