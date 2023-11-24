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

### 1. Define the `Player` entity

First, decide which prefab should be your `Player` entity. Add an `RG Entity` component to this prefab, and give it
a type of `Player`.

Next, implement the action that will handle movement. It should be placed within a component that is on your Player
prefab, and should have the following method signature:

```csharp
[RGAction("MoveInDirection")]
public void MoveInput(Vector2 newMoveDirection)
{
    // Use the newMoveDirection to move the player in the desired direction
}
```

Then implement the action that will allow attacking the player. It should be placed within a component that is on your Player
prefab, and should have the following method signature:

```csharp
[RGAction("SelectAndAttackEnemy")]
public void SelectAndAttackEnemy(int enemyId, int ability)
{
    // Activate the attack ability on the given enemy.
    // You can find the enemy and once of its components with the following code:
    var enemy = RGFindUtils.Instance.FindOneByInstanceId<...>(enemyId);
    ...
}
```

Finally, implement the state that will indicate if the player is attacking. It should be placed within a component that is on your Player
prefab, and should be attached to either a boolean variable or a method that returns a boolean:

```csharp

[RGState]
public bool IsAttacking;

// Or....

[RGState]
public bool IsAttacking()
{
    // Return true if the player is currently attacking, false otherwise.
}
```

### 2. Define the `Enemy` entity

Next, decide which prefabs should by your `Enemy` entity. Add an `RG Entity` component to this prefab, and give it
a type of `Enemy`.

### 3. Generate components and attach to the prefab

Finally, in the **Regression Games** menu, click **Generate Scripts**. This will create components for the above actions.
Open your `Player` prefab, and attach the following components by searching for them in the add component dialog:

* `RG State_Player STATE_COMPONENT_NAME` where `STATE_COMPONENT_NAME` is the name of the component that contains the `IsAttacking` state.
* `RG Action_Select And Attack Enemy`
* `RG Action_Move In Direction`

## Recommended Extensions and Modifications

The bounding box of where the bot can move is set to a fixed size and location for our demo game. Please update
this if you plan on using this in other games!

## Known Limitations

Since the bot is navigating via a direction, rather than a requested location, it does no path-finding, and simply sets
a direction to move in. This means that the bot will not avoid obstacles, and will simply move in a straight line.
Feel free to add a new action that requests a location, and use Unity's path-finding to move to that location.