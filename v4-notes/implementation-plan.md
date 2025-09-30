# Outrank V4 - Implementation Plan

## Overview
Building the V4 prototype from scratch, implementing the Draft & Guess mechanic with complete state management.

**Approach**: Incremental development with testing at each phase

---

## Implementation Phases

### Phase 1: Foundation & Structure
**Goal**: Set up HTML structure, basic CSS, and core state management

**Tasks**:
1. ✅ Create clean HTML structure
   - Game setup screen
   - Main game screen
   - Player info panels
   - Action buttons area
   - Modals (cash-out, results)

2. ✅ Set up CSS framework
   - Mobile-first responsive design
   - Color scheme (consistent with V3 purple/gradient theme)
   - Token display styles
   - Button styles
   - Animation foundations

3. ✅ Initialize game state structure
   ```javascript
   gameState = {
       phase: 'setup',
       round: 0,
       currentPlayer: 0,
       firstGuesser: 0,
       players: [],
       centerToken: null,
       draftPool: [],
       categoryPools: {},
       retiredTokens: [],
       passedPlayers: new Set(),
       currentChallenge: null
   }
   ```

4. ✅ Create token database
   - Import/adapt movie data from V3 (40 movies with tags)
   - Structure: { id, name, tags: [A, B, C, D], stats: {} }

**Testing**: Game state initializes correctly, UI renders

---

### Phase 2: Game Setup & Challenge Selection
**Goal**: Players can set up game and start first challenge

**Tasks**:
1. ✅ Player setup screen
   - Input number of players (2-6)
   - Enter player names
   - Select starting player
   - Initialize player state (score: 0, hand: [], thisRound: [])

2. ✅ Challenge system
   - Define challenge objects: { category, stat, name, direction }
   - Example: { category: 'movies', stat: 'boxOffice', name: 'Box Office Revenue', direction: 'both' }
   - Challenge selection UI (for first guesser)

3. ✅ Token pool setup
   - Draw 13 tokens from selected category
   - Place 1 in center (revealed with value)
   - Place 12 in draft pool (visible)
   - Display all tokens with names and tags

4. ✅ First guesser marker
   - Visual indicator of who goes first
   - Marker passes on first pass/fail

**Testing**: Can set up game, select challenge, see 13 tokens displayed

---

### Phase 3: Draft & Guess Mechanic (Core Gameplay)
**Goal**: Players can draft tokens and guess higher/lower

**Tasks**:
1. ✅ Draft token selection
   - Click token from draft pool
   - Highlight selected token
   - Show token details (name, visible stat value)

2. ✅ Higher/Lower guess UI
   - Large HIGHER and LOWER buttons
   - Show comparison: "Is [Token] HIGHER or LOWER than [Center]?"
   - Display both values clearly

3. ✅ Guess validation logic
   - Compare selected token stat vs center token stat
   - Determine correct/wrong based on guess

4. ✅ Correct guess flow
   - Add 1 point to player score (immediate)
   - Move center token to player's "thisRound" pile
   - Move drafted token to center
   - Show success animation (✅ +1pt)
   - Next player's turn

5. ✅ Wrong guess flow
   - Return all "thisRound" tokens to draft pool
   - Return drafted token to draft pool
   - Points stay (already added)
   - Mark player as "first guesser" for next round
   - Show fail animation (❌ tokens lost, points kept)
   - Next player's turn

6. ✅ Turn management
   - Advance to next player
   - Skip passed players
   - Detect when all passed (round end)
   - Handle "last player standing" scenario

**Testing**: Can draft, guess, see correct/wrong outcomes, turns advance properly

---

### Phase 4: Scoring & Hand Management
**Goal**: Track scores accurately and manage player hands

**Tasks**:
1. ✅ Score display
   - Real-time score updates
   - Show points per player
   - Highlight point gains (+1, +2, +5, +8)

2. ✅ Hand separation
   - "This Round" section (at risk, highlighted red/yellow)
   - "Hand" section (safe, highlighted green)
   - Visual distinction clear
   - Show token count for each

3. ✅ Hand limit enforcement
   - Check if player has 8+ tokens
   - Block draft action if at limit
   - Show warning: "Must cash out or discard"

4. ✅ Round end logic
   - Detect all players passed
   - Award "last standing" bonus (+1pt)
   - Move "thisRound" → "hand" for all players
   - Clear passedPlayers set
   - Assign first guesser for next round

5. ✅ Stats tracking
   - Count correct guesses per player
   - Count cash-outs per player
   - Show in player panel

**Testing**: Scores update correctly, hand limits work, round ends properly

---

### Phase 5: Cash-Out System
**Goal**: Players can cash out sets for points

**Tasks**:
1. ✅ Detect available sets
   - Scan player hand + thisRound tokens
   - Find all matching tags (A, B, C, D)
   - Count tokens per tag
   - Show which sets are available (2, 3, or 4 tokens)

2. ✅ Cash-out UI
   - "Cash Out" button (enabled when sets available)
   - Modal with token selection
   - Group tokens by tag
   - Show point values (2→2pts, 3→5pts, 4→8pts)

3. ✅ Tag selection
   - Player selects which tokens to cash
   - Player chooses which tag to use (if tokens share multiple)
   - Highlight selected tokens
   - Show total points

4. ✅ Cash-out execution
   - Add points to score
   - Remove cashed tokens from hand
   - Add to retiredTokens pool
   - Show success message (💰 +Xpts)
   - End player's turn

5. ✅ Validation
   - Must have 2+ tokens with matching tag
   - Can only cash one set per turn
   - Each token used for one tag only

**Testing**: Can cash out 2/3/4-token sets, points added correctly, tokens removed

---

### Phase 6: Pass Action & Round Flow
**Goal**: Players can pass and rounds transition properly

**Tasks**:
1. ✅ Pass button
   - Always available
   - Confirms "Are you sure? Tokens move to hand (safe)"

2. ✅ Pass logic
   - Add player to passedPlayers set
   - Move "thisRound" → "hand"
   - End player's turn
   - Cannot draft again this round

3. ✅ Last standing detection
   - Check if only 1 non-passed player remains
   - Allow them to continue solo
   - Award bonus when they pass

4. ✅ Round end screen
   - Show results: Who passed when, who earned what
   - Show last standing bonus recipient
   - Show first guesser for next round
   - "Next Round" button

5. ✅ Next round setup
   - Clear passedPlayers
   - Refill draft pool to minimum 8 tokens
   - First guesser selects new challenge
   - Increment round counter

**Testing**: Pass works, rounds end cleanly, next round starts properly

---

### Phase 7: UI Polish & Feedback
**Goal**: Make the game feel good to play

**Tasks**:
1. ✅ Animations
   - Correct guess: Green flash, +1pt float up
   - Wrong guess: Red shake, tokens return with motion
   - Cash out: Coins/money animation, +Xpts
   - Pass: Tokens slide to hand area
   - Last standing: Confetti/celebration

2. ✅ Visual clarity
   - Current player highlighted prominently
   - Center token large and clear
   - Draft pool organized (grid or carousel)
   - Color coding (success/fail/info)

3. ✅ Notifications
   - Toast messages for actions
   - "Alice guessed correctly! +1pt"
   - "Bob lost 3 tokens!"
   - "Carol cashed out 3 tokens for 5pts!"

4. ✅ Responsive design
   - Works on mobile (375px)
   - Works on tablet (768px)
   - Works on desktop (1200px+)
   - Touch-friendly buttons

5. ✅ Error handling
   - Can't draft when at 8 tokens
   - Can't cash when no sets available
   - Clear error messages

**Testing**: Smooth animations, clear feedback, works on all devices

---

### Phase 8: Game End & Final Scoring
**Goal**: Game ends properly and winner declared

**Tasks**:
1. ⏳ Game end detection
   - Implement chosen end condition (TBD during playtesting)
   - Show "Game Over" screen

2. ⏳ Final scoring
   - Add up all points earned
   - Show uncashed tokens (worth 0)
   - Declare winner

3. ⏳ Stats summary
   - Show per-player stats
   - Correct guesses, cash-outs, final score

4. ⏳ New game option
   - Reset button
   - Return to setup

**Testing**: Game ends correctly, winner determined, can restart

---

## Development Priorities

### Must-Have (MVP):
- ✅ Phase 1-6: Core gameplay loop
- ⏳ Basic UI (functional, not pretty)
- ⏳ Single category (movies only)

### Should-Have (V1):
- Phase 7: Polish and animations
- Multiple categories
- AI opponents

### Nice-to-Have (V2):
- Sound effects
- Custom challenges
- Save/load games
- Statistics tracking

---

## Testing Strategy

### Unit Testing:
- State transitions
- Scoring calculations
- Set detection logic
- Hand limit enforcement

### Integration Testing:
- Complete round flow
- Pass → Cash Out → Draft sequences
- Edge cases (all pass immediately, solo play)

### Playtesting:
- 2-player game
- 4-player game
- Balance testing (guess points vs set points)
- Game length

---

## File Structure

```
outrank-v4-prototype.html (all-in-one for now)
├── HTML Structure
│   ├── Setup Screen
│   ├── Game Screen
│   ├── Player Panels
│   └── Modals
├── CSS Styles
│   ├── Layout
│   ├── Tokens
│   ├── Buttons
│   └── Animations
└── JavaScript
    ├── Game State
    ├── Token Database
    ├── Challenge System
    ├── Draft & Guess Logic
    ├── Scoring System
    ├── Cash-Out Logic
    ├── UI Updates
    └── Event Handlers
```

---

## Implementation Order

1. **Phase 1** (Foundation) - 1-2 hours
2. **Phase 2** (Setup) - 1 hour
3. **Phase 3** (Core Gameplay) - 2-3 hours ← Most critical
4. **Phase 4** (Scoring) - 1 hour
5. **Phase 5** (Cash-Out) - 1-2 hours
6. **Phase 6** (Pass/Rounds) - 1 hour
7. **Phase 7** (Polish) - 1-2 hours
8. **Phase 8** (Game End) - 30 min

**Total Estimated Time**: 8-12 hours of coding

---

## Risks & Mitigation

**Risk**: State management gets complex
**Mitigation**: Start simple, centralize state updates, test frequently

**Risk**: UI becomes cluttered with info
**Mitigation**: Progressive disclosure, show only what's needed per phase

**Risk**: Balance issues (guess points vs sets)
**Mitigation**: Make scoring values configurable, easy to tune

**Risk**: Token pool depletion edge cases
**Mitigation**: Implement minimum 8 refill early, test thoroughly

---

## Success Criteria

✅ Can play a complete round
✅ Guess points awarded correctly
✅ Wrong guess loses tokens but keeps points
✅ Can cash out sets
✅ Hand limit enforced
✅ Rounds transition properly
✅ Game is fun to play!

---

## Next Action

Start with **Phase 1: Foundation & Structure**
- Create clean HTML skeleton
- Set up basic CSS
- Initialize game state
- Load token database

Ready to proceed?
