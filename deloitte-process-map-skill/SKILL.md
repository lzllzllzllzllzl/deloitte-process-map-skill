---
name: deloitte-process-map
description: Generate Deloitte-standard horizontal swimlane flowcharts with strict layout rules. Perfect for business process mapping, methodology diagrams, and consulting deliverables. Enforces: horizontal swimlanes, no crossing edges, numbered activities (01, 02...), green system inputs, yellow document outputs, roles on left side, and decision points with Yes/No labels.
version: 1.3.0
---

# Deloitte Process Mapping Skill

## Overview

Generate professional Deloitte-standard horizontal swimlane flowcharts in draw.io XML format. This skill enforces strict layout conventions required for consulting deliverables and methodology documentation.

**Key Features:**
- Horizontal swimlane structure with roles on left
- Numbered activities (01, 02, 03...)
- No crossing edges - orthogonal routing
- Color-coded elements: green for systems/inputs, yellow for documents/outputs
- Start and End in same swimlane (first role's lane)
- Decision points with explicit Yes/No labels
- Editable .drawio XML output
- Export to PNG, SVG, PDF

## When to Use

**Use this skill for:**
- Business process mapping
- Methodology and workflow diagrams
- Consulting deliverables requiring standardization
- Cross-functional process documentation
- Standard operating procedures (SOPs)

**Do NOT use for:**
- Freeform brainstorming or sketching → use excalidraw
- Quick simple diagrams without swimlanes → use ai-drawio
- Code diagrams or architecture → use drawio-skill
- Data models or ERDs → use drawio-skill

## Drawing Rules (Strict)

### Layout Structure

1. **Horizontal Orientation**: All swimlanes are horizontal (horizontal=0)
   - Roles are displayed vertically on the left side
   - Process flows left-to-right
   - Activities progress through the lanes

2. **Role Organization**:
   - Roles are placed in vertical lane headers on the left
   - Each role gets its own swimlane
   - Lane width matches role label
   - Separate lanes for different roles even if activities are sparse

3. **Activity Numbering**:
   - Use simple sequential numbering: 01, 02, 03, 04...
   - Number appears in activity box: `01&#xa;Activity Name`
   - Numbers are sequential across the entire flow
   - Never skip numbers

4. **Start and End**:
   - **CRITICAL: Both Start and End go in the FIRST swimlane** (not separate lanes)
   - **Start**: Placed in top-left corner of FIRST swimlane (leftmost position)
   - **End**: Placed in top-right corner of FIRST swimlane (rightmost position)
   - Use rounded rectangles with white border on dark background
   - Do NOT create separate "流程驱动（空白泳道）" lanes for start/end
   - First lane contains: Start → First Activity → ... → End

5. **Activity Box Format**:
   - Rectangular boxes (not rounded)
   - Activity number in first line (01, 02...)
   - Activity name in second line
   - Example: `01&#xa;供应商申请`

6. **Connection Rules**:
   - **NEVER cross edges** - must use orthogonal routing
   - Every activity must have left input (entry from left or top)
   - Every activity must have right output (exit to right or bottom)
   - Use `exitX=1;exitY=0.5` for right-side exits
   - Use `entryX=0;entryY=0.5` for left-side entries
   - Top entry: `entryX=0.5;entryY=0`
   - Bottom exit: `exitX=0.5;exitY=1`

7. **Decision Points**:
   - Diamond shape (rhombus)
   - Must have exactly **two exits**: Yes and No
   - Label both exits: `value="是"` and `value="否"` (or Yes/No)
   - Yes typically goes to next activity (right/down)
   - No typically goes back or to exception handler (left/up)

8. **Input/Output Documentation**:
   - **System Input (绿色)**: Always place at activity's **TOP** (上方)
   - **Document Input (黄色, 流入本活动)**: Place at activity's **TOP** (上方)
     - 例：供应商资质资料、供应商准入申请表
   - **Document Output (黄色, 归档/存档/不传递)**: Place at activity's **BOTTOM** (下方)
     - 例：《考评计划》、《评价报告》、《样品测试报告》
   - **Document Output (黄色, 流转给下游)**: Place at activity's **RIGHT** (右侧) - 仅当明确需要传递给下游活动时
   - Use document shapes for documents (yellow color)
   - Analyze each document to determine: is it an INPUT (上方), or OUTPUT (下方或右侧)?

9. **Collaboration/Grouping**:
   - When multiple activities belong to one phase or system, use collaboration boxes
   - Dashed border around grouped activities
   - Grouped activities should flow left-to-right within the group
   - 3+ activities with no downstream connections can be grouped

### Color Coding (Deloitte Standard)

**Swimlane Backgrounds:**
- Primary lanes: `#2A2A2A` (dark gray)
- Secondary lanes: `#333333` (medium dark gray)
- Borders: `#CCCCCC` (light gray)

**Activity Colors:**
- Activity boxes: `#000000` fill, `#FFFFFF` stroke, `#FFFFFF` font
- Activity borders: 2px solid white
- Font size: 16pt

**System/Input (Green):**
- Fill: `#D1EDA0`
- Stroke: `#00AA00` or `#D1EDA0`
- Font: `#000000` (black)
- Used for: Systems, databases, input sources
- Example: `采购系统`, `供应商管理`, `MOM系统`

**Document/Output (Yellow):**
- Fill: `#FFC000`
- Stroke: `#FFD700` or `#FFC000`
- Font: `#000000` (black)
- Used for: Documents, reports, outputs
- Example: `《样品测试报告》`, `《评价报告》`

**Decision Points:**
- Fill: `#000000`
- Stroke: `#FFFFFF`
- Font: `#FFFFFF`
- Border: 2px solid white

**Start/End:**
- Fill: `#000000`
- Stroke: `#FFFFFF`
- Font: `#FFFFFF`
- Border: 2px solid white
- Rounded rectangle shape

### Edge Routing Rules

1. **Orthogonal Routing Only**: Always use `edgeStyle=orthogonalEdgeStyle`
2. **No Crossing**: Plan paths mentally before generating XML
3. **Clean Paths**: 90-degree bends only, no diagonal lines
4. **Exit/Entry Points**: Be explicit:
   - Right exit: `exitX=1;exitY=0.5;exitDx=0;exitDy=0`
   - Left entry: `entryX=0;entryY=0.5;entryDx=0;entryDy=0`
   - Bottom exit: `exitX=0.5;exitY=1;exitDx=0;exitDy=0`
   - Top entry: `entryX=0.5;entryY=0;entryDx=0;entryDy=0`
5. **Waypoints**: Use `<Array as="points">` when path must detour
6. **Spacing**: Leave 80px+ corridors for edge routing between shape rows

## XML Structure

### File Skeleton

```xml
<?xml version="1.0" encoding="UTF-8"?>
<mxfile host="Electron">
  <diagram name="Process Name" id="process-map">
    <mxGraphModel dx="1500" dy="900" grid="0" gridSize="10" guides="1" tooltips="1" connect="1" arrows="1" fold="1" page="1" pageScale="1" pageWidth="1600" pageHeight="900" background="#000000" math="0" shadow="0">
      <root>
        <mxCell id="0" />
        <mxCell id="1" parent="0" />
        <!-- Title -->
        <!-- FIRST Swimlane (with Start + First Activity + End) -->
        <!-- Other Swimlanes -->
        <!-- Activities -->
        <!-- Edges -->
      </root>
    </mxGraphModel>
  </diagram>
</mxfile>
```

**Critical Rules:**
- `id="0"` and `id="1"` are required root cells
- User shapes start at `id="2"` and increment
- Background color: `#000000` (black)
- Grid disabled: `grid="0"`
- All text uses `html=1` for proper rendering
- Multi-line text: use `&#xa;` for line breaks
- **First swimlane contains Start, First Activity, and End**

### Swimlane Template

```xml
<!-- FIRST Swimlane (Lane 1) - contains Start, First Activity, and End -->
<mxCell id="lane1" parent="1" style="shape=swimlane;startSize=80;horizontal=0;swimlaneLine=1;fillColor=#2A2A2A;strokeColor=#CCCCCC;fontColor=#FFFFFF;fontSize=11;" value="" vertex="1">
  <mxGeometry height="90" width="1570" x="30" y="50" as="geometry" />
</mxCell>

<!-- Role label (vertical on left) -->
<mxCell id="role1" parent="lane1" style="text;whiteSpace=wrap;fontColor=#FFFFFF;fontSize=16;" value="Role Name" vertex="1">
  <mxGeometry height="36" width="76" x="8" y="27" as="geometry" />
</mxCell>

<!-- Start (leftmost position in first swimlane) -->
<mxCell id="start" parent="lane1" style="rounded=1;whiteSpace=wrap;fillColor=#000000;strokeColor=#FFFFFF;fontColor=#FFFFFF;strokeWidth=2;fontSize=12;" value="开始" vertex="1">
  <mxGeometry height="40" width="80" x="150" y="25" as="geometry" />
</mxCell>

<!-- End (rightmost position in first swimlane) -->
<mxCell id="end" parent="lane1" style="rounded=1;whiteSpace=wrap;fillColor=#000000;strokeColor=#FFFFFF;fontColor=#FFFFFF;strokeWidth=2;fontSize=12;" value="结束" vertex="1">
  <mxGeometry height="40" width="80" x="1490" y="25" as="geometry" />
</mxCell>

<!-- Other Swimlane (Lane 2) - only activities -->
<mxCell id="lane2" parent="1" style="shape=swimlane;startSize=80;horizontal=0;swimlaneLine=1;fillColor=#2A2A2A;strokeColor=#CCCCCC;fontColor=#FFFFFF;fontSize=11;" value="" vertex="1">
  <mxGeometry height="90" width="1570" x="30" y="140" as="geometry" />
</mxCell>
<mxCell id="role2" parent="lane2" style="text;whiteSpace=wrap;fontColor=#FFFFFF;fontSize=16;" value="Other Role" vertex="1">
  <mxGeometry height="36" width="76" x="8" y="27" as="geometry" />
</mxCell>
```

### Activity Template

```xml
<!-- Standard activity with number and name -->
<mxCell id="step01" parent="lane1" style="rounded=0;whiteSpace=wrap;fillColor=#000000;strokeColor=#FFFFFF;fontColor=#FFFFFF;strokeWidth=2;fontSize=16;" value="01&#xa;Activity Name" vertex="1">
  <mxGeometry height="50" width="180" x="280" y="20" as="geometry" />
</mxCell>

<!-- Activity with system input (green, top-left) - always same position -->
<mxCell id="sys01" parent="lane1" style="shape=document;whiteSpace=wrap;fillColor=#D1EDA0;strokeColor=#D1EDA0;fontColor=#000000;fontSize=12;fontStyle=1;size=0;" value="System Name" vertex="1">
  <mxGeometry height="30" width="80" x="280" y="-5" as="geometry" />
</mxCell>

<!-- CASE 1: Output flows to next activity (流转给下游) → RIGHT side -->
<mxCell id="doc01" parent="lane1" style="shape=document;whiteSpace=wrap;fillColor=#FFC000;strokeColor=#FFC000;fontColor=#000000;fontSize=12;fontStyle=1;" value="《流转文档》" vertex="1">
  <mxGeometry height="29" width="100" x="480" y="35" as="geometry" />
</mxCell>

<!-- CASE 2: Output is archived/final product (最终产物/存档) → BOTTOM side -->
<mxCell id="doc02" parent="lane1" style="shape=document;whiteSpace=wrap;fillColor=#FFC000;strokeColor=#FFC000;fontColor=#000000;fontSize=12;fontStyle=1;" value="《存档记录》" vertex="1">
  <mxGeometry height="29" width="100" x="350" y="80" as="geometry" />
</mxCell>
```

### Decision Point Template

```xml
<!-- Decision diamond -->
<mxCell id="decision01" parent="lane1" style="rhombus;whiteSpace=wrap;fillColor=#000000;strokeColor=#FFFFFF;fontColor=#FFFFFF;strokeWidth=2;fontSize=16;" value="06&#xa;Decision Question?" vertex="1">
  <mxGeometry height="70" width="120" x="500" y="10" as="geometry" />
</mxCell>

<!-- Yes label -->
<mxCell id="label_yes" parent="lane1" style="text;fontSize=12;fontColor=#FFFFFF;fontStyle=1;align=center;" value="是" vertex="1">
  <mxGeometry height="25" width="25" x="625" y="20" as="geometry" />
</mxCell>

<!-- No label -->
<mxCell id="label_no" parent="lane1" style="text;fontSize=12;fontColor=#FFFFFF;fontStyle=1;align=center;" value="否" vertex="1">
  <mxGeometry height="25" width="25" x="500" y="90" as="geometry" />
</mxCell>
```

### Edge Template

```xml
<!-- Horizontal edge (right exit to left entry) -->
<mxCell id="edge01" edge="1" parent="1" source="start" target="step01" style="edgeStyle=orthogonalEdgeStyle;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;exitX=1;exitY=0.5;exitDx=0;exitDy=0;entryX=0;entryY=0.5;entryDx=0;entryDy=0;strokeColor=#FFFFFF;strokeWidth=2;">
  <mxGeometry relative="1" as="geometry" />
</mxCell>

<!-- Vertical edge (bottom exit to top entry) -->
<mxCell id="edge02" edge="1" parent="1" source="step01" target="step02" style="edgeStyle=orthogonalEdgeStyle;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;exitX=0.5;exitY=1;exitDx=0;exitDy=0;entryX=0.5;entryY=0;entryDx=0;entryDy=0;strokeColor=#FFFFFF;strokeWidth=2;">
  <mxGeometry relative="1" as="geometry" />
</mxCell>

<!-- Edge with waypoints (to avoid crossing) -->
<mxCell id="edge03" edge="1" parent="1" source="lastactivity" target="end" style="edgeStyle=orthogonalEdgeStyle;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;strokeColor=#FFFFFF;strokeWidth=2;">
  <mxGeometry relative="1" as="geometry">
    <Array as="points">
      <mxPoint x="500" y="150" />
      <mxPoint x="500" y="300" />
    </Array>
  </mxGeometry>
</mxCell>
```

### Collaboration Box Template

```xml
<!-- Dashed border grouping multiple activities -->
<mxCell id="group01" parent="lane1" style="rounded=0;whiteSpace=wrap;html=1;fillColor=none;strokeColor=#FFFFFF;dashed=1;strokeWidth=2;" value="" vertex="1">
  <mxGeometry height="180" width="400" x="350" y="5" as="geometry" />
</mxCell>
```

## Workflow

### Step 1: Understand Request

Gather these details before generating:
- **Process name**: What is this process about?
- **Number of roles**: How many swimlanes needed?
- **Role names**: What are the role titles?
- **Activities per role**: What activities does each role perform?
- **Decision points**: Are there Yes/No branches?
- **Inputs/Outputs**: What systems/documents are involved?
- **Output format**: PNG, SVG, PDF, or all?

Skip clarification if details are already provided.

### Step 2: Plan Layout

Before writing XML, sketch the structure:

1. **Assign activities to roles** (which swimlane gets which activities)
2. **Determine sequence** (01, 02, 03... across the entire flow)
3. **Identify decision points** and their Yes/No branches
4. **Map inputs/outputs** to each activity (system/document)
5. **Analyze document flow** - CRITICAL for positioning:
   - **Document as INPUT to this activity** → Mark for TOP placement (上方)
   - **Document as OUTPUT (archived/归档)** → Mark for BOTTOM placement (下方)
   - **Document as OUTPUT (flows downstream/流转)** → Mark for RIGHT placement (右侧) - 少见
6. **Place Start and End in first swimlane** (not separate lanes)
7. **Calculate spacing**:
   - Horizontal gap between activities: 200-280px
   - Vertical gap between swimlanes: 90-100px
   - Edge routing corridors: 80px minimum

### Step 3: Generate XML

Build the XML systematically:

1. Create file skeleton with correct background
2. Add title (optional, at top center)
3. **Create FIRST swimlane with Start, First Activity, and End**
4. Create other swimlanes with their activities
5. Add role labels (left side of each swimlane)
6. Place activities (with numbers, left-to-right)
7. Add system inputs (green, **TOP** of activity)
8. **Add document inputs (yellow, TOP of activity) and document outputs (yellow, BOTTOM or RIGHT based on flow analysis)**
9. Add decision points with Yes/No labels
10. Create edges (check for crossing!)
11. Add collaboration boxes if needed

**Save file**: `process-name.drawio`

### Step 4: Preview Export (Without -e)

Export preview PNG for self-check (NO embedded XML):

```bash
drawio -x -f png --width 2000 -o process-name.png process-name.drawio
```

Or if binary is in different location:
```bash
/Applications/draw.io.app/Contents/MacOS/draw.io -x -f png --width 2000 -o process-name.png process-name.drawio
```

### Step 5: Self-Check (Vision)

Read the PNG and verify:

| Check | What to Look For | Auto-Fix |
|-------|-----------------|----------|
| Crossing edges | Any arrows intersecting each other | Reroute with waypoints |
| Activity numbering | Sequential: 01, 02, 03... | Renumber |
| Color coding | Green for systems, yellow for docs | Correct colors |
| **Start/End placement** | **Both in FIRST swimlane** | Reposition to first lane |
| **Document position** | **Inputs on TOP, archived outputs on BOTTOM, flow outputs on RIGHT** | Reposition based on document type |
| Connection directions | Left-in, right-out (or top-in, bottom-out) | Adjust entry/exit points |
| Decision labels | Both Yes and No present | Add missing labels |
| Overlapping shapes | Shapes stacked on each other | Shift apart (200px+) |
| Clipped labels | Text cut off at boundaries | Increase shape size |

Max 2 self-check rounds. If issues persist, proceed anyway.

### Step 6: Review Loop

Show PNG to user, collect feedback:

| User Request | XML Edit Action |
|-------------|----------------|
| Move activity X | Update `x`, `y` in mxGeometry |
| Resize activity | Update `width`, `height` in mxGeometry |
| Change color | Update `fillColor`/`strokeColor` in style |
| Add activity | Append new mxCell, renumber subsequent |
| Remove activity | Delete mxCell + edges, renumber |
| Change label text | Update `value` attribute |
| Fix crossing edge | Add `<Array as="points">` waypoints |
| **Move Start/End** | **Move to first swimlane, update connections** |
| **Move document output** | **Adjust position based on flow type (RIGHT or BOTTOM)** |

After each fix, re-export and show updated PNG.

### Step 7: Final Export

Once approved, export to requested formats:

```bash
# PNG with embedded XML (editable in draw.io)
drawio -x -f png -e -s 2 -o process-name.drawio.png process-name.drawio
python3 <skill-dir>/scripts/repair_png.py process-name.drawio.png

# SVG (always editable)
drawio -x -f svg -e -o process-name.drawio.svg process-name.drawio

# PDF
drawio -x -f pdf -e -o process-name.drawio.pdf process-name.drawio
```

Report file paths and offer to open in draw.io desktop.

## Complete Example

Here's a minimal 3-role, 5-activity process with Start/End in first swimlane:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<mxfile host="Electron">
  <diagram name="Supplier Onboarding" id="supplier-onboarding">
    <mxGraphModel dx="1200" dy="800" grid="0" gridSize="10" guides="1" tooltips="1" connect="1" arrows="1" fold="1" page="1" pageScale="1" pageWidth="1600" pageHeight="900" background="#000000" math="0" shadow="0">
      <root>
        <mxCell id="0" />
        <mxCell id="1" parent="0" />

        <!-- Title -->
        <mxCell id="title" parent="1" style="text;html=1;fontSize=18;fontStyle=1;align=center;fontColor=#FFFFFF;" value="X.X.X.X 供应商准入流程" vertex="1">
          <mxGeometry height="30" width="400" x="550" y="10" as="geometry" />
        </mxCell>

        <!-- Lane 1 (FIRST LANE) - Contains Start, First Activity, and End -->
        <mxCell id="lane1" parent="1" style="shape=swimlane;startSize=80;horizontal=0;swimlaneLine=1;fillColor=#2A2A2A;strokeColor=#CCCCCC;fontColor=#FFFFFF;fontSize=11;" value="" vertex="1">
          <mxGeometry height="90" width="1570" x="30" y="50" as="geometry" />
        </mxCell>
        <mxCell id="role1" parent="lane1" style="text;whiteSpace=wrap;fontColor=#FFFFFF;fontSize=16;" value="业务需求&#xa;负责人" vertex="1">
          <mxGeometry height="50" width="76" x="8" y="20" as="geometry" />
        </mxCell>
        <!-- Start (leftmost in first lane) -->
        <mxCell id="start" parent="lane1" style="rounded=1;whiteSpace=wrap;fillColor=#000000;strokeColor=#FFFFFF;fontColor=#FFFFFF;strokeWidth=2;fontSize=12;" value="开始" vertex="1">
          <mxGeometry height="40" width="80" x="150" y="25" as="geometry" />
        </mxCell>
        <!-- First Activity -->
        <mxCell id="step01" parent="lane1" style="rounded=0;whiteSpace=wrap;fillColor=#000000;strokeColor=#FFFFFF;fontColor=#FFFFFF;strokeWidth=2;fontSize=16;" value="01&#xa;供应商申请" vertex="1">
          <mxGeometry height="50" width="180" x="280" y="20" as="geometry" />
        </mxCell>
        <mxCell id="sys01" parent="lane1" style="shape=document;whiteSpace=wrap;fillColor=#D1EDA0;strokeColor=#D1EDA0;fontColor=#000000;fontSize=12;fontStyle=1;size=0;" value="采购系统" vertex="1">
          <mxGeometry height="30" width="80" x="280" y="-5" as="geometry" />
        </mxCell>
        <mxCell id="doc01" parent="lane1" style="shape=document;whiteSpace=wrap;fillColor=#FFC000;strokeColor=#FFC000;fontColor=#000000;fontSize=12;" value="《供应商&#xa;资质资料》" vertex="1">
          <mxGeometry height="35" width="80" x="380" y="70" as="geometry" />
        </mxCell>
        <!-- End (rightmost in first lane) -->
        <mxCell id="end" parent="lane1" style="rounded=1;whiteSpace=wrap;fillColor=#000000;strokeColor=#FFFFFF;fontColor=#FFFFFF;strokeWidth=2;fontSize=12;" value="结束" vertex="1">
          <mxGeometry height="40" width="80" x="1490" y="25" as="geometry" />
        </mxCell>

        <!-- Lane 2: Business Department -->
        <mxCell id="lane2" parent="1" style="shape=swimlane;startSize=80;horizontal=0;swimlaneLine=1;fillColor=#2A2A2A;strokeColor=#CCCCCC;fontColor=#FFFFFF;fontSize=11;" value="" vertex="1">
          <mxGeometry height="90" width="1570" x="30" y="140" as="geometry" />
        </mxCell>
        <mxCell id="role2" parent="lane2" style="text;whiteSpace=wrap;fontColor=#FFFFFF;fontSize=16;" value="业务部门&#xa;负责人" vertex="1">
          <mxGeometry height="50" width="76" x="8" y="20" as="geometry" />
        </mxCell>
        <mxCell id="step02" parent="lane2" style="rounded=0;whiteSpace=wrap;fillColor=#000000;strokeColor=#FFFFFF;fontColor=#FFFFFF;strokeWidth=2;fontSize=16;" value="02&#xa;业务审核" vertex="1">
          <mxGeometry height="50" width="180" x="550" y="20" as="geometry" />
        </mxCell>
        <mxCell id="sys02" parent="lane2" style="shape=document;whiteSpace=wrap;fillColor=#D1EDA0;strokeColor=#D1EDA0;fontColor=#000000;fontSize=12;fontStyle=1;size=0;" value="采购系统" vertex="1">
          <mxGeometry height="30" width="80" x="550" y="-5" as="geometry" />
        </mxCell>

        <!-- Lane 3: Procurement -->
        <mxCell id="lane3" parent="1" style="shape=swimlane;startSize=80;horizontal=0;swimlaneLine=1;fillColor=#2A2A2A;strokeColor=#CCCCCC;fontColor=#FFFFFF;fontSize=11;" value="" vertex="1">
          <mxGeometry height="90" width="1570" x="30" y="230" as="geometry" />
        </mxCell>
        <mxCell id="role3" parent="lane3" style="text;whiteSpace=wrap;fontColor=#FFFFFF;fontSize=16;" value="采购专员" vertex="1">
          <mxGeometry height="36" width="76" x="8" y="27" as="geometry" />
        </mxCell>
        <mxCell id="step03" parent="lane3" style="rounded=0;whiteSpace=wrap;fillColor=#000000;strokeColor=#FFFFFF;fontColor=#FFFFFF;strokeWidth=2;fontSize=16;" value="03&#xa;合规初审" vertex="1">
          <mxGeometry height="50" width="180" x="820" y="20" as="geometry" />
        </mxCell>
        <mxCell id="step04" parent="lane3" style="rounded=0;whiteSpace=wrap;fillColor=#000000;strokeColor=#FFFFFF;fontColor=#FFFFFF;strokeWidth=2;fontSize=16;" value="04&#xa;终审准入" vertex="1">
          <mxGeometry height="50" width="180" x="1150" y="20" as="geometry" />
        </mxCell>

        <!-- Decision point in Lane 3 -->
        <mxCell id="decision01" parent="lane3" style="rhombus;whiteSpace=wrap;fillColor=#000000;strokeColor=#FFFFFF;fontColor=#FFFFFF;strokeWidth=2;fontSize=16;" value="是否&#xa;需要样品？" vertex="1">
          <mxGeometry height="70" width="120" x="1050" y="10" as="geometry" />
        </mxCell>
        <mxCell id="label_yes" parent="lane3" style="text;fontSize=12;fontColor=#FFFFFF;fontStyle=1;" value="是" vertex="1">
          <mxGeometry height="25" width="25" x="1175" y="20" as="geometry" />
        </mxCell>
        <mxCell id="label_no" parent="lane3" style="text;fontSize=12;fontColor=#FFFFFF;fontStyle=1;" value="否" vertex="1">
          <mxGeometry height="25" width="25" x="1050" y="90" as="geometry" />
        </mxCell>

        <!-- Edges -->
        <mxCell id="edge01" edge="1" parent="1" source="start" target="step01" style="edgeStyle=orthogonalEdgeStyle;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;exitX=1;exitY=0.5;exitDx=0;exitDy=0;entryX=0;entryY=0.5;entryDx=0;entryDy=0;strokeColor=#FFFFFF;strokeWidth=2;">
          <mxGeometry relative="1" as="geometry" />
        </mxCell>
        <mxCell id="edge02" edge="1" parent="1" source="step01" target="step02" style="edgeStyle=orthogonalEdgeStyle;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;exitX=0.5;exitY=1;exitDx=0;exitDy=0;entryX=0.5;entryY=0;entryDx=0;entryDy=0;strokeColor=#FFFFFF;strokeWidth=2;">
          <mxGeometry relative="1" as="geometry" />
        </mxCell>
        <mxCell id="edge03" edge="1" parent="1" source="step02" target="step03" style="edgeStyle=orthogonalEdgeStyle;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;exitX=0.5;exitY=1;exitDx=0;exitDy=0;entryX=0;entryY=0.5;entryDx=0;entryDy=0;strokeColor=#FFFFFF;strokeWidth=2;">
          <mxGeometry relative="1" as="geometry" />
        </mxCell>
        <mxCell id="edge04" edge="1" parent="1" source="step03" target="decision01" style="edgeStyle=orthogonalEdgeStyle;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;exitX=1;exitY=0.5;exitDx=0;exitDy=0;entryX=0;entryY=0.5;entryDx=0;entryDy=0;strokeColor=#FFFFFF;strokeWidth=2;">
          <mxGeometry relative="1" as="geometry" />
        </mxCell>
        <mxCell id="edge05" edge="1" parent="1" source="decision01" target="step04" style="edgeStyle=orthogonalEdgeStyle;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;exitX=1;exitY=0.5;exitDx=0;exitDy=0;entryX=0;entryY=0.5;entryDx=0;entryDy=0;strokeColor=#FFFFFF;strokeWidth=2;" value="">
          <mxGeometry relative="1" as="geometry" />
        </mxCell>
        <mxCell id="edge06" edge="1" parent="1" source="step04" target="end" style="edgeStyle=orthogonalEdgeStyle;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;exitX=0.5;exitY=0;exitDx=0;exitDy=0;entryX=1;entryY=0.5;entryDx=0;entryDy=0;strokeColor=#FFFFFF;strokeWidth=2;">
          <mxGeometry relative="1" as="geometry" />
        </mxCell>
      </root>
    </mxGraphModel>
  </diagram>
</mxfile>
```

## Common Mistakes

| Problem | Cause | Solution |
|---------|-------|----------|
| Edges crossing | Poor path planning | Add waypoints, reroute |
| Wrong numbering | Skipping numbers | Renumber sequentially |
| Wrong colors | Not following Deloitte standard | Use green (#D1EDA0) for systems, yellow (#FFC000) for docs |
| Missing decision labels | No Yes/No on branches | Add explicit labels |
| Activities not numbered | Forgot numbering | Add 01, 02, 03... |
| **Start/End in separate lanes** | **Created extra blank lanes** | **Move both to first swimlane** |
| **Document output in wrong position** | **Not analyzing document flow type** | **Flow docs (下游) on RIGHT, archived docs (存档) on BOTTOM** |
| Diagonal lines | Not orthogonal | Use edgeStyle=orthogonalEdgeStyle |
| Clipped labels | Shape too small | Increase width/height |
| Overlapping shapes | No spacing | Separate by 200px+ |

## Troubleshooting

**Export fails:**
- Check if draw.io CLI is installed: `drawio --version`
- Try full path: `/Applications/draw.io.app/Contents/MacOS/draw.io --version`
- If sandbox issue: deliver XML only and ask user to export manually

**Vision API rejects PNG:**
- Exported with `-e` flag? Re-export without it for preview
- Use `--width 2000` to cap dimensions
- Run `repair_png.py` on final `-e` exports

**XML parse error:**
- Check for `--` in comments (illegal in XML)
- Verify all `&` are `&amp;`, `<` are `&lt;`, `>` are `&gt;`
- Ensure `id="0"` and `id="1"` exist

## Prerequisites

- draw.io desktop app installed
- CLI accessible (try `drawio --version`)
- For vision self-check: Claude Sonnet or Opus model

Install draw.io if missing:
```bash
brew install --cask drawio
```

## References

- Deloitte process mapping standards
- Draw.io XML specification
- ai-drawio skill (for simpler diagrams)
- drawio-skill (for architecture diagrams)

---

**Version**: 1.3.0
**Last Updated**: 2026-06-22
**Author**: Claude Cowork
**Changes**:
- v1.1.0: Updated rule 4 - both Start and End must be in FIRST swimlane (not separate lanes)
- v1.2.0: Updated rule 8 - Document output positioning based on flow analysis
- v1.3.0: Refined document positioning rules based on Deloitte standard examples:
  - System inputs (green) → Always TOP (上方)
  - Document inputs (yellow, flowing into activity) → TOP (上方)
  - Document outputs (yellow, archived/归档) → BOTTOM (下方)
  - Document outputs (yellow, flowing downstream/流转) → RIGHT (右侧) - rare case
