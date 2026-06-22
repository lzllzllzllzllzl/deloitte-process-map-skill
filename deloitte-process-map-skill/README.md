# Deloitte Process Mapping Skill

A professional draw.io skill for creating Deloitte-standard horizontal swimlane flowcharts with strict layout conventions.

## Features

✅ **Horizontal swimlane structure** with roles on left side
✅ **Numbered activities** (01, 02, 03...) with sequential numbering
✅ **No crossing edges** enforced through orthogonal routing
✅ **Color-coded elements**: 
  - Green (#D1EDA0) for system inputs
  - Yellow (#FFC000) for document outputs
✅ **Start/End placement**: Start in top-left, end in top-right
✅ **Decision points** with explicit Yes/No labels
✅ **Complete workflow**: Generate → Preview → Self-check → Review → Export
✅ **Multiple export formats**: PNG, SVG, PDF
✅ **Troubleshooting guide** and quick reference

## Installation

### Option 1: Copy to Claude Skills Directory

```bash
# Copy skill to Claude's skill directory
cp -r deloitte-process-map-skill ~/.claude/skills/

# Or if using Cowork mode
cp -r deloitte-process-map-skill "/Users/linzhili/Library/Application Support/Claude-3p/local-agent-mode-sessions/742ac7a5-ced7-433f-a578-d7c7cb706391/00000000-0000-4000-8000-000000000001/local_17623ddb-2686-4d68-b394-b5b610d9563f/skills/"
```

### Option 2: Use as Reference

If you just want to reference the standards without installing:
- See `references/quick-reference.md` for color codes and templates
- See `references/examples.md` for complete XML examples
- See `references/troubleshooting.md` for common issues

## Usage

### Basic Command

Ask Claude to create a Deloitte process map:

```
Create a Deloitte process map for [process name] with the following roles:
- Role 1: [name]
- Role 2: [name]
- Role 3: [name]

Activities:
1. [Activity 1] (Role 1)
2. [Activity 2] (Role 2)
3. [Activity 3] (Role 3)
...

Decision points:
- [Decision question] → Yes: [action], No: [action]

Systems/Inputs: [list]
Documents/Outputs: [list]
```

### Example Request

```
Create a Deloitte process map for supplier onboarding:

Roles:
- Business Demand Owner
- Business Department Head
- Procurement Specialist

Activities:
1. Supplier Application (Business Demand Owner)
2. Business Review (Business Department Head)
3. Compliance Check (Procurement Specialist)
4. Final Approval (Procurement Specialist)

Decision: Needs Sample? → Yes: Sample Testing, No: Skip to Approval

Systems: Procurement System
Documents: Supplier Application Form, Qualification Documents
```

### What Claude Will Do

1. **Understand**: Parse your request and clarify missing details
2. **Plan**: Determine layout, numbering, and connection points
3. **Generate**: Create complete draw.io XML following Deloitte standards
4. **Preview**: Export PNG for self-check (without -e flag)
5. **Self-check**: Vision verification for common issues
6. **Review**: Show you the PNG for feedback
7. **Export**: Final PNG, SVG, or PDF with embedded XML

## Color Standards (Memorize These)

| Element | fillColor | strokeColor | Use |
|---------|-----------|-------------|-----|
| **Background** | #000000 | - | Dark theme |
| **Swimlane** | #2A2A2A | #CCCCCC | Role lanes |
| **Activity** | #000000 | #FFFFFF | Work steps |
| **System/Input** | **#D1EDA0** | #00AA00 | Green boxes |
| **Document/Output** | **#FFC000** | #FFD700 | Yellow boxes |
| **Decision** | #000000 | #FFFFFF | Diamond shape |
| **Start/End** | #000000 | #FFFFFF | Rounded rect |

## Layout Rules (Critical)

### Activity Numbering
- Sequential: 01, 02, 03, 04...
- Format: `01&#xa;Activity Name`
- Across entire process, not per swimlane

### Connection Directions
- **Activities**: Left-in, right-out (or top-in, bottom-out)
- **Decisions**: Multiple exits with Yes/No labels
- **No crossing edges**: Use waypoints to detour

### Start/End Placement
- **Start**: Top-left corner (first swimlane, leftmost)
- **End**: Top-right corner (first swimlane, rightmost)

### Input/Output Placement
- **System inputs**: Green box at activity's top-left
- **Document outputs**: Yellow box at activity's bottom-right

## File Structure

```
deloitte-process-map-skill/
├── SKILL.md                          # Main skill documentation
├── README.md                         # This file
├── styles/
│   └── deloitte-standard.json        # Style preset
└── references/
    ├── quick-reference.md            # Color codes & templates
    ├── examples.md                   # Complete XML examples
    └── troubleshooting.md            # Common issues & fixes
```

## Prerequisites

- **draw.io desktop app** installed
- **Claude Cowork mode** enabled
- **Vision model** (Claude Sonnet or Opus) for self-check

### Install draw.io

```bash
brew install --cask drawio
```

## Export Commands

```bash
# Preview (for self-check, no -e)
drawio -x -f png --width 2000 -o process.png process.drawio

# Final PNG (with -e, editable in draw.io)
drawio -x -f png -e -s 2 -o process.drawio.png process.drawio
python3 scripts/repair_png.py process.drawio.png

# SVG (always editable)
drawio -x -f svg -e -o process.drawio.svg process.drawio

# PDF
drawio -x -f pdf -e -o process.drawio.pdf process.drawio
```

## Common Issues

| Issue | Solution |
|-------|----------|
| Edges crossing | Add waypoints to reroute |
| Wrong colors | Use #D1EDA0 (green) for systems, #FFC000 (yellow) for docs |
| Missing Yes/No | Add text cells with "是" and "否" |
| Export fails | Check draw.io CLI is installed: `drawio --version` |
| Vision rejects PNG | Export without -e for preview |

## References

- **SKILL.md**: Complete workflow and XML structure
- **quick-reference.md**: Fast color/layout lookup
- **examples.md**: Copy-paste XML examples
- **troubleshooting.md**: Debug common problems

## Comparison with Other Skills

| Feature | deloitte-process-map | ai-drawio | drawio-skill |
|---------|---------------------|-----------|--------------|
| Horizontal swimlanes | ✅ | ❌ | ✅ |
| Numbered activities | ✅ | ❌ | ❌ |
| Color standards | ✅ | Generic | Generic |
| No crossing edges | ✅ | Partial | Partial |
| Start/End placement | ✅ | ❌ | ❌ |
| Decision labels | ✅ | Partial | Partial |
| System/Document colors | ✅ | ❌ | ❌ |

**Use deloitte-process-map for**: Business processes, consulting deliverables, methodology diagrams
**Use ai-drawio for**: Quick simple diagrams, casual sketches
**Use drawio-skill for**: Architecture, ERD, UML, complex diagrams

## License

MIT License

## Version

1.0.0 (2026-06-22)

## Author

Claude Cowork
