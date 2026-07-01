# Dark Mode & Light Mode Implementation Prompt
## Copy and send this to your other systems agents

---

**COPY BELOW THIS LINE:**

---

# Task: Implement Dark Mode & Light Mode Toggle

## Overview
Add a dark mode/light mode toggle to this system with a consistent theme across all pages.

## Brand Color Reference (MCN-LTD Style)

### Primary Colors
- Navy Blue: `#254a93`
- Accent Green: `#36bb25`
- Dark Navy: `#1f233e`
- Golden: `#f6bb08`

### Light Mode Colors
- Background: `#fffcf4`
- Card Background: `#ffffff`
- Text: `#0c0b09`
- Header: `#1f233e`

### Dark Mode Colors
- Background: `#1a1a2e`
- Card Background: `#16213e`
- Text: `#f0f0f0`
- Header: `#0f0f1a`

## Implementation Steps

### 1. Add CSS Variables
```css
:root {
  --bg-primary: #fffcf4;
  --bg-secondary: #ffffff;
  --bg-header: #1f233e;
  --text-primary: #0c0b09;
  --accent-primary: #254a93;
  --accent-secondary: #36bb25;
}

[data-theme="dark"] {
  --bg-primary: #1a1a2e;
  --bg-secondary: #16213e;
  --bg-header: #0f0f1a;
  --text-primary: #f0f0f0;
  --accent-primary: #3a6bc4;
  --accent-secondary: #45d42f;
}
```

### 2. Add Toggle Button HTML
```html
<button id="theme-toggle" aria-label="Toggle dark mode">
  <i class="fas fa-moon"></i>
</button>
```

### 3. Add JavaScript
```javascript
const toggle = document.getElementById('theme-toggle');
const root = document.documentElement;
const saved = localStorage.getItem('theme') || 'light';
root.setAttribute('data-theme', saved);

toggle.addEventListener('click', () => {
  const current = root.getAttribute('data-theme');
  const next = current === 'light' ? 'dark' : 'light';
  root.setAttribute('data-theme', next);
  localStorage.setItem('theme', next);
});
```

### 4. Apply Variables
Replace all hardcoded background colors and text colors with CSS variables (var(--bg-primary), var(--text-primary), etc.)

## Requirements
- Toggle must persist user preference (use localStorage)
- Smooth transition between modes
- Consistent across ALL pages
- Accessible (aria-labels, good contrast)
- Mobile responsive

## Deliverable
Working dark/light mode toggle that persists across page refreshes.

---

**COPY ABOVE THIS LINE**
