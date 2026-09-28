# BUG-002 — Text Entry Causes Bolt UI to Become Unresponsive for Approximately 4–5 Seconds

## Environment

- **OS:** Windows 11 Home Single Language
- **OS Version:** 25H2
- **OS Build:** 26200.9457
- **Device:** ASUS TUF A17
- **CPU:** AMD Ryzen 7 4800H
- **RAM:** 8 GB
- **GPU:** NVIDIA GeForce RTX 3050 4 GB + AMD Radeon Graphics
- **Architecture:** 64-bit x64
- **Bolt Version:** 0.1.162
- **Edition:** Enterprise
- **Platform:** Desktop
- **Build:** `22f4dd5d+457ed915b+a1abb511`
- **Build Timestamp:** 2026-09-15 05:30:14 UTC
- **Installation:** Fresh installation
- **Network:** Tested online and offline

---

## Summary

Entering or pasting text into a focused Bolt text field causes the entire Bolt UI to become unresponsive for approximately 4–5 seconds before recovering.

The behavior can be reproduced through two paths:
- **External application switching:** Switching from Bolt to another application (e.g., Chrome, Microsoft Edge, or File Explorer), switching back to Bolt, and then entering or pasting text into a focused text field.
- **Internal Bolt navigation:** Navigating between screens within Bolt and then entering or pasting text into a focused text field, without switching to an external application.

The behavior is reproducible across the tested text fields and occurs with both keyboard typing and `Ctrl + V` paste operations.

---

## Known Starting State

- Bolt v0.1.162 is freshly installed.
- Bolt is launched and fully loaded.
- Bolt is responsive before text interaction begins.
- No modal dialog or blocking overlay is open.
- App screen is on Zen mode
- Bolt is responsive before text is entered.

---

### Reproduction Path A — Internal Bolt Navigation

1. Launch Bolt.
2. Wait until the application is fully loaded.
3. Navigate between screens within Bolt.
4. Open a screen containing an editable text field, e.g., the Search bar or Chat input.
5. Click inside the text field to place the cursor.
6. Type a character or paste text using `Ctrl + V`.
7. Observe the Bolt UI.
8. Wait approximately 4–5 seconds for Bolt to become responsive again.

### Reproduction Path B — External Application Switching

1. Launch Bolt.
2. Wait until the application is fully loaded.
3. Navigate to any screen containing an editable text field, e.g., the Search bar or Chat input.
4. Switch from Bolt to another application, such as Chrome, Microsoft Edge, or File Explorer.
5. Switch back to Bolt.
6. Click inside the text field to place the cursor.
7. Type a character or paste text using `Ctrl + V`.
8. Observe the Bolt UI.
9. Wait approximately 4–5 seconds for Bolt to become responsive again.
---

## Expected Result

Text should be entered into the focused text field and Bolt should remain responsive without a significant delay.

---

## Actual Result

After text is entered, the entire Bolt UI becomes unresponsive for approximately 4–5 seconds.

After the delay, Bolt becomes responsive again and the entered text is displayed.

---

## Reproduction Rate

1. Internal Bolt Navigation :
**3/5**

2. External Application Switching : 
**5/5**

### Initial measurements

- Attempt 1 : 4.61 seconds
- Attempt 2 : 4.59 seconds
- Attempt 3 : 4.91 seconds
- Attempt 4 : 4.65 seconds
- Attempt 5 : 4.52 seconds

**Observed range:** 4.52–4.91 seconds

### Additional measurements

Individual characters:

- `A` → 4.56 seconds
- `B` → 4.64 seconds
- `C` → 4.77 seconds
- `D` → 4.85 seconds

Continuous typing:

- Approximately 4.67 seconds

Single `Ctrl + V` paste:

- Approximately 4.62 seconds

---

## Narrowing Performed

- The issue reproduces when switching back to Bolt from external applications such as Chrome, Edge, and File Explorer.
- The issue also reproduces during navigation between screens within Bolt; therefore, switching from an external application is not required.
- Clicking/focusing the text field itself does not cause the freeze. The cursor can be positioned normally.
- The freeze begins when text is inserted into the focused text field.
- The issue occurs across the tested Bolt text fields rather than being isolated to one field.
- Individual keyboard input reproduces the issue.
- Continuous typing reproduces the issue.
- A single `Ctrl + V` paste also reproduces the issue.
- Waiting before focusing the text field does not prevent the behavior.
- During the observed delay, the Bolt UI becomes unresponsive.
- After recovery, the entered text is displayed.
- When entering longer text, portions of the entered text may appear after the initial delay, followed by the remaining text after the application becomes responsive.

---

## Impact

Users entering or pasting text into Bolt may experience an approximately 4–5 second application-wide UI freeze after text insertion, interrupting normal interaction and making text entry feel unresponsive.

---

## Severity

**Medium**

### Severity Rationale

Text input is a fundamental interaction within a desktop application. The issue affects the responsiveness of the entire Bolt UI rather than only the text field and reproduces across the tested text fields with both typing and paste operations.

---

## Evidences
- Screenshot showing the affected text field
   
1. Zen Mode
   <img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/67d29851-ca79-432b-ab2b-f776ec34f9f8" />


2. Setting search bar
   <img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/854ca3ec-a007-484d-8b67-ec203963e36f" />


3. Session screen
   <img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/5aa408c5-2284-4de6-be63-7ae7c1176700" />

- Short screen recording demonstrating the freeze and recovery
      
  https://github.com/user-attachments/assets/2fd280c6-e54e-4cea-99d2-9e3ed6502338
