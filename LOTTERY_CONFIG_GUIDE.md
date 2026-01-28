# Lottery Configuration Guide

## Rendering Modes

The SKAI system supports two rendering modes for lottery results:

### 1. Daily Digit Games
**Renders:** Exact number of picks (e.g., Pick 3 shows 3 numbers, Pick 5 shows 5 numbers)
**Use for:** Daily games with digit-by-digit analysis (0-9 domain)

### 2. Regular Lotteries
**Renders:** Top 20 results pool
**Use for:** Traditional lotteries (e.g., Powerball, Mega Millions, state lotteries)

## Configuration

Add the `is_daily` or `isDaily` field to your lottery JSON configuration:

### Example: Daily Pick 3 Game
```json
{
  "game_id": "pick3",
  "lotteryName": "Pick 3",
  "is_daily": true,
  "pickSize": 3,
  "mainNumbersMax": 9,
  "mainNumbersMin": 0,
  "hasExtraBall": false
}
```

### Example: Regular Pick 3 Lottery
```json
{
  "game_id": "cash3",
  "lotteryName": "Cash 3",
  "is_daily": false,
  "pickSize": 3,
  "mainNumbersMax": 39,
  "mainNumbersMin": 1,
  "hasExtraBall": false
}
```

### Example: Daily Pick 5 Game
```json
{
  "game_id": "pick5",
  "lotteryName": "Pick 5",
  "is_daily": true,
  "pickSize": 5,
  "mainNumbersMax": 9,
  "mainNumbersMin": 0,
  "hasExtraBall": false
}
```

### Example: Regular 6/49 Lottery
```json
{
  "game_id": "lotto649",
  "lotteryName": "Lotto 6/49",
  "is_daily": false,
  "pickSize": 6,
  "mainNumbersMax": 49,
  "mainNumbersMin": 1,
  "hasExtraBall": false
}
```

## Field Reference

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `is_daily` or `isDaily` | boolean | Yes | `true` for daily digit games, `false` for regular lotteries |
| `pickSize` | integer | Yes | Number of balls drawn |
| `mainNumbersMax` | integer | Yes | Maximum number in the pool |
| `mainNumbersMin` | integer | No | Minimum number (default: 1 for regular, 0 for daily) |
| `hasExtraBall` | boolean | No | Whether the game has an extra/bonus ball |

## Default Behavior

If `is_daily` or `isDaily` is not specified or is `false`, the lottery will render in **regular mode** showing top 20 results.
