# Test Charter — Reset App & Keyboard Shortcut

## 1. Feature Area

**Reset App / Keyboard Shortcut**

---

## 2. Objective

Verify that the Reset App functionality can be triggered through its
available user interface and documented keyboard shortcut, and that
the application behaves consistently when the reset operation is
invoked under normal, failure, and edge-case conditions.

The primary focus is to determine:

- Whether the Reset App action can be successfully triggered.
- Whether the documented keyboard shortcut invokes the same action.
- Whether the application provides appropriate feedback when the
  operation cannot be completed.
- Whether reset behavior remains consistent across relevant application
  states and environmental conditions.
- Whether the application remains stable when the reset operation is
  interrupted or performed under unusual conditions.

---

## 3. Environment

### Primary Environment

- OS: Windows 11 Home Single Language
- Version: 25H2
- OS Build: 26200.9457
- Device: ASUS TUF A17
- CPU: AMD Ryzen 7 4800H
- RAM: 8 GB
- GPU: NVIDIA GeForce RTX 3050 4 GB + AMD Radeon Graphics
- Architecture: 64-bit, x64-based processor
- Bolt Version: 0.1.162
- Bolt Build: 22f4dd5d+457ed915b+a1abb511
- Edition: Enterprise
- Platform: Desktop
- Installation Type: Fresh installation

### Network Conditions

Testing should be performed under:

- Online
- Offline
- Network transition where relevant

---

## 4. Starting State

Unless a specific scenario requires another state:

- Bolt is installed and launches successfully.
- The main application window is fully loaded.
- No modal dialog is open.
- The application is in a stable/idle state.
- The documented Reset App shortcut is visible/available through the
  application menu when required for verification.

---

# 5. Happy Path Testing

## HP-01 — Reset App through the application menu

### Objective

Verify that the Reset App command available through the Bolt menu
can successfully trigger the reset operation.

### Steps

1. Launch Bolt.
2. Wait until the application is fully loaded.
3. Open the Bolt menu.
4. Select `Reset App`.
5. Observe the application behavior.
6. Verify the resulting application state.

### Expected

The Reset App action should execute successfully according to the
product's defined reset behavior.

---

## HP-02 — Verify documented keyboard shortcut

### Objective

Verify that the documented keyboard shortcut invokes the same Reset App
action as the menu command.

### Steps

1. Launch Bolt.
2. Wait until the main application window is fully loaded.
3. Ensure the Bolt menu is closed.
4. Ensure the main application window has focus.
5. Press `Shift + Windows + Backspace`.
6. Wait for the application to respond.
7. Observe the resulting application state.

### Expected

The keyboard shortcut should trigger the same Reset App action as:

`Bolt → Reset App`

---

## HP-03 — Compare menu and keyboard invocation

### Objective

Verify behavioral consistency between the menu command and its
documented keyboard shortcut.

### Steps

1. Execute `Bolt → Reset App`.
2. Record the observable result.
3. Return the application to an appropriate test state.
4. Execute `Shift + Windows + Backspace`.
5. Compare the result with the menu invocation.

### Expected

Both invocation methods should trigger the same Reset App operation.

---

# 6. Failure Path Testing

## FP-01 — Shortcut with message input focused

### Objective

Verify that the Reset App shortcut behaves correctly when the message
input field has focus.

### Steps

1. Launch Bolt.
2. Focus the message input field.
3. Press `Shift + Windows + Backspace`.
4. Observe the application.

### Expected

The documented Reset App shortcut should behave according to the
product's intended keyboard shortcut behavior and should not be
incorrectly intercepted by the focused input control.

---

## FP-02 — Shortcut with another text field focused

### Objective

Verify shortcut behavior when another text input/control has focus.

### Steps

1. Navigate to a screen containing a text field.
2. Place keyboard focus in the field.
3. Press `Shift + Windows + Backspace`.
4. Observe the application.

### Expected

The application should handle the documented shortcut consistently
with its defined shortcut behavior.

---

## FP-03 — Shortcut while the application menu is open

### Objective

Determine whether the shortcut behaves differently when the Bolt menu
is open.

### Steps

1. Launch Bolt.
2. Open the Bolt menu.
3. Press `Shift + Windows + Backspace`.
4. Observe the application.

### Expected

The shortcut should either trigger Reset App or follow the documented
menu/shortcut interaction behavior without causing an unexpected state.

---

## FP-04 — Shortcut while offline

### Objective

Determine whether Reset App shortcut behavior depends on network
connectivity.

### Steps

1. Launch Bolt while offline.
2. Ensure the main window has focus.
3. Press `Shift + Windows + Backspace`.
4. Observe the application.

### Expected

Reset App should behave according to its intended local application
behavior and should not fail unexpectedly because of network
connectivity.

---

# 7. Interruption Testing

## INT-01 — System sleep during reset

### Objective

Determine application behavior when the machine enters sleep while
Reset App is executing.

### Steps

1. Trigger Reset App.
2. Put the machine into sleep during the operation.
3. Resume the machine.
4. Observe Bolt.

### Expected

The application should recover according to the intended reset behavior
without an unexpected crash or corrupted state.

---

## INT-02 — Kill Bolt during reset operation

### Objective

Determine how Bolt behaves if the application process is forcibly
terminated while the Reset App operation is in progress.

### Steps

1. Launch Bolt.
2. Wait until the application is fully loaded.
3. Trigger `Bolt → Reset App`.
4. While the reset operation is in progress, forcibly terminate the
   Bolt application using an operating-system-level process termination
   method.
5. Relaunch Bolt.
6. Observe the resulting application state.
7. Verify whether the reset operation completed, failed, or left the
   application in an inconsistent state.

### Expected

After an interrupted reset operation, Bolt should recover safely on the
next launch.

---

# 8. Edge-Case Testing

## EC-01 — Rapid repeated shortcut

### Objective

Determine whether rapidly invoking the Reset App shortcut creates
unexpected behavior.

### Steps

1. Launch Bolt.
2. Press `Shift + Windows + Backspace` repeatedly.
3. Observe the application.

### Expected

The application should handle repeated invocation safely without
crashing, freezing, or entering an inconsistent state.

---

## EC-02 — Shortcut immediately after application launch

### Objective

Determine whether the shortcut behaves correctly before the application
has completely settled after launch.

### Steps

1. Launch Bolt.
2. Press the shortcut shortly after the window becomes available.
3. Observe the application.

### Expected

The application should handle the shortcut safely according to its
defined lifecycle behavior.

---

## EC-03 — Keyboard-only operation

### Objective

Verify that the Reset App operation can be accessed using the keyboard
without requiring mouse interaction.

### Steps

1. Launch Bolt.
2. Navigate using keyboard controls.
3. Use the documented Reset App shortcut.
4. Observe the application.

### Expected

The documented keyboard interaction should function as intended.

---

# 9. Cross-Environment Testing

Where the required hardware is available, repeat the relevant charter
items across:

- Windows
- macOS
- Linux
