# 📘 Panduan Setup OpenCode + Superpowers + Antigravity

Panduan lengkap instalasi dan konfigurasi OpenCode dengan Superpowers skills dan koneksi ke Antigravity untuk akses model AI gratis.

---

## 📋 Daftar Isi

1. [Prasyarat](#1-prasyarat)
2. [Instalasi OpenCode](#2-instalasi-opencode)
3. [Konfigurasi Antigravity](#3-konfigurasi-antigravity)
4. [Setup Plugin Superpowers](#4-setup-plugin-superpowers)
5. [Konfigurasi Plugin Tambahan](#5-konfigurasi-plugin-tambahan)
6. [File Konfigurasi Lengkap](#6-file-konfigurasi-lengkap)
7. [Troubleshooting](#7-troubleshooting)

---

## 1. Prasyarat

### Software yang Dibutuhkan:

- **Node.js** v18+ (https://nodejs.org/)
- **Bun** (https://bun.sh/) - digunakan oleh OpenCode secara internal
- **Git** (https://git-scm.com/)
- **Browser** - untuk autentikasi OAuth

### Akun yang Dibutuhkan:

- **Google Account** - untuk autentikasi Antigravity

---

## 2. Instalasi OpenCode

### Langkah 1: Install OpenCode via Bun

```powershell
bun install -g opencode
```

### Langkah 2: Verifikasi Instalasi

```powershell
opencode --version
```

---

## 3. Konfigurasi Antigravity

Antigravity adalah layanan yang menyediakan akses gratis ke model AI seperti Gemini 3 Pro, Claude Sonnet/Opus, dll.

### Langkah 1: Buat File Konfigurasi

Buat file `opencode.json` di lokasi:

- **Windows:** `C:\Users\<username>\.config\opencode\opencode.json`
- **macOS/Linux:** `~/.config/opencode/opencode.json`

### Langkah 2: Tambahkan Plugin Antigravity Auth

Gunakan plugin **shekohex** (`opencode-google-antigravity-auth`) yang memiliki fitur lengkap:

```json
{
  "$schema": "https://opencode.ai/config.json",
  "model": "google/claude-opus-4-5-thinking",
  "plugin": [
    "opencode-google-antigravity-auth"
  ]
}
```

### Langkah 3: Autentikasi dengan Google

```powershell
opencode auth login
```

1. Pilih **Google** sebagai provider
2. Pilih **OAuth with Google (Antigravity)**
3. Browser akan terbuka untuk login Google
4. Setelah login, kembali ke terminal

### Langkah 4: Definisikan Model Antigravity

> **PENTING:** Konfigurasi model harus mengikuti format resmi dari [shekohex/opencode-google-antigravity-auth](https://github.com/shekohex/opencode-google-antigravity-auth).
>
> Model Claude menggunakan prefix `gemini-claude-*` dan suffix level thinking (`-high`, `-medium`, `-low`).

Tambahkan model Antigravity yang tersedia ke konfigurasi:

```json
{
  "provider": {
    "google": {
      "npm": "@ai-sdk/google",
      "models": {
        "gemini-3-pro-preview": {
          "id": "gemini-3-pro-preview",
          "name": "Gemini 3 Pro Preview",
          "reasoning": true,
          "limit": { "context": 1000000, "output": 64000 },
          "modalities": { "input": ["text", "image", "video", "audio", "pdf"], "output": ["text"] }
        },
        "gemini-3-pro-high": {
          "id": "gemini-3-pro-preview",
          "name": "Gemini 3 Pro (High Thinking)",
          "options": { "thinkingConfig": { "thinkingLevel": "high", "includeThoughts": true } }
        },
        "gemini-3-pro-medium": {
          "id": "gemini-3-pro-preview",
          "name": "Gemini 3 Pro (Medium Thinking)",
          "options": { "thinkingConfig": { "thinkingLevel": "medium", "includeThoughts": true } }
        },
        "gemini-3-pro-low": {
          "id": "gemini-3-pro-preview",
          "name": "Gemini 3 Pro (Low Thinking)",
          "options": { "thinkingConfig": { "thinkingLevel": "low", "includeThoughts": true } }
        },
        "gemini-3-flash": {
          "id": "gemini-3-flash",
          "name": "Gemini 3 Flash",
          "reasoning": true,
          "limit": { "context": 1048576, "output": 65536 },
          "modalities": { "input": ["text", "image", "video", "audio", "pdf"], "output": ["text"] }
        },
        "gemini-3-flash-high": {
          "id": "gemini-3-flash",
          "name": "Gemini 3 Flash (High Thinking)",
          "options": { "thinkingConfig": { "thinkingLevel": "high", "includeThoughts": true } }
        },
        "gemini-2.5-flash": {
          "id": "gemini-2.5-flash",
          "name": "Gemini 2.5 Flash",
          "reasoning": true,
          "limit": { "context": 1048576, "output": 65536 },
          "modalities": { "input": ["text", "image", "audio", "video", "pdf"], "output": ["text"] }
        },
        "gemini-claude-sonnet-4-5": {
          "id": "gemini-claude-sonnet-4-5",
          "name": "Claude Sonnet 4.5",
          "limit": { "context": 200000, "output": 64000 },
          "modalities": { "input": ["text", "image", "pdf"], "output": ["text"] }
        },
        "gemini-claude-sonnet-4-5-thinking-high": {
          "id": "gemini-claude-sonnet-4-5-thinking",
          "name": "Claude Sonnet 4.5 (High Thinking)",
          "reasoning": true,
          "limit": { "context": 200000, "output": 64000 },
          "modalities": { "input": ["text", "image", "pdf"], "output": ["text"] },
          "options": { "thinkingConfig": { "thinkingBudget": 32000, "includeThoughts": true } }
        },
        "gemini-claude-opus-4-5-thinking-high": {
          "id": "gemini-claude-opus-4-5-thinking",
          "name": "Claude Opus 4.5 (High Thinking)",
          "reasoning": true,
          "limit": { "context": 200000, "output": 64000 },
          "modalities": { "input": ["text", "image", "pdf"], "output": ["text"] },
          "options": { "thinkingConfig": { "thinkingBudget": 32000, "includeThoughts": true } }
        },
        "gemini-claude-opus-4-5-thinking-medium": {
          "id": "gemini-claude-opus-4-5-thinking",
          "name": "Claude Opus 4.5 (Medium Thinking)",
          "reasoning": true,
          "limit": { "context": 200000, "output": 64000 },
          "modalities": { "input": ["text", "image", "pdf"], "output": ["text"] },
          "options": { "thinkingConfig": { "thinkingBudget": 16000, "includeThoughts": true } }
        }
      }
    }
  }
}
```

**Model yang Tersedia:**

| Model | Tipe | Catatan |
|-------|------|---------|
| `gemini-3-pro-preview` | Gemini | Base model tanpa thinking |
| `gemini-3-pro-high/medium/low` | Gemini | Dengan thinking level |
| `gemini-3-flash` | Gemini | Fast model |
| `gemini-2.5-flash` | Gemini | Legacy stable |
| `gemini-claude-sonnet-4-5` | Claude | Tanpa thinking |
| `gemini-claude-sonnet-4-5-thinking-high` | Claude | Dengan thinking budget 32K |
| `gemini-claude-opus-4-5-thinking-high/medium` | Claude | Opus dengan thinking |

---


## 4. Setup Plugin Superpowers

Superpowers adalah plugin yang menyediakan skills/workflows untuk meningkatkan produktivitas.

> **Repository Resmi:** https://github.com/obra/superpowers
>
> **Dokumentasi:** https://github.com/obra/superpowers/blob/main/docs/README.opencode.md

---

### Langkah 1: Clone Repository Superpowers

**Windows (PowerShell):**

```powershell
# Clone langsung ke folder superpowers di .config/opencode
git clone https://github.com/obra/superpowers.git "$env:USERPROFILE\.config\opencode\superpowers"

# Verifikasi
ls "$env:USERPROFILE\.config\opencode\superpowers"
```

**Linux/macOS:**

```bash
# Clone langsung ke folder superpowers
mkdir -p ~/.config/opencode/superpowers
git clone https://github.com/obra/superpowers.git ~/.config/opencode/superpowers

# Verifikasi
ls ~/.config/opencode/superpowers
```

---

### Langkah 2: Buat Folder Plugin dan Symlink

**Windows (PowerShell sebagai Administrator):**

```powershell
# Buat folder plugin
New-Item -ItemType Directory -Force -Path "$env:USERPROFILE\.config\opencode\plugin"

# Buat symlink ke plugin superpowers
New-Item -ItemType SymbolicLink `
  -Path "$env:USERPROFILE\.config\opencode\plugin\superpowers.js" `
  -Target "$env:USERPROFILE\.config\opencode\superpowers\.opencode\plugin\superpowers.js"
```

**Linux/macOS:**

```bash
mkdir -p ~/.config/opencode/plugin
ln -sf ~/.config/opencode/superpowers/.opencode/plugin/superpowers.js ~/.config/opencode/plugin/superpowers.js
```

---

### Langkah 3: Perbaiki Bug Import Path (PENTING!)

> ⚠️ **BUG:** Plugin asli menggunakan relative import `'../../lib/skills-core.js'` yang tidak berfungsi dengan symlink.
>
> **PERBAIKAN:** Ganti dengan absolute path menggunakan `os.homedir()`.

**Edit file plugin:**

```powershell
# Windows
notepad "$env:USERPROFILE\.config\opencode\plugin\superpowers.js"
```

**GANTI SELURUH ISI FILE dengan kode yang sudah diperbaiki (VERSI 1.0.1 FIXED):**

```javascript
/**
 * Superpowers plugin for OpenCode.ai
 * VERSI: 1.0.1 (FIXED - Absolute path untuk symlink compatibility)
 * 
 * BUG YANG DIPERBAIKI:
 * - Import path '../../lib/skills-core.js' tidak berfungsi dengan symlink
 * - Solusi: Menggunakan absolute path dengan os.homedir()
 */

import path from 'path';
import fs from 'fs';
import os from 'os';
import { fileURLToPath } from 'url';
import { tool } from '@opencode-ai/plugin/tool';

const __dirname = path.dirname(fileURLToPath(import.meta.url));
const homeDir = os.homedir();

// PERBAIKAN BUG: Absolute path berdasarkan os.homedir()
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

export const SuperpowersPlugin = async ({ client, directory }) => {
  const core = await loadSkillsCore();
  
  const projectSkillsDir = path.join(directory, '.opencode', 'skills');
  const superpowersSkillsDir = path.join(superpowersDir, 'skills');
  const personalSkillsDir = path.join(homeDir, '.config', 'opencode', 'skills');

  const getBootstrapContent = (compact = false) => {
    const usingSuperpowersPath = core.resolveSkillPath('using-superpowers', superpowersSkillsDir, personalSkillsDir);
    if (!usingSuperpowersPath) return null;

    const fullContent = fs.readFileSync(usingSuperpowersPath.skillFile, 'utf8');
    const content = core.stripFrontmatter(fullContent);

    const toolMapping = compact
      ? `**Tool Mapping:** TodoWrite->update_plan, Task->@mention, Skill->use_skill
**Skills naming:** project: > personal > superpowers:`
      : `**Tool Mapping for OpenCode:**
- \`TodoWrite\` → \`update_plan\`
- \`Task\` with subagents → OpenCode's @mention system
- \`Skill\` tool → \`use_skill\`
- File operations → Native OpenCode tools

**Skills priority:** project: > personal > superpowers:`;

    return `<EXTREMELY_IMPORTANT>
You have superpowers.
${content}
${toolMapping}
</EXTREMELY_IMPORTANT>`;
  };

  const injectBootstrap = async (sessionID, compact = false) => {
    const bootstrapContent = getBootstrapContent(compact);
    if (!bootstrapContent) return false;
    try {
      await client.session.prompt({
        path: { id: sessionID },
        body: { noReply: true, parts: [{ type: "text", text: bootstrapContent, synthetic: true }] }
      });
      return true;
    } catch (err) { return false; }
  };

  return {
    tool: {
      use_skill: tool({
        description: 'Load a skill to guide your work.',
        args: { skill_name: tool.schema.string().describe('Skill name (e.g., "superpowers:brainstorming")') },
        execute: async (args, context) => {
          const { skill_name } = args;
          const forceProject = skill_name.startsWith('project:');
          const actualSkillName = forceProject ? skill_name.replace(/^project:/, '') : skill_name;
          let resolved = null;

          if (forceProject || !skill_name.startsWith('superpowers:')) {
            const projectSkillFile = path.join(projectSkillsDir, actualSkillName, 'SKILL.md');
            if (fs.existsSync(projectSkillFile)) {
              resolved = { skillFile: projectSkillFile, sourceType: 'project', skillPath: actualSkillName };
            }
          }
          if (!resolved && !forceProject) {
            resolved = core.resolveSkillPath(skill_name, superpowersSkillsDir, personalSkillsDir);
          }
          if (!resolved) return `Error: Skill "${skill_name}" not found. Run find_skills.`;

          const fullContent = fs.readFileSync(resolved.skillFile, 'utf8');
          const { name, description } = core.extractFrontmatter(resolved.skillFile);
          const content = core.stripFrontmatter(fullContent);
          const skillHeader = `# ${name || skill_name}\n# ${description || ''}\n# Directory: ${path.dirname(resolved.skillFile)}`;

          try {
            await client.session.prompt({
              path: { id: context.sessionID },
              body: { noReply: true, parts: [
                { type: "text", text: `Loading skill: ${name || skill_name}`, synthetic: true },
                { type: "text", text: `${skillHeader}\n\n${content}`, synthetic: true }
              ]}
            });
          } catch (err) { return `${skillHeader}\n\n${content}`; }
          return `Launching skill: ${name || skill_name}`;
        }
      }),
      find_skills: tool({
        description: 'List all available skills.',
        args: {},
        execute: async () => {
          const projectSkills = core.findSkillsInDir(projectSkillsDir, 'project', 3);
          const personalSkills = core.findSkillsInDir(personalSkillsDir, 'personal', 3);
          const superpowersSkills = core.findSkillsInDir(superpowersSkillsDir, 'superpowers', 3);
          const allSkills = [...projectSkills, ...personalSkills, ...superpowersSkills];
          if (allSkills.length === 0) return 'No skills found.';
          let output = 'Available skills:\n\n';
          for (const skill of allSkills) {
            const ns = skill.sourceType === 'project' ? 'project:' : skill.sourceType === 'personal' ? '' : 'superpowers:';
            output += `${ns}${skill.name || path.basename(skill.path)}\n  ${skill.description || ''}\n  ${skill.path}\n\n`;
          }
          return output;
        }
      })
    },
    event: async ({ event }) => {
      const sessionID = event.properties?.info?.id || event.properties?.sessionID || event.session?.id;
      if (event.type === 'session.created' && sessionID) await injectBootstrap(sessionID, false);
      if (event.type === 'session.compacted' && sessionID) await injectBootstrap(sessionID, true);
    }
  };
};
```

---

### Langkah 4: Verifikasi Skills

```powershell
# Hitung jumlah skill folders
(Get-ChildItem -Directory "$env:USERPROFILE\.config\opencode\superpowers\skills").Count
```

**Output:** `14` atau lebih

---

### Langkah 5: Test di OpenCode

```powershell
opencode
```

Ketik di OpenCode:

```
find_skills
```

---

### Update Superpowers

```powershell
cd "$env:USERPROFILE\.config\opencode\superpowers"
git pull
```

> ⚠️ Setelah `git pull`, edit kembali `superpowers.js` dengan versi fixed (Langkah 3)

---

## 5. Konfigurasi Plugin Tambahan

### Plugin yang Direkomendasikan:

| Plugin                                   | Fungsi                                    | Kompatibilitas Windows |
| ---------------------------------------- | ----------------------------------------- | ---------------------- |
| `opencode-google-antigravity-auth`     | Autentikasi Antigravity + Google Search   | ✅                     |
| `@nick-vi/opencode-type-inject`        | Type injection                            | ✅                     |
| `@franlol/opencode-md-table-formatter` | Format tabel markdown                     | ✅                     |
| `@tarquinen/opencode-dcp@latest`       | Dynamic Context Pruning (optimize tokens) | ✅                     |
| `opencode-zellij-namer`                | Rename Zellij sessions                    | ❌ (Linux/macOS only)  |

### Menambahkan Plugin:

Edit `opencode.json`:

```json
{
  "plugin": [
    "opencode-google-antigravity-auth",
    "@nick-vi/opencode-type-inject@1.3.1",
    "@franlol/opencode-md-table-formatter@0.0.3",
    "@tarquinen/opencode-dcp@latest"
  ]
}
```

### Konfigurasi DCP (Dynamic Context Pruning):

Buat file `~/.config/opencode/dcp.jsonc`:

```jsonc
{
  // Enable or disable the plugin
  "enabled": true,
  // Enable debug logging
  "debug": false,
  // Summary display: "off", "minimal", or "detailed"
  "pruningSummary": "detailed",
  "strategies": {
    "deduplication": {
      "enabled": true,
      "protectedTools": []
    },
    "supersedeWrites": {
      "enabled": true
    },
    "pruneTool": {
      "enabled": true,
      "protectedTools": [],
      "nudge": {
        "enabled": true,
        "frequency": 10
      }
    },
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

## 6. File Konfigurasi Lengkap

### `~/.config/opencode/opencode.json`

> **Referensi:** [shekohex/opencode-google-antigravity-auth](https://github.com/shekohex/opencode-google-antigravity-auth)

```json
{
  "$schema": "https://opencode.ai/config.json",
  "model": "google/gemini-3-pro-high",
  "plugin": [
    "opencode-google-antigravity-auth",
    "@nick-vi/opencode-type-inject@1.3.1",
    "@franlol/opencode-md-table-formatter@0.0.3",
    "@tarquinen/opencode-dcp@latest"
  ],
  "mcp": {
    "context7": {
      "type": "local",
      "command": ["npx", "-y", "@upstash/context7-mcp", "--api-key", "YOUR_API_KEY"],
      "enabled": true
    },
    "shadcn": {
      "type": "local",
      "command": ["npx", "-y", "shadcn", "mcp"],
      "enabled": true
    }
  },
  "provider": {
    "google": {
      "npm": "@ai-sdk/google",
      "models": {
        "gemini-3-pro-preview": {
          "id": "gemini-3-pro-preview",
          "name": "Gemini 3 Pro Preview",
          "reasoning": true,
          "limit": { "context": 1000000, "output": 64000 },
          "modalities": { "input": ["text", "image", "video", "audio", "pdf"], "output": ["text"] }
        },
        "gemini-3-pro-high": {
          "id": "gemini-3-pro-preview",
          "name": "Gemini 3 Pro (High Thinking)",
          "options": { "thinkingConfig": { "thinkingLevel": "high", "includeThoughts": true } }
        },
        "gemini-3-pro-medium": {
          "id": "gemini-3-pro-preview",
          "name": "Gemini 3 Pro (Medium Thinking)",
          "options": { "thinkingConfig": { "thinkingLevel": "medium", "includeThoughts": true } }
        },
        "gemini-3-pro-low": {
          "id": "gemini-3-pro-preview",
          "name": "Gemini 3 Pro (Low Thinking)",
          "options": { "thinkingConfig": { "thinkingLevel": "low", "includeThoughts": true } }
        },
        "gemini-3-flash": {
          "id": "gemini-3-flash",
          "name": "Gemini 3 Flash",
          "reasoning": true,
          "limit": { "context": 1048576, "output": 65536 },
          "modalities": { "input": ["text", "image", "video", "audio", "pdf"], "output": ["text"] }
        },
        "gemini-3-flash-high": {
          "id": "gemini-3-flash",
          "name": "Gemini 3 Flash (High Thinking)",
          "options": { "thinkingConfig": { "thinkingLevel": "high", "includeThoughts": true } }
        },
        "gemini-2.5-flash": {
          "id": "gemini-2.5-flash",
          "name": "Gemini 2.5 Flash",
          "reasoning": true,
          "limit": { "context": 1048576, "output": 65536 },
          "modalities": { "input": ["text", "image", "audio", "video", "pdf"], "output": ["text"] }
        },
        "gemini-claude-sonnet-4-5": {
          "id": "gemini-claude-sonnet-4-5",
          "name": "Claude Sonnet 4.5",
          "limit": { "context": 200000, "output": 64000 },
          "modalities": { "input": ["text", "image", "pdf"], "output": ["text"] }
        },
        "gemini-claude-sonnet-4-5-thinking-high": {
          "id": "gemini-claude-sonnet-4-5-thinking",
          "name": "Claude Sonnet 4.5 (High Thinking)",
          "reasoning": true,
          "limit": { "context": 200000, "output": 64000 },
          "modalities": { "input": ["text", "image", "pdf"], "output": ["text"] },
          "options": { "thinkingConfig": { "thinkingBudget": 32000, "includeThoughts": true } }
        },
        "gemini-claude-opus-4-5-thinking-high": {
          "id": "gemini-claude-opus-4-5-thinking",
          "name": "Claude Opus 4.5 (High Thinking)",
          "reasoning": true,
          "limit": { "context": 200000, "output": 64000 },
          "modalities": { "input": ["text", "image", "pdf"], "output": ["text"] },
          "options": { "thinkingConfig": { "thinkingBudget": 32000, "includeThoughts": true } }
        },
        "gemini-claude-opus-4-5-thinking-medium": {
          "id": "gemini-claude-opus-4-5-thinking",
          "name": "Claude Opus 4.5 (Medium Thinking)",
          "reasoning": true,
          "limit": { "context": 200000, "output": 64000 },
          "modalities": { "input": ["text", "image", "pdf"], "output": ["text"] },
          "options": { "thinkingConfig": { "thinkingBudget": 16000, "includeThoughts": true } }
        },
        "gemini-claude-opus-4-5-thinking-low": {
          "id": "gemini-claude-opus-4-5-thinking",
          "name": "Claude Opus 4.5 (Low Thinking)",
          "reasoning": true,
          "limit": { "context": 200000, "output": 64000 },
          "modalities": { "input": ["text", "image", "pdf"], "output": ["text"] },
          "options": { "thinkingConfig": { "thinkingBudget": 4000, "includeThoughts": true } }
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

---


## 7. Troubleshooting

### Error: "Requested entity was not found" (404)

**Penyebab:** OpenCode mencoba menggunakan model yang tidak tersedia di Antigravity.

**Solusi:** Pastikan ada konfigurasi `"model":` di `opencode.json`:

```json
"model": "google/claude-opus-4-5-thinking"
```

### Error: EBUSY saat instalasi plugin

**Penyebab:** Native binary conflicts di Windows.

**Solusi:**

```powershell
cd C:\Users\<username>\.cache\opencode
Remove-Item -Recurse -Force node_modules, bun.lock
bun install --ignore-scripts
bun pm trust --all
```

### Error: "Configuration is invalid"

**Penyebab:** Kesalahan sintaks JSON.

**Solusi:** Gunakan JSON validator online untuk mengecek file `opencode.json`.

### Plugin superpowers tidak berfungsi

**Penyebab:** Path import yang salah.

**Solusi:** Pastikan:

1. Folder `superpowers/` ada di `~/.config/opencode/`
2. File `lib/skills-core.js` ada
3. Folder `skills/` berisi 14 skill folders

### Cara melihat skills yang tersedia

Di OpenCode, ketik:

```
find_skills
```

Atau gunakan tool `use_skill` dengan nama skill:

```
use_skill superpowers:brainstorming
```

---

## 📚 Referensi

- [OpenCode Documentation](https://opencode.ai/docs/)
- [Antigravity Auth Plugin (shekohex)](https://github.com/shekohex/opencode-google-antigravity-auth)
- [Superpowers Skills](https://github.com/obra/superpowers)
- [DCP Plugin](https://github.com/Opencode-DCP/opencode-dynamic-context-pruning)

---

**Dibuat oleh Jarvis untuk Tuan Fadhli** | Terakhir diperbarui: 23 Desember 2025
