# Setting Up Caveman as Default for a Git Repository

This guide walks you through installing necessary dependencies, obtaining the Caveman repository locally, and configuring any of your Git projects to use Caveman mode by default across supported AI agents (like GitHub Copilot, Cline, Cursor, and Windsurf).

## Why Use Caveman?

AI coding assistants like GitHub Copilot, Cursor, and Cline often generate overly verbose responses, filled with polite filler ("Sure! I can help with that!") and redundant explanations. Caveman mode enforces an ultra-compressed, terse communication style.

**Benefits:**
- **Saves Context Window:** Stripping out conversational fluff preserves your precious context window, allowing agents to retain more relevant code history in long sessions.
- **Faster Reading:** Get straight to the technical substance, reducing your cognitive load so you stay in the flow.
- **Zero Loss of Accuracy:** All code snippets, exact technical terms, and logic remain perfectly intact.
- **Cost Efficiency:** For agents where you pay per token (like Cline or open-source CLI tools), fewer output tokens means noticeably lower API costs over time.

## Prerequisites: Install Node.js & npm

Caveman's setup scripts require Node.js. If you don't have it installed, choose one of the following methods for Windows:

### Option 1: Using Winget (Command Line)
Open PowerShell and run:
```powershell
winget install OpenJS.NodeJS.LTS
```
*Note: Restart your terminal after installation so the new `node` and `npm` commands are available.*

### Option 2: Official Installer
1. Visit [nodejs.org](https://nodejs.org/).
2. Download and run the **LTS (Long Term Support)** `.msi` installer.
3. Accept the default settings.

Verify the installation by opening a new terminal and running:
```powershell
node -v
npm -v
```

---

## Step 1: Clone the Caveman Repository

To ensure you have the latest local copy of the installer (including any local fixes for Windows path execution), clone the repository to your machine. 

Open your terminal and run:
```powershell
# Navigate to a directory where you keep your code, e.g., D:\Code
cd D:\Code

# Clone the repository
git clone https://github.com/JuliusBrussee/caveman.git
```

This creates a local copy of Caveman at `D:\Code\caveman`.

---

## Step 2: Configure Your Target Repository

Now, apply Caveman's "always-on" rules to the project or repository where you want Caveman active by default.

1. Open your terminal and navigate to the root folder of your **target repository**:
   ```powershell
   cd C:\Path\To\Your\TargetProject
   ```

2. Run the local Caveman installer using the `--with-init` flag. Point `node` to the exact path where you cloned Caveman in Step 1:
   ```powershell
   node D:\Code\caveman\bin\install.js --with-init
   ```

### What this does:
The installer will detect which AI coding agents you use and automatically drop the appropriate rule files directly into your project's root folder. Examples include:
- `.github/copilot-instructions.md` (for GitHub Copilot in VS & VS Code)
- `.clinerules/caveman.md` (for Cline)
- `.cursor/rules/caveman.mdc` (for Cursor)
- `.windsurf/rules/caveman.md` (for Windsurf)
- `AGENTS.md` (for compatible open-standard agents)

---

## Step 3: Commit the Generated Files

To enforce Caveman mode for everyone working on this repository—and to ensure the rules persist—commit the newly generated configuration files to your version control.

```powershell
git add .
git commit -m "chore: enable caveman mode by default for AI agents"
git push
```

Now, whenever you or your team open this repository in an IDE with a supported agent, Caveman mode will automatically be active—no need to type `/caveman` in the prompt!

---

## Disabling Caveman Mode Temporarily
If Caveman mode is set as the repository default but you need a highly detailed response for a specific prompt, simply instruct the agent in your message:
> *"ignore caveman mode and explain this in full detail"*
