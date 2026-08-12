# Monopoly Deal: No Mercy — Game Rules Specification

**Ruleset Version:** 1.0
**Status:** Verified
**Game:** Monopoly Deal: No Mercy
**Players:** 2–5
**Primary Objective:** Be the first player to collect 3 complete Property Sets of different colors.

---

# 1. Purpose

This document is the canonical rules specification for the digital implementation of Monopoly Deal: No Mercy.

The game engine must use this document as its source of truth.

The digital implementation must not allow the user interface to independently determine whether an action is legal. All game actions must be validated by the game engine.

---

# 2. Components

The game contains:

* 120 cards
* 15 Debt Chips
* 5 Reference Cards

The 120 cards consist of:

| Card Type               | Quantity |
| ----------------------- | -------: |
| Money                   |       18 |
| Standard Property       |       28 |
| Rent                    |        5 |
| Double Rent             |        5 |
| Rent Any Color          |        3 |
| Double Rent Any Color   |        3 |
| Two-Color Wild Property |        9 |
| Any-Color Wild Property |        2 |
| Deal Breaker            |        3 |
| Forced Debt             |        3 |
| Go Again                |        3 |
| Heist                   |        3 |
| Just Say No             |        5 |
| Market Crash            |        3 |
| Pass Go, Go Go!         |        4 |
| Repossession            |        2 |
| Shack                   |        3 |
| Super Sly Deal          |        3 |
| Tax Collector           |        2 |
| Tough Luck              |        3 |
| Unfair Trade            |        2 |
| Yoink!                  |        3 |
| Reference Cards         |        5 |

The 120 game cards exclude the 5 Reference Cards.

There are 15 Debt Chips:

* 3 chips for each of the 5 player colors.

---

# 3. Objective

The objective is to collect:

> **3 complete Property Sets of 3 different colors.**

The moment a player has 3 complete sets of different colors, that player wins.

The game ends immediately.

---

# 4. Players

The game supports:

* Minimum: 2 players
* Maximum: 5 players

Each player has:

```text
Hand
Bank
Property Collection
Debt Chips currently held by opponents
Player Color
```

A player's Hand is private.

A player's Bank and Property Collection are public.

---

# 5. Setup

## 5.1 Player Color

Each player chooses an available player color.

Each player receives the 3 Debt Chips matching their chosen color.

Each player receives one Reference Card.

Unused Reference Cards are removed from the game.

---

## 5.2 Shuffle and Deal

1. Shuffle all game cards.
2. Deal 5 cards to each player.
3. Players may look at their own cards.
4. Players must keep their Hands hidden from opponents.
5. Place the remaining cards face down to form the Draw Pile.
6. Place the Discard Pile beside the Draw Pile.

---

# 6. Starting Player

If this is a continuation of an existing game sequence:

> The player who won the previous game starts.

If this is the first game and there is no previous winner:

> The starting player is selected randomly.

For the digital implementation, an alphabetical ordering of player names may be used as a deterministic fallback where a random selection is not desired.

After the starting player, play proceeds clockwise.

---

# 7. Turn Structure

At the beginning of a player's turn:

1. Resolve all outstanding Debt Chips.
2. Draw cards.
3. Play up to 3 cards.
4. Resolve all applicable actions and responses.
5. Check the winning condition.
6. If the player has more than 7 cards in their Hand, discard down to 7.
7. End the turn.
8. Play passes clockwise.

---

# 8. Drawing Cards

Normally, a player draws:

> **2 cards at the beginning of their turn.**

If a player has **zero cards in their Hand at the beginning of their turn**, they draw:

> **5 cards instead of 2.**

Cards are added to the player's Hand.

---

# 9. Draw Pile Exhaustion

When the Draw Pile becomes empty:

1. Take the entire Discard Pile.
2. Shuffle it.
3. Make the shuffled cards the new Draw Pile.
4. Continue drawing.

This cycle repeats for the entire game.

If cards need to be drawn and the Discard Pile is also empty, there are no cards available to draw.

---

# 10. Three-Card Play Limit

During their turn, a player may play up to:

> **3 cards.**

A player may choose to play fewer than 3 cards.

A player may also play zero cards.

The 3-card limit applies to cards played by the active player for themselves.

Cards played as responses outside the active player's turn follow the response rules.

---

# 11. Ways to Play a Card

A card can generally be used in one of three ways:

### 11.1 Bank

Place the card into the player's Bank.

### 11.2 Property

Place the card into the player's Property Collection.

### 11.3 Action

Play the card for its printed Action effect.

After an Action card is played for its effect, it is placed face up in the Discard Pile after the action resolves.

---

# 12. Banking Cards

Money cards are placed into the player's Bank.

Action cards may also be placed into the Bank instead of being played for their Action.

Once an Action card has been placed into a Bank:

> It can no longer be played for its Action effect.

Banked Action cards permanently function as money.

All Bank cards are public information.

---

# 13. Bank Value

Every bankable card has a monetary value printed on it.

When a card is placed into a Bank, its printed Bank Value determines how much it is worth for payments.

Examples:

```text
5M Deal Breaker in Bank = 5M
3M Heist in Bank = 3M
2M Go Again in Bank = 2M
```

The card's original Action is irrelevant once it has been banked.

---

# 14. Pure Money Cards

There are 18 pure Money cards:

| Card | Quantity | Value |
| ---- | -------: | ----: |
| 2M   |        5 |    2M |
| 3M   |        5 |    3M |
| 4M   |        5 |    4M |
| 10M  |        3 |   10M |

Total pure Money-card value:

> **55M**

---

# 15. Property Cards

Property cards are placed in a player's Property Collection.

Properties are grouped by color.

Each Property card has:

* Property name
* Property color
* Bank/payment value
* Rent table
* Number of cards required to complete the set

There is no limit to the number of Property cards a player may have.

---

# 16. Standard Property Sets

There are 10 standard Property colors/groups.

| Set         | Properties                                                        | Cards Required |
| ----------- | ----------------------------------------------------------------- | -------------: |
| Brown       | Mediterranean Avenue, Baltic Avenue                               |              2 |
| Light Blue  | Oriental Avenue, Vermont Avenue, Connecticut Avenue               |              3 |
| Pink/Purple | St. Charles Place, States Avenue, Virginia Avenue                 |              3 |
| Orange      | St. James Place, Tennessee Avenue, New York Avenue                |              3 |
| Red         | Kentucky Avenue, Indiana Avenue, Illinois Avenue                  |              3 |
| Yellow      | Atlantic Avenue, Ventnor Avenue, Marvin Gardens                   |              3 |
| Green       | Pacific Avenue, North Carolina Avenue, Pennsylvania Avenue        |              3 |
| Dark Blue   | Park Place, Boardwalk                                             |              2 |
| Railroad    | Reading Railroad, Pennsylvania Railroad, B&O Railroad, Short Line |              4 |
| Utility     | Electric Company, Water Works                                     |              2 |

---

# 17. Property Bank Values and Rent

| Property Set | Bank Value / Card | 1 Card | 2 Cards | 3 Cards | 4 Cards | Complete |
| ------------ | ----------------: | -----: | ------: | ------: | ------: | -------: |
| Brown        |                1M |     1M |      2M |       — |       — |        2 |
| Light Blue   |                1M |     1M |      2M |      3M |       — |        3 |
| Pink/Purple  |                2M |     1M |      2M |      4M |       — |        3 |
| Orange       |                2M |     1M |      3M |      5M |       — |        3 |
| Red          |                3M |     2M |      3M |      6M |       — |        3 |
| Yellow       |                3M |     2M |      4M |      6M |       — |        3 |
| Green        |                4M |     2M |      4M |      7M |       — |        3 |
| Dark Blue    |                4M |     3M |      8M |       — |       — |        2 |
| Railroad     |                2M |     1M |      2M |      3M |      4M |        4 |
| Utility      |                2M |     1M |      2M |       — |       — |        2 |

---

# 18. Complete Property Set

A Property Set is complete when the player has the required number of Properties for that color.

The required number is:

* Brown: 2
* Dark Blue: 2
* Light Blue: 3
* Pink/Purple: 3
* Orange: 3
* Red: 3
* Yellow: 3
* Green: 3
* Railroad: 4
* Utility: 2

Wild Properties may contribute toward completing a set according to the Wild rules.

---

# 19. Wild Property Cards

There are 11 Wild Property cards.

## 19.1 Two-Color Wilds

There are 9:

| Wild                  | Quantity | Bank Value |
| --------------------- | -------: | ---------: |
| Light Blue / Brown    |        1 |         1M |
| Light Blue / Railroad |        1 |         4M |
| Pink / Orange         |        2 |         2M |
| Red / Yellow          |        2 |         3M |
| Dark Blue / Green     |        1 |         4M |
| Railroad / Green      |        1 |         4M |
| Utility / Railroad    |        1 |         2M |

---

# 20. Two-Color Wild Rules

A Two-Color Wild can represent either of its two printed colors.

The player chooses its current color.

The card may be rotated/represented so that the selected color is the active color.

A Two-Color Wild:

* Can complete a Property Set.
* Can be used as payment.
* Has its own Bank Value.
* Can be stolen.
* Can be transferred.
* Can change between its two available colors during its owner's turn.
* Does not consume one of the owner's 3 card plays when changing color.

Its rent contribution is determined by the Property Set color it currently represents.

---

# 21. Any-Color Wild Properties

There are 2 Any-Color/Multi-Color Wild Property cards.

Bank Value:

> **0M**

They cannot be placed into a Bank.

They cannot be used as payment.

They can represent any Property color.

They cannot form a complete Property Set by themselves.

They must be combined with at least one qualifying Property of the selected color.

---

# 22. Any-Color Wild as a Property

An Any-Color Wild is still a Property card.

It can:

* Be placed in a Property Collection.
* Contribute to rent.
* Be transferred.
* Be stolen.
* Be affected by Property Actions.

It cannot:

* Be banked.
* Be used to pay debt.
* Be used as the only card in a complete Property Set.

---

# 23. Wild Color Changes

Changing the active color of a Wild:

* Can occur during the owner's turn.
* Does not count as a card play.
* Changes the Property Set to which the Wild contributes.
* Can change rent.
* Can change whether a Property Set is complete.
* Can change whether the player has won.

---

# 24. Rent

Rent Actions charge opponents according to the Property color selected on the Rent card.

The player:

1. Selects an allowed color.
2. Counts the Properties currently representing that color.
3. Determines the corresponding rent from the Property rent table.
4. Applies any Shack bonus.
5. Applies any applicable rent multiplier.
6. Each affected opponent owes the resulting amount.

---

# 25. Rent Against Multiple Players

When a Rent Action affects all other players:

> Every affected opponent separately owes the calculated rent.

Example:

```text
Rent = 4M

Player A → owes 4M
Player B → owes 4M
Player C → owes 4M
```

Each player resolves their own payment independently.

A player may use Just Say No against their own portion of an applicable Action.

---

# 26. Rent Any Color

Rent Any Color allows the player to choose the Property color for which rent is charged.

The player calculates rent using the Properties currently representing that color.

---

# 27. Double Rent

Double Rent calculates the normal rent first.

If a Shack is attached:

```text
Normal Property Rent
+
Shack Bonus
=
Adjusted Rent
```

Then:

```text
Adjusted Rent × 2
=
Final Rent
```

The Shack bonus is therefore included **before** the doubling.

---

# 28. Double Rent Any Color

Double Rent Any Color combines:

1. Choosing the applicable Property color.
2. Calculating rent.
3. Adding any Shack bonus.
4. Doubling the resulting amount.

---

# 29. Paying Another Player

A player may pay another player using:

* Cards in their Bank.
* Property cards in their Property Collection.
* Any combination of the two.

Cards still in the player's Hand cannot be voluntarily used for normal payment.

---

# 30. Bank Payment

When paying with Bank cards:

* The debtor selects cards from their Bank.
* The creditor receives those cards.
* The cards are placed into the creditor's Bank.
* A banked Action card remains banked.
* A banked Action card cannot be activated after being transferred.

---

# 31. Property Payment

When paying with Property cards:

* The debtor selects Property cards from their collection.
* The creditor receives those Property cards.
* The Properties are added to the creditor's Property Collection.
* Any attached Shack transfers with the Property according to the Shack rules.

---

# 32. No Change

There is no change.

A player must pay:

> The exact amount owed or more.

If a player owes 2M but their only available card is worth 5M:

> They must give the 5M card.

---

# 33. Insufficient Payment

If a player cannot fully pay an amount owed:

1. The player gives the creditor all eligible Bank cards and Properties available for payment.
2. The player gives the creditor one Debt Chip.
3. The unresolved debt is represented by that Debt Chip.
4. The debtor resolves the Debt Chip on their next turn.

A player cannot voluntarily choose Debt instead of using available Bank/Property assets.

---

# 34. Debt Chip Limit

Each player starts with 3 Debt Chips.

A Debt Chip represents one outstanding debt to its holder.

If a player has already given away all 3 of their Debt Chips:

> They cannot give another Debt Chip.

No additional Debt Chip is created.

No additional effect occurs.

The creditor simply does not receive another Debt Chip for that payment.

Existing Debt Chips remain valid.

---

# 35. Multiple Debt Chips

A player can owe:

* Multiple players.
* Multiple Debt Chips to the same player.

Example:

```text
Player A
├── Debt Chip → Player B
├── Debt Chip → Player C
└── Debt Chip → Player C
```

Each Debt Chip must be resolved separately.

---

# 36. Resolving Debt

At the beginning of a player's next turn:

1. The player draws their normal cards.
2. Before playing cards for themselves, they resolve every outstanding Debt Chip they have given away.
3. The player chooses the order in which debts are resolved.
4. For each Debt Chip, the debtor gives one card from their Hand to the player holding that Debt Chip.
5. The value of the card does not matter.
6. The recipient immediately processes the card.
7. The Debt Chip is returned to the debtor.

---

# 37. Card Given for Debt

The debtor may choose any card from their Hand.

The value of the card does not matter.

The card cannot remain in the recipient's Hand.

The recipient immediately chooses how to process it.

### Money Card

Placed into the recipient's Bank.

### Property Card

Placed into the recipient's Property Collection.

### Two-Color Wild

Placed into the recipient's Property Collection.

### Any-Color Wild

Placed into the recipient's Property Collection.

### Action Card

The recipient chooses:

* Bank it, or
* Immediately play its Action.

---

# 38. Action Card Received Through Debt

If the recipient chooses to play an Action card received through Debt:

> The Action is immediately played and resolved normally.

It follows all normal Action rules.

It may create:

* Targets
* Responses
* Just Say No chains
* Property transfers
* Payments
* Other effects

The debtor does not receive control of the Action merely because they originally owned the card.

The recipient controls the Action.

---

# 39. Debt Card Play Accounting

Each card given by the debtor to resolve one of their Debt Chips counts as:

> **One of the debtor's three card plays for that turn.**

If a player has multiple Debt Chips, each card given to resolve a Debt Chip consumes one applicable card play.

The recipient's immediate processing of the received card is governed by the recipient's own Action/play rules.

---

# 40. Just Say No

Just Say No is a response Action.

It can be played when an Action card affects the player.

It can be played outside the player's normal turn.

When successfully resolved:

> The Action no longer affects the player who used Just Say No.

---

# 41. Just Say No and Multiple Players

If an Action affects multiple players:

```text
Original Action
├── Player A
├── Player B
└── Player C
```

If Player B plays Just Say No:

```text
Player A → affected
Player B → protected
Player C → affected
```

Just Say No protects only the player who played it.

Other affected players remain affected unless they also respond with their own Just Say No.

---

# 42. Just Say No Chains

A Just Say No can itself be countered by another Just Say No.

Example:

```text
Original Action
      ↓
Just Say No
      ↓
Just Say No
      ↓
Just Say No
```

The chain continues until no further Just Say No is played.

The player who plays the final Just Say No determines whether the original Action ultimately takes effect.

---

# 43. Just Say No on the Active Player's Turn

If a player plays Just Say No during their own turn:

> It counts as one of their three card plays.

---

# 44. Just Say No and Debt

Just Say No cannot be used to avoid ordinary debt caused by insufficient payment.

Example:

```text
Player owes 10M
Player has only 6M eligible assets
```

They cannot play Just Say No to avoid the resulting Debt.

However:

> Just Say No may be used against an applicable Forced Debt Action.

---

# 45. Deal Breaker

Deal Breaker targets another player who has a complete Property Set.

The player playing Deal Breaker:

1. Selects an opponent.
2. Selects one complete Property Set belonging to that opponent.
3. Takes the entire Property Set.
4. Takes any Shack attached to the Set.
5. Adds the stolen Set to their own Property Collection.

The stolen complete Set is no longer owned by the original player.

---

# 46. Forced Debt

Forced Debt targets another player.

The player playing Forced Debt takes one of the target player's Debt Chips.

The targeted player now owes the player who played Forced Debt.

On their next turn, the targeted player must give one card from their Hand to the Debt Chip holder.

The normal Debt resolution rules apply.

Just Say No may be used against Forced Debt.

---

# 47. Go Again

Go Again grants the active player another complete turn.

Go Again must be played:

> **As the final card played during the current turn.**

After the current turn ends:

> The player immediately starts a new turn.

The new turn is a separate turn and receives its own normal draw and play allowance.

Go Again does not simply add additional plays to the current turn.

---

# 48. Heist

Heist targets every opponent.

For each opponent:

1. Look at their Bank.
2. Choose exactly one card from that Bank.
3. Take that card.
4. Add it to your own Bank.

If an opponent has no Bank cards:

> Nothing is taken from that opponent.

No Debt Chip is created because of an empty Bank.

The stolen card becomes part of the attacker's Bank.

---

# 49. Market Crash

Market Crash targets the Property Collections of opponents.

For each opponent:

1. Select exactly one Property from that opponent's Property Collection.
2. Transfer the selected Property to the player who played Market Crash.
3. Add it to the attacker's Property Collection.

The selected Property may be:

* A standard Property.
* A Two-Color Wild.
* An Any-Color Wild.
* Part of a complete Set.
* A Property with an attached Shack.

Complete Sets do not provide protection.

A Shack attached to a transferred Property transfers with that Property.

---

# 50. Pass Go, Go Go!

Pass Go, Go Go! allows the player to draw cards until their Hand contains 7 cards.

If the player currently has fewer than 7 cards:

> Draw until Hand size = 7.

If the player already has 7 or more cards:

> Pass Go, Go Go! has no effect.

The card is still played and discarded.

The normal Draw Pile recycling rule applies while drawing.

---

# 51. Repossession

Repossession targets another player.

The targeted player:

1. Chooses exactly one Property to keep.
2. Gives every other Property in their collection to other players.
3. Chooses which player receives each Property.

Complete Sets are not protected.

Wild Properties are not protected.

The targeted player may choose to keep:

* A standard Property.
* A Two-Color Wild.
* An Any-Color Wild.

If a Property being transferred has an attached Shack:

> The Shack must transfer with that Property.

The targeted player may distribute different Properties to different players.

---

# 52. Shack

Shack is a Building card.

A Shack may be played onto a Property in the player's Property Collection.

The Property:

* Does not need to be part of a complete Set.
* May already be part of a complete Set.

A Shack increases the rent generated by the Property Set by:

> **5M**

---

# 53. Shack Limit

There may be:

> **A maximum of one Shack per Property Set.**

A Shack cannot be added if that Property Set already has a Shack.

The Shack remains associated with that Property Set.

---

# 54. Shack Movement

Once a Shack is placed:

> It cannot voluntarily be moved to another Property or Property Set.

If the Property carrying the Shack changes ownership:

> The Shack transfers with the Property.

If a Property is transferred as part of a Repossession:

> The Shack transfers with that Property.

---

# 55. Shack in a Bank

A Shack may be placed in a Bank instead of being played as a Building.

Its Bank Value is:

> **1M**

Once banked, it behaves as a Bank card.

If a banked Shack is transferred as payment:

> It remains a Bank card for the recipient.

It cannot be converted into an active Shack after being banked.

---

# 56. Super Sly Deal

Super Sly Deal targets a Property color.

The player chooses one Property color that at least one opponent currently has.

The player then takes:

> **Every Property of that color from every opponent.**

This includes Properties belonging to complete Sets.

It does not affect cards in players' Hands.

---

# 57. Super Sly Deal and Wilds

Super Sly Deal applies to Wild Properties.

### Two-Color Wild

If the chosen color appears on the Wild:

> The Wild is taken, regardless of whether that color is currently active.

Example:

```text
Wild = Green / Dark Blue
Active Color = Green

Chosen Super Sly Deal color = Dark Blue

→ Wild is still taken.
```

### Any-Color Wild

An Any-Color Wild matches every color.

Therefore:

> An Any-Color Wild is taken regardless of which color is chosen.

---

# 58. Tax Collector

Tax Collector targets another player.

The targeted player must:

> Give all but one card from their Bank to other players.

The targeted player chooses:

* Which one Bank card to keep.
* Which player receives each remaining Bank card.

The cards are transferred directly between Banks.

---

# 59. Tough Luck

Tough Luck targets another player.

The attacker chooses one category:

* Property
* Action
* Money

The attacker then takes:

> Every card of that category currently in the target's Hand.

The cards are transferred directly to the attacker's Hand.

Tough Luck does not affect:

* Bank cards.
* Properties already on the table.

The card category is determined by the card's type, not by where the card is currently located.

---

# 60. Unfair Trade

Unfair Trade targets another player.

The two players exchange:

> **All cards in their Banks.**

The entire Bank of Player A becomes the Bank of Player B.

The entire Bank of Player B becomes the Bank of Player A.

Properties and Hands are not exchanged.

A player cannot play Unfair Trade if:

> Their own Bank is empty.

---

# 61. Yoink!

Yoink! targets one opponent.

The targeted player owes:

> **10M**

The payment follows the normal payment rules.

The debtor may pay using:

* Bank cards.
* Properties.
* A combination of both.

If the debtor cannot fully pay:

* Eligible assets are transferred.
* One Debt Chip is given if the debtor still has an available Debt Chip.
* If all 3 Debt Chips have already been given away, no additional Debt Chip is created.

---

# 62. Action Card Bank Values

All Action cards except Any-Color/Multi-Color Wild Properties can be banked.

| Action                | Bank Value |
| --------------------- | ---------: |
| Pass Go, Go Go!       |         1M |
| Rent                  |         1M |
| Shack                 |         1M |
| Go Again              |         2M |
| Just Say No           |         2M |
| Super Sly Deal        |         2M |
| Rent Any Color        |         2M |
| Tax Collector         |         2M |
| Double Rent           |         3M |
| Double Rent Any Color |         3M |
| Forced Debt           |         3M |
| Heist                 |         3M |
| Market Crash          |         3M |
| Yoink!                |         3M |
| Repossession          |         4M |
| Tough Luck            |         4M |
| Unfair Trade          |         4M |
| Deal Breaker          |         5M |

---

# 63. Card Discarding

When an Action card is played for its Action:

1. Resolve the Action.
2. Resolve any applicable response chain.
3. Place the Action card into the Discard Pile.

A Just Say No used in response is also discarded after its resolution.

---

# 64. Action Resolution

An Action must be validated before its effects are applied.

The conceptual resolution process is:

```text
Play Action
     ↓
Validate Action
     ↓
Identify Targets
     ↓
Create Pending Action
     ↓
Allow Responses
     ↓
Resolve Response Chain
     ↓
Apply Action
     ↓
Discard Action
     ↓
Check Winning Condition
```

---

# 65. Pending Actions

Actions that permit responses must be represented as a pending game state.

A pending Action contains, conceptually:

```text
Action Card
Source Player
Target Player(s)
Current Responder
Response Chain
Resolution Status
```

This is particularly important for:

* Just Say No
* Just Say No chains
* Actions affecting multiple players

---

# 66. Action Effects and Multiple Targets

When an Action affects multiple opponents, each affected opponent is evaluated separately where applicable.

For example:

```text
Rent
├── Player B → payment/resolution
├── Player C → payment/resolution
└── Player D → payment/resolution
```

One player's response does not automatically protect another player.

---

# 67. Winning Condition

After a game-state-changing effect, the engine checks whether any player has:

> 3 complete Property Sets of 3 different colors.

If yes:

> That player immediately wins.

---

# 68. Winning During an Action

A player may win because of:

* Playing a Property.
* Changing a Wild's color.
* Receiving a Property through payment.
* Receiving a Property through an Action.
* Stealing a Property.
* Stealing a complete Set.
* Receiving Properties through Repossession.
* Any other legal Property transfer.

The winning condition must be checked after each state-changing effect.

---

# 69. Winning During Go Again

Go Again creates a new turn.

The game engine must check the winning condition before starting another turn.

If the player has already won:

> No additional turn is created.

---

# 70. Hand Limit

At the end of every turn:

```text
If Hand Size > 7:
    Player chooses cards to discard
    until Hand Size = 7
```

The player chooses which cards to discard.

Discarded cards enter the Discard Pile.

---

# 71. Hand Size During the Turn

There is no general maximum Hand size during the player's turn.

A player may temporarily have more than 7 cards.

The 7-card limit is enforced at the end of the turn.

Pass Go, Go Go! specifically draws only until the player reaches 7.

---

# 72. Zero-Card Hand

If a player has zero cards in their Hand at the beginning of their turn:

> Draw 5 cards instead of 2.

Debt resolution then occurs before the player plays cards for themselves.

---

# 73. Property Ownership

Every Property belongs to exactly one player's Property Collection.

A Property cannot simultaneously belong to multiple players.

When a Property changes ownership:

```text
Old Owner
    ↓
Property Transfer
    ↓
New Owner
```

Any applicable attached Shack transfers with the Property.

---

# 74. Bank Ownership

Every Bank card belongs to exactly one player's Bank.

When a Bank card is transferred:

> It moves directly from one Bank to another Bank.

A banked Action card remains a banked Action card.

---

# 75. Hand Ownership

Every card in a player's Hand belongs exclusively to that player.

When an Action such as Tough Luck transfers Hand cards:

> The cards move directly from the target's Hand to the attacker's Hand.

The recipient does not immediately play the cards unless another rule explicitly requires immediate processing.

---

# 76. Card Location Invariant

Every card in the game must exist in exactly one location:

```text
Draw Pile
OR
Discard Pile
OR
Player Hand
OR
Player Bank
OR
Player Property Collection
OR
Temporary/Pending Action State
```

A card must never exist in two locations simultaneously.

---

# 77. Debt Chip Ownership

Each Debt Chip represents a debt from:

```text
Debtor → Creditor
```

A Debt Chip is held by the creditor.

When the debtor pays the Debt Chip:

```text
Debtor gives card
      ↓
Creditor processes card
      ↓
Debt Chip returns to debtor
```

---

# 78. Debt Chip Exhaustion

Each player begins with exactly 3 Debt Chips.

If all 3 have already been transferred:

> The player cannot transfer another Debt Chip.

The unresolved payment does not create another Debt Chip.

No additional penalty or alternative debt marker is created.

---

# 79. Property Transfers and Attached Shacks

Whenever a Property carrying a Shack is transferred:

> The Shack transfers with the Property.

This applies to:

* Payment.
* Deal Breaker.
* Market Crash.
* Super Sly Deal.
* Repossession.
* Other legal Property transfers.

---

# 80. Wild Transfers

Wild Properties are ordinary Property cards for transfer purposes.

They can be:

* Paid as Properties if eligible.
* Stolen.
* Repossessed.
* Transferred.
* Used in Property Sets.

An Any-Color Wild cannot be used as payment because it has no payment value.

---

# 81. Wild and Rent

A Wild contributes to the rent of whichever color it currently represents.

Two-Color Wild:

```text
Current Color
      ↓
Count with that color
      ↓
Use that color's Rent Table
```

Any-Color Wild:

```text
Chosen Color
      ↓
Count with that color
      ↓
Use that color's Rent Table
```

---

# 82. Wild and Complete Sets

Two-Color Wilds can complete Property Sets.

Any-Color Wilds cannot create a complete Property Set by themselves.

A complete set involving an Any-Color Wild must contain at least one other qualifying Property.

---

# 83. Complete Sets Are Not Generally Protected

Complete Sets may be affected by applicable Actions.

Examples include:

* Deal Breaker
* Market Crash
* Repossession
* Super Sly Deal
* Other legal Property transfers

A complete Property Set does not become permanently protected merely because it is complete.

---

# 84. Property Set Changes

A Property Set can change state during the game.

For example:

```text
Complete
   ↓
Property Stolen
   ↓
Incomplete
```

or:

```text
Incomplete
   ↓
Wild Changes Color
   ↓
Complete
```

The engine must recalculate Set status after relevant Property changes.

---

# 85. Rent Calculation

Rent is determined from the number of Properties currently representing the selected color.

Conceptually:

```text
Selected Color
      ↓
Count Properties
      ↓
Look up Base Rent
      ↓
Add Shack Bonus
      ↓
Apply Double Rent if applicable
      ↓
Final Amount Owed
```

---

# 86. No Change Rule

When paying a debt:

```text
Amount Owed = X
Payment = Y

Y must be >= X
```

If the smallest available payment exceeds the amount owed:

> The entire card/asset is transferred.

The creditor does not return excess value.

---

# 87. Action Cards and Banking

The same physical Action card can have two possible uses before it is played:

```text
ACTION CARD
├── Play for Action
└── Bank for Monetary Value
```

After it has been banked:

```text
BANKED ACTION
└── Monetary Value Only
```

The Action cannot be recovered as an Action later.

---

# 88. Card Play vs Automatic Effects

The engine must distinguish:

```text
Card Played
Response Played
Automatic Effect
Property Color Change
Debt Resolution
Turn Transition
```

Not every state change is itself a card play.

For example:

> Changing the color of a Wild does not consume a card play.

---

# 89. Turn End

A turn ends when:

* The player has played 3 applicable cards, or
* The player voluntarily stops playing cards.

After the turn ends:

1. Enforce the 7-card Hand limit.
2. Check the game state.
3. Move to the next player clockwise.

If Go Again was played as the final card:

> The same player receives the next turn instead.

---

# 90. Game State

The digital game state should conceptually contain:

```text
GameState
├── Game ID
├── Players
├── Draw Pile
├── Discard Pile
├── Current Player
├── Turn Number
├── Pending Action
├── Game Status
└── Winner
```

---

# 91. Player State

Each player should conceptually contain:

```text
PlayerState
├── Player ID
├── Name
├── Player Color
├── Hand
├── Bank
├── Properties
└── Debt Chips Held By Opponents
```

---

# 92. Server Authority

In the multiplayer implementation:

> The server/game engine is authoritative.

The client may request an action.

The server must:

1. Validate the action.
2. Validate the current game state.
3. Validate the player's authority.
4. Apply the rules.
5. Update the game state.
6. Broadcast the resulting state.

A client must never be trusted to determine whether an Action is legal.

---

# 93. Invalid Actions

If a player attempts an illegal action:

* The game state must not change.
* The attempted card must not be consumed.
* No card play should be counted.
* The player should receive an appropriate error.

Examples:

```text
Attempt to play a card outside your turn
Attempt to play more than 3 cards
Attempt to bank an Any-Color Wild
Attempt to use an Action after it was banked
Attempt to place a second Shack on the same Set
Attempt to use Just Say No against ordinary debt
Attempt Unfair Trade with an empty own Bank
```

---

# 94. State Consistency

After every legal action, the engine must maintain:

* Exactly one owner per card.
* Exactly one location per card.
* Correct Bank values.
* Correct Property ownership.
* Correct Wild color assignment.
* Correct Shack attachment.
* Correct Debt Chip ownership.
* Correct active player.
* Correct turn play count.
* Correct pending response state.

---

# 95. Core Action Resolution Model

The recommended engine flow is:

```text
Player requests action
        ↓
Validate player turn / response authority
        ↓
Validate card ownership
        ↓
Validate card availability
        ↓
Validate Action conditions
        ↓
Create pending Action
        ↓
Collect allowed responses
        ↓
Resolve Just Say No chain if applicable
        ↓
Apply Action
        ↓
Apply Property / Bank / Debt changes
        ↓
Discard Action cards
        ↓
Check winning condition
        ↓
Continue / end turn
```

---

# 96. Rules Priority

When determining the legality of an action, use this priority:

1. Specific card rule.
2. Specific No Mercy rule.
3. General game rule.
4. Current game-state restriction.
5. User-interface restriction.

The UI must never override a legal game rule.

---

# 97. Reference Implementation Principles

The following principles are mandatory for the digital implementation:

### Rule 1 — Server Authority

The server decides what happens.

### Rule 2 — No Client-Side Rule Authority

The frontend only requests actions and displays results.

### Rule 3 — Atomic State Changes

Actions should be resolved in a controlled manner so cards cannot temporarily exist in invalid states.

### Rule 4 — Explicit Pending States

Actions requiring responses must create explicit pending states.

### Rule 5 — Deterministic Resolution

Given the same starting state and same player actions, the game engine must produce the same resulting state.

### Rule 6 — Testable Rules

Every significant rule should have automated tests.

---

# 98. Complete Action Card Summary

| Card                  | Qty | Bank | Primary Effect                                        |
| --------------------- | --: | ---: | ----------------------------------------------------- |
| Rent                  |   5 |   1M | Charge rent using an allowed color                    |
| Double Rent           |   5 |   3M | Double rent                                           |
| Rent Any Color        |   3 |   2M | Choose rent color                                     |
| Double Rent Any Color |   3 |   3M | Choose color and double rent                          |
| Deal Breaker          |   3 |   5M | Steal a complete Property Set                         |
| Forced Debt           |   3 |   3M | Take one opponent Debt Chip                           |
| Go Again              |   3 |   2M | Take another turn                                     |
| Heist                 |   3 |   3M | Take one Bank card from each opponent                 |
| Just Say No           |   5 |   2M | Cancel an Action affecting you                        |
| Market Crash          |   3 |   3M | Take one Property from each opponent                  |
| Pass Go, Go Go!       |   4 |   1M | Draw until Hand reaches 7                             |
| Repossession          |   2 |   4M | Target keeps one Property; distributes rest           |
| Shack                 |   3 |   1M | Add 5M rent to a Property Set                         |
| Super Sly Deal        |   3 |   2M | Steal all Properties of a chosen color from opponents |
| Tax Collector         |   2 |   2M | Target distributes all but one Bank card              |
| Tough Luck            |   3 |   4M | Take all chosen card type from target's Hand          |
| Unfair Trade          |   2 |   4M | Exchange Banks                                        |
| Yoink!                |   3 |   3M | Target owes 10M                                       |

---

# 99. Complete Property Summary

| Set         | Cards | Complete | Bank Value | Rent          |
| ----------- | ----- | -------: | ---------: | ------------- |
| Brown       | 2     |        2 |         1M | 1 / 2         |
| Light Blue  | 3     |        3 |         1M | 1 / 2 / 3     |
| Pink/Purple | 3     |        3 |         2M | 1 / 2 / 4     |
| Orange      | 3     |        3 |         2M | 1 / 3 / 5     |
| Red         | 3     |        3 |         3M | 2 / 3 / 6     |
| Yellow      | 3     |        3 |         3M | 2 / 4 / 6     |
| Green       | 3     |        3 |         4M | 2 / 4 / 7     |
| Dark Blue   | 2     |        2 |         4M | 3 / 8         |
| Railroad    | 4     |        4 |         2M | 1 / 2 / 3 / 4 |
| Utility     | 2     |        2 |         2M | 1 / 2         |

---

# 100. Verified Ruleset Status

The following areas are considered verified for implementation:

* Game objective
* Player count
* Components
* Setup
* Starting player
* Turn order
* Drawing
* Draw-pile recycling
* Three-card play limit
* Banking
* Bank values
* Property cards
* Property sets
* Property rent
* Wild Properties
* Wild color changes
* Any-Color Wild restrictions
* Payment
* No-change rule
* Debt
* Debt Chips
* Debt Chip exhaustion
* Debt repayment
* Debt Action-card handling
* Just Say No
* Just Say No chains
* Rent
* Double Rent
* Shack
* Deal Breaker
* Forced Debt
* Go Again
* Heist
* Market Crash
* Pass Go, Go Go!
* Repossession
* Super Sly Deal
* Tax Collector
* Tough Luck
* Unfair Trade
* Yoink!
* Hand limit
* Property transfers
* Shack transfers
* Winning
* Action resolution
* Pending responses
* Game-state invariants
* Multiplayer authority model

---

# 101. Canonical Rule

If a future implementation decision appears ambiguous, the implementation must refer to this document first.

If the rules document does not explicitly cover a situation, that situation must be added to this document and assigned a rule before the corresponding game-engine behavior is finalized.

The objective is:

> **No game-state situation should require the programmer to guess what the rules mean.**

---

# 102. Version History

## v1.0

Initial verified ruleset.

Major areas finalized:

* Complete game structure
* Complete Property system
* Complete Money system
* Complete Action system
* Wild Property rules
* Shack mechanics
* Debt system
* Debt Chips
* Payment system
* Just Say No response system
* Property-transfer mechanics
* Hand limits
* Draw-pile recycling
* Winning conditions
* Digital game-state principles

**Status: VERIFIED — READY FOR IMPLEMENTATION**
