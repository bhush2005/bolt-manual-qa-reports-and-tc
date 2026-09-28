# BUG-001 — App Reset Shortcut `shift+windows+backcpace` Does Not Triggering Reset Action

## Environment

- OS: Windows 11 Home Single Language
- Version: 25H2
- OS Build: 26200.9457
- Device: ASUS TUF A17
- CPU: AMD Ryzen 7 4800H
- RAM: 8 GB
- GPU: NVIDIA GeForce RTX 3050 4 GB + AMD Radeon Graphics
- Architecture: 64-bit, x64-based processor
- Bolt Version: 0.1.162
- Build: 22f4dd5d+457ed915b+a1abb511
- Edition: Enterprise
- Platform: Desktop
- Installation Type: Fresh installation
- Network: Reproduced both online and offline

## Summary

The documented `Shift + Windows + Backspace` keyboard shortcut does not trigger the **Reset App** action in Bolt v0.1.162.

The issue is reproducible in **5/5 attempts** across the tested signed-in/signed-out states, online/offline conditions, menu states, and focus states. The equivalent `Bolt → Reset App` menu action works consistently and remains available as a workaround.

## Known Starting State

- Bolt v0.1.162 is freshly installed.
- Bolt is launched and the main application window is fully loaded.
- The Bolt menu is closed.
- The main Bolt window has focus.
- No dialog or modal window is open.

## Steps to Reproduce

1. Launch Bolt v0.1.162.
2. Wait until the main application window is fully loaded.
3. Ensure the Bolt menu is closed and the main application window has focus.
4. Press `Shift + Windows + Backspace` simultaneously.
5. Wait approximately 5 seconds and observe the application.

## Expected Result

Pressing `Shift + Windows + Backspace` should trigger the same Reset App action as selecting `Bolt → Reset App` from the menu.

## Actual Result

Pressing `Shift + Windows + Backspace` produces no visible response or error message and does not trigger the Reset App action.

## Reproduction Rate

**5/5 attempts**

## Severity

**Low**

## Impact

Users attempting to reset Bolt using the documented keyboard shortcut cannot trigger the Reset App action; the equivalent `Bolt → Reset App` menu action remains available as a workaround. No crash, data loss, or data corruption was observed during the shortcut failure.

## Investigation / Narrowing

- `Bolt → Reset App` works 5/5.
- `Shift + Windows + Backspace` fails 5/5.
- The shortcut failure was reproduced while signed in and signed out.
- The shortcut failure was reproduced both online and offline.
- The shortcut failure was reproduced with the Bolt menu open and closed.
- The shortcut failure was reproduced across the tested focus states.
- `Shift`, `Windows`, and `Backspace` were individually verified to work normally at the Windows OS level.
- No visible error or feedback is displayed when the shortcut is pressed.

## Evidence

### Screenshot 1 — Documented Shortcut
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/059723f6-8e4a-47d2-bc15-6af0e2be263b" />


### Screenshot 2 — Build Information
<img width="1463" height="136" alt="{30F92DD3-B17D-4F62-BC50-253F84D3CBA3}" src="https://github.com/user-attachments/assets/f15a697c-86ef-475e-b21d-1cafae0e3354" />

### Screen recording - Demonistarting the reset keyboard shortcut failure and equivalent `bolt -> reset app` in menu option working

https://github.com/user-attachments/assets/52ea4bc1-37a4-40ce-84a0-e61dd24fab58
