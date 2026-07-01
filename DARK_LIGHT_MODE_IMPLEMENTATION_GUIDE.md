# Dark Mode & Light Mode Implementation Guide
## For MCN-LTD Website Systems

---

## 🎨 Current Color Scheme (MCN-LTD Brand)

### Primary Colors
| Color Name | Hex Code | Usage |
|------------|----------|-------|
| **Navy Blue** | `#254a93` | Headers, buttons, primary elements |
| **Accent Green** | `#36bb25` | Highlights, underlines, CTAs |
| **Dark Navy** | `#1f233e` | Header background, dark elements |
| **Golden Yellow** | `#f6bb08` | Accent buttons |

### Text Colors
| Mode | Text Color | Hex Code |
|------|------------|----------|
| Light Mode | Dark text | `#0c0b09` |
| Light Mode | Light text | `#fefefe` |
| Dark Mode | Dark text | `#f0f0f0` |
| Dark Mode | Light text | `#e0e0e0` |

### Background Colors
| Mode | Background | Hex Code |
|------|------------|----------|
| Light Mode | Page background | `#fffcf4` |
| Light Mode | Card background | `#ffffff` |
| Dark Mode | Page background | `#1a1a2e` |
| Dark Mode | Card background | `#16213e` |
| Dark Mode | Header | `#0f0f1a` |

---

## 📋 Implementation Checklist

### Step 1: Add CSS Variables

```css
/* Add to your main CSS file (e.g., style.css) */

:root {
  /* Light Mode (Default) */
  --bg-primary: #fffcf4;
  --bg-secondary: #ffffff;
  --bg-header: #1f233e;
  --text-primary: #0c0b09;
  --text-secondary: #fefefe;
  --accent-primary: #254a93;
  --accent-secondary: #36bb25;
  --border-color: #e0e0e0;
}

[data-theme="dark"] {
  /* Dark Mode */
  --bg-primary: #1a1a2e;
  --bg-secondary: #16213e;
  --bg-header: #0f0f1a;
  --text-primary: #f0f0f0;
  --text-secondary: #e0e0e0;
  --accent-primary: #3a6bc4; /* Slightly lighter for contrast */
  --accent-secondary: #45d42f; /* Slightly brighter green */
  --border-color: #2a2a4a;
}
```

### Step 2: Apply CSS Variables to Elements

```css
/* Replace hardcoded colors with variables */
body {
  background-color: var(--bg-primary);
  color: var(--text-primary);
}

.header_section {
  background-color: var(--bg-header);
  color: var(--text-secondary);
}

.btn-primary {
  background-color: var(--accent-primary);
  color: var(--text-secondary);
}

.card {
  background-color: var(--bg-secondary);
  border: 1px solid var(--border-color);
}
```

### Step 3: Add Theme Toggle Button (JavaScript)

```javascript
// Add to your main JS file
const themeToggle = document.getElementById('theme-toggle');
const root = document.documentElement;

// Check for saved theme preference
const savedTheme = localStorage.getItem('theme') || 'light';
root.setAttribute('data-theme', savedTheme);

themeToggle.addEventListener('click', () => {
  const currentTheme = root.getAttribute('data-theme');
  const newTheme = currentTheme === 'light' ? 'dark' : 'light';
  
  root.setAttribute('data-theme', newTheme);
  localStorage.setItem('theme', newTheme);
  
  // Update button icon
  themeToggle.innerHTML = newTheme === 'dark' 
    ? '<i class="fas fa-sun"></i>' 
    : '<i class="fas fa-moon"></i>';
});
```

### Step 4: Add Toggle Button to HTML

```html
<!-- Add this button to your header/navigation -->
<button id="theme-toggle" class="theme-toggle-btn" aria-label="Toggle dark mode">
  <i class="fas fa-moon"></i>
</button>
```

```css
/* Add button styling */
.theme-toggle-btn {
  background: transparent;
  border: 2px solid var(--accent-secondary);
  border-radius: 50%;
  width: 40px;
  height: 40px;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  color: var(--text-secondary);
  transition: all 0.3s ease;
}

.theme-toggle-btn:hover {
  background-color: var(--accent-secondary);
  color: var(--bg-header);
}
```

### Step 5: Add Transition Effects

```css
/* Smooth transition between themes */
body, .header_section, .footer_section, .card, button, a {
  transition: background-color 0.3s ease, color 0.3s ease, border-color 0.3s ease;
}
```

---

## 🔧 System-Specific Recommendations

### For React/Next.js Systems
```jsx
// Use context or state management for theme
// Wrap app with ThemeProvider
// Use useTheme() hook in components
```

### For Vue.js Systems
```javascript
// Use VueUse composables
// Or create a simple plugin
```

### For Backend Systems (Django/Rails/Express)
```javascript
// Store theme preference in user session/database
// Apply class to body element server-side
```

### For WordPress/CMS Systems
```javascript
// Add to theme's functions.php or custom plugin
// Use wp_enqueue_script for JS
```

---

## ✅ Testing Checklist

- [ ] Toggle works on all pages
- [ ] Theme preference persists on reload
- [ ] All colors change correctly
- [ ] No flash of wrong theme on page load
- [ ] Images/icons adjust for dark mode (optional)
- [ ] Mobile responsiveness maintained
- [ ] No accessibility issues (contrast ratios)

---

## 📱 Mobile Considerations

```css
/* Ensure toggle is easily accessible on mobile */
@media (max-width: 768px) {
  .theme-toggle-btn {
    width: 48px;
    height: 48px;
    margin: 5px;
  }
}
```

---

## 🔒 Accessibility Requirements

| WCAG Guideline | Implementation |
|----------------|-----------------|
| Contrast Ratio | Minimum 4.5:1 for text |
| Focus Indicators | Visible focus states in both modes |
| Screen Readers | `aria-label` on toggle button |
| Reduced Motion | Respect `prefers-reduced-motion` |

```css
@media (prefers-reduced-motion: reduce) {
  * {
    transition: none !important;
  }
}
```

---

## 📂 File Structure Example

```
your-project/
├── css/
│   ├── variables.css      # CSS variables definition
│   ├── light-mode.css     # Light mode overrides (if needed)
│   ├── dark-mode.css      # Dark mode overrides (if needed)
│   └── main.css           # Main styles using variables
├── js/
│   └── theme-toggle.js    # Theme toggle functionality
└── html/
    └── index.html         # Include toggle button
```

---

## 💡 Pro Tips

1. **Start with CSS Variables** - This makes the implementation 10x easier
2. **Test on real devices** - Colors may render differently
3. **Consider high contrast mode** - Some users need extra contrast
4. **Image handling** - Use CSS filters for images in dark mode:
   ```css
   [data-theme="dark"] img {
     filter: brightness(0.9) contrast(1.1);
   }
   ```
5. **Icons** - Use SVG icons that can change color with CSS

---

## 📞 Need Help?

If you encounter issues implementing dark mode, share:
1. Your current CSS structure
2. Your framework (React, Vue, plain HTML, etc.)
3. Any existing theme toggle code

We'll help you integrate it properly!
