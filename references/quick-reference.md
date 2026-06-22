# Deloitte Process Mapping Quick Reference

## Color Codes (Memorize These)

| Element | fillColor | strokeColor | fontColor |
|---------|-----------|-------------|-----------|
| Background | `#000000` | - | - |
| Swimlane (primary) | `#2A2A2A` | `#CCCCCC` | `#FFFFFF` |
| Swimlane (secondary) | `#333333` | `#CCCCCC` | `#FFFFFF` |
| Activity | `#000000` | `#FFFFFF` | `#FFFFFF` |
| **System/Input** | `#D1EDA0` | `#00AA00` | `#000000` |
| **Document/Output** | `#FFC000` | `#FFD700` | `#000000` |
| Decision | `#000000` | `#FFFFFF` | `#FFFFFF` |
| Start/End | `#000000` | `#FFFFFF` | `#FFFFFF` |
| Edge | - | `#FFFFFF` | - |

## Activity Numbering

Format: `01&#xa;Activity Name`

- Sequential: 01, 02, 03, 04, 05...
- Never skip numbers
- Across entire process (not per swimlane)

## Connection Points (Critical!)

| Direction | exitX | exitY | entryX | entryY |
|-----------|-------|-------|--------|--------|
| **Right exit** | 1 | 0.5 | - | - |
| **Left entry** | - | - | 0 | 0.5 |
| **Bottom exit** | 0.5 | 1 | - | - |
| **Top entry** | - | - | 0.5 | 0 |
| **Top exit** | 0.5 | 0 | - | - |
| **Bottom entry** | - | - | 0.5 | 1 |

**Golden Rule**: Never let edges cross each other!

## XML Templates

### Swimlane
```xml
<mxCell id="lane1" parent="1" style="shape=swimlane;startSize=80;horizontal=0;swimlaneLine=1;fillColor=#2A2A2A;strokeColor=#CCCCCC;fontColor=#FFFFFF;fontSize=11;" value="" vertex="1">
  <mxGeometry height="90" width="1570" x="30" y="50" as="geometry" />
</mxCell>
```

### Activity
```xml
<mxCell id="step01" parent="lane1" style="rounded=0;whiteSpace=wrap;fillColor=#000000;strokeColor=#FFFFFF;fontColor=#FFFFFF;strokeWidth=2;fontSize=16;" value="01&#xa;Activity Name" vertex="1">
  <mxGeometry height="50" width="180" x="200" y="20" as="geometry" />
</mxCell>
```

### System Input (Green)
```xml
<mxCell id="sys01" parent="lane1" style="shape=document;whiteSpace=wrap;fillColor=#D1EDA0;strokeColor=#D1EDA0;fontColor=#000000;fontSize=12;fontStyle=1;size=0;" value="System Name" vertex="1">
  <mxGeometry height="30" width="80" x="200" y="-5" as="geometry" />
</mxCell>
```

### Document Output (Yellow)
```xml
<mxCell id="doc01" parent="lane1" style="shape=document;whiteSpace=wrap;fillColor=#FFC000;strokeColor=#FFC000;fontColor=#000000;fontSize=12;" value="《Document》" vertex="1">
  <mxGeometry height="29" width="100" x="300" y="70" as="geometry" />
</mxCell>
```

### Decision
```xml
<mxCell id="decision01" parent="lane1" style="rhombus;whiteSpace=wrap;fillColor=#000000;strokeColor=#FFFFFF;fontColor=#FFFFFF;strokeWidth=2;fontSize=16;" value="Question?" vertex="1">
  <mxGeometry height="70" width="120" x="500" y="10" as="geometry" />
</mxCell>
```

### Yes/No Labels
```xml
<mxCell id="label_yes" parent="lane1" style="text;fontSize=12;fontColor=#FFFFFF;fontStyle=1;" value="是" vertex="1">
  <mxGeometry height="25" width="25" x="625" y="20" as="geometry" />
</mxCell>
<mxCell id="label_no" parent="lane1" style="text;fontSize=12;fontColor=#FFFFFF;fontStyle=1;" value="否" vertex="1">
  <mxGeometry height="25" width="25" x="500" y="90" as="geometry" />
</mxCell>
```

### Edge (No Crossing)
```xml
<mxCell id="edge01" edge="1" parent="1" source="step01" target="step02" style="edgeStyle=orthogonalEdgeStyle;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;exitX=1;exitY=0.5;exitDx=0;exitDy=0;entryX=0;entryY=0.5;entryDx=0;entryDy=0;strokeColor=#FFFFFF;strokeWidth=2;">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

## Layout Dimensions

| Element | Width | Height |
|---------|-------|--------|
| Swimlane | 1570px | 90px |
| Activity | 180px | 50px |
| Decision | 120px | 70px |
| System Input | 80px | 30px |
| Document Output | 100px | 29px |
| Role Label | 76px | 36-50px |

**Horizontal gap between activities**: 200-280px
**Vertical gap between swimlanes**: 90-100px

## Export Commands

```bash
# Preview (no -e, for self-check)
drawio -x -f png --width 2000 -o process.png process.drawio

# Final (with -e, for delivery)
drawio -x -f png -e -s 2 -o process.drawio.png process.drawio
drawio -x -f svg -e -o process.drawio.svg process.drawio
drawio -x -f pdf -e -o process.drawio.pdf process.drawio

# After -e PNG export
python3 scripts/repair_png.py process.drawio.png
```

## Common Issues

| Issue | Fix |
|-------|-----|
| Edges crossing | Add waypoints: `<Array as="points"><mxPoint x="500" y="150" /></Array>` |
| Labels clipped | Increase width/height in mxGeometry |
| Wrong colors | Reference color table above |
| Missing Yes/No | Add text cells with "是" and "否" |
| Diagonal lines | Use `edgeStyle=orthogonalEdgeStyle` |
| Activity not numbered | Add "01&#xa;" prefix to value |
| Start/End misplaced | Start: top-left (x=30, y=50), End: top-right (x=1400, y=50) |

## Self-Check Checklist

- [ ] No crossing edges
- [ ] Activities numbered sequentially (01, 02, 03...)
- [ ] Green (#D1EDA0) for systems
- [ ] Yellow (#FFC000) for documents
- [ ] Start in top-left
- [ ] End in top-right
- [ ] Decision points have Yes/No labels
- [ ] All text readable (not clipped)
- [ ] No overlapping shapes
- [ ] Orthogonal edges only (90° bends)
- [ ] Connection points explicit (exitX, entryX, etc.)
