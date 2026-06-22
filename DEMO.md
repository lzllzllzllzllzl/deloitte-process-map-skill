# Deloitte Process Mapping Skill - Demo

## Your Files Analyzed

I've analyzed your two drawio files:
1. **X.X.X.X 供应商评价管理V1.2.drawio** - 7 activities, 3 roles, complex decision points
2. **X.X.X.X 供应商准入流程.drawio** - 9 activities, 7 roles, straightforward flow

## Key Improvements Applied

### 1. ✅ Horizontal Swimlanes with Vertical Role Labels
**Before**: Unclear orientation
**After**: 
```xml
<mxCell id="lane1" parent="1" style="shape=swimlane;startSize=80;horizontal=0;swimlaneLine=1;fillColor=#2A2A2A;strokeColor=#CCCCCC;fontColor=#FFFFFF;fontSize=11;">
  <mxGeometry height="90" width="1570" x="30" y="50" as="geometry" />
</mxCell>
<mxCell id="role1" parent="lane1" style="text;whiteSpace=wrap;fontColor=#FFFFFF;fontSize=16;" value="Role Name" vertex="1">
  <mxGeometry height="36" width="76" x="8" y="27" as="geometry" />
</mxCell>
```

### 2. ✅ Numbered Activities
**Before**: No consistent numbering
**After**:
```xml
<mxCell id="step01" parent="lane1" style="rounded=0;whiteSpace=wrap;fillColor=#000000;strokeColor=#FFFFFF;fontColor=#FFFFFF;strokeWidth=2;fontSize=16;" value="01&#xa;Activity Name" vertex="1">
  <mxGeometry height="50" width="180" x="200" y="20" as="geometry" />
</mxCell>
```

### 3. ✅ Color-Coded Inputs/Outputs
**System Inputs (Green)**: 
```xml
<mxCell id="sys01" parent="lane1" style="shape=document;whiteSpace=wrap;fillColor=#D1EDA0;strokeColor=#D1EDA0;fontColor=#000000;fontSize=12;fontStyle=1;size=0;" value="System Name" vertex="1">
  <mxGeometry height="30" width="80" x="200" y="-5" as="geometry" />
</mxCell>
```

**Document Outputs (Yellow)**:
```xml
<mxCell id="doc01" parent="lane1" style="shape=document;whiteSpace=wrap;fillColor=#FFC000;strokeColor=#FFC000;fontColor=#000000;fontSize=12;" value="《Document》" vertex="1">
  <mxGeometry height="29" width="100" x="300" y="70" as="geometry" />
</mxCell>
```

### 4. ✅ No Crossing Edges with Orthogonal Routing
```xml
<mxCell id="edge01" edge="1" parent="1" source="step01" target="step02" 
  style="edgeStyle=orthogonalEdgeStyle;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;
         exitX=1;exitY=0.5;exitDx=0;exitDy=0;entryX=0;entryY=0.5;entryDx=0;entryDy=0;
         strokeColor=#FFFFFF;strokeWidth=2;">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

### 5. ✅ Start/End Placement
**Start**: Top-left corner (x=30, y=50)
**End**: Top-right corner (x=1400, y=50)

### 6. ✅ Decision Points with Yes/No Labels
```xml
<mxCell id="decision01" parent="lane1" style="rhombus;whiteSpace=wrap;fillColor=#000000;strokeColor=#FFFFFF;fontColor=#FFFFFF;strokeWidth=2;fontSize=16;" value="Decision Question?" vertex="1">
  <mxGeometry height="70" width="120" x="500" y="10" as="geometry" />
</mxCell>
<mxCell id="label_yes" parent="lane1" style="text;fontSize=12;fontColor=#FFFFFF;fontStyle=1;" value="是" vertex="1">
  <mxGeometry height="25" width="25" x="625" y="20" as="geometry" />
</mxCell>
<mxCell id="label_no" parent="lane1" style="text;fontSize=12;fontColor=#FFFFFF;fontStyle=1;" value="否" vertex="1">
  <mxGeometry height="25" width="25" x="500" y="90" as="geometry" />
</mxCell>
```

## Your Supplier Access Process (Refactored)

Based on your file, here's how the improved structure would look:

**Roles** (7 swimlanes):
1. 流程驱动 (Process Driver)
2. 业务需求负责人 (Business Demand Owner)
3. 业务部门负责人 (Business Department Head)
4. 采购专员 (Procurement Specialist)
5. 风控专员 (Risk Control Specialist)
6. 财务专员 (Finance Specialist)
7. 技术工程师 (Technical Engineer)

**Activities** (9 numbered):
- 01: 供应商申请 (Business Demand Owner)
- 02: 业务审核 (Business Department Head)
- 03: 合规资质初审 (Procurement Specialist)
- 04: 风控合规审核 (Risk Control Specialist)
- 05: 财务资信审核 (Finance Specialist)
- 06: 是否需要样品 (Decision Point)
- 07: 样品测试验证 (Technical Engineer)
- 08: 终审准入与定级 (Procurement Specialist)
- 09: 建档归档 (Archivist)

**Systems**: 采购系统, 样品管理系统, 档案系统 (Green)
**Documents**: 《供应商资质资料》, 《样品》, 《样品测试报告》 (Yellow)

## Skill Files Created

```
deloitte-process-map-skill/
├── SKILL.md                          # Complete workflow & standards
├── README.md                         # Installation & usage guide
├── styles/
│   └── deloitte-standard.json        # Color/layout preset
└── references/
    ├── quick-reference.md            # Fast lookup table
    ├── examples.md                   # 3 complete XML examples
    └── troubleshooting.md            # Debug guide
```

## How to Use This Skill

### Step 1: Install

```bash
# Copy to Claude's skill directory
cp -r deloitte-process-map-skill ~/.claude/skills/
```

### Step 2: Request Process Map

Tell Claude:

```
Create a Deloitte process map for [your process]:

Roles:
- [Role 1]
- [Role 2]
- [Role 3]

Activities:
1. [Activity 1] ([Role])
2. [Activity 2] ([Role])
...

Systems: [list]
Documents: [list]
```

### Step 3: Review & Export

Claude will:
1. Generate complete XML
2. Export preview PNG (without -e)
3. Self-check for issues
4. Show you for feedback
5. Make corrections if needed
6. Final export (with -e)

## Key Benefits

✅ **Consistent Standards**: All Deloitte process maps look professional
✅ **No Crossing Edges**: Orthogonal routing enforced
✅ **Color-Coded**: Systems (green), Documents (yellow) at a glance
✅ **Numbered Activities**: Easy reference and tracking
✅ **Self-Checking**: Vision verification catches issues
✅ **Multiple Formats**: PNG, SVG, PDF exports
✅ **Editable**: Embedded XML keeps diagrams editable in draw.io

## Next Steps

1. **Try it**: Create a simple process map using the skill
2. **Customize**: Adjust colors in `styles/deloitte-standard.json` if needed
3. **Reference**: Keep `references/quick-reference.md` handy
4. **Feedback**: Report issues in `references/troubleshooting.md`

## Questions?

See:
- **SKILL.md** for complete documentation
- **README.md** for installation and usage
- **references/quick-reference.md** for fast lookup
- **references/troubleshooting.md** for debugging

---

**Version**: 1.0.0
**Created**: 2026-06-22
**Status**: Ready to use
