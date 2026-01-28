# SKAI Computation Visibility - Visual Reference

## Before vs After

### BEFORE (Original System)
```
┌──────────────────────────────────────────────────────────┐
│ SKAI Analysis Progress                                   │
│                                                           │
│ ████████████████░░░░░░░░░░░░░ 62%                       │
│                                                           │
│ Training 45/90... (ETA 2m 15s)                          │
└──────────────────────────────────────────────────────────┘

Users see:
✗ Just a percentage
✗ Generic message
✗ No sense of actual work being done
✗ Can't tell if progress is real or fake
```

### AFTER (With 3-Layer Visibility)
```
┌──────────────────────────────────────────────────────────┐
│ SKAI Analysis Progress                                   │
│                                                           │
│ ████████████████░░░░░░░░░░░░░ 62%  ← Existing bar kept │
│                                                           │
│ Training 45/90... (ETA 2m 15s)      ← Existing status   │
├──────────────────────────────────────────────────────────┤
│ LAYER 1: What's happening now                           │
│ Training neural network - Main numbers • seed 1337      │
│ (45/90 epochs)                                           │
├──────────────────────────────────────────────────────────┤
│ LAYER 2: Live work metrics                              │
│ Draws analyzed: 458 / 500                               │
│ Window evaluations: 412 / 450                           │
│ Pairwise comparisons: 287,420                           │
│ Batches processed: 142                                  │
│ Total computations: 3,482,119                           │
├──────────────────────────────────────────────────────────┤
│ LAYER 3: Completed phases                               │
│ ┏━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓ │
│ ┃ Data preparation complete                           ┃ │
│ ┃ • Analyzed 500 data points                          ┃ │
│ ┃ • Evaluated 845,100 relationships                   ┃ │
│ ┃ • Generated 450 training samples from 500 draws     ┃ │
│ ┗━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┛ │
└──────────────────────────────────────────────────────────┘

Users see:
✓ Clear phase description
✓ Real work metrics increasing
✓ Summary of what was accomplished
✓ Justification for processing time
```

## Real-Time Behavior

### Scenario: Analyzing 500 historical draws, 90 epochs

**T=0s (Start)**
```
┌──────────────────────────────────────────────────────────┐
│ ███░░░░░░░░░░░░░░░░░░░░░░░░░░░ 5%                       │
│                                                           │
│ Preparing historical data - Loading draw history        │
│                                                           │
│ Draws analyzed: 1 / 500                                 │
│ Total computations: 125                                 │
└──────────────────────────────────────────────────────────┘
```

**T=3s (Data Processing)**
```
┌──────────────────────────────────────────────────────────┐
│ ████████░░░░░░░░░░░░░░░░░░░░░░ 15%                      │
│                                                           │
│ Building training samples - Window size: 50 draws       │
│                                                           │
│ Draws analyzed: 158 / 500                               │
│ Window evaluations: 108 / 450                           │
│ Pairwise comparisons: 27,000                            │
│ Total computations: 135,000                             │
└──────────────────────────────────────────────────────────┘
```

**T=8s (Data Prep Complete)**
```
┌──────────────────────────────────────────────────────────┐
│ ████████████░░░░░░░░░░░░░░░░░░ 30%                      │
│                                                           │
│ Building training samples - Window size: 50 draws       │
│                                                           │
│ Draws analyzed: 450 / 500                               │
│ Window evaluations: 450 / 450                           │
│ Pairwise comparisons: 112,500                           │
│ Total computations: 562,500                             │
│                                                           │
│ ┏━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓ │
│ ┃ Data preparation complete                           ┃ │
│ ┃ • Analyzed 500 data points                          ┃ │
│ ┃ • Evaluated 112,500 relationships                   ┃ │
│ ┃ • Generated 450 training samples from 500 draws     ┃ │
│ ┗━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┛ │
└──────────────────────────────────────────────────────────┘
```

**T=20s (Training In Progress)**
```
┌──────────────────────────────────────────────────────────┐
│ ████████████████░░░░░░░░░░░░░░ 62%                      │
│                                                           │
│ Training neural network - Main numbers • seed 1337      │
│ (25/90 epochs)                                           │
│                                                           │
│ Draws analyzed: 450 / 500                               │
│ Window evaluations: 450 / 450                           │
│ Pairwise comparisons: 112,500                           │
│ Batches processed: 350                                  │
│ Total computations: 15,890,340                          │
│                                                           │
│ ┏━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓ │
│ ┃ Data preparation complete                           ┃ │
│ ┃ • Analyzed 500 data points                          ┃ │
│ ┃ • Evaluated 112,500 relationships                   ┃ │
│ ┃ • Generated 450 training samples from 500 draws     ┃ │
│ ┗━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┛ │
└──────────────────────────────────────────────────────────┘
```

**T=60s (Training Complete)**
```
┌──────────────────────────────────────────────────────────┐
│ ████████████████████████████████ 100%                   │
│                                                           │
│ Training neural network - Main numbers • seed 1337      │
│ (90/90 epochs)                                           │
│                                                           │
│ Draws analyzed: 450 / 500                               │
│ Window evaluations: 450 / 450                           │
│ Pairwise comparisons: 112,500                           │
│ Batches processed: 1,260                                │
│ Total computations: 57,204,120                          │
│                                                           │
│ ┏━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓ │
│ ┃ Data preparation complete                           ┃ │
│ ┃ • Analyzed 500 data points                          ┃ │
│ ┃ • Evaluated 112,500 relationships                   ┃ │
│ ┃ • Generated 450 training samples from 500 draws     ┃ │
│ ┗━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┛ │
│                                                           │
│ ┏━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓ │
│ ┃ Main numbers • seed 1337 complete                   ┃ │
│ ┃ • Analyzed 90 data points                           ┃ │
│ ┃ • Evaluated 1,260 relationships                     ┃ │
│ ┃ • Model trained for 90 epochs, final loss: 0.0234  ┃ │
│ ┗━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┛ │
└──────────────────────────────────────────────────────────┘
```

## Color & Style Reference

### Layer 1: Status Line
- **Font:** 14px, medium weight (500)
- **Color:** Dark gray (#1f2937)
- **Style:** Plain text, no decoration
- **Example:** `Training neural network - Main numbers • seed 1337`

### Layer 2: Counter Lines
- **Font:** 13px, normal weight
- **Color:** Medium gray (#4b5563)
- **Style:** Line height 1.6 for readability
- **Format:** `Label: X,XXX` or `Label: X / Y`
- **Example:** `Total computations: 3,482,119`

### Layer 3: Phase Summaries
- **Border:** 3px solid green (#10b981) on left
- **Background:** Very light gray (#f9fafb)
- **Padding:** 8px
- **Border radius:** 4px

**Title:**
- **Font:** 12px, semi-bold (600)
- **Color:** Dark green (#065f46)
- **Example:** `Data preparation complete`

**Details:**
- **Font:** 12px, normal
- **Color:** Medium gray (#4b5563)
- **Format:** Bulleted list
- **Example:** `• Analyzed 500 data points`

## Responsive Behavior

### On Small Screens (< 600px)
- Counters stack vertically
- Summary cards remain full width
- Font sizes reduce slightly (13px → 12px, 12px → 11px)
- Spacing tightens (12px → 8px margins)

### On Large Screens (> 1200px)
- Can show counters in 2-column layout if desired
- Maximum width constrains to ~800px for readability
- Spacing remains comfortable

## Animation & Transitions

**Counter Updates:**
- No animation
- Instant number change
- Throttled to 100ms updates

**Phase Summaries:**
- Fade in over 200ms when complete
- Slide down slightly (subtle)
- No continuous animations

**Status Line:**
- Instant text change
- No fade or transition

## Accessibility

- Semantic HTML (divs with IDs)
- Proper text contrast ratios (WCAG AA)
- Screen reader friendly (text content, no ARIA needed)
- No reliance on color alone
- Numbers formatted for readability

## Browser Rendering

**Chrome/Edge:**
- Uses system-ui font (Segoe UI on Windows, San Francisco on Mac)
- Smooth rendering with subpixel anti-aliasing

**Firefox:**
- Slightly different number formatting
- All features work identically

**Safari:**
- Native fonts (San Francisco)
- requestAnimationFrame performs well

## Print Styles

If page is printed:
- Progress bar hidden
- Status and counters visible
- Summaries visible
- Clean black text on white

## Dark Mode Support

Not implemented in initial version, but could add:
```css
@media (prefers-color-scheme: dark) {
  #skai-visibility-status { color: #e5e7eb; }
  #skai-visibility-counters { color: #9ca3af; }
  .skai-visibility-summary { 
    background: #1f2937; 
    border-left-color: #34d399; 
  }
}
```

## Performance Metrics

**Target Performance:**
- UI update < 16ms (60fps capable)
- Throttled to 100ms in practice
- No layout thrashing
- No forced reflows

**Memory Usage:**
- Minimal (< 1MB for counters & summaries)
- No leaks (arrays cleared on reset)
- DOM nodes reused

## Integration Points

**Existing System:**
- Works alongside existing progress bar
- Uses existing SKAI event system
- No conflicts with existing UI

**New System:**
- Self-contained in SKAI_RUNTIME_STATS
- Clean separation of concerns
- Easy to disable if needed
