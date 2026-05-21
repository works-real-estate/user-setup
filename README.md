# Setting Up Claude for Content Edits

This walks you through getting Claude ready to make content edits to our codebase. Setup is one-time per Mac and takes about 30 minutes. An engineer will help during the group meeting if you get stuck.

## Before the meeting

You'll need:

- A **GitHub account** — create one at [github.com](https://github.com) if you don't have one, and save the password somewhere safe.
- **Membership in the `works-real-estate` GitHub org** with Write access on the project repo. Ask the dev team if you're not sure whether this is set up.
- **Claude desktop app** installed and signed in with your work email. ([Download for Mac](https://claude.ai/download))

## Setup steps

1. **Open Terminal.app** on your Mac (press Cmd+Space, type "Terminal", hit return).

2. **Run the setup script:**
   ```
   curl -fsSL https://raw.githubusercontent.com/works-real-estate/user-setup/main/setup.sh | bash
   ```

3. **Follow whatever the script prints.** The script handles most of the work automatically. It will:
   - Install Node.js and the GitHub CLI for you (it asks for your Mac password — that's normal).
   - Sometimes exit and ask you to run a one-off command yourself, then run the curl line again. Two cases where this happens:
     - **First time on this Mac**: it tells you to run `xcode-select --install`, click through the GUI prompt that appears, and wait for the install to finish.
     - **After GitHub CLI is installed**: it tells you to run `gh auth login` and follow the browser sign-in flow.
   - Each time the script exits with a prompt, do what it says, then **re-run the same `curl ... | bash` command**. The script picks up where it left off.

4. **Open the Claude desktop app** → **Code tab** → **New session** → set **Environment** to **Local** → pick the project folder the script set up (`~/dev/wre-dashboards` by default).

5. **Verify the preview pane** starts the dev server cleanly. If you see the running app in the preview pane next to the chat — you're set.

## If something goes wrong

The script prints clear messages whenever it can't continue. Most common cases:

- **"Xcode Command Line Tools not installed"** → script tells you the command (`xcode-select --install`). After it finishes, re-run the curl.
- **"GitHub CLI not authenticated"** → script tells you the command (`gh auth login`). After signing in, re-run the curl.
- **Wrong Node version** → the script auto-installs the right one; no action needed.

For anything else, ask in the meeting or in the `#dev` Slack channel.

## Day-to-day workflow

Once setup is done, the rhythm is:

1. Open Claude desktop, Code tab, pick the project.
2. Describe what you want to change in chat.
3. Claude makes edits; you see them live in the preview pane next to the chat.
4. When you're happy with the result, ask Claude to commit, push, and open a PR — it handles the git work.

You don't need to learn git commands. Claude follows the team's workflow rules (branch naming, where PRs go, what tests must pass) automatically. An engineer reviews your PR before it ships.

## Asking for an edit — what works well

Be specific about what you want and where. Examples that work well:

- "On the agent dashboard, change the header 'Top Performers' to 'Top Producing Agents'."
- "The 'New Deal' card description is too long. Trim it to two short sentences."
- "Make the section heading on the ZHL Funnel page use sentence case instead of title case."

Claude can navigate the codebase to find the right file, but pointing it at the page or component you're talking about speeds things up. Screenshots help when you're describing a visual issue.

## What Claude won't do

This setup is for **content edits** — copy, layout tweaks, visual changes. For anything that changes how the app behaves (data, calculations, user permissions, logic), Claude should hand off to engineering. If you're not sure whether your request is a content edit or a functional change, ask in the session — Claude will flag it.
