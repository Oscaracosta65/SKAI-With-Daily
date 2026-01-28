# Testing the 3-Layer Computation Visibility System

## How to Test

1. **Load a lottery page** with SKAI analysis
2. **Click "Run SKAI Analysis"** button
3. **Observe the three layers** appear below the progress bar

## Expected Behavior

### Phase 1: Data Preparation (First 5-10 seconds)

**Layer 1 Status:**
```
Preparing historical data - Loading draw history
↓
Building training samples - Window size: 50 draws
```

**Layer 2 Counters (growing in real time):**
```
Draws analyzed: 1 / 500
Window evaluations: 1 / 450
Pairwise comparisons: 250
Total computations: 1,250
↓ (numbers increase)
Draws analyzed: 450 / 500
Window evaluations: 450 / 450
Pairwise comparisons: 112,500
Total computations: 562,500
```

**Layer 3 Summary (appears when phase completes):**
```
┌─────────────────────────────────────────────┐
│ Data preparation complete                   │
│ • Analyzed 500 data points                  │
│ • Evaluated 112,500 relationships           │
│ • Generated 450 training samples from...    │
└─────────────────────────────────────────────┘
```

### Phase 2: Training (Next 30-60 seconds)

**Layer 1 Status:**
```
Training neural network - Main numbers • seed 1337 (1/90 epochs)
↓ (updates each epoch)
Training neural network - Main numbers • seed 1337 (45/90 epochs)
↓
Training neural network - Main numbers • seed 1337 (90/90 epochs)
```

**Layer 2 Counters (continue growing):**
```
Batches processed: 14
Total computations: 589,320
↓ (numbers increase rapidly)
Batches processed: 1,260
Total computations: 45,892,340
```

**Layer 3 Summary (appears when training completes):**
```
┌─────────────────────────────────────────────┐
│ Data preparation complete                   │
│ • Analyzed 500 data points                  │
│ • Evaluated 112,500 relationships           │
│ • Generated 450 training samples from...    │
└─────────────────────────────────────────────┘

┌─────────────────────────────────────────────┐
│ Main numbers • seed 1337 complete           │
│ • Analyzed 90 data points                   │
│ • Evaluated 1,260 relationships             │
│ • Model trained for 90 epochs, final loss...│
└─────────────────────────────────────────────┘
```

## Verification Checklist

### Layer 1: Dynamic Status
- [ ] Status line updates when computation phase changes
- [ ] Text is plain English (no jargon)
- [ ] Shows meaningful detail (window size, epoch count)
- [ ] Never shows percentages

### Layer 2: Live Counters
- [ ] Counters increase in real time
- [ ] Numbers have thousands separators (1,234,567)
- [ ] Shows X / Y format when total is known
- [ ] Never resets mid-run
- [ ] No percentages shown
- [ ] Updates are smooth (not janky)

### Layer 3: Phase Summaries
- [ ] Only appear when phase completes
- [ ] Show actual metrics (processed, relationships)
- [ ] Describe what changed
- [ ] Stack nicely (multiple phases visible)
- [ ] Use bullet points for readability
- [ ] Have green accent border

## Performance Checks

- [ ] UI updates don't slow down computation
- [ ] No visible lag or jank
- [ ] Updates are throttled (not 60fps crazy)
- [ ] Works on large datasets (500+ draws)
- [ ] Works on small datasets (50 draws)

## Browser Compatibility

Test in:
- [ ] Chrome/Edge (primary)
- [ ] Firefox
- [ ] Safari

## Edge Cases

### Very Fast Run (small dataset)
- Counters should still update (even if briefly)
- Summaries should still appear
- No errors in console

### Very Slow Run (large dataset, many epochs)
- Counters should keep growing smoothly
- No memory leaks (check DevTools)
- Status updates appropriately

### Multiple Runs
- Previous counters clear on new run
- Summaries reset
- No stale data displayed

## Visual Inspection

**Styling should match:**
- System fonts (San Francisco on Mac, Segoe UI on Windows)
- Clean, minimalist design
- Subtle colors (grays for text, green for completed phases)
- Good spacing and readability
- No flashy animations

**Tone should feel like:**
- Apple system dialogs (calm, technical)
- Stripe dashboards (trustworthy, precise)
- NOT like: Loading spinners, "AI is thinking", marketing fluff

## Console Output

Check browser console for:
- [ ] No errors related to SKAI_RUNTIME_STATS
- [ ] No warnings about missing elements
- [ ] Clean execution

## Troubleshooting

### If Layer 1 doesn't update:
- Check `SKAI_RUNTIME_STATS.setPhase()` calls are executing
- Verify `skai-visibility-status` element exists

### If Layer 2 doesn't show numbers:
- Check increment methods are being called in loops
- Verify batching logic (every 10 iterations)
- Check throttling isn't too aggressive

### If Layer 3 is empty:
- Verify `completePhase()` is called after each phase
- Check summary HTML generation logic
- Ensure `skai-visibility-summaries` element exists

### If UI looks broken:
- Check CSS was injected (style tag in head)
- Verify container structure matches expected DOM
- Check for CSS conflicts with existing styles

## Success Metrics

**Users should be able to:**
1. Understand what SKAI is doing at any moment
2. See that real work is being performed (not fake progress)
3. Know how much computation has occurred
4. See what changed after each major phase
5. Feel that long runtimes are justified by the visible work

**Users should NOT see:**
- Percentages (existing progress bar has them, but our 3 layers don't)
- Jargon or technical terms
- Marketing language or hype
- Fake/mock numbers
- Broken or janky UI
