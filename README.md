# 🧩 Programmers IT — Antigravity Skills & Customizations

> A collection of production-tested **Antigravity (AGY) skills** built by the [Programmers IT](https://programmersit.com) team.
> Drop the `.agents/` folder into any project to instantly teach your AI assistant our battle-tested workflows.

---

## 📦 Available Skills

### [`instagram-puzzle-design`](.agents/skills/instagram-puzzle-design/SKILL.md)

**Design pixel-perfect seamless Instagram Puzzle Grids (بازل إنستغرام).**

Covers everything derived from real production work:

| Topic | What's Inside |
| :--- | :--- |
| 📐 Master Canvas | Exact pixel dimensions for 3, 6, and 9-post grids |
| 🛡️ Horizontal Tangent Rule | How to prevent line-break artifacts at slice borders |
| 🔲 Safe Zones | 1:1 profile crop areas — where to place text & logos |
| 📅 Publishing Order | Right → Center → Left (bottom row first for multi-row) |
| ✂️ Slicing Coordinates | Pixel-exact crop coordinates for every post |
| 🔷 SVG Bezier Path | Mathematically correct laser ribbon across all 3 posts |
| 🤖 AI Prompts | Midjourney v6 / SD / Gemini prompts for backgrounds |
| 🎨 Brand System | Programmers IT colors (emerald + cyan) & fonts (Cairo + Plus Jakarta Sans) |

---

## 🚀 How to Use

### Option A — Use in your project (recommended)

Copy the `.agents/` folder into the root of your project:

```bash
cp -r .agents/ /path/to/your-project/
```

Antigravity will auto-discover the skills and load them on demand.

### Option B — Use globally on your machine

Copy the skills folder to your global Antigravity config:

```bash
# Windows
xcopy /E /I .agents\skills "%USERPROFILE%\.gemini\config\skills"

# macOS / Linux
cp -r .agents/skills ~/.gemini/config/skills/
```

### Option C — Reference via `skills.json`

Add to your project's `.agents/skills.json`:

```json
{
  "skills": [
    {
      "path": "https://raw.githubusercontent.com/Hamza-Abu-Jamous/instagram-puzzle-design/main/.agents/skills/instagram-puzzle-design/SKILL.md"
    }
  ]
}
```

---

## 📁 Repository Structure

```
.
├── .agents/
│   └── skills/
│       └── instagram-puzzle-design/
│           └── SKILL.md          ← Main skill file
├── Instagram Design/             ← Sample outputs and HTML previews
│   ├── instagram_grid_3post_perfect/
│   ├── instagram_grid_4x5/
│   ├── instagram_grid_bright_future/
│   └── instagram_grid_light_sample/
└── README.md
```

---

## 🤝 Contributing

Found a better formula or a new grid size? Open a PR!

1. Fork this repo
2. Add your skill under `.agents/skills/<skill-name>/SKILL.md`
3. Update this README
4. Open a Pull Request

---

## 📄 License

MIT — free to use, modify, and share.

---

> Built with ❤️ by **Programmers IT** · [programmersit.com](https://programmersit.com)
