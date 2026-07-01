# Course Status Widget

A lightweight Brightspace (D2L) widget that displays the current active/inactive status of a course and lets instructors toggle it directly from the course homepage — no page navigation required.

Works with any Brightspace instance.

---

## What it does

- Shows **ACTIVE** (green) or **INACTIVE** (red) status with a lock icon
- Provides a **Make Active / Make Inactive** button to toggle the status inline
- Updates instantly without leaving the homepage

---

## How it works

The widget uses a hidden iframe to load the standard Brightspace course edit page in the background. When the instructor clicks the button, it checks or unchecks the Active checkbox on that page and submits the form — exactly as if they had done it manually through Course Admin. It also attempts to read the status via the LP REST API first (faster), falling back to the iframe if that returns a 403.

---

## Permissions

**No extra permissions are required.** The widget operates entirely through Brightspace's own UI. If an instructor already has permission to change the course active status through **Course Admin → Course Offering Information**, this widget will work for them. Nothing additional needs to be granted by an administrator.

---

## Setup — adding to a course homepage

### Step 1 — Create the widget

1. Go to **Admin Tools → Widgets**
2. Click **New Widget**
3. Give it a name, e.g. `Course Status`
4. Under **Content**, select **Free-Form HTML** (or the HTML source editor depending on your version)
5. Paste the entire contents of `status-widget.html` into the content area
6. Save the widget

> **Important:** The widget uses the Brightspace replacement string `{OrgUnitId}` which is automatically substituted with the current course's org unit ID when the widget renders. Do not replace this manually — Brightspace handles it at runtime.

### Step 2 — Add to a homepage

1. Go to the course or org-level homepage you want to add it to
2. Click **Edit Homepage** (or go via **Admin Tools → Homepages**)
3. Add the widget to a panel
4. Save and publish the homepage

### Step 3 — Apply to courses

Assign the homepage to the relevant courses through your normal homepage management process.

---

## Configuration

The LP API version is set at the top of the script:

```javascript
var LP_VERSION = '1.49';
```

Update this to match your Brightspace instance's supported LP API version if needed.

---

## Assets & dependencies

**None.** The widget is entirely self-contained in a single HTML file.

The lock icons are inline SVG paths encoded as data URIs directly in the JavaScript — no image files, no CDN, no external requests. The spinner and button styling use standard D2L CSS custom properties (`--d2l-color-celestine` etc.) so they automatically match your Brightspace theme.

## Browser support

Works in all modern browsers. Uses standard Fetch API and async/await — no external dependencies.
