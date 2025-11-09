---
layout: page
title: CRC Card Tables
---



We used Class–Responsibility–Collaborator (CRC) cards to plan how different parts of our game fit together in the Entity–Component–System (ECS) architecture.  
Each CRC card explains what something does (its responsibility) and who it works with (its collaborators).

Our ECS approach splits the game into:
- **Components** -> store data  
- **Systems** -> handle behaviour and logic  
- **Messages** -> let different systems talk to each other  

This makes it easier to add new features or change old ones without breaking everything else.

## Components

These are the data bits attached to entities. They don’t do anything on their own - the systems read from them and update them.

| Component | Responsibilities | Collaborators |
|------------|--------------|-------------|
| **CameraFollowComponent** | Tells the camera which entity to follow (usually the player). | WorldCameraSystem, TransformComponent |
| **GooseComponent** | Stores info for the goose enemy, like if it's chasing the player or patrolling. | GooseSystem, TransformComponent, PhysicsComponent, PlayerComponent |
| **InteractableComponent** | Marks an object as interactable (like a button, switch, or collectible). Can also send messages or disappear when used. | InteractableSystem, MessagePublisher, PlayerComponent |
| **PhysicsComponent** | Holds the Box2D body and its physics settings (mass, type, shape, etc.). | PhysicsSystem, PhysicsSyncSystem, PhysicsToTransformSystem |
| **PlayerComponent** | Keeps track of player movement direction, speed, and animation state. | PlayerSystem, PhysicsComponent, AnimationComponent, TransformComponent |
| **SpriteComponent** | Contains the texture and render layer for drawing on screen. | RenderingSystem, RenderOrderComparator, TransformComponent |
| **TimerComponent** | A simple countdown timer that sends a message when it finishes. | TimerSystem, MessagePublisher |
| **TransformComponent** | Stores an entity's position, rotation, and scale. Used by nearly every system. | PhysicsToTransformSystem, RenderingSystem, CameraFollowComponent, PlayerSystem |
| **AnimationComponent** | Keeps track of animation state, current clip, and frame speed. | RenderingSystem, PlayerSystem, AssetLoader |
| **AudioListenerComponent** | Marks which entity the audio listener follows (usually the player). | AudioSystem, TransformComponent |
| **HiddenWallComponent** | For walls that appear or disappear when triggered. | HiddenWallSystem, InteractableSystem, MessagePublisher |

---

## Systems

These handle the behaviour and logic. Each one focuses on a single job, like physics, input, rendering, or audio.

| Component | Responsibilities | Collaborators |
|--------|---------------|-------------|
| **PlayerSystem** | Reads player input, moves the character, and updates animations or sounds. | PlayerComponent, PhysicsComponent, AnimationComponent, AudioSystem |
| **PhysicsSystem** | Runs Box2D physics at a fixed timestep to keep movement smooth and stable. | PhysicsComponent, TransformComponent, SafeBodyDestroy, MessagePublisher |
| **PhysicsSyncSystem** | Syncs transforms with physics bodies after updates. | TransformComponent, PhysicsComponent |
| **PhysicsToTransformSystem** | Copies body positions from Box2D to the entity transforms before rendering. | TransformComponent, PhysicsComponent, RenderingSystem |
| **RenderingSystem** | Draws all sprites and animations in the correct order (based on Y-position and layer). | SpriteComponent, AnimationComponent, TransformComponent, RenderOrderComparator |
| **AudioSystem** | Plays sounds in response to messages (like footsteps, goose bites, or the victory sound). | AudioListenerComponent, SoundMessage, WorldSoundMessage, MessagePublisher |
| **HiddenWallSystem** | Toggles hidden walls when it receives the right trigger message. | HiddenWallComponent, MessagePublisher, InteractableSystem |
| **InteractableSystem** | Checks if the player interacts with an object and sends out messages (like collecting an item). | InteractableComponent, PlayerComponent, MessagePublisher |
| **GooseSystem** | Controls the goose AI - handles chasing the player and reacting to collisions. | GooseComponent, PlayerComponent, MessagePublisher |
| **TimerSystem** | Counts down timers and fires messages when they expire. | TimerComponent, MessagePublisher |
| **WorldCameraSystem** | Makes the camera follow an entity with a CameraFollowComponent. | CameraFollowComponent, TransformComponent |
| **GameStateSystem** | Checks win or lose conditions and shows end screens or messages. | ScoreCard, MessagePublisher, GameOverScreen, WinScreen |

---

## Messages and Other Helpers

These are the classes that connect systems together and handle smaller jobs like asset loading and sorting.

| Component | Responsibilities | Collaborators |
|--------|--------------|-------------|
| **Message** | The base class for sending events around the game. | MessagePublisher, MessageListener |
| **MessagePublisher** | Sends messages to anything that's subscribed. | All Systems |
| **MessageListener** | Used by systems that need to react to messages. | MessagePublisher, various Systems |
| **MessageType** | Enum of different message categories (SOUND, INTERACT, LEVEL_COMPLETE, etc.). | All message subclasses |
| **CollisionConverter** | Converts Box2D collision events into game messages. | PhysicsSystem, InteractableSystem |
| **AssetLoader** | Loads and manages textures, sounds, and fonts. | RenderingSystem, AudioSystem, EntityMaker |
| **EntityMaker** | Builds entities by attaching the right components. | AssetLoader, all Components |
| **FixedStepper / FixedStepSystem** | Keeps physics and timer updates consistent regardless of frame rate. | PhysicsSystem, TimerSystem |
| **SafeBodyDestroy** | Queues up physics bodies for safe removal (prevents Box2D errors). | PhysicsSystem |
| **RenderOrderComparator** | Sorts entities for proper drawing order (layer then Y-position). | RenderingSystem, SpriteComponent |
| **EventCounter / ScoreCard** | Tracks score and progress for the game state logic. | GameStateSystem |
| **FontGenerator** | Creates fonts used in the menus and HUD. | BaseMenuScreen, LevelScreen |

---

## Why We Used CRC Cards

Making CRC cards helped us figure out what each part of the game should be responsible for.  
It stopped us from putting too much logic into one system and made it easier for everyone on the team to see how things connected.

They also helped us link our requirements to the actual code. For example:

- **Door and pressure plate feature:**  
  Done with InteractableComponent, InteractableSystem, and HiddenWallSystem.  
  When the player steps on the plate, a PressurePlateTriggerMessage tells the wall to open.

- **Audio feedback:**  
  Done through the AudioSystem, which plays sounds when it receives SoundMessage or WorldSoundMessage.

---

## Notes

Making these cards early on was really helpful. It let us spot overlap between systems and simplify the design.
For example, we originally put the camera logic in PlayerSystem, but moving it into a separate WorldCameraSystem made things much cleaner.

Overall, the CRC cards gave us a simple way to plan and communicate how everything fits together in our ECS design.
