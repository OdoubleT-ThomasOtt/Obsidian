# UI Conventions

## CSS Architecture (EPIC-049 Consolidation)

### File Structure
The CSS architecture consists of **7 consolidated files** in `/Frontend/Web/wwwroot/css/`:

1. **variables.css** (23KB) - Design tokens: colors, spacing, typography, breakpoints
2. **base.css** (12KB) - CSS reset and HTML element defaults
3. **layout.css** (44KB) - Page structures, grid systems, containers
4. **components.css** (84KB) - All BEM component styles
5. **utilities.css** (35KB) - Helper classes and utility overrides
6. **theme-dark.css** (12KB) - Dark theme variable overrides
7. **print.css** (3KB) - Print media specific styles

### Load Order (CRITICAL)
Files MUST be loaded in this exact sequence in `App.razor`:
```
1. variables.css      // Foundation layer
2. base.css          // Reset layer
3. bootstrap.min.css // Framework layer (external)
4. layout.css        // Structure layer
5. components.css    // Component layer
6. utilities.css     // Override layer
7. theme-dark.css    // Theme layer (conditional)
8. print.css         // Print layer (media="print")
```

### Naming Convention
**BEM (Block Element Modifier)** - MANDATORY for all components:
- Block: `.tender-card`
- Element: `.tender-card__header`
- Modifier: `.tender-card--active`
- State: `.tender-card.is-loading`

### CSS Variables
All design tokens use CSS custom properties defined in `variables.css`:
```css
/* Colors */
--primary-color, --secondary-color, --danger-color
/* Spacing */
--spacing-xs, --spacing-sm, --spacing-md, --spacing-lg
/* Typography */
--font-size-base, --font-weight-normal, --line-height-base
/* Shadows */
--shadow-sm, --shadow-md, --shadow-lg
```

### Component Styling Rules

#### Location
- Component styles: `components.css` only
- No component styles in other CSS files
- No inline styles in Razor components (except CSS custom properties)

#### Pattern
```css
/* Component Block */
.component-name { }
/* Component Elements */
.component-name__element { }
/* Component Modifiers */
.component-name--modifier { }
/* Component States */
.component-name.is-state { }
```

### Dark Theme Implementation
- Theme overrides: `theme-dark.css` only
- Applied via `data-theme="dark"` on `<html>` element
- Override CSS variables only, never direct properties
```css
[data-theme="dark"] {
  --background-color: #1a1a1a;
  --text-color: #ffffff;
}
```

### Utility Classes
Helper classes in `utilities.css` follow patterns:
- Spacing: `.m-{size}`, `.p-{size}`, `.mt-{size}`
- Display: `.d-none`, `.d-block`, `.d-flex`
- Text: `.text-center`, `.text-primary`, `.fw-bold`
- Visibility: `.show`, `.hide`, `.invisible`

### Forbidden Practices
❌ **NEVER** add inline styles (style="...")
❌ **NEVER** create new CSS files
❌ **NEVER** mix component styles into utility files
❌ **NEVER** use !important (except utilities.css)
❌ **NEVER** bypass BEM naming convention
❌ **NEVER** hardcode colors - use variables

### File Modification Guidelines

#### When adding new components:
1. Add styles ONLY to `components.css`
2. Follow BEM naming strictly
3. Use existing CSS variables
4. Group related component styles together

#### When modifying existing styles:
1. Check impact across all components
2. Maintain BEM structure
3. Update dark theme if needed
4. Test responsive breakpoints

#### When adding utilities:
1. Add ONLY to `utilities.css`
2. Keep atomic and single-purpose
3. Use !important sparingly
4. Document usage pattern

### Responsive Design
Breakpoints defined in `variables.css`:
```css
--breakpoint-sm: 576px;
--breakpoint-md: 768px;
--breakpoint-lg: 992px;
--breakpoint-xl: 1200px;
--breakpoint-xxl: 1400px;
```

### Testing Requirements
- Visual regression testing for any CSS changes
- Dark/light theme toggle verification
- Responsive breakpoint testing
- Print preview validation
- No inline styles audit

### Performance Metrics
Target metrics from EPIC-049:
- CSS files: Maximum 7 (achieved)
- Total CSS size: <160KB (excluding Bootstrap)
- Inline styles: 0 (CSS properties only)
- Duplication: <5%

## Summary
This convention ensures consistent, maintainable, and performant CSS architecture following the EPIC-049 consolidation. All UI implementations MUST adhere to these patterns without exception.