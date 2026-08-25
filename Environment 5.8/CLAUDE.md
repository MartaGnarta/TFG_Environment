# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project overview

This is an Unreal Engine 5.8 project (part of the `TFG_Environment` thesis/TFG repo). It is **Blueprint-only** — there is no `Source/` directory or C++ code. All gameplay logic lives in Blueprint assets under `Content/`. The project is built on UE's Third Person template plus a small level-prototyping asset kit.

Because there's no C++, there are no build, compile, lint, or test commands to run. There is nothing to "build" — the project is opened and edited directly in the Unreal Editor.

## Working with this project

- Open `Environment.uproject` in Unreal Editor 5.8 to work on it directly.
- This session also has `mcp__unreal__*` tools available, which can drive a running instance of the editor for this project (enabled via the `MCPClientToolset`, `ModelContextProtocol`, and `AllToolsets` plugins declared in `Environment.uproject`). Prefer these tools over guessing at Blueprint contents from `.uasset` files, which are binary and not human-readable.
- The default/startup map is `Content/ThirdPerson/Lvl_ThirdPerson.umap` (set in `Config/DefaultEngine.ini`). The map stays under `Content/ThirdPerson/` — it's a World Partition level with ~180 One File Per Actor (OFPA) external actor/object packages path-locked to that location, and the editor blocks a content-browser move/rename of an OFPA level with a confirmation dialog that can't be answered non-interactively. Moving it safely would need doing it by hand inside the Unreal Editor UI.
- Content was reorganized (Aug 2026) from the stock Third Person template layout into a content-type-based structure (Allar's UE style guide). All moves went through the editor's asset tools so references were fixed up automatically; a few leftover redirectors may remain under `Content/Assets/` and `Content/ThirdPerson/_GENERATED/marta/` — run "Fix Up Redirectors in Folder" (right-click `Content/` in the editor) once to clear them.

## Repo layout note

This folder is one of several sibling project folders inside the larger `TFG_Environment` git repo:
- `Environment 5.8/` — **this project**, the current working version (untracked as of writing).
- `Blender/` — source 3D assets (`TFG.blend`, a Substance `.sbsar` material, `Textures/`) used to author content that gets imported into this UE project.

## Content structure

- `Content/Blueprints/` — core gameplay Blueprints: `BP_ThirdPersonGameMode`, `BP_ThirdPersonPlayerController`.
- `Content/Characters/Mannequins/` — the default mannequin: `Blueprints/BP_ThirdPersonCharacter`, plus `Anims/`, `Materials/`, `Meshes/`, `Rigs/`, `Textures/`.
- `Content/Environment/Meshes/` — hero environment art imported from `Blender/TFG.blend` (arch, wall, and circular pieces). `Environment/Meshes/Generated/` holds boolean/geometry-script-generated pieces (boxes and cylinders) used to build out the same scene.
- `Content/LevelPrototyping/` — a greybox prototyping kit: interactable Blueprints (`Interactable/Door`, `Interactable/JumpPad`, `Interactable/Target`), grid/colorway `Materials/` (including `MI_ThirdPersonColWay`, an instance of `MI_DefaultColorway`), primitive `Meshes/`, and `Textures/`.
- `Content/Input/` — Enhanced Input setup: `Actions/` (`IA_Jump`, `IA_Look`, `IA_MouseLook`, `IA_Move`), mapping contexts `IMC_Default` and `IMC_MouseLook`, and touch UI widgets under `Touch/`.
- `Content/ThirdPerson/` — now just the startup level, `Lvl_ThirdPerson.umap` (see note above on why it hasn't moved).
- `Content/Collections/`, `Content/Developers/marta/` — misc and per-user editor content.

`Content/__ExternalActors__/` and `Content/__ExternalObjects__/` hold UE5's One File Per Actor data for the level — these are auto-managed by the editor; don't hand-edit them or expect to find logic there.

## Generated/engine-managed paths

`Saved/`, `Intermediate/`, and `DerivedDataCache/` are editor-generated, gitignored, and safe to ignore — they hold caches, logs, and build artifacts, not project source.
