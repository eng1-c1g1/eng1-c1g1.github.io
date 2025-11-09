---
layout: default
title: Architecture
---

# Architecture Overview
Detailed information of our technical contributions in *Escape from Uni*.

---

## Debugging Tools 
**What:** It displays green hitbox lines, grid lines, a small box at the player's feet, an interaction circle and a center X so collision and alignment areas are visible on screen.

**Why:** It helps us debug faster and fix issues quickly by showing green hitbox lines, grid lines, a small box at the player's feet, an interaction circle and a center X. 

**Evidence:** [View PDF](https://drive.google.com/file/d/17xTfgkl-RQKob_yBaxysSAwXCa2PwdAW/view?usp=sharing)

---

## Rendering System 
**What:** The system renders the objects in the game in the correct order. It uses each object's sprite and position, then draw them and decides the order based on layer and Y position. Additionally, the camera keeps the view smooth by following the player.

**Why:** Because the player can be hidden behind walls and furniture, it sorts by layer first and then by Y- position to ensure a smooth top-down view. Moreover, the camera keeps the gameplay visually consistent and easy to follow the screen.

**Evidence:** 

---

## Editor 
**What:** EntityMaker automatically creates game objects such as the player, collectables, and enemies, then attaches the components like sprite, physics, animation, and interactions. It is designed for quick placement, and can integrate with drag-and-drop editors(e.g., Tiled)

**Why:** It helps reduce the time and issues because we do not have to write new code for creating objects every time.

**Evidence:** 

---

## Testability 
**What:**  Each system (RenderOrderComparator, WorldCameraSystem, EntityMaker, MazeGame) is independent, so we can test code in parts.

**Why:** The system are separated from each other, so it is easy to find issues, edit safely, and keep the maintenance consistent.

**Evidence:** 

---

## Modularity (Extreme Decoupling)
**What:** Functions such as rendering, camera, physics, and entitymaker are separated into individual systems.

**Why:** Because each system is independent, the structure stays clean, making the project easy to update and flexible.

**Evidence:** [View PDF](https://drive.google.com/file/d/1JIuPX_ObCz7U2jNfdZ0B1K2PS-U4s4uY/view?usp=sharing)

---

## Interaction System 
**What:** This system detects interactions between the player and objects such as items and enemies,sends the designated message for the object, makes it inactive when it runs once, and get rid of the object depending on the setting.
 
**Why:** This systems only send the message detected from interactions between the player and objects. Moreover, it is really easy to add new interactions, so it does not require editing the system code, which means the code is very reusable for reuse and easy to test.

**Evidence:** 

---

## Assets 
**What:** AssetLoader acts as the centralized manager for the project assets. Assets are referenced by the AssetId, and actual file paths are stored in AssetPaths. At startup, it loads textures and TMX maps via LibGDX AssetManager, and game retrieves assets with get(id, type).

**Why:** All paths are stored and managed in AssetPaths, and assets are referenced by AssetId, so access and maintenance are easier, reducing errors.

**Evidence:** [View PDF](https://drive.google.com/file/d/1uWOgICmCNWdo_z_wbghFepQwf6J2ruC5/view?usp=sharing)

---

## Fixed time-step engine
**What:** Regardless of performance level, the game uses a fixed time step (1/60s). When the accumulated time reaches this step, it calls fixedUpdate() once, keeping the behaviour the same across different performance levels.

**Why:** If we update the game logic with a fixed time step, then speed and physics stay identical across different performance levels, and collisions and interactions are easier to test and predict.

**Evidence:** [View PDF](https://drive.google.com/file/d/10f5QukcNfUdNz1gvv2VNHTW42xBPlCT6/view?usp=sharing)

---

## **Diagrams:** 
[see more diagrams]({{ '/architecture-diagrams/' | relative_url }})


