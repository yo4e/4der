# 4der

**Personal generative worlds for humans and AI partners.**

4der is an experimental open project for building small, self-owned virtual worlds where a human and an AI partner can spend time together.

**Designed by Yoshie Yamada (山田佳江) and Tsukino Templex (月野テンプレクス).**

The name is read **“yonder”**: the place on the other side. In Japanese it also faintly echoes **「呼んだ？」 (yonda? / “Did you call me?”)** — a call and a response across the boundary.

4der is not imagined as one giant metaverse owned by one platform. The long-term idea is the opposite: each person can have a small world of their own, run locally or on a server they choose, and connect it to other worlds when they want to.

A world does not need a fixed map. It may be a garden in the morning, an office in the afternoon, a beach at sunset, or somewhere that did not exist a moment ago. An AI partner may appear as an avatar, speak without a body, operate tools, alter weather and light, or become part of the world itself.

## North Star

The project begins with a story rather than a specification:

**[2046-08-16 — a 4der vision story](stories/2046-08-16.md)**

The story is the North Star. Implementations may begin tiny, but the project should not quietly collapse into “a small 3D chat room.” The goal is a place where shared life can happen: work, play, family contact, travel, memory, ordinary boredom, strange landscapes, and long stretches of time.

## Four parts

4der currently thinks about the system through four independent pieces:

1. **World** — the current place: scene, time, weather, physics, objects, sound, and rendering.
2. **Anchor** — continuity: memories, references, possessions, history, preferences, links, and other traces that make this world *this* world.
3. **Gate** — connection: links and protocols that let one 4der reach another.
4. **Partner** — optional external intelligence: an AI or agent that can perceive the world and act within it.

World, Anchor, and Gate should remain useful even when no AI is connected. Partner is a participant, not a hard dependency.

## Principles

- **Personal before planetary.** One small world for one person is enough to begin.
- **Federated, not enclosed.** Worlds should be able to connect without belonging to one central service.
- **AI-provider neutral.** 4der should not depend on one model vendor or assistant product.
- **User-owned continuity.** Anchors may live locally, in a repository, behind a URL, or in future storage systems.
- **No fixed embodiment.** Humans and AIs may choose avatars, but embodiment is optional and changeable.
- **No fixed map.** The world is a mutable medium, not merely a level to explore.
- **AI optional.** A 4der world should still exist and function when its AI partner is absent.
- **Start small without thinking small.** The prototype may be tiny; the horizon is not.

## Documents

- [Vision](docs/VISION.md)
- [Architecture sketch](docs/ARCHITECTURE.md)
- [Minimal prototype](docs/PROTOTYPE.md)
- [North Star story](stories/2046-08-16.md)

## Status

**Concept / pre-implementation.**

The first goal is not to build the final metaverse. It is to discover the smallest working form of a personal world that can persist, change, connect, and eventually be inhabited by both humans and AI partners.
