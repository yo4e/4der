# 4der Architecture Sketch

Status: early concept. Names and boundaries may change.

4der currently separates the idea into four parts so that the world can remain useful even when an AI partner is unavailable.

## 1. World

**World is “now and here.”**

It owns or coordinates the current executable environment:

- scene and spatial structure,
- time and time-of-day,
- weather,
- lighting,
- sound,
- physics,
- objects and their state,
- human presence and avatars,
- rendering or references to an external renderer.

World does not need to own a permanent map. A world may reconstruct or replace scenes at runtime. The garden, office, beach, city, and night sky can all be states of the same 4der.

A minimal World may be a single web scene. A future World may delegate large parts of rendering or generation to external engines.

## 2. Anchor

**Anchor is “what continues.”**

Anchor is intentionally not defined as one database format. It is an abstraction for the traces that let a 4der remain itself across sessions, devices, scene regeneration, AI-provider changes, and long periods of time.

An Anchor may include:

- memories and episode summaries,
- places and their meanings,
- objects or possessions,
- user and partner preferences,
- project references,
- relationship history,
- permissions,
- world configuration,
- links to photos, documents, repositories, media, or external services,
- a history of Gate visits,
- references to other Anchors.

Possible Anchor backends include:

- local files,
- JSON,
- Markdown,
- SQLite or another database,
- a Git repository,
- a personal website,
- a list of URLs,
- remote storage,
- future personal data systems.

The important part is not where the data lives. The important part is that World and permitted participants can resolve continuity through a stable Anchor interface.

An Anchor can therefore be thought of as both storage **and a map to storage**.

## 3. Gate

**Gate is “elsewhere.”**

A Gate connects one 4der to another world or external simulation.

At the smallest scale, a Gate may be only a URL with some metadata. Later versions may support negotiated capabilities, identity, permissions, presence transfer, asset exchange, shared sessions, or federation.

Potential Gate targets include:

- another user's 4der,
- a public shared world,
- a shop or service sim,
- a game world,
- a work environment,
- a family space,
- a temporary event.

A Gate should not imply that all worlds share one owner, physics model, renderer, AI provider, or data store.

Long term, Gate is what turns many personal worlds into a network.

## 4. Partner

**Partner is “someone else acting here.”**

Partner is an optional interface for an external intelligence or autonomous agent. An AI partner should be able to enter a 4der without the World being built specifically for that AI vendor.

A possible Partner capability model includes:

- `observe` — receive permitted world state and events,
- `speak` — emit speech, text, or other communicative output,
- `move` — control a body or point of presence,
- `act` — manipulate permitted objects or tools,
- `shape_world` — request changes to weather, light, sound, scene, or generated environment,
- `anchor.read` — access permitted continuity,
- `anchor.write` — add permitted traces or memories,
- `gate.use` — participate in travel or cross-world communication.

Capabilities should be permissioned. An AI that can speak in a room does not automatically need permission to replace the landscape, read private memories, or open a Gate.

Partner should be provider-neutral. A ChatGPT connector, another hosted assistant, a local model, a scripted agent, or a future system should all be able to target the same conceptual interface.

## AI absence is a valid state

A key architectural rule is:

> **World + Anchor + Gate must still make sense without Partner.**

If the AI service is down, disconnected, changed, or intentionally absent, the user should still be able to enter their world, access its continuity, and use its Gates.

This prevents 4der from becoming a fragile visual wrapper around one AI API.

## Human and AI embodiment

Embodiment should be treated as a replaceable presentation layer.

A human may use:

- first-person presence,
- a young or old human avatar,
- a stylized avatar,
- an abstract form,
- accessibility-oriented representations.

An AI may use:

- a persistent avatar,
- temporary bodies,
- voice only,
- environmental effects,
- multiple manifestations,
- no visible form,
- the world itself as a medium of expression.

Neither identity should be hard-bound to one mesh or one body.

## A rough relationship

```text
                    Anchor
               continuity / refs
                       │
                       ▼
Human presence ────── World ────── Gate ────── other worlds
                       ▲
                       │
                    Partner
               optional external AI
```

This diagram is deliberately simple. Implementations may split rendering, simulation, identity, permissions, networking, and storage into additional services.

## Open questions

- How should a 4der instance identify itself without requiring a central registry?
- What is the minimum useful Anchor schema?
- Which Anchor data should be portable across worlds, and which should remain private?
- What does crossing a Gate mean: opening a link, moving presence, copying state, or negotiating a shared session?
- How should two AI partners authenticate and communicate across worlds?
- How should world-changing capabilities be permissioned and audited?
- What parts of generated scenery should persist, and what parts should be ephemeral?
- How can a world remain usable over decades as renderers, models, and devices change?

These questions should remain open until prototypes make them concrete.
