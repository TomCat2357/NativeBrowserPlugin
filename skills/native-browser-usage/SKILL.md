---
name: Native Browser Usage
description: This skill should be used when the user asks about "NativeBrowserControl", "browser automation", "Chrome automation", "Edge automation", "UI Automation", "scan elements", "click element", or needs help with browser control workflows without Selenium.
version: 0.1.0
---

# Native Browser Control

NativeBrowserControl is an MCP server that controls Chrome and Edge browsers on Windows using UI Automation (pywinauto/pywin32) without Selenium. It provides direct window manipulation, element scanning, and browser interaction capabilities.

## Core Concepts

### Browser Connection Model

NativeBrowserControl operates on already-running browser windows or can launch new ones:

1. **List available windows**: Use `/browser:list-windows` to see all running browser instances
2. **Connect to specific window**: Use `/browser:connect` with window index (0=first, -1=last)
3. **Auto-launch if needed**: Connection automatically launches browser if none running

### Element Interaction Pattern

The recommended workflow for reliable element interaction:

1. **Scan elements**: `/browser:scan-elements` returns indexed list of UI elements
2. **Identify target**: Find element by name, type, or automation_id in scan results
3. **Interact by index**: Use `/browser:click-element <index>` or `/browser:set-element-text <index> <text>`
4. **Re-scan as needed**: Element indices change when page updates

**Critical**: Always scan before clicking elements. Indices are session-specific.

### Browser Selection

All tools accept optional `browser` parameter:
- `chrome` (default): Control Chrome browser
- `edge`: Control Microsoft Edge

Pass browser type in command arguments when needed.

## Common Workflows

### Basic Navigation Workflow

```
1. /browser:connect
2. /browser:navigate https://example.com
3. /browser:screenshot
4. /browser:get-page-text
```

### Element Interaction Workflow

```
1. /browser:scan-elements
2. Identify target element index from results
3. /browser:click-element <index>
4. /browser:wait 2
5. /browser:screenshot
```

### Form Filling Workflow

```
1. /browser:scan-elements control_type="Edit"
2. /browser:set-element-text <index> "text to input"
3. /browser:scan-elements control_type="Button"
4. /browser:click-element <button_index>
```

### File Dialog Handling

File open dialogs require special handling:

```
1. Trigger dialog (e.g., click upload button)
2. /browser:wait 2
3. /browser:scan-elements
4. Find <Edit> element for filename field
5. /browser:set-element-text <index> "C:\\full\\path\\to\\file.txt"
6. Find "開く(O)" or "Open" button
7. /browser:click-element <button_index>
```

**Note**: File paths must be absolute Windows paths with backslashes.

### Tab Management Workflow

```
1. /browser:new-tab
2. /browser:navigate <url>
3. /browser:switch-tab direction="previous"
4. /browser:close-tab
```

## Scanning and Filtering

`/browser:scan-elements` supports powerful filtering:

**By control type**:
```
/browser:scan-elements control_type="Button"
/browser:scan-elements control_type="Edit"
/browser:scan-elements control_type="Link"
```

**By name**:
```
/browser:scan-elements name_contains="Submit"
/browser:scan-elements name_regex="^Login.*"
```

**By visibility and state**:
```
/browser:scan-elements only_visible=true
/browser:scan-elements require_enabled=true
/browser:scan-elements only_focusable=true
```

**By size**:
```
/browser:scan-elements min_width=100 min_height=30
```

**Index range**:
```
/browser:scan-elements start_index=0 end_index=50
/browser:scan-elements start_index=100 end_index=200
```

**Limit results**:
```
/browser:scan-elements max_elements=100
```

Combine filters to narrow results effectively.

## Screenshot Modes

### Window Screenshot

Captures only the browser window:
```
/browser:screenshot
/browser:screenshot format="JPEG" quality=90
```

Returns base64-encoded image. Supports PNG (default) and JPEG.

### Full Screen Screenshot

Captures entire screen or specific monitor:
```
/browser:full-screenshot
/browser:full-screenshot monitor=1
/browser:full-screenshot monitor=2 format="PNG"
```

Monitor options:
- `0`: All monitors
- `1`: Primary monitor
- `2+`: Secondary monitors

## Text Input Methods

### Type Text Tool

For focused elements:
```
/browser:type-text text="Hello World"
/browser:type-text text="Hello" method="paste"
/browser:type-text text="Hello" method="type"
```

Methods:
- `paste` (default): Clipboard-based, fast
- `type`: Character-by-character, slower but more reliable for some inputs

### Set Element Text Tool

For specific elements (recommended):
```
1. /browser:scan-elements
2. /browser:set-element-text <index> "text content"
```

Directly sets text on Edit controls without focus concerns.

## Scrolling Patterns

```
/browser:scroll direction="down"
/browser:scroll direction="up"
/browser:scroll direction="page_down"
/browser:scroll direction="page_up"
/browser:scroll direction="top"
/browser:scroll direction="bottom"
/browser:scroll direction="down" amount=1000
```

Use `amount` parameter (pixels) only with `down` or `up` directions.

## Timing and Waits

Page load and dynamic content require explicit waits:

```
/browser:navigate https://example.com
/browser:wait 3
/browser:scan-elements
```

Common wait scenarios:
- After navigation: 2-3 seconds
- After dialog open: 1-2 seconds
- After form submission: 3-5 seconds
- After element click: 1-2 seconds

Adjust based on page complexity and network speed.

## Clipboard Operations

### Copy Selected Text

```
1. /browser:scan-elements
2. /browser:click-element <text_start_index>
3. Select text manually or use Ctrl+A
4. /browser:copy-selected
```

Returns copied text content.

### Paste Content

```
/browser:paste
```

Pastes current clipboard content to focused element.

## Important Limitations

### Window Visibility

Browser window must be:
- Foreground (front-most)
- Not minimized
- Visible on screen

The driver attempts auto-restore if window is minimized.

### DPI and Scaling

Coordinate-based operations depend on:
- Standard DPI settings (100%)
- Single monitor or primary monitor use
- No virtual desktop complications

If coordinates are misaligned, check display scaling settings.

### Element Stability

Element indices from scan results are:
- Valid only for current page state
- Invalidated by page changes, reloads, dynamic content
- Session-specific (not persistent across scans)

Always re-scan after page updates.

### Manual Intervention

During automation:
- Avoid manual mouse/keyboard input
- Browser window loses focus → operations may fail
- Clicking outside browser → need to re-focus

## Troubleshooting

### Cannot Find Element

```
1. /browser:screenshot to verify page loaded
2. /browser:wait <seconds> for dynamic content
3. /browser:scan-elements with specific filters
4. Check element name, type, and visibility
5. Try broader filters or no filters
```

### Click Not Working

```
1. Verify element enabled: scan with require_enabled=true
2. Verify element visible: scan with only_visible=true
3. Try scanning with only_focusable=true
4. Wait longer before clicking
5. Check browser window is foreground
```

### Coordinate Misalignment

```
1. Check Windows display scaling (should be 100%)
2. Verify single monitor or primary monitor use
3. Ensure browser window is maximized
4. Use element-based clicking instead of coordinate clicking
```

### Browser Not Responding

```
1. /browser:list-windows to check browser state
2. /browser:connect to reconnect
3. Close and reopen browser manually
4. Verify browser not in fullscreen mode
```

## Best Practices

1. **Always scan before interact**: Element indices are not stable
2. **Use specific filters**: Reduce scan results to relevant elements
3. **Prefer element operations over coordinates**: More reliable across DPI settings
4. **Add explicit waits**: Don't assume instant page loads
5. **Take screenshots for debugging**: Visual confirmation of state
6. **Handle file dialogs carefully**: Use absolute paths, verify element indices
7. **Re-scan after page changes**: Dynamic content invalidates indices
8. **Keep browser in foreground**: Automation requires window visibility
9. **Use set-element-text for inputs**: More reliable than type-text for forms
10. **Check browser parameter**: Specify `edge` when needed, default is `chrome`

## MCP Resources

NativeBrowserControl provides Tips resources accessible via MCP:

- **tips://file-dialog-text-input**: Complete guide for file dialog text input
- **tips://gemini-file-upload**: Step-by-step Gemini file upload workflow

Access these resources through the MCP server's resource endpoints for detailed walkthroughs.

## Additional Resources

### Reference Files

For advanced techniques and detailed patterns (when added):
- **`references/advanced-patterns.md`** - Complex automation workflows
- **`references/troubleshooting.md`** - Detailed error resolution

### Example Files

Working examples for common scenarios (when added):
- **`examples/gemini-upload.md`** - Complete Gemini file upload example
- **`examples/form-automation.md`** - Multi-step form filling

Future additions will expand documentation while keeping this core guide lean.

## Quick Reference

| Task | Command |
|------|---------|
| Connect browser | `/browser:connect` |
| Navigate to URL | `/browser:navigate <url>` |
| Take screenshot | `/browser:screenshot` |
| Scan elements | `/browser:scan-elements` |
| Click element | `/browser:click-element <index>` |
| Type text | `/browser:type-text <text>` |
| Set element text | `/browser:set-element-text <index> <text>` |
| Scroll page | `/browser:scroll direction="down"` |
| Wait | `/browser:wait <seconds>` |
| New tab | `/browser:new-tab` |
| Get page text | `/browser:get-page-text` |

Use these commands through Claude Code's slash command interface to control Chrome and Edge browsers efficiently.
