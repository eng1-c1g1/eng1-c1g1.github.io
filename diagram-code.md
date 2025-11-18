---
title: PlantUML Diagrams
layout: default
---

<details markdown="1">
<summary><strong>Architecture Structural Diagram - show/hide</strong></summary>

```plantuml
@startuml architectureStructuralDiagram

title __Structural Diagram__


entity Player{
    + int id
}

entity Coffee{
    + int id
}

entity Goose{
    + int id
}

entity CheckInCode{
    + int id
}

entity Timer{
    + int id
}

entity Walls{
    int id
}

entity HiddenWalls{
    int id
}

entity PressurePlate{
    int id
}


class CameraFollowComponent{
    + boolean active
    + Vector2 offset
}

class PhysicsComponent{
    + Body body
    + enum ColliderType
    - ColliderType colliderType
    - float colliderWidth
    - colliderHeight
    - float colliderWidth
    - float colliderHeight
    - float colliderRadius
    - Vector2 colliderOffset
}

class PlayerComponent{
    + final float maxSpeed
    + List<SpeedBonus> speedBonuses
    + final float acceleration
    + final foat deceleration
    + final float knockbackRecovery
    + Vector2 currentKnockback
    + Vector2 naturalVelocity
    + enum PlayerState
    + PlayerState currentState
    

}

class SpriteComponent{
    + Texture texture
    + boolean isShown
    + RenderLayer randerLayer
    + Vector2 textureOffset
    + Vector2 size

}

class TransformComponent{
    + Vector2 position
    + Vector2 scale
}

class GooseComponent{
    + GooseState state
    + float chaseSpeed
    + float retreatSpeed
    + float wanderSpeed
    + float wanderRadius
    + float wanderAcceptDistance
    + Vector2 currentWanderWaypoint
    + float detectionRadius
    + float forgetRadius
    + float retreatTime
    + float retreatTimeElapsed
    + Vector2 homePosition

}

class InteractableComponent{
    + InteractableMessage activationMessage
    + boolean disappearOnInteract
    + boolean interactionEnabled
}

class TimerComponent{
    + float timeRemaining
    + float totalTime
    + boolean isRunning
    + boolean hasExpried

}

class HiddenWallsComponent{
    + String triggeredBy
}

class AnimationComponent{
    + Hash Map<typeOfState, Animation<TextureRegion>> animations
    + typeOfState currentState
    + float elapsed
    + TextureRegion currentFrame
}

class AudioListenerComponent{
    + Vector2 offet
}


Player *-- PlayerComponent
Player *-- PhysicsComponent
Player *-- SpriteComponent
Player *-- TransformComponent
Player *-- CameraFollowComponent
Player *-- AnimationComponent
Player *-- AudioListenerComponent

Coffee *-- InteractableComponent
Coffee *-- TransformComponent
Coffee *-- PhysicsComponent

Goose *-- InteractableComponent
Goose *-- GooseComponent
Goose *-- PhysicsComponent
Goose *-- TransformComponent
Goose *-- AnimationComponent

Timer *-- TimerComponent

CheckInCode *-- InteractableComponent
CheckInCode *-- TransformComponent
CheckInCode *-- PhysicsComponent

Walls *-- PhysicsComponent
Walls *-- TransformComponent

PressurePlate *-- InteractableComponent
PressurePlate *-- TransformComponent

HiddenWalls *-- PhysicsComponent
HiddenWalls *-- HiddenWallsComponent
HiddenWalls *-- TransformComponent
@enduml
```

</details>

<details markdown="1">
<summary><strong>Prototype Architecture Behavioural Diagram - show/hide</strong></summary>

```plantuml
@startuml PrototypeArchitectureBehavorialDiagram
title __Prototype Activity Diagram__
start

repeat


:GameStateSystem: update;
:InteractableSystem: update;
:GooseSystem: update;
:PlayerSystem: update;
:PhysicsSyncSystem: update;
:PhysicsSystem: update;
:PhysicsToTransformSystem: update;
:WorldCameraSystem: update;
:RenderingSystem: update;
:TimerSystem: update;
:TimerRendererSystem: update;

repeat while()


@enduml
```

</details>

<details markdown="1">
<summary><strong>Architecture Behavioural Diagram - show/hide</strong></summary>

```plantuml
@startuml "ArchitectureBehavorialDiagram"

title __Behavorial Activity Diagram__
start

repeat

if(fixed update due?) then(yes)
    :GooseSystem: fixed update;
    :PlayerSystem: fixed update;
    :HiddenWallsSystem: fixed update;
    :PhysicsSyncSystem: fixed update;
    :PhysicsSystem: fixed update;
    :PhysicsToTransformSystem: fixed update;
else(no)
    :GameStateSystem: update;
    :InteractableSystem: update;
    :PlayerSystem: update;
    :AudioSystem: update;
    :WorldCameraSystem: update;
    :RenderingSystem: update;
    :TimerSystem: update;
endif
repeat while()

@enduml
```

</details>

<details markdown="1">
<summary><strong>Architecture Class Diagram - show/hide</strong></summary>

```plantuml
@startuml architectureClassDiagram

title __Game Architecture__

class Entity{
    + int id
    + List<Component> Components

}

class Engine{
    + List<Entity> entities
    + List<System> systems

}

interface MessageListener{
    + recieve(message)
}


interface Component{


}

interface System{
    + update()
}

interface Publisher{
    + publish(message)
}

System <..> MessageListener : " 0..1"
MessageListener <..> Publisher: "1"

Engine *-- System: "*"
Engine *-- Entity: "*"
Entity *-- Component: " 1 -- *"


@enduml
```

</details>

<details markdown="1">
<summary><strong>Sequence Diagram - show/hide</strong></summary>

```plantuml
@startuml

title __Sequence Diagram__

participant ConstructListener
participant InteractableSystem
participant PlayerSystem
participant Publisher

ConstructListener -> Publisher: "Player collided with coffee"

Publisher -> InteractableSystem: "Player collided with coffee"

InteractableSystem -> Publisher: "Coffee collected"

Publisher -> PlayerSystem: "Coffee Collected"



@enduml
```

</details>