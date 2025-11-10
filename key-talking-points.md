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

Each technical feature was implemented to meet specific functional and architectural requirements:

| Requirement | Implementation | Related Feature |
|--------------|----------------|-----------------|
| **FR_POSITIVE_EVENT** - Game must include a positive event | Coffee collectables increase score | Reusable Player-Entity Interaction System |
| **FR_NEGATIVE_EVENT** - Game must include a negative event | Goose enemy damages player | Reusable Player-Entity Interaction System |
| **FR_HIDDEN_EVENT** - Game must include a hidden event | Hidden wall triggered by pressure plate | Interaction System, HiddenWallSystem |
| **UR_TIMER_5_MIN** - Game must include a timer | Countdown handled by TimerSystem | Fixed Time-Step Engine |
| **UR_EVENT_COUNTER** - Game must track completed events | EventCounter tracks triggers and progress | Debugging Tools, ECS Modularity |
| **UR_ECS_ARCHITECTURE** - Game must use an ECS design | Implemented through modular components and systems | Extreme Decoupling, Generalised Rendering |

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


