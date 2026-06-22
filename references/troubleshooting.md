# Deloitte Process Mapping Troubleshooting

## Common Problems and Solutions

### Export Issues

#### Problem: `drawio: command not found`

**Cause**: draw.io CLI not installed or not in PATH

**Solution**:
```bash
# Check if draw.io is installed
ls /Applications/draw.io.app/Contents/MacOS/draw.io

# If found, use full path
/Applications/draw.io.app/Contents/MacOS/draw.io -x -f png -o diagram.png diagram.drawio

# Or install via Homebrew
brew install --cask drawio

# Check which binary name works
which drawio || which draw.io || echo "Use full path"
```

#### Problem: Export fails with "Could not process image"

**Cause**: Vision APIs reject PNGs exported with `-e` flag (truncated IEND chunk)

**Solution**:
```bash
# For preview/self-check: export WITHOUT -e
drawio -x -f png --width 2000 -o diagram.png diagram.drawio

# For final export: use -e, then repair
drawio -x -f png -e -s 2 -o diagram.drawio.png diagram.drawio
python3 scripts/repair_png.py diagram.drawio.png
```

#### Problem: Export fails with "Permission denied"

**Cause**: Trying to write to protected directory

**Solution**:
```bash
# Create output directory first
mkdir -p ./artifacts

# Export to that directory
drawio -x -f png -e -o ./artifacts/diagram.drawio.png diagram.drawio
```

#### Problem: Export fails on Linux server

**Cause**: No display available (headless environment)

**Solution**:
```bash
# Install xvfb
sudo apt-get install xvfb

# Run with virtual display
xvfb-run -a drawio -x -f png -e -o diagram.drawio.png diagram.drawio

# If running as root
export HOME=${HOME:-/tmp}
xvfb-run -a --server-args="-screen 0 1280x1024x24" drawio -x -f png -e -o diagram.drawio.png diagram.drawio --disable-gpu --no-sandbox
```

### XML Issues

#### Problem: XML parse error

**Cause**: Invalid XML characters or structure

**Solution**:
```xml
<!-- WRONG: -- in comments is illegal -->
<!-- This is a comment -- this part is wrong -->

<!-- RIGHT: Avoid -- in XML comments -->
<!-- This is a comment -->

<!-- WRONG: Unescaped & -->
&

<!-- RIGHT: Escaped & -->
&amp;

<!-- WRONG: Missing root cells -->
<mxCell id="2" ... />

<!-- RIGHT: Root cells required -->
<mxCell id="0" />
<mxCell id="1" parent="0" />
<mxCell id="2" ... />
```

#### Problem: Shapes not rendering

**Cause**: Wrong `id` or `parent` assignment

**Solution**:
```xml
<!-- WRONG: Wrong parent -->
<mxCell id="step01" parent="2" ... />

<!-- RIGHT: Parent should be 1 or container id -->
<mxCell id="step01" parent="1" ... />

<!-- RIGHT: Child of container -->
<mxCell id="step01" parent="lane1" ... />
```

#### Problem: Labels not showing

**Cause**: Missing `html=1` in style

**Solution**:
```xml
<!-- WRONG: No html attribute -->
<mxCell id="step01" style="rounded=0;fillColor=#000000;" ... />

<!-- RIGHT: html=1 enables proper text rendering -->
<mxCell id="step01" style="rounded=0;html=1;fillColor=#000000;" ... />
```

### Layout Issues

#### Problem: Edges crossing each other

**Cause**: Poor path planning, no waypoints

**Solution**:
```xml
<!-- WRONG: Direct edge that crosses -->
<mxCell id="edge01" edge="1" source="A" target="D" ... />

<!-- RIGHT: Add waypoints to avoid crossing -->
<mxCell id="edge01" edge="1" source="A" target="D" ...>
  <mxGeometry relative="1" as="geometry">
    <Array as="points">
      <mxPoint x="200" y="150" />
      <mxPoint x="400" y="300" />
    </Array>
  </mxGeometry>
</mxCell>
```

#### Problem: Activity labels overlapping

**Cause**: Activities too close together

**Solution**:
- Increase horizontal gap to 200-280px
- Use smaller font size (12-14pt instead of 16pt)
- Split into multiple lines: `01&#xa;Short&#xa;Name`

#### Problem: Swimlane text cramped

**Cause**: Role label too wide or activity too narrow

**Solution**:
```xml
<!-- Increase lane width -->
<mxGeometry height="90" width="1700" ... />

<!-- Or decrease role label width -->
<mxCell id="role1" ... style="...fontSize=14;" ... >
  <mxGeometry height="36" width="60" ... />
</mxCell>
```

#### Problem: Start/End not in correct position

**Cause**: Random placement

**Solution**:
- **Start**: Place at `x=30, y=50` (top-left of first swimlane)
- **End**: Place at `x=1400, y=50` (top-right of first swimlane)
- Use consistent coordinates across diagrams

### Vision/Review Issues

#### Problem: Self-check returns 400 error

**Cause**: PNG exported with `-e` flag

**Solution**:
```bash
# Re-export WITHOUT -e for preview
drawio -x -f png --width 2000 -o diagram.png diagram.drawio
```

#### Problem: Vision can't read image

**Cause**: Image too large (>2576×2576px)

**Solution**:
```bash
# Use --width to cap dimensions
drawio -x -f png --width 2000 -o diagram.png diagram.drawio
```

#### Problem: Colors look wrong in export

**Cause**: Color codes incorrect

**Solution**:
Reference the color table:
- Systems/Inputs: `#D1EDA0` fill, `#00AA00` stroke
- Documents/Outputs: `#FFC000` fill, `#FFD700` stroke
- Background: `#000000`
- Activity boxes: `#000000` fill, `#FFFFFF` stroke
- Swimlanes: `#2A2A2A` or `#333333` fill

### Performance Issues

#### Problem: Large diagrams slow to render

**Cause**: Too many shapes or complex edges

**Solution**:
- Use `--width` instead of `-s` for previews
- Simplify edge paths (fewer waypoints)
- Group related activities
- Break into multiple diagrams if >50 activities

#### Problem: Export takes forever

**Cause**: Complex diagram, high resolution

**Solution**:
```bash
# Reduce scale for faster export
drawio -x -f png -e -s 1 -o diagram.drawio.png diagram.drawio

# Or reduce width
drawio -x -f png -e --width 1000 -o diagram.drawio.png diagram.drawio
```

## Debugging Steps

1. **Check XML validity**:
   - Are `id="0"` and `id="1"` present?
   - All `&` escaped as `&amp;`?
   - No `--` in comments?
   - All shapes have `parent="1"` or valid container?

2. **Check colors**:
   - System inputs: `#D1EDA0` fill?
   - Document outputs: `#FFC000` fill?
   - Background: `#000000`?

3. **Check layout**:
   - Activities numbered sequentially?
   - Start in top-left?
   - End in top-right?
   - No crossing edges?

4. **Check export**:
   - Preview without `-e`?
   - Final with `-e`?
   - Ran `repair_png.py` on `-e` PNG?

## Getting Help

If issues persist:

1. Check draw.io desktop can open the file manually
2. Try browser fallback: `python3 scripts/encode_drawio_url.py diagram.drawio`
3. Deliver XML only and ask user to export manually
4. Check draw.io GitHub issues for known bugs

## References

- draw.io CLI documentation: https://github.com/jgraph/drawio-desktop
- Deloitte process mapping standards
- SKILL.md main documentation
- quick-reference.md for color/layout cheatsheet
