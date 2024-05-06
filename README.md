# Advanced Computer Lab Winter 2023 Final Project: Resident Evil X Dead Space

## Project Overview
The main aim of this project is to test your skills in using Unity to create a fully functioning game as a part of a gaming studio. This project should be done in groups of minimum 8 and maximum 10 students. All teams must implement the main level. Teams consisting of 9 members must additionally implement 1 of the extra levels. Note: The entire gameplay of the game should take 5 to 10 minutes. 

## Game Overview
This project is mainly inspired by Resident Evil 2 (2019), Resident Evil 4 (2023), and Dead Space (2023), all of which are third-person shooters survival horror games. In the first two games, you play as Leon S. Kennedy, while in the latter you play as Isaac Clarke. Despite the different settings, both protagonists encounter mindless enemies that they must defeat. This could be achieved by weaponry, items, or abilities. However, combat is not the only part of the game, as the player must make strategic decisions based on the limited amount of resources available to them. For simplicity, the protagonist of the game to be implemented will be referred to as Leon in this document.
If you are unfamiliar with the games, you can check out some example gameplay by following these links:
- [Gameplay Example 1](https://youtu.be/EyYbXNsE2k4)
- [Gameplay Example 2](https://youtu.be/IYaHTRlkJVY)
- [Gameplay Example 3](https://youtu.be/qUl3wVEh2oU)

You are not required to implement all the features in these videos, only the ones specified in this document.

## Player Mechanics

### Health Points and Movement
Leon is controlled from a third person’s perspective. Initially, Leon starts with 8 health points and can never exceed that value. Leon can lose health points when being attacked based on the attack damage points (see section 4.1), as well as gain health points when using items based on the item’s restorative points (see section 3.4). Whenever Leon’s health points reach zero, he dies, and the “Game Over” screen is displayed. Leon can move using the movement buttons and can move faster by holding the sprint button while pressing the movement buttons. Sprinting should double Leon’s original movement speed.

### Primary Weapons

#### Weapons’ Description
Leon can only have one weapon equipped (active) at a time. Leon can choose a primary weapon to equip from the inventory (see section 3.2). Each weapon has unique characteristics which make it distinct from the other weapons. You are required to have all of the following primary weapons in your game. Each weapon has the following properties:

#### 2.2 Primary Weapons
##### 2.2.1 Weapons’ Description
- Firing Mode: Automatic (fires by holding)/ Single-shot(Fires on singles press)
- Damage Amount: The amount of damage each bullet deals.
- Time between Shots: The amount of time between each shot.
  - For automatic weapons, this determines the time until the next fire bullet while the fire button is being held.
  - For single-shot weapons, this determines the time during which pressing the fire button again does not shoot a bullet.
- Range: The distance the bullets are effective for, after which no damage is dealt.
- Clip Capacity: The maximum amount of ammo held inside the weapon.

| Name          | Firing Mode | Damage | Time bet. Shots | Range   | Capacity |
|---------------|-------------|--------|-----------------|---------|----------|
| Pistol        | Single-Shot  | 2      | 0.2 seconds     | Medium  | 12       |
| Assault Rifle | Automatic    | 1      | 0.2 seconds     | Medium  | 30       |
| Shotgun       | Single-Shot  | 3      | 0.5 seconds     | Short   | 8        |
| Revolver      | Single-Shot  | 5      | 1 second        | Long    | 6        |

#### 2.2.2 Aiming and Shooting
In order to fire his weapon, Leon must be aiming it. Aiming zooms the camera closer to Leon, providing an over-the-shoulder view. Leon is able to walk while aiming but is unable to sprint while doing so. When a bullet is fired, its ammo count is affected accordingly. Leon cannot fire if the weapon has no ammo inside it.

#### 2.2.3 Reloading
In order to replenish the ammo inside the currently equipped weapon, Leon must reload it. Reloading is the process of moving the ammo from the inventory (see section 3.2), into the weapon to refill it, provided that there is sufficient ammo for the corresponding weapon in the inventory. Leon cannot reload a weapon if it is already full (i.e. ammo count is the same as the clip capacity), or if there is no ammo for the weapon in the inventory.
Reloading a weapon subtracts the difference between the current ammo in the weapon and its clip capacity from the ammo in the inventory, and adds it to the ammo count of the currently equipped weapon. If the ammo in the inventory is less than the ammo missing from the weapon, all inventory ammo is added to the weapon.

### 2.3 Grenades

Grenades are an essential part of Leon’s toolkit, as they allow him to affect multiple entities within a radius. Leon can have one grenade equipped at a time, which can be done from the inventory (see section 3.2). By pressing the grenade button, Leon can use grenades for two purposes. Successfully using a grenade removes it from Leon’s inventory, and resets the currently equipped grenade (i.e. set to none).
The first is to attack enemies from a distance by throwing the currently equipped grenade in a projectile motion ahead of him. All grenades automatically detonate (explode) 3 seconds after being thrown, and affect all enemies within the detonation radius. The second purpose is to break him free from an enemy grapple (see section 4.1.2). By pressing the grenade button while being grappled, Leon uses his currently equipped grenade (if available) to defend himself. The grenade also detonates after 3 seconds.

#### 2.3.1 Hand Grenade
Detonations make the hand grenade explode into shrapnel, causing all entities within the radius to receive 4 damage. Leon must be careful, as the hand grenade can affect him as well if he is within its radius when detonating.
### 2.3.2 Flash Grenade
Detonations make the flash grenade emit a bright light, causing all entities within the radius to become knocked down for 3 seconds (see section 4.1.3), allowing Leon to escape or use the knife to kill the knocked down enemies.

## Knife

### 2.4 Knife
One of Leon’s tools is the knife, allowing him to defend himself in tough situations, as well as incapacitate vulnerable enemies. Leon always keeps his knife available, so it does not take space in his inventory. Leon’s knife starts with 10 durability points and can not be used if it doesn’t have enough durability. Leon can regain durability points by repairing his knife (see section 3.3.4). By pressing the interact button, Leon can use his knife for two purposes.
The first use is to stab knocked down enemies as an interaction (see section 2.5). This depletes all the enemy’s remaining health points, and consumes 1 durability point. The second purpose is to break him free from an enemy grapple (see section 4.1.2), which consumes 2 durability points.

## Interactions

### 2.5 Interactions
When Leon is close to certain objects, he is able to interact with them, resulting in different actions based on the object and the state it is in. Interactable objects are indicated through a UI element appearing above them. In the case of multiple interactable objects being near Leon, pressing the interact button will only activate the closest one.

## Resource Management

### 3 Resource Management 

#### 3.1 Gold Coins
Leon starts the game with 30 gold coins. Leon can gain gold by picking it up from fallen enemies, or by selling items in the store. Leon can spend gold in the store.

#### 3.2 Inventory
Leon is only able to hold a certain amount of items which are stored in his inventory. Leon has to carefully manage it, which can be done in the inventory screen. Opening the inventory screen pauses the game. The inventory screen shows critical pieces of information; the player’s health points, stasis points (Boss level), gold coins, the knife’s durability, the currently equipped weapon, and the currently equipped grenade. The inventory screen also shows the player’s currently held items. An item with ammo in it (i.e. weapon or ammo stack) should also display the amount of ammo next to its name. The player is able to perform certain actions based on the selected item.

##### 3.2.1 Capacity
Leon is only able to hold a maximum of 6 items in his inventory and thus must make careful decisions regarding which items to pick up, and which to ignore.
#### 3.2.2 Starting Equipment
Initially, Leon starts the game with a pistol containing 12 ammo inside it, 12 pistol ammo, and one green herb in his inventory.

#### 3.2.3 Ammo Stacking
While for most items, each instance occupies a slot. Ammo for the same weapon can be included in the same slot. Meaning that a single inventory slot can hold several bullets for the same weapon. This is done automatically, meaning it should not be possible to have multiple inventory slots occupied by instances of ammo for the same weapon. This must be handled when crafting ammo, purchasing ammo from the store, as well as moving ammo from/to the storage.

#### 3.2.4 Equipping Items
After selecting an inventory item, Leon can choose to equip it, setting it as the currently equipped item. This is done by selecting an item, and then pressing the “Equip” button. This can only be done for weapons (which sets the weapon as the currently equipped weapon), and grenades (which sets the grenade as the currently equipped grenade).

#### 3.2.5 Using Items
After selecting an inventory item, Leon can choose to use it, instantly activating its effect. This is done by selecting an item, then pressing the “Use” button. This can only be done for herbs or mixtures.

#### 3.2.6 Discarding Items
After selecting an inventory item, Leon can choose to discard it, completely removing it from the inventory and the game. This is done by selecting an item, then pressing the “Discard” button. This can be done to all items except weapons and key-items.

#### 3.2.7 Combining Items (Crafting)
By combining basic ingredients, Leon is able to craft useful items, aiding him in his journey. Crafting is the process of selecting an inventory item, choosing to combine it, and then selecting another item, resulting in the removal of the original two items from the inventory. This is done by selecting the first item, pressing the “Combine” button, and then selecting the second item. This can only be done for the specific combinations.
Both original items must already be in Leon’s inventory. Additionally, Leon cannot combine an item with itself but can combine two different instances of the same item (e.g. two instances of green herbs). The order of the combination (i.e. items 1 and 2) does not affect the crafting process. The possible item combinations are:

| Item 1         | Item 2              | Resulting Item      |
|----------------|---------------------|---------------------|
| Green Herb     | Green Herb          | Green + Green Mixture |
| Red Herb       | Green Herb          | Green + Red Mixture |
| Red Herb       | Red Herb            | Red + Red Mixture   |
| Normal Gunpowder | Normal Gunpowder | 12 Pistol Ammo       |
| Normal Gunpowder | High-Grade Gunpowder | 8 Shotgun Ammo  |
| High-Grade Gunpowder | High-Grade Gunpowder | 30 Assault Rifle Ammo |

### 3.3 Store

Leon can use the store to buy and sell items, allowing him to reallocate his resources depending on the situation. When Leon is next to the store, interacting with it opens the store menu. The store menu pauses the game and consists of multiple screens.

#### 3.3.1 Buy Items

The buy items screen is where Leon gets to restock needed items in exchange for gold. The buy item section should display the player’s gold count, a list of buyable items to be purchased and their prices (e.g. Shotgun: 140 Gold), as well as the player’s inventory items. The player can buy one item at a time. The player clicks on the item to be purchased and the purchase is successful if and only if the player has enough gold. The player can not purchase an item from the store if his inventory is at maximum capacity. Once an item is purchased, it should appear in the player’s inventory and the player’s gold count should decrease accordingly.

#### 3.3.2 Sell Items

The sell item screen is where the player gets to sell his picked-up, purchased or crafted items in exchange for gold in order to buy more valuable item(s) from the store. The sell item screen should display the player’s gold count, items in the player’s inventory and their prices. The player can sell one item at a time. The player clicks on the item to be sold. Once the item is sold, it should disappear from the player’s inventory and the player’s gold count should increase accordingly.

#### 3.3.3 Storage

Since Leon’s inventory space is limited, he needs a place to store items that he might not need at the moment. The storage allows him to do so by providing a location to store his items with infinite capacity, albeit at the cost of the need to physically go to the store to move his items from the storage to the inventory and vice-versa. The storage screen is where Leon can view the items placed in the storage box and Leon’s inventory, and can switch item(s) between them. In the storage section, the content of the storage box is displayed on the left of the screen while Leon’s inventory items are on the right. Leon can move an item(s) from his inventory to his item box and can move item(s) to his inventory as long as it is not at maximum capacity (see section 3.2.1). Leon can not move his currently equipped weapon. Leon moves one item at a time by clicking on the item. The item should automatically disappear from its current position and be placed in the targeted destination.

## Knife Repair

### 3.3.4 Knife Repair

The knife repair screen is where Leon can recharge his knife’s durability in exchange for gold. The knife repair screen should display Leon’s gold count, the knife’s current durability points and a “Repair” button. Repairing the knife costs 100 gold coins and restores all durability points. Leon cannot repair the knife unless he has enough gold. Once the repair is successful, the durability points should increase to their maximum capacity and Leon’s gold count should decrease accordingly.

## Items

### 3.4 Items

Leon can find, craft, and purchase different types of items. These items provide him with precious resources, unlock new paths, as well as allowing him to more easily dispose of enemies. Some items can only be found in the environment. When Leon is next to an item that can be picked up, interacting with it moves it to the inventory (if there is sufficient space in the inventory). Some items can only be obtained by combining certain items in the inventory (see section 3.2.7). Some items are only found in the store (see section 3.3), and others might have multiple ways to obtain them.

#### 3.4.1 Herbs

Herbs allow Leon to regain resources by immediately using them, or opting to combine them to create mixtures, which are more powerful. Leon can obtain herbs from the store, or find them in the environment.

| Item       | Usage                        | Buy Price | Sell Price |
|------------|------------------------------|-----------|------------|
| Green Herb | Can be used to create mixtures<br>Gain 2 health points | 20        | 15         |
| Red Herb   | Can be used to create mixtures<br>Gain 2 stasis points (Boss Level ONLY) | 10        | 5          |

#### 3.4.2 Mixtures

Mixtures provide Leon with large amounts of resources. Mixtures can only be obtained via crafting.

| Item                 | Usage              | Buy Price | Sell Price |
|----------------------|--------------------|-----------|------------|
| Green + Green Mixture| Gain 6 health points | -         | 30         |
| Green + Red Mixture  | Gain 8 health points | -         | 20         |
| Red + Red Mixture    | Gain 6 stasis points (Boss Level) | -         | 10         |

#### 3.4.3 Gunpowder

While gunpowder itself has no immediate uses, it can be combined to create ammo for different weapons. Leon can obtain gunpowder from the store, or find it in the environment.

| Item            | Usage                           | Buy Price | Sell Price |
|-----------------|---------------------------------|-----------|------------|
| Normal Gunpowder| Can be used to create ammo      | 10        | 5          |
| High-Grade Gunpowder | Can be used to create ammo | 20        | 15         |

#### 3.4.4 Grenades

Grenades are useful supplementary offensive tools utilized by Leon (see section 2.3). Leon can obtain grenades from the store, or find them in the environment.

| Item          | Usage                 | Buy Price | Sell Price |
|---------------|-----------------------|-----------|------------|
| Hand Grenade  | Gain a hand grenade   | 15        | 10         |
| Flash Grenade | Gain a flash grenade  | 15        | 10         |

#### 3.4.5 Primary Weapons

Weapons are Leon’s main tool for handling enemies (see section 2.2.1).

| Item           | Usage                  | Buy Price | Sell Price |
|----------------|------------------------|-----------|------------|
| Pistol         | Gain a pistol          | -         | -          |
| Assault Rifle  | Gain an assault rifle  | 150       | -          |
| Shotgun        | Gain a shotgun         | 140       | -          |
| Revolver       | Gain a revolver        | -         | -          |

## Ammo

### 3.4.6 Ammo

In order to be able to fire his weapons, Leon must have enough ammo. Leon can craft ammo, or obtain it from the store. Obtaining an ammo type which already exists in the inventory follows the ammo stacking rules (see section 3.2.3).

| Item                | Usage                 | Buy Price | Sell Price |
|---------------------|-----------------------|-----------|------------|
| 12 Pistol Ammo      | Gain 12 pistol ammo   | 30        | -          |
| 30 Assault Rifle Ammo | Gain 30 assault rifle ammo | 50        | -          |
| 8 Shotgun Ammo      | Gain 8 shotgun ammo   | 40        | -          |
| 6 Revolver Ammo     | Gain 6 revolver ammo  | 70        | -          |

## Treasures

### 3.4.7 Treasures

During exploration, Leon can find valuable treasures. Leon can sell these treasures in the store to earn significant amounts of gold. Leon can only find treasures in the environment. There must be at least 2 different implemented treasures in your game. Multiple instances of a treasure can exist in different areas.

| Item       | Usage               | Buy Price | Sell Price |
|------------|---------------------|-----------|------------|
| Gold Bar   | Can be sold for gold | -         | 100        |
| Ruby       | Can be sold for gold | -         | 200        |
| Emerald    | Can be sold for gold | -         | 500        |

## Key-Items

### 3.4.8 Key-Items

While exploring the environment, Leon’s progress will be blocked by locked doors. Leon must find the appropriate key-item to open its corresponding door. Each key-item unlocks its corresponding door only. The “Emblem” and “Key Card” key-items are required to be implemented, in addition to at least 2 other key-items. Only one instance of a key-item can exist in the game.

| Item      | Usage                                    | Buy Price | Sell Price |
|-----------|------------------------------------------|-----------|------------|
| Emblem    | Unlocks door to end level                | -         | -          |
| Key Card  | Unlocks door for room containing revolver | -         | -          |
| Spade Key | Unlocks door locked with spade key       | -         | -          |
| Heart Key | Unlocks door locked with heart key       | -         | -          |
| Diamond Key | Unlocks door locked with diamond key    | -         | -          |
| Club Key  | Unlocks door locked with club key        | -         | -          |

# Main Level

The main level is where Leon explores, picks up items, and fights enemies before reaching the end. It consists of a series of enclosed spaces or rooms connected by doors that are either unlocked or require a key-item to be opened so that Leon can access the room behind them.

When Leon is next to a door which is not locked, interacting with the door makes it open permanently. Additionally, when Leon is next to a locked door, interacting with it attempts to unlock it. If the corresponding key-item (see section 3.4.8) is in Leon’s inventory, the locked door becomes permanently unlocked, and the key-item is removed from the inventory. Otherwise, the door remains unaffected.

## Enemies

### 4.1 Enemies

#### 4.1.1 Health Points and Movement

Enemies can be found in different rooms in the normal combat level(s). Initially, enemies have 5 health points and are either idly standing in small groups or patrolling (walking) around in a specific area within the same room. Enemies can lose health points when being attacked based on the attack performed by Leon. Whenever an enemy’s health points reach zero, the enemy dies and drops a random amount between 5 to 50 gold coins upon their death for Leon to pick up.

#### 4.1.2 Attacks

Once Leon enters a room, enemies are alerted and should automatically start attacking Leon. Enemies should keep attacking Leon until either Leon leaves the current room or dies. When Leon leaves the room, enemies are unable to follow him. An alerted enemy can perform different actions, attack, try to reach Leon if he is out of range, react to damage upon being hit, briefly wait between attacks, or die upon their health points reaching zero. Whether the enemy is armed or unarmed determines which attacks can be performed. Some enemies are initially armed, while others are initially unarmed.

Below is a description of the different attack behaviours that enemies can exhibit:

| Name    | State   | Description                                                                                         | Damage |
|---------|---------|-----------------------------------------------------------------------------------------------------|--------|
| Swing   | Armed   | The enemy approaches Leon, and swings their weapon against him.                                      | 2      |
| Throw   | Armed   | The enemy looks at Leon, and throws their weapon in a projectile motion towards him.                 | 3      |
| Punch   | Unarmed | The enemy approaches Leon and attempts to punch him.                                                  | 1      |
| Grapple | Unarmed | The enemy approaches Leon, and attempts to start grappling him. The enemy grapples Leon for 4 seconds during which Leon is immobilized and only has the option to use his defensive items (see sections 2.4, 2.3) to be released. If Leon does not use an item, the attack’s damage is dealt. While being grappled, Leon is not affected by other enemies’ attacks. | 5      |

#### 4.1.3 Knocked Down State

An enemy is knocked down if they are within the detonation radius of a flash grenade. A knocked-down enemy falls on the floor for 5 seconds and is unable to perform any actions. While an enemy is knocked down, Leon is able to use his knife to kill them (see section 2.4). If another flash grenade detonates while an enemy is already knocked down, they remain unaffected.

## Level Design

- Leon starts the level in the safe room where he can access the store to equip himself before engaging with enemies in other rooms.
- Rooms may contain items that Leon can place in his inventory, or they may contain enemies that he must fight.
- The level should contain 4 to 5 rooms with only items and no enemies.
- Leon should encounter a total of 10 to 15 enemies scattered in multiple rooms.
- The level should contain 4 to 5 rooms with differing numbers of enemies.
- A room with enemies can hold up to a maximum of 5 enemies who are unable to leave the room.
- A room with enemies can include any findable items except key-items.
- The level should contain a total of 4 to 6 doors that connect to other rooms that require key items to unlock.
- The revolver (see section 3.4.5) should be placed solely in a room behind a locked door and can only be accessed using the “Key Card” key-item.
- Leon finishes the level by picking up the “Emblem” key-item and using it to unlock a door found in the safe room that leads Leon to the next level (if exists), or the game ends and the studio credits roll.

# Zero-G Level (Extra Level)

In the Zero-G level, Leon is transferred into an open area in outer space. Leon must use his abilities while maneuvering in zero gravity to reach the end while blocking turret attacks, that shoot lasers in his direction. Leon has an oxygen tank that he must replenish to stay alive. In the Zero-G area, Leon cannot use any of his weapons; however, he can use items in his inventory collected from the previous level to help him while navigating (e.g., Herbs). Leon can also combine items to create powerful mixtures.

## 5.1 Player Movement

In the Zero-G area, in addition to normal movement options, Leon can float upward and downward, making him able to move in a total of 6 directions. Leon’s up and down movements are controlled by additional movement buttons alongside the original ones. Leon can move faster by holding the sprint button while pressing the movement buttons. Sprinting should double Leon’s original movement speed.

## 5.2 Oxygen Supply

Leon starts the Zero-G level with 100 oxygen points and can never exceed that value. Leon automatically loses 1 oxygen point per second in the Zero-G area. When Leon is next to an oxygen station, interacting with it refills his oxygen supply to its maximum. The oxygen station can be used multiple times. When the oxygen supply runs out, Leon dies immediately, and the “Game Over screen” is displayed.

## 5.3 Kinesis

Kinesis enables Leon to hold and manipulate objects in the scene by suspending the selected objects mid-air. This ability is used in different ways, including picking up and transporting objects that are out of Leon’s reach. This allows Leon to lift up, move, and place down any object from afar (without any physical contact).

Holding the kinesis button while the camera is looking at a nearby object selects it and moves it based on the camera look-at position, as well as Leon’s movements. Releasing the ability button reverts the object to normal (e.g., when an object is in midair and the button is released, it stays suspended). The affected object should still be affected by collisions, not go through walls, and remain in the play area at all times. Leon can manipulate a maximum of 1 object at a time.

## 5.4 Turrets

Turrets are immobile machines that can only be found in the Zero-G area. Each turret emits a security laser that can detect Leon. If the detection laser touches Leon, the turret switches to offensive mode. In the offensive mode, the damaging laser activates every 4 seconds for 2 seconds. Each time Leon touches the damaging laser, he loses 4 health points. Leon can manipulate the objects in the environment using his abilities to block the turrets’ detection and damaging lasers.

## Level Design

- If the level is loaded after a previous one, Leon’s health points, gold coins, inventory items, and storage items persist from the end of the previous level.
- If the level is restarted or loaded from the level select, Leon starts the level with the starting equipment (see section 3.2.2).
- In this level, Leon cannot access the store or use any of his weapons or grenades. The level should contain findable items that Leon can pick up.
- The level should contain 2 to 3 oxygen stations for Leon to use to refill his oxygen tank.
- The level should contain 3 to 4 immobile turrets placed in different areas in the level.
- The level should include multiple objects that Leon can use to block turrets’ attacks. Leon must use both his abilities to block turrets’ attacks and finish the level.
- Leon must use both his abilities to block turrets’ attacks and finish the level.
- Once Leon reaches the trigger area at the end of the level, he goes automatically to the next level (if exists), or the game ends, and studio credits roll.

# Boss Level (Extra Level)

At the end of Leon’s journey, he encounters a powerful foe, forcing him to use all the tools in his arsenal.

## 6.1 Stasis

Stasis allows Leon to stun the boss for a limited amount of time. Leon initially starts with 6 stasis points, and can never exceed that value. Each use of the stasis power consumes 1 point from Leon’s stasis points. Leon is unable to use the ability if he has no stasis points and can regain stasis points by consuming items (see section 3.4).

Pressing the stasis button while the camera is looking at the boss stuns him. While stunned, the boss stands dizzily for 8 seconds, and is unable to perform any attacks.

## 6.2 G-Creature (Boss)

The G-Creature is the scientist Dr. William Birkin, after he was forced to inject himself with the G-Virus which he created, turning him into a horrifying monster. Before Leon enters the arena, the boss is idly waiting for him. When the fight starts, the boss initially behaves in a certain way, referred to as “Phase 1”, then after a certain condition is met, he switches to a more lethal behavior, referred to as “Phase 2”.

### 6.2.1 Health Points and Movement

Unlike normal enemies, the G-Creature does not have traditional health points, and is unaffected by direct shots. Additionally, the boss does not react to hits and is unaffected by the detonation of grenades. Instead, vulnerable eyes appear on his body, which must be shot by Leon in order to defeat him. In phase 1, the boss has 3 eyes around his body, where each eye has 10 health points. An eye is automatically destroyed after reaching 0 health points. After all 3 eyes are destroyed, the boss switches to phase 2, where a large eye appears on his back. This eye has 25 health points, and the boss is defeated once it reaches 0 health points.

### 6.2.2 Attacks

The boss can perform different actions, attack, try to reach Leon if he is out of range, briefly wait between attacks, or die upon their health points reaching zero. Whether the boss is in phase 1 or 2 determines which attacks can be performed.

| Name          | Phase | Description                                                                                                    | Damage |
|---------------|-------|---------------------------------------------------------------------------------------------------------------|--------|
| Kick          | 1     | The boss approaches Leon, and attempts to kick him.                                                           | 3      |
| Mega-Grapple  | 1     | The boss approaches Leon, and attempts to start grappling him. The boss grapples Leon for 4 seconds.           | 6      |
| Swipe         | 2     | The boss approaches Leon, and swipes at him.                                                                  | 4      |
| Rock Throw    | 2     | The boss approaches one of the rocks in the boss arena, lifts it and throws it towards Leon in a projectile motion. | 7      |


# 6.3 Level Design

- If the level is loaded after a previous one, Leon’s health points, gold coins, inventory items, and storage items persist from the end of the previous level.

- If the level is restarted, or is loaded from the level select, Leon starts the level with the starting equipment (see section 3.2.2).

- Leon starts the level in a safe room where he can access the store to equip himself before engaging with the boss.

- After Leon enters the boss’s room, he is unable to go back to the safe room. Both Leon and the boss are confined to the arena, and Leon must defeat the boss to finish the level.

- There must be enough room for the boss to be able to perform all their behaviors, as well as for Leon to attack, take cover and evade boss attacks.

- The Boss arena must include at least 3 rocks for the boss to be able to perform the Rock Throw attack.

- When Leon defeats the boss, the game ends and studio credits roll.

# 7 Controls

- The player controls the camera rotation with the mouse.

- The player controls Leon’s walking movements forward and backward using the arrow up and down keys as well as the “W” and “S” keys respectively.

- The player controls the left and right movements using the right and left keys or the “A” and “D” keys respectively.

- The player runs/sprints by holding down “left-shift” along with one of the movement keys.

- The player controls the upward and downward movements using the “Z” and “C” keys respectively.

- The player aims their currently equipped weapon by holding down right mouse button.

- The player fires their currently equipped weapon by pressing the left mouse button.

- The player reloads their currently equipped weapon by pressing “R”.

- The player throws their currently equipped grenade by pressing “G” button.

- The player interacts with specific objects by pressing the “E” button.

- The player uses the stasis ability by pressing the “F” button.

- The player uses the kinesis ability by holding the “Q” button.

- The player opens and closes their inventory by pressing the “Tab” button.
  
- The player can select items and buttons in the UI screens using the mouse movement and the left mouse button.
  
- The player pauses and resumes playing, as well as close UI screens by pressing the “ESC” button.

# 8 Heads-Up Display (HUD)

The HUD is the display area where the player can see important information about the player’s status, such as health, equipped abilities, and ammo count.

- Health Points: The health points are displayed as a glowing segmented bar on the back of the player where each segment represents 1 health point.
- Ammo count: The ammo count is displayed as an anchored text to the weapon. It shows the current amount of ammo count in the currently equipped weapon.
- Stasis (Boss Level): The stasis is displayed as a circle on the back of the player. The circle angle represents the amount of stasis points left.
- Oxygen gauge (Zero-G): The oxygen supply is displayed as an anchored text to Leon’s back. It shows the current amount of oxygen points.

# 9 Screens

### 9.1 Main menu
  - Play
    - New Game: Starts a new game from the Combat level
    - Level Select: Allows the player to directly play a specific level if there are multiple levels.
  - Options
    - Audio
      - Music level
      - Effects Level
    - Team Credits: Lists each team member’s name and project role.
    - Asset Credits: Lists all external assets and their sources.
  - Quit Game
### 9.2 Pause Screen
- Resume
- Restart Level
- Quit to Main Menu

### 9.3 Game Over Screen
- Restart Level
- Quit to Main Menu

### 9.4 Inventory Screen
All UI elements (e.g. text, buttons) relevant to the inventory (see section 3.2) should be visible.

### 9.5 Store Screen
The store screen consists of multiple sub-screens. All UI elements (e.g. text, buttons) relevant to the store (see section 3.3) should be visible.
- Buy Tab
- Sell Tab
- Storage Tab
- Knife Repair Tab

## 10 Graphics

### 10.1 Models
You will need models for the environment, characters, and weapons. You can use models from the game or alternative models as long as they are fairly representative of the requirements.

### 10.2 Animations

#### 10.2.1 Leon Animations
- Idle
- Walking
- Floating (Zero-G)
- Sprinting
- Aiming
- Firing Weapon
- Throwing Grenade
- Using Knife
- Hit Reaction
- Being Grappled
- Dying

#### 10.2.2 Enemy Animations

- Idle
- Walking
- Animations for Each Attack
- Hit Reaction
- Knocked-down
- Dying

#### 10.2.3 Boss Animations

- Idle
- Walking
- Animations for Each Attack
- Stunned
- Dying

## 11 Audio

### 11.1 Sound Settings

The audio in your game should be divided into at least two independently controllable categories: Music and Sound effects (SFX).

### 11.2  Sound Effects

#### 11.2.1 Effects

- Footsteps of Leon as he moves.
- Footsteps of an enemy as he moves.
- Footsteps of the boss as he moves.

#### 11.2.2 Feedback

- When a weapon is fired.
- When a grenade detonates.
- When an item is picked up.
- When a door is unlocked.
- When Leon is hit.
- When Leon dies.
- When an enemy is hit.
- When an enemy dies.
- When a turret detects Leon.
- When a turret fires laser.
- When a boss is hit.
- When a boss dies.

### 11.3 Music

- Slow-paced track for the main and pause menus.
- A different track for each of the game level(s) depending on the atmosphere.

## 12 Cheats

Implementing cheat codes is required, as they will help us to test individual aspects of your project, in case we were not able to test them throughout the normal gameplay.

- Heal: Increases Leon’s health by 4 health points.
- Toggle Invincibility: Prevents Leon from taking damage when enabled.
- Toggle Slow Motion: Makes the gameplay in half speed when enabled.
- Add Gold: Increases Leon’s gold count by 1000 gold coins.
- Door Unlock: Unlocks all locked doors enabling Leon to move to other rooms.
