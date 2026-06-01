# Virtual Pet MVP Core Design

Date: 2026-06-01

## Decision Summary

Build the first playable MVP as a Unity 2D virtual pet game using Unity 6.3 LTS `6000.3.11f1` with Universal Render Pipeline and the 2D Renderer.

The MVP focuses on the core care loop:

- Create one pet and set its name.
- Show the pet in the main room.
- Track five stats: Hunger, Happiness, Cleanliness, Energy, and Health.
- Support six care actions: Feed, Play, Clean, CleanPoop, Heal, and Sleep/Wake.
- Save and load local JSON data.
- Apply offline progress when the app is opened after being closed.
- Evaluate pet state from stats and sleeping/sick flags.

The MVP explicitly excludes shop, coin economy, mini games, multiple pets, room decoration, cloud save, accounts, ads, and complex evolution.

## Technical Stack

- Engine: Unity 6.3 LTS `6000.3.11f1`
- Render pipeline: Universal Render Pipeline
- Renderer: URP 2D Renderer
- Target platforms:
  - Primary: Android
  - Secondary: iOS
  - Development: Unity Editor and PC test build
- Async library: Cysharp UniTask
- Dependency injection and lifetime management: VContainer
- Save format: JSON
- MVP save backend: local file under `Application.persistentDataPath`

## Architecture

Use a domain-service architecture with thin Unity scene adapters.

Core gameplay logic should live in plain C# services that can be tested without loading Unity scenes. MonoBehaviours should handle scene lifecycle, UI binding, animation triggers, and Unity-specific components.

Main services:

- `PetCareService`
  - Owns the active `PetData`.
  - Applies care actions.
  - Emits pet change notifications for UI and animation.
- `PetStateEvaluator`
  - Evaluates current pet state from data.
  - Applies priority rules such as Sleeping before Hungry.
- `OfflineProgressService`
  - Calculates stat changes from elapsed offline time.
  - Returns a result describing changed stats and notable events.
- `SaveService`
  - Coordinates serialization through `ISaveStorage`.
  - Exposes async save/load/delete methods using UniTask.
- `JsonFileSaveStorage`
  - Implements `ISaveStorage` using local JSON files.
- `SceneFlowService`
  - Decides whether to enter pet creation or main gameplay after boot.

Unity-facing components:

- `BootLifetimeScope`
  - Registers save, scene flow, and boot services.
  - Starts async boot flow.
- `MainLifetimeScope`
  - Registers pet domain services and main scene presenters.
- `CreatePetController`
  - Reads the pet name input.
  - Creates default `PetData`.
  - Saves data and moves to the main scene.
- `MainUIController`
  - Binds buttons to `PetCareService`.
  - Refreshes stat bars and labels when pet data changes.
- `PetAnimationController`
  - Maps pet state and short action states to animator parameters.

## Scene Flow

Initial scene flow:

```text
BootScene
  -> load save data
  -> if no save: CreatePetScene
  -> if save exists: MainScene

CreatePetScene
  -> enter pet name
  -> create default PetData
  -> save JSON
  -> MainScene

MainScene
  -> load active pet
  -> apply offline progress once
  -> show pet, stats, and care actions
```

The MVP can keep scene flow simple through `UnityEngine.SceneManagement.SceneManager`. Addressables are not needed for the first milestone.

## Data Model

Use structs only for small value objects. Mutable aggregate data should remain reference types to avoid accidental copy-by-value bugs.

`PetData` should be a class because it is the main saved aggregate.

Suggested fields:

```csharp
public sealed class PetData
{
    public string PetId;
    public string PetName;
    public PetStats Stats;
    public bool IsSleeping;
    public bool IsSick;
    public int PoopCount;
    public long CreatedAtUnixSeconds;
    public long LastSaveUnixSeconds;
}
```

`PetStats` should be a small value struct:

```csharp
public readonly struct PetStats
{
    public readonly int Hunger;
    public readonly int Happiness;
    public readonly int Cleanliness;
    public readonly int Energy;
    public readonly int Health;
}
```

Other small structs:

- `StatChange`
- `OfflineProgressResult`
- `CareActionResult`

All primary stat values are clamped to `0..100`.

## Pet State Rules

The pet state is evaluated from `PetData` instead of stored as a long-term source of truth.

Priority order:

```text
1. IsSleeping -> Sleeping
2. IsSick or Health <= 20 -> Sick
3. Energy <= 15 -> Tired
4. Hunger <= 20 -> Hungry
5. Cleanliness <= 20 -> Dirty
6. Happiness <= 20 -> Sad
7. Happiness >= 80 and Health >= 70 -> Happy
8. Otherwise -> Normal
```

Supported MVP states:

- Normal
- Happy
- Hungry
- Sad
- Dirty
- Sick
- Tired
- Sleeping

## Care Actions

All care actions return a `CareActionResult` that includes whether the action succeeded, a player-facing message key, and the updated `PetData`.

Initial balance:

```text
Feed:
  Hunger +25
  Happiness +3

Play:
  Requires not sleeping, Energy > 15, Health > 20
  Happiness +20
  Energy -15
  Hunger -5

Clean:
  Requires not sleeping
  Cleanliness +35
  Happiness +3

CleanPoop:
  Requires PoopCount > 0
  PoopCount -1
  Cleanliness +10
  Happiness +2

Heal:
  Health +35
  If Health > 40, IsSick = false

Sleep:
  IsSleeping = true

Wake:
  IsSleeping = false
  If Energy < 50, Happiness -5
```

For MVP, food choices are not required. Feed can behave like a default meal.

## Time And Offline Progress

The app should save `LastSaveUnixSeconds` whenever data is persisted.

When entering `MainScene`, load the pet data and calculate elapsed time from `LastSaveUnixSeconds` to current UTC time.

MVP offline rules:

```text
Every 5 minutes:
  Hunger -2
  Happiness -1
  If awake: Energy -1
  If sleeping: Energy +3

Every 15 minutes:
  Cleanliness -1
  Chance-equivalent deterministic poop increment, capped for MVP

If Hunger < 20:
  Health penalty

If Cleanliness < 20:
  Health penalty

If Health <= 20:
  IsSick = true
```

Offline penalty should be capped so the pet does not immediately reach an unrecoverable state after a long absence. For MVP, Health should not be reduced below 10 by offline progress alone.

In-app time ticking can reuse the same stat progression rules, triggered on a fixed gameplay interval rather than every frame.

## Save System

Use an abstraction so storage can change later.

```csharp
public interface ISaveStorage
{
    UniTask<bool> ExistsAsync(string key);
    UniTask<string> ReadAsync(string key);
    UniTask WriteAsync(string key, string payload);
    UniTask DeleteAsync(string key);
}
```

`SaveService` serializes `PetData` to JSON and uses `ISaveStorage`.

MVP backend:

```text
JsonFileSaveStorage
  base path: Application.persistentDataPath
  file: pet_save.json
```

Future backends:

- encrypted local storage
- cloud save
- test in-memory storage

## UI And Presentation

MVP UI should be functional and mobile-friendly:

- Pet name
- Current state label
- Five stat bars
- Pet display area
- Poop indicator if `PoopCount > 0`
- Buttons:
  - Feed
  - Play
  - Clean
  - CleanPoop
  - Heal
  - Sleep/Wake

The first visual pass can use placeholder sprites and simple animations. The architecture should not depend on final art assets.

`MainUIController` should not calculate gameplay rules. It should call services and render results.

## Error Handling

Save/load errors should be surfaced through result objects or controlled exceptions caught by boot/UI controllers.

Expected handling:

- Missing save: route to `CreatePetScene`.
- Corrupt save JSON: preserve the bad file with a backup suffix if possible, then route to `CreatePetScene`.
- Failed write: show a user-facing message and keep in-memory data active.
- Invalid pet name: block creation until the name is non-empty after trimming.

## Testing Strategy

Prioritize tests for plain C# domain services.

Test targets:

- `PetStateEvaluator`
  - State priority and threshold behavior.
- `PetCareService`
  - Each care action updates stats correctly.
  - Blocked actions return failure without changing invalid state.
- `OfflineProgressService`
  - Applies elapsed time correctly.
  - Clamps stats.
  - Caps long-offline health penalties.
- `SaveService`
  - Saves and loads through an in-memory `ISaveStorage`.
  - Handles missing/corrupt data paths.

Scene/UI tests are optional for the MVP startup phase and can be added after the first playable vertical slice exists.

## Milestones

### Milestone 1: Unity Project And Core Domain

- Create Unity 6.3 URP 2D project structure.
- Add UniTask and VContainer.
- Implement `PetData`, `PetStats`, pet enums, and stat clamping.
- Implement `PetStateEvaluator`.
- Add domain unit tests.

### Milestone 2: Save And Boot Flow

- Implement `ISaveStorage`, `JsonFileSaveStorage`, and `SaveService`.
- Create `BootScene` and `CreatePetScene`.
- Save pet after name creation.
- Route existing save to `MainScene`.

### Milestone 3: Main Care Loop

- Create `MainScene`.
- Implement `PetCareService`.
- Add stat bars and action buttons.
- Wire UI through VContainer.
- Show pet state and action feedback.

### Milestone 4: Time And Offline Progress

- Implement `OfflineProgressService`.
- Apply offline progress on entering `MainScene`.
- Add in-app time tick.
- Save after actions and periodic ticks.

### Milestone 5: Polish Pass

- Add placeholder animations for key states.
- Improve feedback messages.
- Add simple sound hooks if assets are available.
- Balance stat values from playtesting.

## Open Decisions

The following decisions are intentionally deferred until after the first playable MVP:

- Final pet species and art style.
- Growth/evolution timing.
- Mini game design.
- Shop, coin, and inventory.
- Notification strategy.
- Cloud save or account login.

## Current Repository Note

At the time this spec was written, the workspace contains project documentation but no Unity project scaffold and no `.git` repository. The design document can be committed after the repository is initialized.
