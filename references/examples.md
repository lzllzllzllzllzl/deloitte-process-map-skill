# Deloitte Process Mapping Examples

This file contains complete XML examples for common Deloitte process patterns.

## Example 1: Simple Linear Process (3 Activities)

**Process**: Basic approval workflow
**Roles**: Requester, Approver, Executor

```xml
<?xml version="1.0" encoding="UTF-8"?>
<mxfile host="Electron">
  <diagram name="Simple Approval" id="simple-approval">
    <mxGraphModel dx="1200" dy="700" grid="0" gridSize="10" guides="1" tooltips="1" connect="1" arrows="1" fold="1" page="1" pageScale="1" pageWidth="1600" pageHeight="900" background="#000000" math="0" shadow="0">
      <root>
        <mxCell id="0" />
        <mxCell id="1" parent="0" />
        
        <!-- Title -->
        <mxCell id="title" parent="1" style="text;html=1;fontSize=18;fontStyle=1;align=center;fontColor=#FFFFFF;" value="Simple Approval Process" vertex="1">
          <mxGeometry height="30" width="400" x="550" y="10" as="geometry" />
        </mxCell>
        
        <!-- Lane 1: Requester -->
        <mxCell id="lane1" parent="1" style="shape=swimlane;startSize=80;horizontal=0;swimlaneLine=1;fillColor=#2A2A2A;strokeColor=#CCCCCC;fontColor=#FFFFFF;fontSize=11;" value="" vertex="1">
          <mxGeometry height="90" width="1570" x="30" y="50" as="geometry" />
        </mxCell>
        <mxCell id="role1" parent="lane1" style="text;whiteSpace=wrap;fontColor=#FFFFFF;fontSize=16;" value="Requester" vertex="1">
          <mxGeometry height="36" width="76" x="8" y="27" as="geometry" />
        </mxCell>
        <mxCell id="step01" parent="lane1" style="rounded=0;whiteSpace=wrap;fillColor=#000000;strokeColor=#FFFFFF;fontColor=#FFFFFF;strokeWidth=2;fontSize=16;" value="01&#xa;Submit Request" vertex="1">
          <mxGeometry height="50" width="180" x="150" y="20" as="geometry" />
        </mxCell>
        
        <!-- Lane 2: Approver -->
        <mxCell id="lane2" parent="1" style="shape=swimlane;startSize=80;horizontal=0;swimlaneLine=1;fillColor=#2A2A2A;strokeColor=#CCCCCC;fontColor=#FFFFFF;fontSize=11;" value="" vertex="1">
          <mxGeometry height="90" width="1570" x="30" y="140" as="geometry" />
        </mxCell>
        <mxCell id="role2" parent="lane2" style="text;whiteSpace=wrap;fontColor=#FFFFFF;fontSize=16;" value="Approver" vertex="1">
          <mxGeometry height="36" width="76" x="8" y="27" as="geometry" />
        </mxCell>
        <mxCell id="step02" parent="lane2" style="rounded=0;whiteSpace=wrap;fillColor=#000000;strokeColor=#FFFFFF;fontColor=#FFFFFF;strokeWidth=2;fontSize=16;" value="02&#xa;Review &amp; Approve" vertex="1">
          <mxGeometry height="50" width="180" x="400" y="20" as="geometry" />
        </mxCell>
        
        <!-- Lane 3: Executor -->
        <mxCell id="lane3" parent="1" style="shape=swimlane;startSize=80;horizontal=0;swimlaneLine=1;fillColor=#2A2A2A;strokeColor=#CCCCCC;fontColor=#FFFFFF;fontSize=11;" value="" vertex="1">
          <mxGeometry height="90" width="1570" x="30" y="230" as="geometry" />
        </mxCell>
        <mxCell id="role3" parent="lane3" style="text;whiteSpace=wrap;fontColor=#FFFFFF;fontSize=16;" value="Executor" vertex="1">
          <mxGeometry height="36" width="76" x="8" y="27" as="geometry" />
        </mxCell>
        <mxCell id="step03" parent="lane3" style="rounded=0;whiteSpace=wrap;fillColor=#000000;strokeColor=#FFFFFF;fontColor=#FFFFFF;strokeWidth=2;fontSize=16;" value="03&#xa;Execute Task" vertex="1">
          <mxGeometry height="50" width="180" x="650" y="20" as="geometry" />
        </mxCell>
        
        <!-- Edges -->
        <mxCell id="edge01" edge="1" parent="1" source="step01" target="step02" style="edgeStyle=orthogonalEdgeStyle;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;exitX=0.5;exitY=1;exitDx=0;exitDy=0;entryX=0;entryY=0.5;entryDx=0;entryDy=0;strokeColor=#FFFFFF;strokeWidth=2;">
          <mxGeometry relative="1" as="geometry" />
        </mxCell>
        <mxCell id="edge02" edge="1" parent="1" source="step02" target="step03" style="edgeStyle=orthogonalEdgeStyle;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;exitX=0.5;exitY=1;exitDx=0;exitDy=0;entryX=0;entryY=0.5;entryDx=0;entryDy=0;strokeColor=#FFFFFF;strokeWidth=2;">
          <mxGeometry relative="1" as="geometry" />
        </mxCell>
      </root>
    </mxGraphModel>
  </diagram>
</mxfile>
```

## Example 2: Process with Decision Point

**Process**: Approval with Yes/No branch
**Decision**: If approved → proceed; if rejected → return

```xml
<?xml version="1.0" encoding="UTF-8"?>
<mxfile host="Electron">
  <diagram name="Approval with Decision" id="approval-decision">
    <mxGraphModel dx="1400" dy="900" grid="0" gridSize="10" guides="1" tooltips="1" connect="1" arrows="1" fold="1" page="1" pageScale="1" pageWidth="1600" pageHeight="900" background="#000000" math="0" shadow="0">
      <root>
        <mxCell id="0" />
        <mxCell id="1" parent="0" />
        
        <!-- Title -->
        <mxCell id="title" parent="1" style="text;html=1;fontSize=18;fontStyle=1;align=center;fontColor=#FFFFFF;" value="Approval with Decision Point" vertex="1">
          <mxGeometry height="30" width="400" x="550" y="10" as="geometry" />
        </mxCell>
        
        <!-- Lane 1: Requester -->
        <mxCell id="lane1" parent="1" style="shape=swimlane;startSize=80;horizontal=0;swimlaneLine=1;fillColor=#2A2A2A;strokeColor=#CCCCCC;fontColor=#FFFFFF;fontSize=11;" value="" vertex="1">
          <mxGeometry height="90" width="1570" x="30" y="50" as="geometry" />
        </mxCell>
        <mxCell id="role1" parent="lane1" style="text;whiteSpace=wrap;fontColor=#FFFFFF;fontSize=16;" value="Requester" vertex="1">
          <mxGeometry height="36" width="76" x="8" y="27" as="geometry" />
        </mxCell>
        <mxCell id="step01" parent="lane1" style="rounded=0;whiteSpace=wrap;fillColor=#000000;strokeColor=#FFFFFF;fontColor=#FFFFFF;strokeWidth=2;fontSize=16;" value="01&#xa;Submit Request" vertex="1">
          <mxGeometry height="50" width="180" x="150" y="20" as="geometry" />
        </mxCell>
        
        <!-- Lane 2: Approver -->
        <mxCell id="lane2" parent="1" style="shape=swimlane;startSize=80;horizontal=0;swimlaneLine=1;fillColor=#2A2A2A;strokeColor=#CCCCCC;fontColor=#FFFFFF;fontSize=11;" value="" vertex="1">
          <mxGeometry height="90" width="1570" x="30" y="140" as="geometry" />
        </mxCell>
        <mxCell id="role2" parent="lane2" style="text;whiteSpace=wrap;fontColor=#FFFFFF;fontSize=16;" value="Approver" vertex="1">
          <mxGeometry height="36" width="76" x="8" y="27" as="geometry" />
        </mxCell>
        <mxCell id="step02" parent="lane2" style="rounded=0;whiteSpace=wrap;fillColor=#000000;strokeColor=#FFFFFF;fontColor=#FFFFFF;strokeWidth=2;fontSize=16;" value="02&#xa;Review Request" vertex="1">
          <mxGeometry height="50" width="180" x="350" y="20" as="geometry" />
        </mxCell>
        <mxCell id="decision01" parent="lane2" style="rhombus;whiteSpace=wrap;fillColor=#000000;strokeColor=#FFFFFF;fontColor=#FFFFFF;strokeWidth=2;fontSize=16;" value="Approved?" vertex="1">
          <mxGeometry height="70" width="120" x="580" y="10" as="geometry" />
        </mxCell>
        <mxCell id="label_yes" parent="lane2" style="text;fontSize=12;fontColor=#FFFFFF;fontStyle=1;" value="是" vertex="1">
          <mxGeometry height="25" width="25" x="705" y="20" as="geometry" />
        </mxCell>
        <mxCell id="label_no" parent="lane2" style="text;fontSize=12;fontColor=#FFFFFF;fontStyle=1;" value="否" vertex="1">
          <mxGeometry height="25" width="25" x="580" y="90" as="geometry" />
        </mxCell>
        
        <!-- Lane 3: Executor -->
        <mxCell id="lane3" parent="1" style="shape=swimlane;startSize=80;horizontal=0;swimlaneLine=1;fillColor=#2A2A2A;strokeColor=#CCCCCC;fontColor=#FFFFFF;fontSize=11;" value="" vertex="1">
          <mxGeometry height="90" width="1570" x="30" y="230" as="geometry" />
        </mxCell>
        <mxCell id="role3" parent="lane3" style="text;whiteSpace=wrap;fontColor=#FFFFFF;fontSize=16;" value="Executor" vertex="1">
          <mxGeometry height="36" width="76" x="8" y="27" as="geometry" />
        </mxCell>
        <mxCell id="step03" parent="lane3" style="rounded=0;whiteSpace=wrap;fillColor=#000000;strokeColor=#FFFFFF;fontColor=#FFFFFF;strokeWidth=2;fontSize=16;" value="03&#xa;Execute Task" vertex="1">
          <mxGeometry height="50" width="180" x="800" y="20" as="geometry" />
        </mxCell>
        
        <!-- Edges -->
        <mxCell id="edge01" edge="1" parent="1" source="step01" target="step02" style="edgeStyle=orthogonalEdgeStyle;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;exitX=0.5;exitY=1;exitDx=0;exitDy=0;entryX=0;entryY=0.5;entryDx=0;entryDy=0;strokeColor=#FFFFFF;strokeWidth=2;">
          <mxGeometry relative="1" as="geometry" />
        </mxCell>
        <mxCell id="edge02" edge="1" parent="1" source="step02" target="decision01" style="edgeStyle=orthogonalEdgeStyle;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;exitX=1;exitY=0.5;exitDx=0;exitDy=0;entryX=0;entryY=0.5;entryDx=0;entryDy=0;strokeColor=#FFFFFF;strokeWidth=2;">
          <mxGeometry relative="1" as="geometry" />
        </mxCell>
        <mxCell id="edge03" edge="1" parent="1" source="decision01" target="step03" style="edgeStyle=orthogonalEdgeStyle;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;exitX=1;exitY=0.5;exitDx=0;exitDy=0;entryX=0;entryY=0.5;entryDx=0;entryDy=0;strokeColor=#FFFFFF;strokeWidth=2;">
          <mxGeometry relative="1" as="geometry" />
        </mxCell>
      </root>
    </mxGraphModel>
  </diagram>
</mxfile>
```

## Example 3: Process with System Inputs and Document Outputs

**Process**: Procurement workflow with green system inputs and yellow document outputs

```xml
<?xml version="1.0" encoding="UTF-8"?>
<mxfile host="Electron">
  <diagram name="Procurement Process" id="procurement">
    <mxGraphModel dx="1500" dy="900" grid="0" gridSize="10" guides="1" tooltips="1" connect="1" arrows="1" fold="1" page="1" pageScale="1" pageWidth="1600" pageHeight="900" background="#000000" math="0" shadow="0">
      <root>
        <mxCell id="0" />
        <mxCell id="1" parent="0" />
        
        <!-- Title -->
        <mxCell id="title" parent="1" style="text;html=1;fontSize=18;fontStyle=1;align=center;fontColor=#FFFFFF;" value="Procurement Process" vertex="1">
          <mxGeometry height="30" width="400" x="550" y="10" as="geometry" />
        </mxCell>
        
        <!-- Lane 1: Purchaser -->
        <mxCell id="lane1" parent="1" style="shape=swimlane;startSize=80;horizontal=0;swimlaneLine=1;fillColor=#2A2A2A;strokeColor=#CCCCCC;fontColor=#FFFFFF;fontSize=11;" value="" vertex="1">
          <mxGeometry height="90" width="1570" x="30" y="50" as="geometry" />
        </mxCell>
        <mxCell id="role1" parent="lane1" style="text;whiteSpace=wrap;fontColor=#FFFFFF;fontSize=16;" value="Purchaser" vertex="1">
          <mxGeometry height="36" width="76" x="8" y="27" as="geometry" />
        </mxCell>
        <mxCell id="step01" parent="lane1" style="rounded=0;whiteSpace=wrap;fillColor=#000000;strokeColor=#FFFFFF;fontColor=#FFFFFF;strokeWidth=2;fontSize=16;" value="01&#xa;Create Purchase Order" vertex="1">
          <mxGeometry height="50" width="180" x="150" y="20" as="geometry" />
        </mxCell>
        <mxCell id="sys01" parent="lane1" style="shape=document;whiteSpace=wrap;fillColor=#D1EDA0;strokeColor=#D1EDA0;fontColor=#000000;fontSize=12;fontStyle=1;size=0;" value="ERP System" vertex="1">
          <mxGeometry height="30" width="80" x="150" y="-5" as="geometry" />
        </mxCell>
        <mxCell id="doc01" parent="lane1" style="shape=document;whiteSpace=wrap;fillColor=#FFC000;strokeColor=#FFC000;fontColor=#000000;fontSize=12;" value="《Purchase&#xa;Order》" vertex="1">
          <mxGeometry height="35" width="80" x="300" y="70" as="geometry" />
        </mxCell>
        
        <!-- Lane 2: Supplier -->
        <mxCell id="lane2" parent="1" style="shape=swimlane;startSize=80;horizontal=0;swimlaneLine=1;fillColor=#2A2A2A;strokeColor=#CCCCCC;fontColor=#FFFFFF;fontSize=11;" value="" vertex="1">
          <mxGeometry height="90" width="1570" x="30" y="140" as="geometry" />
        </mxCell>
        <mxCell id="role2" parent="lane2" style="text;whiteSpace=wrap;fontColor=#FFFFFF;fontSize=16;" value="Supplier" vertex="1">
          <mxGeometry height="36" width="76" x="8" y="27" as="geometry" />
        </mxCell>
        <mxCell id="step02" parent="lane2" style="rounded=0;whiteSpace=wrap;fillColor=#000000;strokeColor=#FFFFFF;fontColor=#FFFFFF;strokeWidth=2;fontSize=16;" value="02&#xa;Fulfill Order" vertex="1">
          <mxGeometry height="50" width="180" x="450" y="20" as="geometry" />
        </mxCell>
        
        <!-- Lane 3: Warehouse -->
        <mxCell id="lane3" parent="1" style="shape=swimlane;startSize=80;horizontal=0;swimlaneLine=1;fillColor=#2A2A2A;strokeColor=#CCCCCC;fontColor=#FFFFFF;fontSize=11;" value="" vertex="1">
          <mxGeometry height="90" width="1570" x="30" y="230" as="geometry" />
        </mxCell>
        <mxCell id="role3" parent="lane3" style="text;whiteSpace=wrap;fontColor=#FFFFFF;fontSize=16;" value="Warehouse" vertex="1">
          <mxGeometry height="36" width="76" x="8" y="27" as="geometry" />
        </mxCell>
        <mxCell id="step03" parent="lane3" style="rounded=0;whiteSpace=wrap;fillColor=#000000;strokeColor=#FFFFFF;fontColor=#FFFFFF;strokeWidth=2;fontSize=16;" value="03&#xa;Receive &amp; Inspect" vertex="1">
          <mxGeometry height="50" width="180" x="700" y="20" as="geometry" />
        </mxCell>
        <mxCell id="sys03" parent="lane3" style="shape=document;whiteSpace=wrap;fillColor=#D1EDA0;strokeColor=#D1EDA0;fontColor=#000000;fontSize=12;fontStyle=1;size=0;" value="WMS" vertex="1">
          <mxGeometry height="30" width="60" x="700" y="-5" as="geometry" />
        </mxCell>
        <mxCell id="doc03" parent="lane3" style="shape=document;whiteSpace=wrap;fillColor=#FFC000;strokeColor=#FFC000;fontColor=#000000;fontSize=12;" value="《Receipt&#xa;Report》" vertex="1">
          <mxGeometry height="35" width="80" x="850" y="70" as="geometry" />
        </mxCell>
        
        <!-- Edges -->
        <mxCell id="edge01" edge="1" parent="1" source="step01" target="step02" style="edgeStyle=orthogonalEdgeStyle;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;exitX=0.5;exitY=1;exitDx=0;exitDy=0;entryX=0;entryY=0.5;entryDx=0;entryDy=0;strokeColor=#FFFFFF;strokeWidth=2;">
          <mxGeometry relative="1" as="geometry" />
        </mxCell>
        <mxCell id="edge02" edge="1" parent="1" source="step02" target="step03" style="edgeStyle=orthogonalEdgeStyle;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;exitX=0.5;exitY=1;exitDx=0;exitDy=0;entryX=0;entryY=0.5;entryDx=0;entryDy=0;strokeColor=#FFFFFF;strokeWidth=2;">
          <mxGeometry relative="1" as="geometry" />
        </mxCell>
      </root>
    </mxGraphModel>
  </diagram>
</mxfile>
```

## Key Patterns Demonstrated

1. **Simple Linear Flow**: Activities progress left-to-right across swimlanes
2. **Decision Points**: Diamond shape with explicit Yes/No labels
3. **System Inputs**: Green (#D1EDA0) placed at activity's top-left
4. **Document Outputs**: Yellow (#FFC000) placed at activity's bottom-right
5. **Connection Points**: Explicit exitX/exitY/entryX/entryY values
6. **No Edge Crossing**: All edges use orthogonal routing with proper waypoints
7. **Sequential Numbering**: 01, 02, 03... across entire process

## Customization Tips

- Change role names by editing `value` attribute of role text cells
- Add more swimlanes by duplicating lane structure and incrementing y-coordinate
- Add more activities by following step01/step02 pattern
- Change colors by updating fillColor/strokeColor values
- Add systems/documents by placing green/yellow shapes at correct positions
