# Monopoly Deal: No Mercy

## Game Rules — Frozen Specification

**Version:** 1.0  
**Status:** FROZEN  
**Purpose:** Canonical rules specification for the digital implementation.

---

# 1. Game Objective

The objective is to be the first player to complete the required number of Property Sets.

A Property Set is complete when the player possesses the required number of Properties of that color, including legally assigned Wild Property cards.

Complete Property Sets are not inherently protected.

---

# 2. Players

Each player has:

- Hand
- Bank
- Property Collection
- Debt Chips

---

# 3. Game Components

The physical deck contains exactly **120 cards**:

| Category | Cards |
|---|---:|
| Money | 18 |
| Standard Properties | 28 |
| Two-Color Wild Properties | 9 |
| Any-Color Wild Properties | 2 |
| Rent / Double Rent | 16 |
| Other Action / Building Cards | 42 |
| Reference Cards | 5 |
| **Total** | **120** |

Reference cards are not part of the playable Draw Pile.

---

# 4. Game Setup

## 4.1 Shuffle

Shuffle all playable cards together to form the Draw Pile.

Reference cards remain separate.

Debt Chips remain separate.

## 4.2 Starting Player

If this is a rematch:

> The player who won the previous game starts.

If this is a new game:

> The starting player is selected randomly.

For deterministic testing, alphabetical order may be used.

## 4.3 Starting Hand

Each player receives the required starting hand from the Draw Pile.

The starting-hand size is a game configuration.

---

# 5. Turn Order

Players take turns clockwise.

At the beginning of a player's turn:

1. Resolve outstanding Debt obligations due on that turn.
2. Draw the required cards.
3. Play up to three cards.
4. Resolve applicable effects.
5. End the turn.

Play then passes to the next player unless an effect grants another turn.

---

# 6. Drawing Cards

Cards are drawn from the top of the Draw Pile.

When the Draw Pile is exhausted:

> Shuffle the entire face-up Discard Pile and make it the new Draw Pile.

The cycle repeats.

Only discarded cards are recycled.

Cards in Hands, Banks, Property Collections, or attached as Shacks are not recycled.

---

# 7. Playing Cards

A player may play a maximum of **3 cards during their turn**.

Each of the following counts as one card play:

- Money card played to Bank
- Property card
- Wild Property card
- Action card
- Shack
- Any card explicitly defined as a card play

---

# 8. Money Cards

A Money card may be placed directly into the player's Bank.

Once placed in the Bank:

> It is treated as money and cannot subsequently be played for another purpose.

---

# 9. Banking Action Cards

An Action card may be placed into the Bank instead of being played for its Action effect.

When banked:

> It acts only as money using its printed Bank Value.

A banked Action card cannot subsequently be played as an Action.

---

# 10. Property Cards

Property cards are placed into the player's Property Collection.

Each standard Property belongs to a specific color.

Properties of the same color contribute toward completing that color's Property Set.

---

# 11. Two-Color Wild Properties

A Two-Color Wild Property can represent either of its two printed colors.

Its active color can be changed between those two colors.

Changing the active color:

> Does not count as a card play.

The Wild contributes to whichever color it currently represents.

It cannot represent a color not printed on the card.

---

# 12. Any-Color Wild Properties

Any-Color Wild Property cards can represent any Property color.

However:

- They cannot be placed in the Bank.
- They have a Bank Value of 0M.
- They cannot be used as payment.
- They cannot by themselves form a complete Property Set.
- They may be added to another Property color/set.

They remain Property cards for applicable Property effects.

---

# 13. Property Set Rules

A Property Set is determined by the required number of Properties for that color.

Wild Property cards may contribute toward a Set when legally assigned to that color.

A complete Set may contain:

- Standard Properties
- Two-Color Wild Properties
- Any-Color Wild Properties where legally applicable

Complete Sets are **not protected**.

Applicable Action cards may therefore affect or break complete Sets.

---

# 14. Hand Size

The maximum Hand size is:

**7 cards.**

If a player already has 7 or more cards, a normal draw effect cannot increase their Hand.

Therefore:

> Additional cards from such a draw effect are useless.

Cards in the Bank and Property Collection do not count toward Hand size.

---

# 15. Rent

Rent is calculated from the Properties currently controlled by the player playing the Rent card.

The amount depends on:

- Selected Property color
- Number of Properties representing that color
- Shack bonus
- Rent modifiers

Rent is calculated using the current game state when the Rent effect resolves.

---

# 16. Shacks

A Shack is attached to one of the player's active Property Sets.

A Shack:

- Increases rent generated by that Property Set.
- Counts as one card play.
- Remains attached.
- Transfers with the relevant Property when ownership changes.

There is a maximum of:

**1 Shack per Property Set.**

A Shack may be placed on an active Set even when that Set is incomplete.

---

# 17. Shack Rent Calculation

The Shack bonus is added before Double Rent.

Formula:

```text
Base Rent + Shack Bonus = Adjusted Rent
Adjusted Rent × 2 = Final Rent
```

Example:

```text
Base Rent = 4M
Shack Bonus = 5M
Adjusted Rent = 9M
Double Rent = 18M
```

---

# 18. Shack Transfer

When a Property carrying a Shack changes ownership:

> The Shack remains attached and transfers with that Property.

This applies to applicable transfers including:

- Payment
- Deal Breaker
- Super Sly Deal
- Market Crash
- Repossession
- Other legal Property transfers

---

# 19. Rent Payment

When Rent resolves:

> The affected player(s) owe the calculated amount to the player who played the Rent Action.

Rent obligations use the game's payment and Debt rules.

---

# 20. Payment Rules

When a player owes another player:

1. Cards in the Bank are used first.
2. If the Bank is insufficient, eligible Properties may be used.
3. The payer chooses which eligible cards to give.
4. Transferred Properties become the creditor's Properties.
5. Any Shack attached to a transferred Property remains attached and transfers with it.

---

# 21. Debt

A player may owe another player because of:

- Rent
- Yoink!
- Forced Debt
- Any other effect explicitly creating a Debt obligation

If the player can fully satisfy the obligation:

> The Debt is paid normally.

If the player cannot fully satisfy it:

> The applicable Debt rules are used.

---

# 22. Debt Chips

Debt Chips represent outstanding obligations.

Each Debt Chip identifies:

- Debtor
- Creditor

A player may have multiple outstanding Debt Chips.

---

# 23. Forced Debt

Forced Debt allows a player to force another player to take one of their Debt Chips.

The receiving player becomes the debtor.

On the debtor's upcoming turn:

> The debtor must give a card to the creditor to satisfy the Debt Chip.

The card is immediately processed according to its type.

---

# 24. Debt Chip Limit

A player may give a maximum of **3 Debt Chips**.

If a player has already given all 3:

> They cannot give another Debt Chip.

Nothing happens.

No additional Debt Chip is created.

---

# 25. Debt Payment Card Processing

When a debtor gives a card to satisfy a Debt:

### Money Card

The creditor places it into their Bank.

### Standard Property

The creditor places it into their Property Collection.

### Two-Color Wild

The creditor places it into their Property Collection.

### Any-Color Wild

The creditor places it into their Property Collection.

### Action Card

The creditor immediately chooses:

- Bank the Action card as money, or
- Play the Action card.

If played:

> Its effect resolves immediately.

The Action is then discarded unless its effect specifies otherwise.

An Action played through Debt counts as one of the three card plays for the debtor's turn.

---

# 26. Action Cards

Action cards are normally played during the player's turn.

After an Action resolves:

> It is placed directly into the face-up Discard Pile.

---

# 27. Action Card Plays

Playing an Action counts as one of the three card plays.

This includes:

- Rent
- Double Rent
- Rent Any Color
- Double Rent Any Color
- Deal Breaker
- Forced Debt
- Go Again
- Heist
- Just Say No
- Market Crash
- Pass Go, Go Go!
- Repossession
- Shack
- Super Sly Deal
- Tax Collector
- Tough Luck
- Unfair Trade
- Yoink!

---

# 28. Just Say No

Just Say No is a defensive Action.

It may be played out of turn when an Action affects the player.

Effect:

> Cancel the Action's effect against the player who played Just Say No.

Just Say No:

- Protects only its user.
- Does not protect other affected players.
- Can itself be countered by another Just Say No.
- Cannot cancel ordinary inability-to-pay Debt.

A Just Say No played during the player's own turn counts as one card play.

---

# 29. Just Say No Chain

If Player A plays an Action against Player B:

```text
A → Action → B
```

B may respond:

```text
B → Just Say No
```

A may respond:

```text
A → Just Say No
```

The chain may continue.

The final resolution determines whether the original Action takes effect.

---

# 30. Rent Actions

A normal Rent card allows the player to select the applicable Property color represented by the card.

The player calculates rent using their Properties currently representing that color.

The resulting obligation is applied to the affected player(s).

---

# 31. Rent Any Color

Rent Any Color allows the player to choose the Property color for the Rent effect.

The chosen color must be legally available for the card.

Rent is then calculated using Properties representing that color.

---

# 32. Double Rent

Double Rent doubles the entire Rent amount.

Order:

```text
Calculate normal rent
        ↓
Add Shack bonus
        ↓
Apply Double Rent
```

---

# 33. Double Rent Any Color

Double Rent Any Color:

1. Selects a legal Property color.
2. Calculates rent.
3. Adds Shack bonus.
4. Doubles the resulting amount.

---

# 34. Deal Breaker

Deal Breaker targets one opponent.

Effect:

> Steal one complete Property Set from that opponent.

The complete Set transfers to the attacker.

Applicable Wild Properties assigned to that Set transfer with it.

Any Shack attached to the Set transfers with it.

Complete Sets are not protected.

---

# 35. Super Sly Deal

Super Sly Deal targets a Property color.

Effect:

> Take all Properties of the chosen color currently laid out by every other player.

This can affect:

- Standard Properties
- Two-Color Wild Properties
- Any-Color Wild Properties
- Incomplete Sets
- Complete Sets
- Properties carrying Shacks

Complete Sets are not protected.

---

# 36. Super Sly Deal and Wild Properties

### Two-Color Wild

A Two-Color Wild may be taken when it represents the chosen color.

### Any-Color Wild

An Any-Color Wild may be taken for any chosen Property color.

---

# 37. Tough Luck

Tough Luck targets one opponent.

Choose exactly one category:

```text
PROPERTY
ACTION
MONEY
```

The target gives **all cards of that category currently in their Hand** to the player who played Tough Luck.

Only the Hand is affected.

The target's Bank, Property Collection, and attached Shacks are not affected.

### Money

Includes all Money cards.

### Property

Includes:

- Standard Properties
- Two-Color Wild Properties
- Any-Color Wild Properties

### Action

Includes all Action and Building cards.

---

# 38. Heist

Heist targets every opponent.

From each opponent's Bank:

> The Heist player chooses exactly one card to take.

If an opponent has no cards in their Bank:

> Nothing is taken from that opponent.

The stolen card is placed into the attacker's Bank.

---

# 39. Yoink!

Yoink! targets one opponent.

Effect:

> The target owes the player 10M.

The 10M obligation is resolved through the Debt/payment system.

---

# 40. Repossession

Repossession targets one opponent.

The target keeps one Property.

The remaining applicable Properties are transferred according to the card's effect.

Any Shack attached to a transferred Property remains attached to that Property.

Complete Sets are not protected.

---

# 41. Market Crash

Market Crash performs the Property transfer specified by the card.

Affected Properties may include:

- Incomplete Sets
- Complete Sets
- Standard Properties
- Wild Properties
- Properties carrying Shacks

Any Shack attached to a transferred Property remains attached.

Complete Sets are not protected.

---

# 42. Unfair Trade

Unfair Trade performs the exchange specified by the card.

Only the assets specified by the card are exchanged.

Cards not included in the effect remain with their current owner.

---

# 43. Tax Collector

Tax Collector targets an opponent and affects their Bank according to the card's effect.

Banked cards are treated as individual cards regardless of whether they are:

- Money cards
- Banked Action cards

---

# 44. Pass Go, Go Go!

Pass Go, Go Go! allows the player to draw cards according to its effect.

If the player already has **7 or more cards**:

> No additional cards are drawn.

The card still counts as one card play.

---

# 45. Go Again

Go Again grants an additional turn.

Restriction:

> Go Again must be played as the final card play of the current turn.

After the current turn ends:

> The player immediately receives another complete turn.

The additional turn follows normal turn rules.

Go Again does not add three extra plays to the current turn.

---

# 46. Card Transfer

Whenever a Property changes ownership:

> It moves to the new owner's Property Collection.

If it has a Shack:

> The Shack moves with it.

A transferred Wild retains its current active color unless the effect specifically requires or allows a color change.

---

# 47. Banked Action Cards

A banked Action card is treated only as monetary value.

Example:

```text
Deal Breaker
Bank Value = 5M
```

Once banked:

```text
Bank = +5M
```

It cannot subsequently be played as Deal Breaker.

---

# 48. Discarding

Action cards played for their effects are discarded immediately after resolution.

Discarded cards are face-up.

When the Draw Pile is exhausted:

> The Discard Pile is shuffled and becomes the new Draw Pile.

---

# 49. End of Game

After every relevant game action, check whether a player has achieved the winning condition.

If a player satisfies the required Property Set condition:

> The game immediately ends.

That player is the winner.

---

# 50. Protection Rules

There is no general protection for:

- Complete Property Sets
- Wild Properties
- Properties within complete Sets

Any Action that explicitly allows those cards to be targeted may affect them.

---

# 51. Card Limit Rule

A player may not increase their Hand beyond 7 through a normal draw effect.

If the player already has 7 or more cards:

> Additional draw effects that only add cards to the Hand have no effect.

This does not prevent a player from receiving cards through gameplay mechanisms where a transfer is explicitly required.

---

# 52. Three-Card Turn Limit

The standard turn allows:

**3 card plays maximum.**

The following consume one play:

- Money
- Property
- Wild Property
- Action
- Shack

Effects generated by an already-played card do not automatically grant additional normal card plays unless the card explicitly grants another turn.

---

# 53. Additional Turns

An additional turn is a completely new turn.

Example:

```text
Turn 1
→ Draw
→ Up to 3 card plays
→ Go Again

Turn 2
→ Draw normally
→ Up to 3 card plays
```

---

# 54. Rule Priority

When resolving an interaction, use this priority:

1. Explicit card effect
2. Specific rule governing that card
3. General game rule
4. Default game behavior

A specific card effect overrides a general rule where the card explicitly says so.

---

# 55. Frozen Rules Checklist

The following are frozen for implementation:

- Previous game winner starts a rematch.
- New games use a random starting player.
- Alphabetical order may be used for deterministic testing.
- The Draw Pile is rebuilt from the shuffled Discard Pile when exhausted.
- The cycle repeats whenever the Draw Pile is exhausted.
- Maximum Hand size is 7.
- Any-Color Wild cannot form a complete Set by itself.
- Any-Color Wild cannot be banked.
- Any-Color Wild cannot be used as payment.
- Any-Color Wild remains a Property card.
- Two-Color Wild can switch between its two printed colors.
- Switching a Wild's active color does not consume a card play.
- Complete Sets are not protected.
- Wild Properties are not inherently protected.
- Shack contributes additional rent.
- Shack bonus is added before Double Rent.
- Maximum one Shack per Property Set.
- Shack transfers with its attached Property.
- Normal turn limit is 3 card plays.
- Go Again must be the final play of the current turn.
- Go Again creates a new complete turn.
- A player can give a maximum of 3 Debt Chips.
- If all 3 Debt Chips have been given, another cannot be created.
- Nothing happens when the Debt Chip limit has already been reached.
- Action cards received through Debt must immediately be played or banked.
- Money received through Debt goes directly into the Bank.
- Properties received through Debt go directly into the Property Collection.
- Any-Color Wild received through Debt goes into the Property Collection.
- Action cards played through Debt resolve immediately.
- Action cards played through Debt count as card plays.
- Played Action cards are discarded after resolution.
- Discarded cards are recycled when the Draw Pile is exhausted.
- Just Say No can counter applicable Actions.
- Just Say No can itself be countered by another Just Say No.
- Just Say No only protects its user.
- Just Say No cannot cancel ordinary inability-to-pay Debt.
- Complete Sets can be broken by applicable Action cards.
- Properties carrying Shacks transfer with their Shacks.
- Any-Color Wild is included in applicable Property-targeting effects.
- A card played during a turn counts toward the three-card limit.
- Draw effects cannot increase a Hand beyond 7.
- Banked Action cards are treated only as money.
- Banked Action cards cannot later be played as Actions.

---

# 56. Rules Freeze

This document is the canonical **Game Rules v1.0** specification.

The implementation must follow this document unless a later version explicitly changes a rule.

Card-specific behavior, card quantities, Bank Values, Property values, Rent values, and exact Action definitions are maintained separately in:

```text
docs/cards/CARD_DATABASE.md
```

The Card Database must not silently change a general rule defined here.

If a card requires a rule exception, the exception must be explicitly documented in the Card Database.
