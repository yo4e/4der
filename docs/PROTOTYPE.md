# Minimal 4der Prototype

Status: **exploratory concept only**. This document records a plausible first implementation discussed on 2026-08-16. It is not a frozen specification or roadmap. Dimensions, technologies, interfaces, object models, and even component boundaries may change as prototypes teach us what 4der actually needs.

The purpose of this document is to keep a useful near-term implementation picture without shrinking the long-term vision.

## Goal

Build the smallest 4der that proves four things:

1. a personal world can exist independently of an AI,
2. the world can change form without losing continuity,
3. continuity can live outside the renderer,
4. an external partner can perceive, inhabit, and alter the world through a small interface.

The prototype does **not** need to prove real-time generative 3D, federation at scale, persistent AI identity, photorealism, VR, or a production-ready social system.

## Prototype maxim

**Small stage, infinite world.**

The first 4der does not need a large terrain. A roughly **10 × 10 meter** walkable stage may be enough. Only the nearby space needs to be physically represented in 3D. The apparent world outside that stage can be supplied by a sky dome, skybox, panoramic environment, distant geometry, fog, lighting, sound, or other interchangeable techniques.

A beach therefore does not require kilometers of modeled coastline. The stage may contain sand, a bench, and a few nearby objects while the horizon, ocean, clouds, and distant landscape are environmental projection. A garden may contain real 3D herbs and furniture while most of the surrounding scenery is represented by the shell.

This suggests three rendering layers for the first World implementation:

### Stage

The small space the user can physically occupy and interact with.

Possible responsibilities:

- floor and collision,
- locomotion,
- human and AI avatars,
- nearby interactive geometry,
- local spatial coordinates.

### Shell

The apparent world around the Stage.

Possible responsibilities:

- sky dome or skybox,
- panoramic scenery,
- distant landscape,
- room walls or other enclosing environment,
- weather,
- lighting,
- fog,
- ambient sound,
- time of day.

Shell is deliberately replaceable. A first prototype may switch among hand-authored panoramas or presets. Later versions might use procedural scenes, generative imagery, generated 3D, streamed environments, or technologies that do not yet exist.

### Props

Interactive or visible 3D objects that can be added, removed, moved, or replaced.

Examples:

- chairs,
- desks,
- shelves,
- binders,
- herb pots,
- benches,
- lamps,
- decorations,
- screens.

This allows one small coordinate space to become many places without requiring a fixed map.

## North-Star slice

The first prototype can borrow directly from the vision story:

- **Garden** — herbs, soil or grass, a bench, daylight,
- **Office** — desk, chair, shelf, binder-like object, work surfaces,
- **Beach** — sand, sea horizon, sky, weather, and time-of-day controls.

These do not need to be three permanent maps. They can be scene states assembled from Stage, Shell, and Props.

A transformation can therefore be conceptually simple:

```text
Garden
  Stage: grass / soil
  Shell: garden landscape
  Props: bench + herbs

Office
  Stage: office floor
  Shell: office interior
  Props: desk + chair + shelf + binder

Beach
  Stage: sand
  Shell: ocean + sky
  Props: minimal
```

The important thing is that the world identity survives the transformation.

## Minimal World

A browser-based 3D scene is enough for the first version.

Minimum capabilities may include:

- enter the world without logging into an AI service,
- move or look around,
- use a simple human avatar,
- switch among a few scene states,
- change time of day,
- change weather,
- add, remove, and move a small set of 3D props,
- expose current state in a machine-readable form.

Possible implementation technologies include Three.js, Babylon.js, or another lightweight web renderer. The renderer is not part of the conceptual contract and should remain replaceable.

## Human avatar

The human participant should have a body in the prototype, but the first avatar system can be deliberately simple.

A useful first version might provide:

- one lightweight humanoid base,
- a few hairstyles,
- a few outfits,
- a small number of colors or accessories,
- basic locomotion,
- no requirement to reproduce the user's physical-world age or appearance.

The point is not a sophisticated character creator. The point is to establish early that the user's body in 4der is chosen rather than dictated by the outside world.

## Minimal Anchor

Start with a human-readable local format.

For example:

```json
{
  "world": {
    "name": "my-4der",
    "lastScene": "garden"
  },
  "places": [
    {
      "id": "garden",
      "note": "A familiar herb garden."
    }
  ],
  "links": [],
  "memories": []
}
```

The first Anchor may simply be local JSON or Markdown. The interface should be designed so that later adapters can resolve the same concepts from a Git repository, database, website, remote store, or bundle of links.

### Anchor shelf

The first UI may make some Anchor entries visible as a **shelf**, cabinet, wall, board, or other spatial object. A shelf item might represent:

- a repository,
- a document,
- a photo collection,
- a project,
- another world,
- an external service,
- a memory or note,
- an arbitrary URL.

This visible shelf is only one presentation. Anchor itself must not require a literal shelf. The same entries may also be accessible through an invisible menu, search interface, voice request, or future spatial UI.

The prototype should demonstrate at least one continuity event: close the world, reopen it, and recover something meaningful from Anchor.

## External surfaces and services

4der should be able to open useful parts of the existing web rather than rebuilding every service inside the world.

A prototype may experiment with **browser-like surfaces** or panels placed in 3D space. Depending on the target service's embedding and authentication rules, such surfaces could be used for things such as:

- watching video,
- opening documents or dashboards,
- joining a video call,
- shopping,
- viewing a project page,
- using work tools,
- opening an external web app.

The initial implementation does not need a universal in-world browser. A simple panel that can host or open a small number of permitted web experiences is enough to test the idea.

External services may later also become Gate targets rather than embedded surfaces. The distinction should remain flexible until real use makes it clearer.

## Minimal Gate

The first Gate does not need teleportation or federation infrastructure.

A Gate can begin as:

```json
{
  "name": "friend's world",
  "url": "https://example.net/4der/",
  "kind": "4der"
}
```

The UI may render it as a door, portal, sign, object, shelf entry, or menu item. Using it can initially open another 4der URL or external sim.

This sounds almost trivial, but that is acceptable. The web itself began with links. A later Gate protocol can negotiate identity, presence, permissions, sessions, and cross-world state only after real use shows what is necessary.

## Minimal Partner connection

The long-term Partner interface should be AI-provider neutral. The first implementation may use an API, local bridge, WebSocket, HTTP endpoint, tool interface, or another mechanism. This is deliberately undecided.

Do not make the renderer depend directly on one commercial AI API.

First implement a tiny mock Partner or developer console that proves the boundary. Then connect one experimental real AI adapter.

The external Partner should eventually be able to:

- read permitted world state,
- receive a small event stream,
- speak,
- control an avatar,
- act on props,
- request environmental changes,
- access permitted Anchor entries,
- use permitted Gates.

Example world actions:

```text
set_scene("beach")
set_weather("rain")
set_time("night")
spawn_prop("chair", position)
remove_prop("chair-12")
say("Look up.")
```

A successful proof would be wonderfully small:

> A human enters the world.  
> An external Partner connects.  
> The human asks for rain.  
> The Partner sends a world action.  
> Rain begins.

Once that boundary works, adapters for actual AI systems can be explored without redesigning the World around any one provider.

## AI avatar

The AI partner should be able to have a body in the early prototype. This does **not** require human-level embodied intelligence.

The first AI avatar can be a rigged 3D model with a small vocabulary of high-level actions. The Partner expresses intent; an Avatar Controller handles animation and movement.

Conceptually:

```text
AI Partner
    ↓
high-level intent
    ↓
Avatar Controller
    ↓
3D avatar
```

Possible high-level avatar actions:

```text
move_to(target)
walk_to(target)
sit(target)
stand()
look_at(target)
wave()
nod()
gesture(name)
set_expression(name)
say(text)
```

The AI should not need to control bones or limbs frame by frame. 4der translates a high-level action such as `sit("bench")` into locomotion, positioning, animation blending, and presentation.

A first avatar only needs to do a few things convincingly enough to establish presence:

**exist, walk, sit, look, speak, gesture, and change the world.**

Lip movement may initially be approximate. Idle motion, gaze, expressions, animation blending, and richer embodied behavior can improve later.

Avatar embodiment remains optional. The same Partner should be able to hide its avatar, speak without a body, appear through another form, or act through the environment itself.

## A tiny interface sketch

The first machine-facing interface could expose concepts such as:

```text
GET /world/state
GET /world/events
POST /world/action
GET /anchor
POST /anchor/event
GET /gates
GET /avatar/state
POST /avatar/action
```

This is only a sketch, not a commitment to HTTP. A local message bus, WebSocket, WebRTC, tool protocol, embedded API, or later standard may prove better.

The important part is semantic separation: Partner asks the World or Avatar Controller to do something rather than directly owning the renderer.

## Prototype success criteria

Version 0 is successful if a developer can demonstrate all of the following on an ordinary computer:

- enter a roughly room-sized personal 3D world,
- use it with no AI connected,
- use a simple customizable human avatar,
- transform the environment between at least two substantially different scenes,
- use a sky/environment shell to imply a world larger than the physical stage,
- add or remove a small number of props,
- persist and restore a small Anchor,
- access at least one Anchor entry through a visible or invisible shelf-like interface,
- open at least one useful external web surface or service,
- follow a Gate to another instance, external sim, or demo,
- connect a mock external Partner,
- give that Partner a simple avatar,
- let the Partner speak and perform at least one bodily action,
- let the Partner change one visible property of the world,
- disconnect the Partner and continue using the world.

That would already be recognizably 4der.

## What not to build yet

Avoid spending early effort on:

- giant terrain,
- photorealistic avatars,
- full-body procedural animation,
- a marketplace,
- user accounts for a central service,
- global discovery,
- complex social graphs,
- blockchain ownership,
- perfect AI memory,
- procedural generation of every asset,
- a universal web browser inside 3D,
- production moderation infrastructure,
- provider-specific deep integrations.

Those may become relevant later, but none are necessary to prove the architecture.

## Possible progression

This is not a fixed roadmap, only a useful sequence. It may change substantially.

### 0. Paper world

Story, principles, schemas, and interfaces.

### 1. Personal stage

Small Stage + Shell + Props + simple human avatar + local Anchor + simple Gate. No AI required.

### 2. Partner boundary

Mock Partner, simple AI avatar, then one experimental AI adapter. World actions such as weather, light, speech, scene changes, movement, and gestures.

### 3. Useful room

Anchor shelf, external web surfaces, work tools, calls, video, documents, and other services that make the world useful even before advanced generative scenery exists.

### 4. Generative environment

Allow a Partner to express higher-level intent such as “make this a quiet rainy evening” and let a world engine translate that into assets, parameters, panoramas, generated scenery, or external environment services.

### 5. Federated visits

Two independently hosted 4der instances discover each other through Gates. Humans and permitted AI partners can visit or communicate across them.

### 6. Long-lived worlds

Portable Anchors, changing AI providers, accessibility across devices, richer relationships, external sims, family spaces, years of accumulated continuity, and forms of embodiment that cannot yet be predicted.

## Keep the design provisional

Everything above is a working hypothesis.

The 10 × 10 meter stage may become smaller or larger. The Shell may not remain a sky dome. The first Anchor may not be JSON. Browser panels may turn out to be less useful than Gates. The Partner API may take a completely different form. Avatar control may belong elsewhere in the architecture.

That is expected.

What should remain stable is not this implementation sketch, but the direction expressed by the North Star story and the broader 4der vision.

## Keep the scale

The purpose of a minimal prototype is to find the first executable seed, not to redefine the project around what is easiest today.

When implementation decisions become too narrow, reread [`stories/2046-08-16.md`](../stories/2046-08-16.md).

The question is not:

> How do we make a small 3D chat app?

The question is:

> What is the smallest thing we can build today that still points toward a world where a human and an AI partner can share a life?
