# Minimal 4der Prototype

Status: concept only. This document describes a deliberately small first implementation without shrinking the long-term vision.

## Goal

Build the smallest 4der that proves four things:

1. a personal world can exist independently of an AI,
2. the world can change form without losing continuity,
3. continuity can live outside the renderer,
4. an external partner can observe and alter the world through a small interface.

The prototype does **not** need to prove real-time generative 3D, federation at scale, persistent AI identity, photorealism, VR, or a production-ready social system.

## North-Star slice

The first prototype can borrow directly from the vision story:

- **Garden** — quiet outdoor scene with herbs and a bench,
- **Office** — desk, chair, shelf, and binder-like object,
- **Beach** — sea, sky, weather, and time-of-day controls.

These do not need to be three permanent maps. They can simply be three scene states or presets that demonstrate that one 4der can transform around the user.

## Minimal World

A browser-based 3D scene is enough for the first version.

Minimum capabilities:

- enter the world without logging into an AI service,
- move or look around,
- switch among a few scene states,
- change time of day,
- change weather,
- change a small number of environmental properties,
- expose current state in a machine-readable form.

Possible implementation technologies include Three.js, Babylon.js, or another lightweight web renderer. The renderer is not part of the conceptual contract and should be replaceable.

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

The prototype should demonstrate at least one continuity event: close the world, reopen it, and recover something meaningful from Anchor.

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

The UI may render it as a door, portal, sign, object, or menu entry. Using it can initially open another 4der URL.

This sounds almost trivial, but that is acceptable. The web itself began with links. A later Gate protocol can negotiate identity, presence, permissions, sessions, and cross-world state only after real use shows what is necessary.

## Minimal Partner

Do not start by integrating a commercial LLM.

First implement a tiny mock Partner or developer console that proves the boundary.

The external process should be able to:

- read current world state,
- receive a small event stream,
- send a line of speech or text,
- request one or more world actions.

Example actions:

```text
set_scene("beach")
set_weather("rain")
set_time("night")
say("Look up.")
```

A successful proof would be wonderfully small:

> A human enters the world.  
> An external Partner connects.  
> The human asks for rain.  
> The Partner sends a world action.  
> Rain begins.

Once that boundary works, adapters for actual AI systems can be explored without redesigning the World around any one provider.

## A tiny interface sketch

The first machine-facing interface could expose concepts such as:

```text
GET /world/state
GET /world/events
POST /world/action
GET /anchor
POST /anchor/event
GET /gates
```

This is only a sketch, not a commitment to HTTP. A local message bus, WebSocket, WebRTC, tool protocol, or embedded API may prove better.

The important part is semantic separation: Partner asks the World to do something rather than directly owning the renderer.

## Prototype success criteria

Version 0 is successful if a developer can demonstrate all of the following on an ordinary computer:

- enter a small personal 3D world,
- use it with no AI connected,
- transform the environment between at least two substantially different scenes,
- persist and restore a small Anchor,
- follow a Gate to another instance or demo,
- connect a mock external Partner,
- let that Partner change one visible property of the world,
- disconnect the Partner and continue using the world.

That is enough.

## What not to build yet

Avoid spending early effort on:

- giant terrain,
- realistic human avatars,
- a marketplace,
- user accounts for a central service,
- global discovery,
- complex social graphs,
- blockchain ownership,
- perfect AI memory,
- procedural generation of every asset,
- production moderation infrastructure,
- provider-specific deep integrations.

Those may become relevant later, but none are necessary to prove the architecture.

## Possible progression

This is not a fixed roadmap, only a useful sequence:

### 0. Paper world

Story, principles, schemas, and interfaces.

### 1. Personal world

World + local Anchor + simple Gate. No AI required.

### 2. Partner boundary

Mock Partner, then one experimental AI adapter. World actions such as weather, light, speech, and scene changes.

### 3. Generative environment

Allow a Partner to express higher-level intent such as “make this a quiet rainy evening” and let a world engine translate that into assets, parameters, or generated scenery.

### 4. Federated visits

Two independently hosted 4der instances discover each other through Gates. Humans and permitted AI partners can visit or communicate across them.

### 5. Long-lived worlds

Portable Anchors, changing AI providers, accessibility across devices, richer relationships, external sims, work tools, family spaces, and years of accumulated continuity.

## Keep the scale

The purpose of a minimal prototype is to find the first executable seed, not to redefine the project around what is easiest today.

When implementation decisions become too narrow, reread [`stories/2046-08-16.md`](../stories/2046-08-16.md).

The question is not:

> How do we make a small 3D chat app?

The question is:

> What is the smallest thing we can build today that still points toward a world where a human and an AI partner can share a life?
