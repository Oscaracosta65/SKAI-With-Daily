# Implementation Checklist

## Completed Changes ✓

1. ✅ Modified rendering logic to use JSON config field instead of inferring from domain/pick
2. ✅ Added `isDaily` field to SKAI_META (exposed in JavaScript)
3. ✅ Daily games (isDaily=true) now render exact pick size
4. ✅ Regular lotteries (isDaily=false/missing) now render top 20 results
5. ✅ Maintained strict UTF-8 encoding (no glyphs or special character replacements)
6. ✅ All syntax checks pass (PHP lint successful)
7. ✅ Created configuration guide with examples

## Required Next Steps

### Update JSON Configuration Files

You need to add the `is_daily` field to your lottery configuration JSON files:

#### Location of JSON Files (EXACT PATHS FROM CODE)
These are the actual files being loaded by the SKAI module:

**Master Config (Regular Lotteries):**
```
/home/oscara/web/lottoexpert.net/public_html/lottery_skip_config.json
```
This file contains regular lotteries (Powerball, Mega Millions, state lotteries, etc.)

**Daily Lotteries Catalog:**
```
/home/oscara/web/lottoexpert.net/public_html/dailylotteries.json
```
This file contains daily digit-based lotteries (Pick 1-5 games with 0-9 domain)

#### What to Add to Each File

**1. lottery_skip_config.json (Regular Lotteries)**
Add to each lottery object:
```json
"is_daily": false
```
OR simply omit the field (defaults to false)

These are traditional lotteries where you want to see **top 20 results pool**.

**2. dailylotteries.json (Daily Games)**
Add to each lottery object:
```json
"is_daily": true
```
These are digit-based games where you want to see **exact pick count** (e.g., Pick 3 shows 3 numbers).

**IMPORTANT:** The `dailylotteries.json` file contains games that ARE daily digit games by definition, so ALL entries in that file should have `"is_daily": true`.

### Examples of Games to Update

**Daily Games (set is_daily: true):**
- Pick 1
- Pick 2
- Pick 3
- Pick 4
- Pick 5
- Any other digit-based daily games

**Regular Lotteries (set is_daily: false or omit):**
- Powerball
- Mega Millions
- Lotto 6/49
- Any Pick 3/4/5 that should show top 20 results
- State lotteries

## Testing

After updating the JSON files:

1. Test a daily game (e.g., Pick 3):
   - Should display exactly 3 numbers
   - Should show digit-by-digit analysis panel

2. Test a regular lottery (e.g., state Pick 3):
   - Should display top 20 results pool
   - Should NOT show digit panel

3. Test a regular lottery (e.g., Powerball Pick 5):
   - Should display top 20 results pool
   - Should show traditional analysis

## Notes

- The default behavior (when `is_daily` is missing) is to treat as a regular lottery showing top 20
- Both field names are supported: `is_daily` or `isDaily`
- No code changes needed beyond updating JSON files
- UTF-8 encoding is strictly maintained (no hyphens, glyphs, or special characters were introduced)
