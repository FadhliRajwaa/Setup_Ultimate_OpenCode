# 📘 Panduan Setup OpenCode + Antigravity + Superpowers

Panduan simple untuk instalasi OpenCode dengan akses ke model AI gratis (Gemini, Claude, GPT).

> **Terakhir diperbarui:** 24 Desember 2025

---

## Step 1: Install OpenCode

Pilih salah satu:

```bash
# Menggunakan Bun (recommended)
bun add -g opencode-ai

# Menggunakan NPM
npm install -g opencode-ai
```

Verifikasi:

```bash
opencode --version
```

---

## Step 2: Buat File Konfigurasi

### 2.1 Buat folder dan file

**Windows:**

```powershell
New-Item -ItemType Directory -Force -Path "$env:USERPROFILE\.config\opencode\plugin"
notepad "$env:USERPROFILE\.config\opencode\opencode.json"
```

**Linux/macOS:**

```bash
mkdir -p ~/.config/opencode/plugin
nano ~/.config/opencode/opencode.json
```

### 2.2 Copy-paste konfigurasi berikut ke `opencode.json`:

```json
{
  "$schema": "https://opencode.ai/config.json",
  "plugin": [
    "opencode-antigravity-auth@1.2.3",
    "opencode-openai-codex-auth@4.2.0",
    "@nick-vi/opencode-type-inject@1.3.1",
    "@franlol/opencode-md-table-formatter@0.0.3",
    "@tarquinen/opencode-dcp@latest"
  ],
  "mcp": {
    "context7": {
      "type": "local",
      "command": ["npx", "-y", "@upstash/context7-mcp", "--api-key", "YOUR-CONTEXT7-API-KEY"],
      "enabled": true
    },
    "shadcn": {
      "type": "local",
      "command": ["npx", "-y", "shadcn", "mcp"],
      "enabled": true
    },
    "grep_app": {
      "type": "remote",
      "url": "https://mcp.grep.app"
    },
    "exa_search": {
      "type": "remote",
      "url": "https://mcp.exa.ai",
      "enabled": true,
      "headers": {
        "Authorization": "Bearer YOUR-EXA-API-KEY"
      }
    },
    "zai-mcp-server": {
      "type": "local",
      "command": ["bunx", "@z_ai/mcp-server"],
      "enabled": true,
      "environment": {
        "Z_AI_API_KEY": "YOUR-ZAI-API-KEY",
        "Z_AI_MODE": "ZAI"
      }
    },
    "web-search-prime": {
      "type": "remote",
      "url": "https://api.z.ai/api/mcp/web_search_prime/mcp",
      "headers": {
        "Authorization": "Bearer YOUR-ZAI-API-KEY"
      }
    },
    "web-reader": {
      "type": "remote",
      "url": "https://api.z.ai/api/mcp/web_reader/mcp",
      "headers": {
        "Authorization": "Bearer YOUR-ZAI-API-KEY"
      }
    }
  },
  "provider": {
    "google": {
      "models": {
        "gemini-3-pro-high": {
          "name": "Gemini 3 Pro High (Antigravity)",
          "limit": { "context": 1048576, "output": 65535 },
          "modalities": { "input": ["text", "image", "pdf"], "output": ["text"] }
        },
        "gemini-3-pro-low": {
          "name": "Gemini 3 Pro Low (Antigravity)",
          "limit": { "context": 1048576, "output": 65535 },
          "modalities": { "input": ["text", "image", "pdf"], "output": ["text"] }
        },
        "gemini-3-flash": {
          "name": "Gemini 3 Flash (Antigravity)",
          "limit": { "context": 1048576, "output": 65536 },
          "modalities": { "input": ["text", "image", "pdf"], "output": ["text"] }
        },
        "claude-sonnet-4-5": {
          "name": "Claude Sonnet 4.5 (Antigravity)",
          "limit": { "context": 200000, "output": 64000 },
          "modalities": { "input": ["text", "image", "pdf"], "output": ["text"] }
        },
        "claude-sonnet-4-5-thinking": {
          "name": "Claude Sonnet 4.5 Thinking (Antigravity)",
          "limit": { "context": 200000, "output": 64000 },
          "modalities": { "input": ["text", "image", "pdf"], "output": ["text"] }
        },
        "claude-opus-4-5-thinking": {
          "name": "Claude Opus 4.5 Thinking (Antigravity)",
          "limit": { "context": 200000, "output": 64000 },
          "modalities": { "input": ["text", "image", "pdf"], "output": ["text"] }
        },
        "gpt-oss-120b-medium": {
          "name": "GPT-OSS 120B Medium (Antigravity)",
          "limit": { "context": 131072, "output": 32768 },
          "modalities": { "input": ["text", "image", "pdf"], "output": ["text"] }
        }
      }
    },
    "openai": {
      "options": {
        "reasoningEffort": "medium",
        "reasoningSummary": "auto",
        "textVerbosity": "medium",
        "include": ["reasoning.encrypted_content"],
        "store": false
      },
      "models": {
        "gpt-5.2-none": {
          "name": "GPT 5.2 None (OAuth)",
          "limit": { "context": 272000, "output": 128000 },
          "modalities": { "input": ["text", "image"], "output": ["text"] },
          "options": { "reasoningEffort": "none", "reasoningSummary": "auto", "textVerbosity": "medium", "include": ["reasoning.encrypted_content"], "store": false }
        },
        "gpt-5.2-low": {
          "name": "GPT 5.2 Low (OAuth)",
          "limit": { "context": 272000, "output": 128000 },
          "modalities": { "input": ["text", "image"], "output": ["text"] },
          "options": { "reasoningEffort": "low", "reasoningSummary": "auto", "textVerbosity": "medium", "include": ["reasoning.encrypted_content"], "store": false }
        },
        "gpt-5.2-medium": {
          "name": "GPT 5.2 Medium (OAuth)",
          "limit": { "context": 272000, "output": 128000 },
          "modalities": { "input": ["text", "image"], "output": ["text"] },
          "options": { "reasoningEffort": "medium", "reasoningSummary": "auto", "textVerbosity": "medium", "include": ["reasoning.encrypted_content"], "store": false }
        },
        "gpt-5.2-high": {
          "name": "GPT 5.2 High (OAuth)",
          "limit": { "context": 272000, "output": 128000 },
          "modalities": { "input": ["text", "image"], "output": ["text"] },
          "options": { "reasoningEffort": "high", "reasoningSummary": "detailed", "textVerbosity": "medium", "include": ["reasoning.encrypted_content"], "store": false }
        },
        "gpt-5.2-xhigh": {
          "name": "GPT 5.2 Extra High (OAuth)",
          "limit": { "context": 272000, "output": 128000 },
          "modalities": { "input": ["text", "image"], "output": ["text"] },
          "options": { "reasoningEffort": "xhigh", "reasoningSummary": "detailed", "textVerbosity": "medium", "include": ["reasoning.encrypted_content"], "store": false }
        },
        "gpt-5.2-codex-low": {
          "name": "GPT 5.2 Codex Low (OAuth)",
          "limit": { "context": 272000, "output": 128000 },
          "modalities": { "input": ["text", "image"], "output": ["text"] },
          "options": { "reasoningEffort": "low", "reasoningSummary": "auto", "textVerbosity": "medium", "include": ["reasoning.encrypted_content"], "store": false }
        },
        "gpt-5.2-codex-medium": {
          "name": "GPT 5.2 Codex Medium (OAuth)",
          "limit": { "context": 272000, "output": 128000 },
          "modalities": { "input": ["text", "image"], "output": ["text"] },
          "options": { "reasoningEffort": "medium", "reasoningSummary": "auto", "textVerbosity": "medium", "include": ["reasoning.encrypted_content"], "store": false }
        },
        "gpt-5.2-codex-high": {
          "name": "GPT 5.2 Codex High (OAuth)",
          "limit": { "context": 272000, "output": 128000 },
          "modalities": { "input": ["text", "image"], "output": ["text"] },
          "options": { "reasoningEffort": "high", "reasoningSummary": "detailed", "textVerbosity": "medium", "include": ["reasoning.encrypted_content"], "store": false }
        },
        "gpt-5.2-codex-xhigh": {
          "name": "GPT 5.2 Codex Extra High (OAuth)",
          "limit": { "context": 272000, "output": 128000 },
          "modalities": { "input": ["text", "image"], "output": ["text"] },
          "options": { "reasoningEffort": "xhigh", "reasoningSummary": "detailed", "textVerbosity": "medium", "include": ["reasoning.encrypted_content"], "store": false }
        },
        "gpt-5.1-codex-max-low": {
          "name": "GPT 5.1 Codex Max Low (OAuth)",
          "limit": { "context": 272000, "output": 128000 },
          "modalities": { "input": ["text", "image"], "output": ["text"] },
          "options": { "reasoningEffort": "low", "reasoningSummary": "detailed", "textVerbosity": "medium", "include": ["reasoning.encrypted_content"], "store": false }
        },
        "gpt-5.1-codex-max-medium": {
          "name": "GPT 5.1 Codex Max Medium (OAuth)",
          "limit": { "context": 272000, "output": 128000 },
          "modalities": { "input": ["text", "image"], "output": ["text"] },
          "options": { "reasoningEffort": "medium", "reasoningSummary": "detailed", "textVerbosity": "medium", "include": ["reasoning.encrypted_content"], "store": false }
        },
        "gpt-5.1-codex-max-high": {
          "name": "GPT 5.1 Codex Max High (OAuth)",
          "limit": { "context": 272000, "output": 128000 },
          "modalities": { "input": ["text", "image"], "output": ["text"] },
          "options": { "reasoningEffort": "high", "reasoningSummary": "detailed", "textVerbosity": "medium", "include": ["reasoning.encrypted_content"], "store": false }
        },
        "gpt-5.1-codex-max-xhigh": {
          "name": "GPT 5.1 Codex Max Extra High (OAuth)",
          "limit": { "context": 272000, "output": 128000 },
          "modalities": { "input": ["text", "image"], "output": ["text"] },
          "options": { "reasoningEffort": "xhigh", "reasoningSummary": "detailed", "textVerbosity": "medium", "include": ["reasoning.encrypted_content"], "store": false }
        },
        "gpt-5.1-codex-low": {
          "name": "GPT 5.1 Codex Low (OAuth)",
          "limit": { "context": 272000, "output": 128000 },
          "modalities": { "input": ["text", "image"], "output": ["text"] },
          "options": { "reasoningEffort": "low", "reasoningSummary": "auto", "textVerbosity": "medium", "include": ["reasoning.encrypted_content"], "store": false }
        },
        "gpt-5.1-codex-medium": {
          "name": "GPT 5.1 Codex Medium (OAuth)",
          "limit": { "context": 272000, "output": 128000 },
          "modalities": { "input": ["text", "image"], "output": ["text"] },
          "options": { "reasoningEffort": "medium", "reasoningSummary": "auto", "textVerbosity": "medium", "include": ["reasoning.encrypted_content"], "store": false }
        },
        "gpt-5.1-codex-high": {
          "name": "GPT 5.1 Codex High (OAuth)",
          "limit": { "context": 272000, "output": 128000 },
          "modalities": { "input": ["text", "image"], "output": ["text"] },
          "options": { "reasoningEffort": "high", "reasoningSummary": "detailed", "textVerbosity": "medium", "include": ["reasoning.encrypted_content"], "store": false }
        },
        "gpt-5.1-codex-mini-medium": {
          "name": "GPT 5.1 Codex Mini Medium (OAuth)",
          "limit": { "context": 272000, "output": 128000 },
          "modalities": { "input": ["text", "image"], "output": ["text"] },
          "options": { "reasoningEffort": "medium", "reasoningSummary": "auto", "textVerbosity": "medium", "include": ["reasoning.encrypted_content"], "store": false }
        },
        "gpt-5.1-codex-mini-high": {
          "name": "GPT 5.1 Codex Mini High (OAuth)",
          "limit": { "context": 272000, "output": 128000 },
          "modalities": { "input": ["text", "image"], "output": ["text"] },
          "options": { "reasoningEffort": "high", "reasoningSummary": "detailed", "textVerbosity": "medium", "include": ["reasoning.encrypted_content"], "store": false }
        },
        "gpt-5.1-none": {
          "name": "GPT 5.1 None (OAuth)",
          "limit": { "context": 272000, "output": 128000 },
          "modalities": { "input": ["text", "image"], "output": ["text"] },
          "options": { "reasoningEffort": "none", "reasoningSummary": "auto", "textVerbosity": "medium", "include": ["reasoning.encrypted_content"], "store": false }
        },
        "gpt-5.1-low": {
          "name": "GPT 5.1 Low (OAuth)",
          "limit": { "context": 272000, "output": 128000 },
          "modalities": { "input": ["text", "image"], "output": ["text"] },
          "options": { "reasoningEffort": "low", "reasoningSummary": "auto", "textVerbosity": "low", "include": ["reasoning.encrypted_content"], "store": false }
        },
        "gpt-5.1-medium": {
          "name": "GPT 5.1 Medium (OAuth)",
          "limit": { "context": 272000, "output": 128000 },
          "modalities": { "input": ["text", "image"], "output": ["text"] },
          "options": { "reasoningEffort": "medium", "reasoningSummary": "auto", "textVerbosity": "medium", "include": ["reasoning.encrypted_content"], "store": false }
        },
        "gpt-5.1-high": {
          "name": "GPT 5.1 High (OAuth)",
          "limit": { "context": 272000, "output": 128000 },
          "modalities": { "input": ["text", "image"], "output": ["text"] },
          "options": { "reasoningEffort": "high", "reasoningSummary": "detailed", "textVerbosity": "high", "include": ["reasoning.encrypted_content"], "store": false }
        }
      }
    }
  },
  "theme": "lucent-orng",
  "tools": {
    "read": true,
    "edit": true,
    "write": true,
    "glob": true,
    "list": true,
    "grep": true
  },
  "permission": {
    "edit": "allow",
    "external_directory": "allow",
    "bash": "allow",
    "webfetch": "allow",
    "doom_loop": "allow"
  }
}
```

> **PENTING:** Ganti semua `YOUR-...-API-KEY` dengan API key Anda masing-masing. MCP servers bersifat **opsional** - hapus yang tidak dibutuhkan.

---

## Step 3: Setup Antigravity (Google Cloud)

Antigravity memerlukan Google Cloud Project untuk autentikasi.

### 3.1 Buat Project di Google Cloud Console

1. Buka https://console.cloud.google.com/
2. Klik **Select a project** → **New Project**
3. Beri nama project (misal: `opencode-antigravity`)
4. Klik **Create**
5. **Copy Project ID** (akan dibutuhkan nanti)

### 3.2 Enable Gemini for Google Cloud API

1. Di Cloud Console, buka **APIs & Services** → **Library**
2. Search **"Gemini for Google Cloud"**
3. Klik pada hasil pencarian
4. Klik **Enable**

### 3.3 Login di OpenCode

```bash
opencode auth login
```

1. Pilih **Google**
2. Pilih **OAuth with Google (Antigravity)**
3. **Paste Project ID** yang sudah di-copy
4. Browser akan terbuka → Login dengan akun Google Cloud yang sama
5. Selesai!

> ⚠️ **PENTING:** Jangan langsung test dengan `opencode`. Lanjut ke **Step 4** dulu untuk buat file `dcp.jsonc`.

---

## Step 4: Buat File DCP Config

DCP (Dynamic Context Pruning) mengoptimalkan penggunaan tokens.

Buat file `dcp.jsonc`:

**Windows:**

```powershell
notepad "$env:USERPROFILE\.config\opencode\dcp.jsonc"
```

**Linux/macOS:**

```bash
nano ~/.config/opencode/dcp.jsonc
```

Copy-paste:

```jsonc
{
  // Enable or disable the plugin
  "enabled": true,
  // Enable debug logging
  "debug": false,
  // Notification display: "off", "minimal", or "detailed"
  "pruneNotification": "detailed",
  // Protect from pruning for <turns> message turns
  "turnProtection": {
    "enabled": false,
    "turns": 4
  },
  // LLM-driven context pruning tools
  "tools": {
    // Shared settings for all prune tools
    "settings": {
      // Nudge the LLM to use prune tools
      "nudgeEnabled": true,
      "nudgeFrequency": 10,
      // Additional tools to protect from pruning
      "protectedTools": []
    },
    // Removes tool content from context without preservation
    "discard": {
      "enabled": true
    },
    // Distills key findings into preserved knowledge
    "extract": {
      "enabled": true,
      "showDistillation": false
    }
  },
  // Automatic pruning strategies
  "strategies": {
    // Remove duplicate tool calls
    "deduplication": {
      "enabled": true,
      "protectedTools": []
    },
    // Prune write tool inputs when file has been subsequently read
    "supersedeWrites": {
      "enabled": true
    },
    // (Legacy) Run an LLM to analyze on idle
    "onIdle": {
      "enabled": false,
      "protectedTools": [],
      "showModelErrorToasts": true,
      "strictModelSelection": false
    }
  }
}
```

---

## Step 5: Test Antigravity

```bash
opencode
```

1. Tekan `Tab` → `switch agent`
2. Pilih `google/claude-opus-4-5-thinking` atau `google/claude-sonnet-4-5-thinking`
3. Ketik prompt test: `hello, who are you?`

✅ **Jika tidak ada error** = Setup OpenCode Model Antigravity berhasil!

---

## Step 6: Install Superpowers (Skills System)

> ⚠️ **Step paling krusial** - Jangan gunakan symlink!

### 6.1 Clone Repository Superpowers

**Windows:**

```powershell
git clone https://github.com/obra/superpowers.git "$env:USERPROFILE\.config\opencode\superpowers"
```

**Linux/macOS:**

```bash
git clone https://github.com/obra/superpowers.git ~/.config/opencode/superpowers
```

### 6.2 Buat File Plugin

**Windows:**

```powershell
notepad "$env:USERPROFILE\.config\opencode\plugin\superpowers.js"
```

**Linux/macOS:**

```bash
nano ~/.config/opencode/plugin/superpowers.js
```

### 6.3 Copy-paste kode berikut (JANGAN gunakan symlink):

```javascript
/**
 * Superpowers plugin for OpenCode.ai
 * VERSI: 2.0.0 (AUTO-ACTIVE - Antigravity & Thinking Compatible)
 * 
 * PERUBAHAN DARI v1.1.0:
 * - Auto-active: Superpowers context otomatis tersedia di tool descriptions
 * - Tidak menggunakan client.session.prompt() (penyebab error thinking)
 * - Tools mengembalikan content langsung sebagai output
 * 
 * KOMPATIBEL DENGAN:
 * - Claude Opus/Sonnet Thinking models
 * - Gemini models
 * - OpenAI GPT models
 */

import path from 'path';
import fs from 'fs';
import os from 'os';
import { tool } from '@opencode-ai/plugin/tool';

const homeDir = os.homedir();
const superpowersDir = path.join(homeDir, '.config', 'opencode', 'superpowers');
const skillsCoreModule = path.join(superpowersDir, 'lib', 'skills-core.js');

let skillsCore = null;
const loadSkillsCore = async () => {
  if (!skillsCore) {
    try {
      skillsCore = await import(skillsCoreModule);
    } catch (err) {
      console.error('Failed to load skills-core.js:', err.message);
      skillsCore = {
        resolveSkillPath: () => null,
        stripFrontmatter: (content) => content,
        extractFrontmatter: () => ({}),
        findSkillsInDir: () => []
      };
    }
  }
  return skillsCore;
};

// Pre-load superpowers context for tool descriptions
let superpowersContext = null;
const getSuperpowersContext = async () => {
  if (superpowersContext) return superpowersContext;
  
  const core = await loadSkillsCore();
  const superpowersSkillsDir = path.join(superpowersDir, 'skills');
  const personalSkillsDir = path.join(homeDir, '.config', 'opencode', 'skills');
  
  const usingSuperpowersPath = core.resolveSkillPath('using-superpowers', superpowersSkillsDir, personalSkillsDir);
  if (!usingSuperpowersPath) {
    superpowersContext = '';
    return superpowersContext;
  }
  
  try {
    const fullContent = fs.readFileSync(usingSuperpowersPath.skillFile, 'utf8');
    superpowersContext = core.stripFrontmatter(fullContent);
  } catch (err) {
    superpowersContext = '';
  }
  
  return superpowersContext;
};

// Initialize context on module load
getSuperpowersContext();

export const SuperpowersPlugin = async ({ client, directory }) => {
  const core = await loadSkillsCore();
  const context = await getSuperpowersContext();
  
  const projectSkillsDir = path.join(directory, '.opencode', 'skills');
  const superpowersSkillsDir = path.join(superpowersDir, 'skills');
  const personalSkillsDir = path.join(homeDir, '.config', 'opencode', 'skills');

  // Build skills list for description
  let skillsList = '';
  try {
    const projectSkills = core.findSkillsInDir(projectSkillsDir, 'project', 3);
    const personalSkills = core.findSkillsInDir(personalSkillsDir, 'personal', 3);
    const superpowersSkills = core.findSkillsInDir(superpowersSkillsDir, 'superpowers', 3);
    const allSkills = [...projectSkills, ...personalSkills, ...superpowersSkills];
  
    skillsList = allSkills.slice(0, 10).map(s => {
      const ns = s.sourceType === 'project' ? 'project:' : s.sourceType === 'personal' ? '' : 'superpowers:';
      return `${ns}${s.name || path.basename(s.path)}`;
    }).join(', ');
  } catch (err) {
    skillsList = 'brainstorming, project-kickoff, code-review, debugging, refactoring';
  }

  return {
    tool: {
      // Main skill loading tool with superpowers context embedded in description
      use_skill: tool({
        description: `Load a skill to guide your work. YOU HAVE SUPERPOWERS - specialized skills for various tasks.

AVAILABLE SKILLS: ${skillsList || 'Run find_skills to see all'}

USAGE: use_skill("superpowers:brainstorming") or use_skill("project:my-skill")

TOOL MAPPING for OpenCode:
- TodoWrite → update_plan
- Task with subagents → @mention system
- Skill tool → use_skill
- File operations → Native OpenCode tools

SKILLS PRIORITY: project: > personal > superpowers:`,
        args: { 
          skill_name: tool.schema.string().describe('Skill name with namespace (e.g., "superpowers:brainstorming", "project:my-skill")') 
        },
        execute: async (args) => {
          const { skill_name } = args;
          const forceProject = skill_name.startsWith('project:');
          const actualSkillName = skill_name.replace(/^(project:|superpowers:|personal:)/, '');
          let resolved = null;

          // Check project skills first
          if (forceProject || !skill_name.startsWith('superpowers:')) {
            const projectSkillFile = path.join(projectSkillsDir, actualSkillName, 'SKILL.md');
            if (fs.existsSync(projectSkillFile)) {
              resolved = { skillFile: projectSkillFile, sourceType: 'project', skillPath: actualSkillName };
            }
          }
        
          // Then check superpowers/personal
          if (!resolved && !forceProject) {
            resolved = core.resolveSkillPath(skill_name, superpowersSkillsDir, personalSkillsDir);
          }
        
          if (!resolved) {
            return `❌ Skill "${skill_name}" not found.\n\nUse find_skills to see available skills.`;
          }

          try {
            const fullContent = fs.readFileSync(resolved.skillFile, 'utf8');
            const { name, description } = core.extractFrontmatter(resolved.skillFile);
            const content = core.stripFrontmatter(fullContent);
          
            // Return content directly - no session.prompt injection
            return `# 🎯 SKILL LOADED: ${name || skill_name}

${description ? `**Description:** ${description}\n` : ''}
**Source:** ${resolved.sourceType}
**Path:** ${path.dirname(resolved.skillFile)}

---

${content}

---
✅ Follow the instructions above to complete this skill.`;
          } catch (err) {
            return `❌ Error loading skill: ${err.message}`;
          }
        }
      }),

      // Find skills tool
      find_skills: tool({
        description: 'List all available superpowers skills. Use this to discover what skills you can load with use_skill.',
        args: {},
        execute: async () => {
          const projectSkills = core.findSkillsInDir(projectSkillsDir, 'project', 3);
          const personalSkills = core.findSkillsInDir(personalSkillsDir, 'personal', 3);
          const superpowersSkills = core.findSkillsInDir(superpowersSkillsDir, 'superpowers', 3);
          const allSkills = [...projectSkills, ...personalSkills, ...superpowersSkills];
        
          if (allSkills.length === 0) {
            return '❌ No skills found. Check if superpowers is installed at ~/.config/opencode/superpowers/';
          }
        
          let output = `# 🦸 SUPERPOWERS SKILLS\n\n`;
          output += `You have ${allSkills.length} skills available. Use \`use_skill("namespace:skill-name")\` to load one.\n\n`;
        
          // Group by source
          const grouped = { project: [], personal: [], superpowers: [] };
          for (const skill of allSkills) {
            grouped[skill.sourceType]?.push(skill);
          }
        
          if (grouped.project.length > 0) {
            output += `## 📁 Project Skills\n`;
            for (const skill of grouped.project) {
              output += `- **project:${skill.name || path.basename(skill.path)}** - ${skill.description || 'No description'}\n`;
            }
            output += '\n';
          }
        
          if (grouped.personal.length > 0) {
            output += `## 👤 Personal Skills\n`;
            for (const skill of grouped.personal) {
              output += `- **${skill.name || path.basename(skill.path)}** - ${skill.description || 'No description'}\n`;
            }
            output += '\n';
          }
        
          if (grouped.superpowers.length > 0) {
            output += `## 🦸 Superpowers Skills\n`;
            for (const skill of grouped.superpowers) {
              output += `- **superpowers:${skill.name || path.basename(skill.path)}** - ${skill.description || 'No description'}\n`;
            }
            output += '\n';
          }
        
          output += `---\n💡 **Tip:** Use \`use_skill("superpowers:brainstorming")\` to load a skill.`;
        
          return output;
        }
      }),

      // Quick superpowers info
      superpowers_info: tool({
        description: 'Get quick info about your superpowers capabilities.',
        args: {},
        execute: async () => {
          const projectSkills = core.findSkillsInDir(projectSkillsDir, 'project', 3);
          const personalSkills = core.findSkillsInDir(personalSkillsDir, 'personal', 3);
          const superpowersSkills = core.findSkillsInDir(superpowersSkillsDir, 'superpowers', 3);
        
          return `# 🦸 SUPERPOWERS ACTIVE

You have superpowers! Here's what you can do:

## Available Skills
- **Project:** ${projectSkills.length} skills
- **Personal:** ${personalSkills.length} skills  
- **Superpowers:** ${superpowersSkills.length} skills

## Quick Commands
- \`find_skills\` - List all available skills
- \`use_skill("superpowers:brainstorming")\` - Load a skill
- \`use_skill("superpowers:code-review")\` - Code review skill
- \`use_skill("superpowers:debugging")\` - Debugging skill

## Tool Mapping
| Claude Code | OpenCode |
|-------------|----------|
| TodoWrite | update_plan |
| Task | @mention |
| Skill | use_skill |

🚀 Ready to use superpowers!`;
        }
      })
    }
    // NOTE: No event handlers - avoiding client.session.prompt() which causes thinking model errors
  };
};
```

### 6.4 Test Superpowers

```bash
opencode
```

Ketik:

```
find_skills
```

✅ **Jika muncul list skills** = Setup Superpowers berhasil!

---

## Step 7: (Opsional) Plugin FS-Tool

Plugin untuk mengakses file yang biasanya diblokir (gitignored, hidden, .env).

> ⚠️ **Berbahaya** - Hanya aktifkan jika benar-benar diperlukan.

### 7.1 Buat File Plugin

```powershell
notepad "$env:USERPROFILE\.config\opencode\plugin\fs-tool.js"
```

### 7.2 Copy-paste kode:

```javascript
import { tool } from '@opencode-ai/plugin/tool';
import path from 'node:path';
import fs from 'node:fs/promises';

/* ===================== helpers ===================== */

function norm(p) {
  return p.replace(/\\/g, '/').trim();
}

function mustEnable() {
  if (process.env.OPENCODE_UNSAFE_FILES !== '1') {
    throw new Error(
      'Unsafe FS tools disabled. Set OPENCODE_UNSAFE_FILES=1 and restart OpenCode.'
    );
  }
}

function baseDirFrom(ctx) {
  return ctx?.worktree || ctx?.directory || process.cwd();
}

function resolvePath(inputPath, baseDir) {
  const p = norm(inputPath);
  return path.isAbsolute(p) ? p : path.resolve(baseDir, p);
}

function assertInBase(absPath, baseDir) {
  if (process.env.OPENCODE_UNSAFE_ALLOW_OUTSIDE === '1') return absPath;

  const rel = path.relative(baseDir, absPath);
  if (rel.startsWith('..') || path.isAbsolute(rel)) {
    throw new Error(`Path outside worktree blocked: ${absPath}`);
  }
  return absPath;
}

function assertNotGitDir(absPath) {
  if (process.env.OPENCODE_UNSAFE_INCLUDE_GIT === '1') return;

  const parts = norm(absPath).split('/');
  if (parts.includes('.git')) {
    throw new Error('Access to .git is blocked by default.');
  }
}

async function safeStat(absPath) {
  const st = await fs.lstat(absPath);
  return {
    isFile: st.isFile(),
    isDir: st.isDirectory(),
    isSymlink: st.isSymbolicLink(),
    size: st.size,
    mtimeMs: st.mtimeMs,
  };
}

/* ===================== plugin ===================== */

export default async function UnsafeFsPlugin(ctx) {
  return {
    tool: {
      fs_read: tool({
        description: 'Read any file (including gitignored & hidden). DANGEROUS.',
        args: {
          path: tool.schema.string(),
          maxBytes: tool.schema.number().optional(),
        },
        async execute({ path: p, maxBytes }, tctx) {
          mustEnable();
          const base = baseDirFrom(tctx);
          const abs = assertInBase(resolvePath(p, base), base);
          assertNotGitDir(abs);

          const limit = typeof maxBytes === 'number' ? maxBytes : 200_000;
          const buf = await fs.readFile(abs);
          if (buf.byteLength > limit) {
            return `File too large (${buf.byteLength} bytes).`;
          }
          return buf.toString('utf8');
        },
      }),

      fs_write: tool({
        description: 'Create or overwrite file (ignored allowed).',
        args: {
          path: tool.schema.string(),
          content: tool.schema.string(),
        },
        async execute({ path: p, content }, tctx) {
          mustEnable();
          const base = baseDirFrom(tctx);
          const abs = assertInBase(resolvePath(p, base), base);
          assertNotGitDir(abs);

          await fs.mkdir(path.dirname(abs), { recursive: true });
          await fs.writeFile(abs, content.replace(/\r\n/g, '\n'), 'utf8');
          return 'ok';
        },
      }),

      fs_append: tool({
        description: 'Append to file.',
        args: {
          path: tool.schema.string(),
          content: tool.schema.string(),
        },
        async execute({ path: p, content }, tctx) {
          mustEnable();
          const base = baseDirFrom(tctx);
          const abs = assertInBase(resolvePath(p, base), base);
          assertNotGitDir(abs);

          await fs.appendFile(abs, content.replace(/\r\n/g, '\n'), 'utf8');
          return 'ok';
        },
      }),

      fs_delete: tool({
        description: 'Delete file or directory.',
        args: {
          path: tool.schema.string(),
          recursive: tool.schema.boolean().optional(),
        },
        async execute({ path: p, recursive }, tctx) {
          mustEnable();
          const base = baseDirFrom(tctx);
          const abs = assertInBase(resolvePath(p, base), base);
          assertNotGitDir(abs);

          await fs.rm(abs, {
            recursive: recursive !== false,
            force: true,
          });
          return 'ok';
        },
      }),

      fs_list_raw: tool({
        description: 'List directory including hidden & ignored files. Returns formatted text list.',
        args: {
          path: tool.schema.string().optional(),
          maxItems: tool.schema.number().optional(),
        },
        async execute({ path: p, maxItems }, tctx) {
          mustEnable();
          const base = baseDirFrom(tctx);
          const abs = assertInBase(resolvePath(p || '.', base), base);
          assertNotGitDir(abs);

          const limit = typeof maxItems === 'number' ? maxItems : 500;
          const entries = await fs.readdir(abs, { withFileTypes: true });

          // Format as text list instead of returning objects
          const items = entries.slice(0, limit).map((e) => {
            const type = e.isDirectory() ? '[DIR]' : e.isFile() ? '[FILE]' : '[OTHER]';
            return `${type} ${e.name}`;
          });

          return `📁 Directory: ${abs}\n\nTotal: ${entries.length} items (showing ${items.length})\n\n${items.join('\n')}`;
        },
      }),

      fs_stat: tool({
        description: 'Get file metadata. Returns formatted text.',
        args: { path: tool.schema.string() },
        async execute({ path: p }, tctx) {
          mustEnable();
          const base = baseDirFrom(tctx);
          const abs = assertInBase(resolvePath(p, base), base);
          assertNotGitDir(abs);
          
          const st = await safeStat(abs);
          
          // Format as text instead of returning object
          return `📄 File: ${abs}
  
Type: ${st.isFile ? 'File' : st.isDir ? 'Directory' : st.isSymlink ? 'Symlink' : 'Other'}
Size: ${st.size} bytes
Modified: ${new Date(st.mtimeMs).toISOString()}`;
        },
      }),
    },
  };
}


```

### 7.3 Aktifkan Environment Variables

Tambahkan ke PowerShell Profile agar permanen:

```powershell
Add-Content -Path $PROFILE -Value @"

# OpenCode Unsafe FS Tools
`$env:OPENCODE_UNSAFE_FILES = '1'
`$env:OPENCODE_UNSAFE_ALLOW_OUTSIDE = '1'
`$env:OPENCODE_UNSAFE_INCLUDE_GIT = '1'
"@
```

Restart PowerShell, lalu jalankan `opencode`.

### 7.4 Fungsi Tools FS-Tool

| Tool            | Fungsi                                                              |
| --------------- | ------------------------------------------------------------------- |
| `fs_read`     | Membaca file apapun termasuk `.env`, `.gitignore`, hidden files |
| `fs_write`    | Menulis/overwrite file apapun                                       |
| `fs_append`   | Menambahkan content ke akhir file                                   |
| `fs_delete`   | Menghapus file/folder (termasuk recursive)                          |
| `fs_list_raw` | List directory termasuk hidden & ignored files                      |
| `fs_stat`     | Mendapatkan metadata file (size, modified time, dll)                |

> ⚠️ **Environment Variables:**
>
> - `OPENCODE_UNSAFE_FILES=1` - Wajib untuk mengaktifkan plugin
> - `OPENCODE_UNSAFE_ALLOW_OUTSIDE=1` - Akses file di luar project
> - `OPENCODE_UNSAFE_INCLUDE_GIT=1` - Akses folder `.git`

---

## ✅ Setup Selesai!

Sekarang Anda memiliki:

- ✅ OpenCode dengan model AI gratis (Antigravity)
- ✅ Claude Opus/Sonnet Thinking
- ✅ OpenAI GPT 5.1/5.2 (opsional)
- ✅ Superpowers skills system
- ✅ FS-Tool untuk akses file unrestricted (opsional)

---

## Referensi

- [NoeFabris/opencode-antigravity-auth](https://github.com/NoeFabris/opencode-antigravity-auth)
- [numman-ali/opencode-openai-codex-auth](https://github.com/numman-ali/opencode-openai-codex-auth)
- [obra/superpowers](https://github.com/obra/superpowers)

---

**Dibuat oleh Jarvis untuk Tuan Fadhli** | 24 Desember 2025
