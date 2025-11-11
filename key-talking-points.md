---

layout: page
title: Technical Information
---


## **Our Key Technical Contributions**
An overview of our team's key contributions to Escape from Uni.

## Codebase Javadoc
- <span style="font-size:1em">[Javadoc](/assets/javadoc)</span>

## **Technologies and Tools Used**

Our game was developed using:
- **Language:** Java 17  
- **Game Framework:** LibGDX  
- **Architecture:** Entity-Component-System (ECS)  
- **Physics Engine:** Box2D (via LibGDX)  
- **Map Editor:** Tiled  
- **Build System:** Gradle  
- **Version Control:** Git & GitHub  
- **Documentation:** Javadoc 

| Feature | Description | Link |
|----------|-------------|------|
|  **Debugging Tools** | Collision debugger for finding and fixing issues quickly | [View](/architecture#debugging-tools) |
|  **Generalised Rendering System** | Rendering system works for all levels and objects | [View](/architecture#rendering-system) |
|  **Editor (Drag-and-Drop)** | Allows users to place objects such as collectables and enemies directly into levels via drag-and-drop | [View](/architecture#editor) |
|  **Easily Testable Code** | Modular code to make testing simple | [View](/architecture#testability) |
|  **Extreme Decoupling** | Easy to update due to clean separation between systems, providing flexibility and easy extension | [View](/architecture#modularity-extreme-decoupling) |
|  **Reusable Player-Entity Interaction System** |  Handles interactions between the player and entities such as collectables, enemies, and triggers| [View](/architecture#interaction-system) |
|  **Centralised Asset Management System** | Automatically loads assets and separates file paths from code for easier access and maintenance | [View](/architecture#assets) |
|  **Fixed Time-Step Engine** | Ensures consistent performance on all devices | [View](/architecture#fixed-time-step-engine) |

## **Relation to Requirements**

This section demonstrates how the implemented systems, components, and features satisfy the defined requirements.  
Each Functional Requirement (FR) is traced to its corresponding User Requirement (UR) and implemented element in the game.

| **Requirement ID** | **Description** | **Implementation / Supporting Systems** | **Linked User Requirement(s)** |
|---------------------|-----------------|------------------------------------------|--------------------------------|
| **FR_MAZE** | The system shall generate a university-themed maze that the player must escape from. | Level layout created using Tiled; loaded and rendered through `AssetLoader`, `RenderingSystem`, and `LevelScreen`. | UR_ESCAPE_MAZE, UR_THEME |
| **FR_WAY_OUT** | The system shall provide an exit point to escape the maze. | Exit tile and trigger area handled by `InteractableSystem`; triggers game completion via `GameStateSystem`. | UR_ESCAPE_MAZE |
| **FR_TIMER** | The system shall provide a timer that tracks playtime and enforces a 5-minute time limit. | `TimerSystem` and `TimerComponent` track countdown; integrated into HUD and triggers `GameOverScreen` when expired. | UR_TIME_LIMIT |
| **FR_END_GAME** | The system shall end the game when the player escapes, is caught by the dean, or the timer expires. | `GameStateSystem` manages transitions to `WinScreen` or `GameOverScreen`; `GooseSystem` triggers loss via `GooseBiteMessage`. | UR_ESCAPE_MAZE, UR_DEAN |
| **FR_PAUSE** | The system shall fully pause all gameplay when the player pauses the game. | `GameStateSystem` halts updates; menus handled by `MenuScreen`. | UR_PAUSE |
| **FR_PAUSE_MENU** | The system shall display a pause menu with appropriate options. | `MenuScreen` and `BaseMenuScreen` provide UI overlays and resume options. | UR_UI, UR_PAUSE |
| **FR_POSITIVE_EVENTS** | The system shall include visible events that provide beneficial effects. | Coffee collectables grant buffs and score boosts via `InteractableSystem` and `CoffeeCollectMessage`. | UR_POSITIVE_EVENTS |
| **FR_NEGATIVE_EVENTS** | The system shall include visible events that hinder progress. | Goose enemy entities damage or chase the player through `GooseSystem` and `GooseBiteMessage`. | UR_NEGATIVE_EVENTS |
| **FR_HIDDEN_EVENTS** | The system shall include hidden events that alter the game. | Pressure plates reveal or open walls using `HiddenWallSystem` and `PressurePlateTriggerMessage`. | UR_HIDDEN_EVENTS |
| **FR_EVENT_TRACKER** | The system shall include counters that track triggered events. | `EventCounter` tallies collected, triggered, and hidden events; data displayed in the HUD. | UR_POSITIVE_EVENTS, UR_NEGATIVE_EVENTS, UR_HIDDEN_EVENTS |
| **FR_SCORE** | The system shall calculate the player's score based on time and events. | `ScoreCard` integrates with `EventCounter` and `TimerSystem` to calculate total score; displayed on `WinScreen`. | UR_SCORE |
| **FR_BOUNDARIES** | The system shall enforce boundaries that the player cannot cross. | Box2D colliders defined in the Tiled map; enforced by `PhysicsSystem` and `CollisionConverter`. | UR_BOUNDARIES |
| **FR_THEME** | The system shall simulate a university-like environment with appropriate scenery. | Assets provided via `AssetLoader` and `AssetPaths`; university buildings, desks, and halls in Tiled maps. | UR_THEME |
| **FR_DIFFICULTY** | The system shall provide a base difficulty with pausing always enabled. | Adjustable gameplay parameters in `GameStateSystem` (enemy speed, timer length). | UR_DIFFICULTY |
| **FR_DO_NOT_SAVE** | The system shall not save progress after completion. | Game state reset on restart; no persistence layer implemented. | UR_DO_NOT_SAVE |
| **FR_DEAN** | The system shall display and control a dean character that the player must avoid. | Represented conceptually by `GooseSystem` (enemy AI); further dean NPC possible for extension. | UR_DEAN |
| **FR_EVENT_AMOUNTS** | The system shall include required minimum numbers of events. | Validated through event spawning logic and object placement in Tiled map. | UR_POSITIVE_EVENTS, UR_NEGATIVE_EVENTS, UR_HIDDEN_EVENTS |


## **Testing and Validation**

Our testing approach combined manual playtesting with automated verification of core systems:
- **Unit testing:** TimerSystem, EventCounter, and PhysicsSyncSystem verified for correct behaviour.
- **Debug tools:** In-game collision visualiser helped confirm accurate physics and interactions.
- **Playtesting:** Conducted across multiple devices to ensure consistent frame timing (verifying Fixed Time-Step Engine).
- **Peer reviews:** Code reviewed via GitHub pull requests before merging into main.

## **Performance**

- **Frame Consistency:** FixedStepSystem ensures stable updates across devices regardless of framerate.  
- **Memory Efficiency:** Component-based ECS avoids large inheritance chains, minimising memory overhead.  
- **Deployment:** Packaged into a runnable JAR and prepared for Web export using LibGDX’s HTML backend.  
- **Optimisation:** Unused entities and Box2D bodies automatically destroyed via SafeBodyDestroy to prevent leaks.

> For detailed class and system diagrams, see our [Architecture Diagrams](/architecture-diagrams).


