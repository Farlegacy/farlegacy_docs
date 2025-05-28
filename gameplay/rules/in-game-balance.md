---
description: Core Card Balance Principle
icon: info
---

# In-game balance

The core of the balance system is a simple formula for calculating a card’s effectiveness:

```
Effective Value = Damage + Defence + Heal + Effect Value
```

Where:

* _Damage — damage dealt by the card_
* _Defence — damage blocked by the card_
* _Heal — health restored by the card_
* _Effect Value — numerical estimate of the card’s special ability (defined based on testing and meta-analysis)_

***

## Card Cost Balance (Energy Efficiency) <a href="#card-cost-balance-mana-efficiency" id="card-cost-balance-mana-efficiency"></a>

For a card to be considered balanced, its efficiency relative to mana cost should stay within a target range:

```
Mana Efficiency = Effective Value / Mana Cost

Target range:
1.5 ≤ Mana Efficiency ≤ 2.5
```

<table><thead><tr><th width="225.3333740234375">Mana Efficiency	</th><th></th></tr></thead><tbody><tr><td>&#x3C; 1.5</td><td>Weak card (niche or situational usage)</td></tr><tr><td>1.5 - 2.5</td><td>Balanced card</td></tr><tr><td>>2.5</td><td>Strong card (limited by mechanics or conditions)</td></tr></tbody></table>

***

## Example of Card Efficiency Calculation <a href="#example-of-card-efficiency-calculation" id="example-of-card-efficiency-calculation"></a>

| Card      | Damage | Defence | Heal | Effect Value                  | Mana cost | Effective Value | Mana Efficiency |
| --------- | ------ | ------- | ---- | ----------------------------- | --------- | --------------- | --------------- |
| MFER      | 1      | 0       | 0    | 0                             | 0         | 1               | -               |
| Nouns     | 2      | 0       | 0    | 0                             | 1         | 2               | 2.0             |
| SHIELD V3 | 0      | 3       | 0    | 0                             | 2         | 3               | 1.5             |
| VITALIK   | 0      | 0       | 0    | 1 (draw a card)               | 1         | 1               | 1.0             |
| MOXIE     | 1      | 0       | 0    | 2 (double next attack damage) | 2         | 3               | 1.5             |

### Card Effect Values <a href="#card-effect-values" id="card-effect-values"></a>

Card effects are difficult to estimate purely with numbers, so the following approximate Effect Values are used for balancing:

| Effect                      | Example Card | Effect Value |
| --------------------------- | ------------ | ------------ |
| Draw 1 card                 | VITALIK      | 1            |
| Double next attack's damage | MOXIE        | 2            |
| Ignore opponent's defence   | BARMSTRONG   | 1            |
| + 1 mana for 2 turns        | PAC          | 2            |
| Reflect 1 attack            | SUPERANON    | 2            |

### Theoretical Battle Balance <a href="#theoretical-battle-balance" id="theoretical-battle-balance"></a>

Under standard game conditions:

* 5 mana per turn
* 8 turns before deck reset
* 40 HP per player

Maximum total mana per deck cycle:

```
Total Mana = Turns * Mana per Turn = 8 * 5 = 40
```

If a player uses only attacking cards with Mana Efficiency ≈ 2.0, they can deal:

```
Max Damage = Total Mana * Mana Efficiency = 40 * 2 = 80
```

Meanwhile, the opponent has:

* 40 HP
* Defensive and healing cards
* Counterplay effects

Thus:

```
Victory = Effective Value per Mana Distribution + Proper Deck Management
```

### Key Game Balance Identity[​](https://docs.farlegacy.com/Gameplay/Balance#key-game-balance-identity) <a href="#key-game-balance-identity" id="key-game-balance-identity"></a>

```
Attack Potential ≈ Defence Potential + HP + Heal Potential + Game Effects
```

<figure><img src="../../.gitbook/assets/image (18).png" alt=""><figcaption></figcaption></figure>

#### Graph explanation[​](https://docs.farlegacy.com/Gameplay/Balance#graph-explanation) <a href="#graph-explanation" id="graph-explanation"></a>

| **Line**      | **Meaning**                                 | **Comment**                                                           |
| ------------- | ------------------------------------------- | --------------------------------------------------------------------- |
| Red (dashed)  | Pure damage without defense and healing     | If the player doesn’t defend or heal, their health drops very quickly |
| Green         | Real damage considering defense and healing | It shows that defense and healing significantly slow down HP loss     |
| Blue (dashed) | Player’s base HP = 40                       | A horizontal reference line for evaluating the speed of taking damage |

This identity means that for a player playing perfectly (without mistakes), the chances of victory are determined not by the raw power of cards, but by the skillful combination and usage of them.

### Calculation Results[​](https://docs.farlegacy.com/Gameplay/Balance#calculation-results) <a href="#calculation-results" id="calculation-results"></a>

#### Used Values[​](https://docs.farlegacy.com/Gameplay/Balance#used-values) <a href="#used-values" id="used-values"></a>

| **Variable** | **Value** | **Description**                  |
| ------------ | --------- | -------------------------------- |
| HP           | 40        | Player’s starting health         |
| D\_avg       | 3.0       | Average damage per attack card   |
| DEF\_avg     | 2.0       | Average defense per defense card |
| H\_avg       | 3.0       | Average heal per heal card       |
| M\_regen     | 5         | Mana regeneration per turn       |

#### HP loss without defense and healing[​](https://docs.farlegacy.com/Gameplay/Balance#hp-loss-without-defense-and-healing) <a href="#hp-loss-without-defense-and-healing" id="hp-loss-without-defense-and-healing"></a>

```
HP_t = HP - t * D_avg
```

After 10 turns: HP = 40 - 10 \* 3 = 10

#### HP loss with defense and healing[​](https://docs.farlegacy.com/Gameplay/Balance#hp-loss-with-defense-and-healing) <a href="#hp-loss-with-defense-and-healing" id="hp-loss-with-defense-and-healing"></a>

```
HP_t = HP - max(0, t * D_avg - t * DEF_avg - t * H_avg)
```

In our case: t \* D\_avg - t \* DEF\_avg - t \* H\_avg = t \* (3 - 2.5 + 1.5) = t \* (2)

| **Metric**      | **Value**  | **What it means**                            |
| --------------- | ---------- | -------------------------------------------- |
| Average damage  | 3          | Deals strong damage                          |
| Average defense | 2          | Partially reduces damage                     |
| Average healing | 3          | Almost compensates for damage, but not fully |
| Total           | -2 HP/turn | The player loses 2 HP each turn              |
