# Simple Kiting Bot (Demo)

The simple kiting bot encodes logic for a bot to simply move to in a random direction within a bounding box and activate an attack when it reaches that destination.

## Bot Summary Card

---

This bot will move to a random location within a bounding box, and then use an ability when it reaches that location.

### `Player` Entity

State Name | State Type | Description |
---------- | ---------- | ----------- |
`IsAttacking` | Boolean | Indicates if the bot is currently attacking and should not be moving. |

Action Name | Parameter | Action Type | Description |
----------- | ----------- | ----------- | ----------- |
`MoveInDirection` | `newMoveDirection` | Vector2 | A Vector2 value that indicates the (x, z) direction the bot should move in. |
`SelectAndAttackEnemy` | `enemyId` | int | The id of the enemy to attack |
`SelectAndAttackEnemy` | `ability` | int | The particular ability to use in the attack |

### `Enemy` Entity

_No additional states or actions required, the built-in RGEntity component contains all required states._

### Recommended Configuration

Tick Rate: 5

### Bot Type

Agent Builder / Behavior Tree

---

## How the Bot Works

The bot works by choosing a random location within a bounding box, and then requests that the character move in the direction towards that location. Once the character reaches that location, it will activate an attack. Once the attack is complete, the bot will choose a new random location and repeat the process.

## How to Integrate the Bot (Entities, States, Actions)

This bot requires two entities to be defined, a `Player` entity and an `Enemy` entity.

The full instructions for integration can be found [within our documentation.](https://docs.regression.gg/tutorials/building-your-first-bot)

## Recommended Extensions and Modifications

The bounding box of where the bot can move is set to a fixed size and location for our demo game. Please update
this if you plan on using this in other games!

## Known Limitations

Since the bot is navigating via a direction, rather than a requested location, it does no path-finding, and simply sets
a direction to move in. This means that the bot will not avoid obstacles, and will simply move in a straight line.
Feel free to add a new action that requests a location, and use Unity's path-finding to move to that location.