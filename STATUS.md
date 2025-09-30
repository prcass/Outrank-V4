# Outrank V4 Development Status

## Last Updated: 2025-09-30

## Repository Information
- **GitHub**: https://github.com/prcass/Outrank-V4
- **Branch**: main
- **Local Path**: `/home/randycass/projects/know-it-all/Outrank-V4/`
- **Parent Project**: Outrank V3 (https://github.com/prcass/Outrank-V3)

## Currently Working On
- Ready to implement V4 prototype

## Completed Changes
1. ✅ Created new separate Outrank-V4 repository
2. ✅ Set up complete documentation framework
3. ✅ Migrated v3 prototype as starting point (outrank-v4-prototype.html)
4. ✅ Migrated v3 rules as starting point (GAME_RULES_V4.md)
5. ✅ Created all documentation templates
6. ✅ Initialized git and pushed to GitHub
7. ✅ **Designed complete V4 gameflow** (Draft & Guess mechanic)
8. ✅ **Documented all design decisions** (6 major decisions with rationale)
9. ✅ **Created comprehensive CHANGELOG** (V3 vs V4 comparison)
10. ✅ **Completed GAMEFLOW_V4.md** (detailed spec with examples)
11. ✅ **Defined scoring system** (1pt/guess + bonuses + cash-out)

## V4 Design Summary

### Core Mechanics:
- **REMOVED**: Bidding, Blocking, Hidden Tokens, Chips
- **NEW**: Draft & Guess (higher/lower)
- **NEW**: Push-your-luck (lose round tokens on wrong guess, keep points)
- **NEW**: Cash out sets anytime (2=2pts, 3=5pts, 4=8pts)
- **NEW**: Hand limit (8 tokens max)
- **NEW**: First Guesser privilege, Last Standing bonus

### Scoring:
- 1 point per correct guess
- 1 bonus point for last to pass
- 2/5/8 points for cashing sets
- First guesser advantage (turn order)

### Key Innovation:
**Points are safe, tokens are at risk** - Wrong guess loses tokens but keeps points earned

## Pending Changes
1. ⏳ Update GAME_RULES_V4.md with player-facing rules
2. ⏳ Implement V4 gameflow in prototype HTML
3. ⏳ Test and validate prototype
4. ⏳ Determine game end condition through playtesting

## Next Steps
1. **Implement prototype** - Build V4 gameflow in HTML/JS
2. **Playtest** - Validate mechanics and balance
3. **Update rulebook** - Player-facing rules document
4. **Iterate** - Tune based on playtest feedback

## Questions/Decisions Needed
- ⏳ Game end condition (needs playtesting to determine)
  - Options: Round limit, score target, token depletion, time limit

## Files Structure
```
Outrank-V4/
├── STATUS.md (this file)
├── outrank-v4-prototype.html ✅
├── GAME_RULES_V4.md ✅
├── CHANGELOG_V3_TO_V4.md ✅
├── GAMEFLOW_V4.md ✅
└── v4-notes/
    ├── design-decisions.md ✅
    ├── implementation-log.md ✅
    └── testing-checklist.md ✅
```

## Version History
- **2025-09-30**: Initial V4 repository created, migrated from V3
