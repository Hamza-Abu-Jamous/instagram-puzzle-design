# 🧩 Instagram Puzzle Design — Universal AI Agent Skill

> Production-tested AI skill and mathematical engineering guide for designing seamless **Instagram Puzzle Grids** (بازل إنستغرام).
> Built to work out-of-the-box with **any AI agent or coding assistant**: Cursor, Claude (Code / Projects), ChatGPT, GitHub Copilot, Windsurf, Antigravity, and any LLM.

---

## 🎯 What Problem Does This Solve?

Creating seamless Instagram puzzle grids with AI often leads to three critical flaws:
1. **Broken Lines at Slice Borders:** Diagonal lines shift vertically across post gaps due to sub-pixel rounding.
2. **Profile Cropping Destruction:** Instagram crops 4:5 portrait posts into 1:1 squares on profile pages, cutting off headlines and logos.
3. **Mirrored Order:** Publishing in normal chronological order flips the puzzle horizontally.

This skill equips your AI assistant with the **exact mathematical rules, crop coordinates, SVG paths, and safe zones** to generate zero-flaw puzzle designs every single time.

---

## 📦 What's Inside the Skill?

See full details in [`SKILL.md`](.agents/skills/instagram-puzzle-design/SKILL.md):

| Rule / Section | Description |
| :--- | :--- |
| 📐 **Master Canvas Dimensions** | Exact pixel dimensions for 3-post (`3240×1350`), 6-post (`3240×2700`), and 9-post (`3240×4050`) grids |
| 🛡️ **Zero-Slope Tangent Rule** | Mathematical rule (`dy/dx = 0`) at slice cuts (`x=1080`, `x=2160`) preventing line breaks |
| 🔲 **1:1 vs 4:5 Safe Zones** | Exact coordinates for the 1080×1080 px safe square (buffers: `y=0–135` & `y=1215–1350`) |
| 📅 **Publishing Sequence** | Reverse chronological publication order (Right → Center → Left) |
| ✂️ **Slice Coordinates** | Pixel-exact crop matrix for image generation and slicing scripts |
| 🔷 **SVG Bezier Laser Path** | Ready-to-use vector laser path with soft glow filter |
| 🤖 **AI Image Prompts** | Tuned prompts for Midjourney v6, Stable Diffusion, and Gemini Imagen |
| 🎨 **Brand Design System** | Modern tech color tokens and typography hierarchy |

---

## 🚀 How to Use With Any AI Agent

This skill is pure Markdown with standard YAML frontmatter. You can use it across any platform:

### 1. Cursor
Create a rule in your project:
* Place the content in `.cursor/rules/instagram-puzzle.mdc` or append it to `.cursorrules`.

### 2. Claude (Claude Code / Claude Desktop / Projects)
* **Claude Code:** Add `@.agents/skills/instagram-puzzle-design/SKILL.md` or append to your `CLAUDE.md`.
* **Claude Projects:** Upload `SKILL.md` directly into your Project Knowledge.

### 3. GitHub Copilot
* Add the skill instructions to `.github/copilot-instructions.md`.

### 4. Windsurf
* Add the skill to `.windsurfrules` in your workspace root.

### 5. Antigravity & Gemini CLI
* Clone or copy the `.agents/` directory into your project root. Antigravity will discover it automatically:
  ```bash
  git clone https://github.com/Hamza-Abu-Jamous/instagram-puzzle-design.git
  cp -r instagram-puzzle-design/.agents /path/to/your-project/
  ```

### 6. ChatGPT / Custom GPTs / Any Web LLM
* Open [`SKILL.md`](.agents/skills/instagram-puzzle-design/SKILL.md), copy the contents, and paste into **Instructions** or **System Prompt**.

---

## 📁 Repository Structure

```
.
├── .agents/
│   └── skills/
│       └── instagram-puzzle-design/
│           └── SKILL.md          ← Universal Skill & Instruction file
└── README.md                     ← Universal Guide & Documentation
```

---

## 📄 License

MIT License — Feel free to use, modify, and share in your commercial and personal projects.

---

> Crafted by [Programmers IT](https://programmersit.com) · Engineering reliable AI workflows.
