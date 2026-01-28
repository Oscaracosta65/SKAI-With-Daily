# SKAI 3-Layer Computation Visibility System

## Overview

This system provides real-time transparency into SKAI lottery analysis computations without using percentages. All metrics are tied directly to actual work being performed.

**✨ Important:** The 3-layer visibility system is now **integrated directly into the SKAI Analysis Progress card** (`#skai-progress-indicator`) for maximum prominence and visibility during analysis.

## UI Layout - Integrated in Progress Card

The visibility system appears inside the SKAI Analysis Progress card, making it highly visible without scrolling:

```
┌─────────────────────────────────────────────────────────────┐
│ SKAI ANALYSIS PROGRESS CARD                                  │
├─────────────────────────────────────────────────────────────┤
│ Progress Steps | Auto-Tune Badge                             │
│ Training Status: Training 45/90... (ETA 2m 15s)             │
├─────────────────────────────────────────────────────────────┤
│ ═══ 3-LAYER COMPUTATION VISIBILITY (integrated) ═══         │
├─────────────────────────────────────────────────────────────┤
│ LAYER 1: DYNAMIC STATUS (what's happening now)              │
│                                                              │
│ Building training samples - Window size: 50 draws           │
├─────────────────────────────────────────────────────────────┤
│ LAYER 2: LIVE COUNTERS (real work metrics)                  │
│                                                              │
│ Draws analyzed: 458 / 500                                   │
│ Window evaluations: 412 / 450                               │
│ Pairwise comparisons: 287,420                               │
│ Batches processed: 142                                      │
│ Total computations: 3,482,119                               │
├─────────────────────────────────────────────────────────────┤
│ LAYER 3: PHASE SUMMARIES (what changed)                     │
│                                                              │
│ ┌───────────────────────────────────────────────────────┐  │
│ │ Data preparation complete                             │  │
│ │ • Analyzed 500 data points                            │  │
│ │ • Evaluated 845,100 relationships                     │  │
│ │ • Generated 450 training samples from 500 draws       │  │
│ └───────────────────────────────────────────────────────┘  │
│                                                              │
│ ┌───────────────────────────────────────────────────────┐  │
│ │ Main numbers • seed 1337 complete                     │  │
│ │ • Analyzed 30 data points                             │  │
│ │ • Evaluated 142 relationships                         │  │
│ │ • Model trained for 30 epochs, final loss: 0.0234    │  │
│ └───────────────────────────────────────────────────────┘  │
└─────────────────────────────────────────────────────────────┘
```

**Placement Benefits:**
- More prominent - inside main progress card
- No scrolling required during analysis  
- Better visual grouping with progress information
- Professional separator (border-top) distinguishes sections

## Layer 1: Dynamic Status Line

**Purpose:** Always answer "What computation is currently running?"

**Examples:**
- `Preparing historical data - Loading draw history`
- `Building training samples - Window size: 50 draws`
- `Training neural network - Main numbers • seed 1337 (30/90 epochs)`

**Rules:**
- Plain English only
- No jargon (tensors, matrices, epochs exposed as "training rounds")
- Updates when phase changes
- Derived from actual code execution state

## Layer 2: Live Numeric Counters

**Purpose:** Show how much work is being performed in real time

**Counters:**
1. **Draws analyzed:** X / Y
   - Incremented as buildSkaiDataset processes historical draws
   - Shows progress through dataset

2. **Window evaluations:** X / Y
   - Each training sample requires evaluating a window of draws
   - Shows pattern analysis progress

3. **Pairwise comparisons:** X,XXX
   - Number relationships examined (W × pick per sample)
   - Grows rapidly, shows intensive computation

4. **Batches processed:** X,XXX
   - Training batches completed
   - Increments per epoch

5. **Total computations:** X,XXX,XXX
   - Cumulative mathematical operations
   - Forward/backward passes × batch × dimensions
   - Most impressive counter for heavy computation

**Rules:**
- NO percentages
- NO fake numbers
- Monotonically increasing (never reset mid-run)
- Batched updates (every 10 iterations) for performance
- Throttled UI updates (100ms minimum between renders)
- Formatted with thousands separators

## Layer 3: Phase Completion Summaries

**Purpose:** Explain the effect of each completed computation phase

**Summary Structure:**
```
Phase Name complete
• Analyzed X data points
• Evaluated Y relationships  
• [Outcome description]
```

**Examples:**

### Data Preparation
```
Data preparation complete
• Analyzed 500 data points
• Evaluated 845,100 relationships
• Generated 450 training samples from 500 draws
```

### Training Phase
```
Main numbers • seed 1337 complete
• Analyzed 30 data points
• Evaluated 142 relationships
• Model trained for 30 epochs, final loss: 0.0234
```

**Rules:**
- Only appear when phase finishes
- Generated from real metrics
- No predictions or marketing language
- Show structural changes (samples generated, loss achieved)

## Technical Architecture

### Core Object: `window.SKAI_RUNTIME_STATS`

```javascript
{
  // Current phase (Layer 1)
  currentPhase: 'Building training samples',
  currentPhaseDetail: 'Window size: 50 draws',
  
  // Counters (Layer 2)
  drawsProcessed: 458,
  windowEvaluations: 412,
  pairwiseComparisons: 287420,
  batchesProcessed: 142,
  totalOperations: 3482119,
  
  // Targets (for X/Y display)
  totalDraws: 500,
  totalWindows: 450,
  
  // Summaries (Layer 3)
  completedPhases: [
    {
      phase: 'Data preparation',
      processed: 500,
      relationships: 845100,
      change: 'Generated 450 training samples...',
      metrics: { samples: 450, windowSize: 50 }
    }
  ],
  
  // Methods
  reset(),
  setPhase(phase, detail),
  incrementDraws(count),
  incrementWindows(count),
  incrementComparisons(count),
  incrementBatches(count),
  incrementOperations(count),
  completePhase(summary)
}
```

### DOM Structure

```html
<div id="skaiProgressHost">
  <div id="skaiProgress"></div> <!-- Existing progress bar -->
</div>

<div id="skai-visibility-container">
  <div id="skai-visibility-status">
    Building training samples - Window size: 50 draws
  </div>
  
  <div id="skai-visibility-counters">
    <div class="skai-visibility-counter-line">Draws analyzed: 458 / 500</div>
    <div class="skai-visibility-counter-line">Window evaluations: 412 / 450</div>
    ...
  </div>
  
  <div id="skai-visibility-summaries">
    <div class="skai-visibility-summary">
      <div class="skai-visibility-summary-title">Data preparation complete</div>
      <ul class="skai-visibility-summary-details">
        <li>Analyzed 500 data points</li>
        ...
      </ul>
    </div>
  </div>
</div>
```

### Event Integration

**Reset on each run:**
```javascript
window.addEventListener('skai:ml:start', function() {
  window.SKAI_RUNTIME_STATS.reset();
});
```

**No new events needed** - uses existing SKAI event system

### Performance Optimizations

1. **Batched counter updates** - Every 10 loop iterations
2. **Throttled UI renders** - 100ms minimum between updates  
3. **requestAnimationFrame** - Non-blocking updates
4. **Silent failures** - Try/catch to never break computation

## Instrumentation Points

### 1. buildSkaiDataset (Data Preparation)

**Location:** Line 19978-20196

**Phase tracking:**
```javascript
// Start
SKAI_RUNTIME_STATS.setPhase('Preparing historical data', 'Loading draw history');

// Processing
SKAI_RUNTIME_STATS.setPhase('Building training samples', 'Window size: ' + W + ' draws');

// Loop (batched every 10 iterations)
if (i % 10 === 0) {
  SKAI_RUNTIME_STATS.incrementWindows(10);
  SKAI_RUNTIME_STATS.incrementDraws(10);
  SKAI_RUNTIME_STATS.incrementComparisons(W * pick * 10);
  SKAI_RUNTIME_STATS.incrementOperations(W * dom * 10);
}

// Complete
SKAI_RUNTIME_STATS.completePhase({
  phase: 'Data preparation',
  processed: hist,
  relationships: totalComps,
  change: 'Generated ' + samples + ' training samples...'
});
```

### 2. fitWithValidation (Training)

**Location:** Line 20877-21059

**Phase tracking:**
```javascript
// Start
onTrainBegin: function() {
  SKAI_RUNTIME_STATS.setPhase('Training neural network', phaseLabel);
}

// Epoch end
onEpochEnd: function(epoch, logs) {
  SKAI_RUNTIME_STATS.incrementBatches(batchesPerEpoch);
  SKAI_RUNTIME_STATS.incrementOperations(batchesPerEpoch * opsPerBatch);
  SKAI_RUNTIME_STATS.setPhase('Training neural network', 
    phaseLabel + ' (' + eff + '/' + tot + ' epochs)');
}

// Complete
model.fit(...).then(function(history) {
  SKAI_RUNTIME_STATS.completePhase({
    phase: phaseLabel,
    processed: totalEpochsCompleted,
    relationships: totalBatches,
    change: 'Model trained for ' + totalEpochsCompleted + ' epochs...'
  });
});
```

## UX Tone Guidelines

**Inspiration:** Apple system dialogs, Stripe dashboards

**Do:**
- Use plain English
- Be calm and technical
- Show real numbers
- Justify long runtimes with actual work metrics
- Be trustworthy

**Don't:**
- Use jargon ("tensors", "backpropagation")
- Say "AI is thinking"
- Use marketing language
- Show fake progress
- Use percentages
- Add unnecessary animations

## Usage for Users

When SKAI analysis runs, users will see:

1. **What's happening:** Clear status line updates
2. **How much work:** Growing counters showing real computation
3. **What changed:** Summaries after each major phase

This makes long runtimes feel justified rather than broken, as users can see the actual mathematical work being performed.

## Maintenance Notes

- All counters must remain tied to real loops
- If adding new computation phases, add instrumentation
- Keep status messages plain and brief
- Test with small and large datasets
- Verify counts are monotonic (always increasing)
