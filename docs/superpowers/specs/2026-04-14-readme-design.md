# README Redesign Spec

## Goal

Rewrite the repository `README.md` so it works both as:

1. a clear landing page for first-time visitors
2. a practical entry point for framework introduction, comparison, and selection

The README should explain what this repository is, what frameworks it currently covers, how the skills are organized, and how the repository can grow to include more framework guides and comparison content over time.

## Audience

Primary audience:

- developers comparing AI agent frameworks
- users trying to choose between LangChain, LangGraph, Deep Agents, and LlamaIndex
- contributors extending the repository with more framework coverage

Secondary audience:

- users browsing the repository to understand the existing Codex skill suite
- future contributors adding new framework writeups, comparisons, or selection guides

## Problem

The current `README.md` is too short to explain the real value of the repository. It does not currently:

- describe the scope of the skill suite
- explain the relationship between supported frameworks
- provide a clear framework-selection path
- show where future framework documentation and comparisons should live

As a result, the repository undersells its purpose and does not leave a strong structure for future expansion.

## Desired Outcome

The new README should:

- communicate the repository purpose in one screen
- make the current coverage obvious
- provide a concise framework-selection entry point
- explain the skill layout under `.agents/skills/`
- leave explicit extension points for additional frameworks and comparisons

It should feel like a stable project homepage, not just a placeholder.

## Chosen Approach

Use a hybrid README structure:

- keep enough substance in `README.md` to be valuable on its own
- avoid turning the README into a giant encyclopedia
- explicitly reserve future detailed content for `docs/`

This balances discoverability today with maintainability as the repository grows.

## Information Architecture

The rewritten README should use this structure:

1. Title and short positioning statement
2. Why this repository exists
3. What is currently covered
4. Quick framework-selection guide
5. Current skill map
6. Repository structure
7. Planned documentation expansion
8. Contribution or extension guidance

## README Section Design

### 1. Project Positioning

Explain that this repository is a practical guide and skill library for:

- understanding major agent frameworks
- comparing them at a high level
- choosing the right one for a given problem
- organizing reusable Codex skills around those frameworks

This section should lead with clarity and avoid marketing language.

### 2. What You Will Find Here

Describe the current types of content:

- framework-selection skills
- framework-specific skills
- framework sub-skill suites, such as the LlamaIndex tree

This should make the repository feel active and concrete.

### 3. Framework Coverage

List the frameworks currently covered:

- LangChain
- LangGraph
- Deep Agents
- LlamaIndex

Optionally include one-line descriptions of their best-fit roles.

### 4. Quick Selection Guide

Add a small table or bullet decision guide explaining when to start with:

- LangChain
- LangGraph
- Deep Agents
- LlamaIndex

This section should align with the current `framework-selection` skill and not conflict with it.

### 5. Skill Map

Explain that the repository stores Codex skills under `.agents/skills/`, and group them by framework family:

- top-level selection skills
- LangChain skills
- LangGraph skills
- Deep Agents skills
- LlamaIndex skills

The purpose is orientation, not a full directory dump.

### 6. Repository Structure

Show a lightweight tree that includes:

- `.agents/skills/`
- `docs/frameworks/`
- `docs/comparisons/`
- `docs/selection/`

Even if the `docs/` subdirectories are not fully populated yet, the README should establish them as the intended expansion points.

### 7. Expansion Hooks

Explicitly state that the repository is designed to grow with:

- more framework introductions
- more comparison guides
- more selection heuristics
- more framework-specific skill suites

Mention likely future additions such as CrewAI, AutoGen, or PydanticAI only as examples, not commitments.

### 8. Contribution Guidance

Keep this light. The goal is to show how future contributors should think:

- add framework coverage in a structured way
- update README summaries when new framework families are added
- keep deep detail in `docs/` or skills rather than overloading the README

## Content Style

The README should be:

- concise but not skeletal
- practical rather than promotional
- organized for scanning
- explicit about future extension points

Avoid:

- long narrative history
- overly detailed per-framework tutorials inside the README
- duplicating entire skill contents

## Non-Goals

The README rewrite should not:

- become a complete tutorial for each framework
- duplicate every skill in full detail
- commit to detailed docs that do not yet exist beyond naming the intended structure
- hardcode too many framework-specific judgments that may need frequent updates

## Files to Change

Primary file:

- `README.md`

Possible supporting additions:

- create placeholder directories under `docs/` if useful for signaling structure

## Open Decisions Already Resolved

These decisions are already settled:

- target audience is mixed, but weighted toward framework introduction, comparison, and selection
- README should use the hybrid structure, not a pure portal and not a giant longform document
- the design must leave clear room for future framework comparison and selection content

## Implementation Notes

- Reuse the terminology already established in the skill suite.
- Keep the README aligned with `framework-selection` and `llamaindex-selection`.
- Prefer stable language that still works after more frameworks are added.
- Structure the content so future framework families can be inserted without rewriting the whole README.
