# Hybrid State Machine
A lightweight state machine for Unity, designed to be friendly
for both beginners and experienced programmers.

## Requirements
- Unity 6000.0b5 or higher
- Unity Input System package (required for `InputBinding`)

## Installation
Install via the Unity Package Manager:
1. Open Package Manager (Window > Package Manager)
2. Click the **+** button > Add package by name
3. Enter: `com.nofraag.hybridstatemachine`

## Features
- **Illegal States** — define conflicting states using `illegalStates`
  with `stateWeight` to resolve battles between them
- **State Bindings** — subscribe to events easily using `StateBinding`
  with full operation support
- **OneShot & Cooldown** — via `StateEntry`, choose if a state is
  `oneshot` (wiped on removal) or has a `cooldown` before reactivation
- **State Lifecycle** — control what your state does with `OnAdd`
  (called on activation), `OnRemoval` (called on removal),
  and `OnUpdate` (called every Unity update)
- **Custom Bindings** — create your own `StateBinding` by implementing
  `Evaluate` (your bool condition) and `Transcript` (inspector label)
- **4 Built-in Bindings** — `InputBinding`, `ConditionBinding`,
  `TimedBinding`, and `BindingFolder` cover most common use cases
- **Readable Inspector** — view state history for `subscribedState`
  and `currentState`, including their bindings, transcripts,
  active state, time of usage, and manual add/remove support

## Quick Start
### 1. Create a State
```csharp
public class FocusedState : State
{
    public override float stateWeight => 0.5f;

    public override List<State> illegalStates => new List<State>
    {
        new SprintingState()
    };

    public override void OnAdd()     => Debug.Log("Focused started.");
    public override void OnRemoval() => Debug.Log("Focused ended.");
    public override void OnUpdate()  => Debug.Log("Focusing...");
}
```

### 2. Subscribe a State
```csharp
stateMachine.subscribeState(
    new FocusedState(),
    new StateEntry
    {
        bindings = new List<StateBinding>
        {
            new InputBinding(input.actions["RightClick"])
        }
    }
);
```

### 3. Or Set a State Directly
```csharp
stateMachine.setState(new FocusedState());
```

For the full documentation visit: [\[docs link here\]](https://nofraag.github.io/Hybrid-State-Machine--Docs/)

## Changelog
See CHANGELOG.md

## License
See LICENSE.md

## Planned
- Visual blueprint editor *(not actively in development)*
