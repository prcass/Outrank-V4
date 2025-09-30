# Outrank V4 - Testing Checklist

## Purpose
Comprehensive testing checklist for all v4 features and gameflow.

---

## Setup Testing

### Initial Configuration
- [ ] Game initializes with 2 players
- [ ] Game initializes with 3 players
- [ ] Game initializes with 4 players
- [ ] Mix of human and AI players works
- [ ] All human players works
- [ ] All AI players works

### Token Distribution
- [ ] Each player receives exactly 2 hidden tokens
- [ ] Center pool has exactly 6 tokens
- [ ] No duplicate tokens in play
- [ ] Tokens match selected category
- [ ] Token pools properly initialized

### Blocking Chips
- [ ] Each player receives correct number of chips
- [ ] Chip values are correct
- [ ] Total chips tracked properly

---

## Challenge Phase Testing

- [ ] Challenge card displays correctly
- [ ] Category shown properly
- [ ] Ranking criteria clear
- [ ] Center pool revealed
- [ ] Hidden tokens visible to owner
- [ ] Transitions to bidding phase

---

## Bidding Phase Testing

### Basic Bidding
- [ ] First player can bid
- [ ] Bid must be higher than current
- [ ] Maximum bid calculated correctly
- [ ] Minimum bid enforced
- [ ] Players can pass
- [ ] Turn order is correct

### Edge Cases
- [ ] Cannot bid more than available tokens
- [ ] All players pass (challenge skipped)
- [ ] Last non-passed player wins automatically
- [ ] Passed players cannot bid again
- [ ] AI players bid reasonably

### Validation
- [ ] Invalid bids rejected
- [ ] Error messages clear
- [ ] UI updates correctly
- [ ] Current bid displayed
- [ ] Passed players indicated

---

## Blocking Phase Testing

### Basic Blocking
- [ ] Only non-winners can block
- [ ] Tokens can be blocked
- [ ] Blocked tokens marked visually
- [ ] Turn order correct
- [ ] Each player gets one turn

### Validation
- [ ] Cannot block if insufficient tokens remain
- [ ] Math validation: available ≥ bid
- [ ] Cannot block already blocked tokens
- [ ] Error messages clear

### Edge Cases
- [ ] Blocking reduces available tokens correctly
- [ ] Hidden + owned tokens counted in validation
- [ ] AI players block strategically
- [ ] Skip blocking works

---

## Ranking Phase Testing

### Token Selection
- [ ] Can select from center pool
- [ ] Can select from hidden tokens
- [ ] Can select from owned tokens
- [ ] Cannot select blocked tokens
- [ ] Must select exactly [bid] tokens
- [ ] All tokens from same category

### Ranking Interface
- [ ] Drag and drop works
- [ ] Tokens can be reordered
- [ ] Current order displayed
- [ ] Challenge criteria shown
- [ ] Submit button appears

### Validation
- [ ] Must rank exactly [bid] tokens
- [ ] Cannot submit incomplete ranking
- [ ] Cannot change after submit

---

## Reveal Phase Testing

- [ ] Ranking validated correctly
- [ ] Correct order displayed
- [ ] Animation plays
- [ ] Success/fail determined properly
- [ ] Results shown clearly

---

## Scoring Phase Testing

### Successful Ranking
- [ ] Bidder gets correct points
- [ ] Bidder gains ownership of tokens
- [ ] Bidder receives blocking chips
- [ ] Blockers lose chips
- [ ] Blockers get no points
- [ ] Blockers get no tokens

### Failed Ranking
- [ ] Bidder gets no points
- [ ] Bidder loses ranked tokens
- [ ] Blockers get points (chip value)
- [ ] Blockers keep chips
- [ ] Blockers gain blocked tokens

### Token Lifecycle
- [ ] Used tokens marked correctly
- [ ] Owned tokens tracked
- [ ] Center pool refilled
- [ ] No duplicate tokens
- [ ] usedTokenIds updated

---

## Game End Testing

- [ ] Game ends at correct time
- [ ] Final scoring calculated
- [ ] Chip bonuses added
- [ ] Token bonuses added
- [ ] Winner determined correctly
- [ ] Results displayed

---

## UI/UX Testing

### Visual
- [ ] All screens render correctly
- [ ] Responsive design works
- [ ] Colors/styling consistent
- [ ] Animations smooth
- [ ] No visual glitches

### Interaction
- [ ] Buttons clickable
- [ ] Modals open/close
- [ ] Notifications appear
- [ ] Forms validate
- [ ] Navigation works

### Mobile
- [ ] Works on small screens
- [ ] Touch interactions work
- [ ] Text readable
- [ ] Layout doesn't break

---

## Browser Testing

- [ ] Chrome
- [ ] Firefox
- [ ] Safari
- [ ] Edge
- [ ] Mobile browsers

---

## Edge Cases & Stress Testing

- [ ] Maximum bid (10 tokens)
- [ ] Minimum bid (1 token)
- [ ] All tokens blocked except bid amount
- [ ] Player with no valid tokens
- [ ] Empty token pools
- [ ] Network interruption (if applicable)

---

## Console Testing

- [ ] No JavaScript errors
- [ ] No warnings
- [ ] Proper logging
- [ ] State updates correctly

---

## Notes

### Testing Strategy
1. Test each phase in isolation
2. Test complete round flow
3. Test edge cases
4. Test browser compatibility
5. Final playthrough test

### Bug Tracking
*Record bugs found during testing*

---

## Test Results

### Test Date: [Date]
### Tester: [Name]

**Passed**: [ ] tests
**Failed**: [ ] tests
**Issues Found**: [List]

---

## Regression Testing

*After changes, re-test these critical paths*

1. Complete game with 2 players
2. Bidding → Blocking → Successful rank
3. Bidding → Blocking → Failed rank
4. All players pass scenario
