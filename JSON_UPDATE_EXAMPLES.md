# JSON File Update Examples

## File 1: lottery_skip_config.json (Regular Lotteries)

This file contains regular lotteries that should show **top 20 results**.

### Example Structure

```json
{
  "lotteries": [
    {
      "game_id": "powerball",
      "lotteryName": "Powerball",
      "is_daily": false,
      "pickSize": 5,
      "mainNumbersMax": 69,
      "mainNumbersMin": 1,
      "hasExtraBall": true,
      "extraBallMax": 26,
      "dbCol": "powerball_draws"
    },
    {
      "game_id": "mega_millions",
      "lotteryName": "Mega Millions",
      "is_daily": false,
      "pickSize": 5,
      "mainNumbersMax": 70,
      "mainNumbersMin": 1,
      "hasExtraBall": true,
      "extraBallMax": 25,
      "dbCol": "mega_millions_draws"
    },
    {
      "game_id": "lotto_649",
      "lotteryName": "Lotto 6/49",
      "is_daily": false,
      "pickSize": 6,
      "mainNumbersMax": 49,
      "mainNumbersMin": 1,
      "hasExtraBall": false,
      "dbCol": "lotto649_draws"
    },
    {
      "game_id": "cash3_regular",
      "lotteryName": "Cash 3",
      "is_daily": false,
      "pickSize": 3,
      "mainNumbersMax": 39,
      "mainNumbersMin": 1,
      "hasExtraBall": false,
      "dbCol": "cash3_draws"
    },
    {
      "game_id": "play4_regular",
      "lotteryName": "Play 4",
      "is_daily": false,
      "pickSize": 4,
      "mainNumbersMax": 49,
      "mainNumbersMin": 1,
      "hasExtraBall": false,
      "dbCol": "play4_draws"
    }
  ]
}
```

### Key Points for lottery_skip_config.json:
- Add `"is_daily": false` to each lottery object
- OR omit the field entirely (defaults to false)
- These show **top 20 results pool**
- Includes all traditional lotteries (Powerball, Mega Millions, state lotteries)
- Can include Pick 3, Pick 4, Pick 5 games that are NOT digit-based daily games

---

## File 2: dailylotteries.json (Daily Digit Games)

This file contains daily digit-based lotteries that should show **exact pick count**.

### Example Structure

```json
{
  "dailyGames": [
    {
      "game_id": "pick1",
      "lotteryName": "Pick 1",
      "is_daily": true,
      "pickSize": 1,
      "mainNumbersMax": 9,
      "mainNumbersMin": 0,
      "hasExtraBall": false,
      "allowZero": true,
      "tableName": "pick1_draws"
    },
    {
      "game_id": "pick2",
      "lotteryName": "Pick 2",
      "is_daily": true,
      "pickSize": 2,
      "mainNumbersMax": 9,
      "mainNumbersMin": 0,
      "hasExtraBall": false,
      "allowZero": true,
      "tableName": "pick2_draws"
    },
    {
      "game_id": "pick3",
      "lotteryName": "Pick 3",
      "is_daily": true,
      "pickSize": 3,
      "mainNumbersMax": 9,
      "mainNumbersMin": 0,
      "hasExtraBall": false,
      "allowZero": true,
      "tableName": "pick3_draws"
    },
    {
      "game_id": "pick4",
      "lotteryName": "Pick 4",
      "is_daily": true,
      "pickSize": 4,
      "mainNumbersMax": 9,
      "mainNumbersMin": 0,
      "hasExtraBall": false,
      "allowZero": true,
      "tableName": "pick4_draws"
    },
    {
      "game_id": "pick5",
      "lotteryName": "Pick 5",
      "is_daily": true,
      "pickSize": 5,
      "mainNumbersMax": 9,
      "mainNumbersMin": 0,
      "hasExtraBall": false,
      "allowZero": true,
      "tableName": "pick5_draws"
    },
    {
      "game_id": "pick3_midday",
      "lotteryName": "Pick 3 Midday",
      "is_daily": true,
      "pickSize": 3,
      "mainNumbersMax": 9,
      "mainNumbersMin": 0,
      "hasExtraBall": false,
      "allowZero": true,
      "tableName": "pick3_midday_draws"
    },
    {
      "game_id": "pick3_evening",
      "lotteryName": "Pick 3 Evening",
      "is_daily": true,
      "pickSize": 3,
      "mainNumbersMax": 9,
      "mainNumbersMin": 0,
      "hasExtraBall": false,
      "allowZero": true,
      "tableName": "pick3_evening_draws"
    }
  ]
}
```

### Key Points for dailylotteries.json:
- Add `"is_daily": true` to **ALL** lottery objects in this file
- These are digit-based games (domain 0-9)
- Shows **exact pick count** (Pick 3 = 3 numbers, Pick 5 = 5 numbers)
- Includes Pick 1, 2, 3, 4, 5 and variants (Midday, Evening, Fireball, etc.)
- `allowZero: true` is typical for these games

---

## Quick Reference Table

| File | Game Type | is_daily Value | Display Mode |
|------|-----------|----------------|--------------|
| lottery_skip_config.json | Regular lotteries | `false` or omit | Top 20 pool |
| dailylotteries.json | Daily digit games | `true` | Exact pick count |

---

## Update Steps

### Step 1: Backup Files
```bash
cp /home/oscara/web/lottoexpert.net/public_html/lottery_skip_config.json /home/oscara/web/lottoexpert.net/public_html/lottery_skip_config.json.backup
cp /home/oscara/web/lottoexpert.net/public_html/dailylotteries.json /home/oscara/web/lottoexpert.net/public_html/dailylotteries.json.backup
```

### Step 2: Edit lottery_skip_config.json
Add `"is_daily": false` to each lottery object (or omit it).

### Step 3: Edit dailylotteries.json
Add `"is_daily": true` to each lottery object.

### Step 4: Test
- Load a daily game (e.g., Pick 3) - should show exactly 3 numbers
- Load a regular lottery (e.g., Powerball) - should show top 20 numbers
- Load a regular Pick 3 game - should show top 20 numbers (not 3)

---

## Note on Field Names

The code supports both naming conventions:
- `is_daily` (snake_case)
- `isDaily` (camelCase)

Use whichever matches your existing JSON structure style.
