# Event Simulation

SharpHook provides the ability to simulate keyboard and mouse events in a cross-platform way as well. It provides the
`IEventSimulator` interface, and the default implementation, `EventSimulator`, which calls `UioHook.PostEvent` to
simulate the events. The methods in this interface return a `UioHookResult` to specify whether the event was simulated
successfully, or not.

Here's a quick example:

```C#
using SharpHook;
using SharpHook.Native;

// ...

var simulator = new EventSimulator();

// Press Ctrl+C
simulator.SimulateKeyPress(KeyCode.VcLeftControl);
simulator.SimulateKeyPress(KeyCode.VcC);

// Release Ctrl+C
simulator.SimulateKeyRelease(KeyCode.VcC);
simulator.SimulateKeyRelease(KeyCode.VcLeftControl);

// Press the left mouse button at (0, 0)
simulator.SimulateMousePress(0, 0, MouseButton.Button1);

// Release the left mouse button at (0, 0)
simulator.SimulateMouseRelease(0, 0, MouseButton.Button1);

// Move the mouse pointer to (0, 0)
simulator.SimulateMouseMovement(0, 0);

// Scroll the mouse wheel at (0, 0)
simulator.SimulateMouseWheel(0, 0, 2, -120);
```

**Note**: When simulating mouse button pressing/releasing or scrolling, the mouse pointer coordinates are required. If
you need to do that at the current coordinates, then simply track the coordinates with a global hook.

Windows defines a single 'step' of a mouse wheel as rotation value 120.

Mouse wheel simulation is a little inconsistent across platforms, and not documented. View the source code of libuiohook
for more details.

Next article: [Logging](logging.md).
