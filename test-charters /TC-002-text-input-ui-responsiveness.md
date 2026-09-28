
# TC-002 — Text Input & UI Responsiveness

## Feature Area

Text input and editable fields within the Bolt desktop application.

## Objective

Explore how Bolt handles text entry across its editable text fields and determine whether typing, pasting, focus changes, navigation, or application switching cause unexpected delays, UI unresponsiveness, input loss, or other interaction problems.

The primary focus is to verify that text-entry interactions remain responsive and that the application continues accepting and displaying user input normally.

---

## Environment

- **OS:** Windows 11 Home Single Language
- **OS Version:** 25H2
- **OS Build:** 26200.9457
- **Device:** ASUS TUF A17
- **CPU:** AMD Ryzen 7 4800H
- **RAM:** 8 GB
- **GPU:** NVIDIA GeForce RTX 3050 4 GB + AMD Radeon Graphics
- **Architecture:** 64-bit, x64
- **Bolt Version:** 0.1.162
- **Build:** `22f4dd5d+457ed915b+a1abb511`
- **Edition:** Enterprise
- **Platform:** Desktop
- **Installation Type:** Fresh installation
- **Network:** Tested online and offline

---

## Starting State

- Bolt is freshly installed and launched.
- The application is fully loaded.
- No modal dialog or blocking overlay is open.
- Bolt is responsive before text interaction begins.
- An editable text field is available.
- Test data consists only of synthetic text.

---

## Exploration Areas

The charter explores the following dimensions rather than testing only one fixed sequence.

### 1. Text Field Interaction

Explore:

- Search fields
- Chat/message input fields
- Setting search field
- Empty fields
- Fields containing existing text
- Short text
- Longer text

### 2. Text Entry Methods

Compare:

- Single-character typing
- Continuous typing
- Longer sentences
- Rapid typing
- `Ctrl + V` paste
- Repeated text insertion

Observe whether the application remains responsive and whether all entered text is displayed correctly.

### 3. Focus Behavior

Explore:

- Clicking directly into a text field
- Focusing a field after navigating to its screen
- Focusing immediately after returning to Bolt
- Waiting before focusing the field
- Repeatedly focusing and unfocusing the same field

### 4. Application Navigation

Explore text entry after:

- Navigating between Bolt screens
- Returning to a previously opened screen
- Switching between different Bolt views
- Focusing a text field after internal navigation

### 5. External Application Switching

Explore:

- Bolt → Chrome → Bolt
- Bolt → Microsoft Edge → Bolt
- Bolt → File Explorer → Bolt
- Other available desktop applications → Bolt

After returning to Bolt, observe text-field focus and text-entry responsiveness.

### 6. UI Responsiveness

During text insertion, observe:

- Whether the text field responds immediately
- Whether the cursor remains responsive
- Whether other Bolt controls respond
- Whether menus can be opened
- Whether scrolling remains responsive
- Whether mouse interaction remains responsive
- Whether the entire application becomes unresponsive
- Whether Bolt recovers automatically
- Time taken for recovery

### 7. Input Preservation

After any delay or UI interruption, verify:

- Whether entered text is preserved
- Whether characters are lost
- Whether text appears immediately or after recovery
- Whether entered text appears in batches
- Whether pasted text is preserved completely

---

## Happy Path

A normal text-entry interaction should behave as follows:

1. Navigate to an editable text field.
2. Focus the field.
3. Type or paste text.
4. Text should appear in the field without significant delay.
5. Bolt should remain responsive while text is being entered.
6. Other UI interactions should remain available.
7. All intended input should be preserved.

---

## Failure Paths

Investigate situations where:

- Text entry causes visible delay.
- The text field becomes temporarily unresponsive.
- The entire Bolt UI becomes unresponsive.
- Input appears only after a delay.
- Input appears in separate batches.
- Characters are lost.
- Pasted text behaves differently from typed text.
- Repeated text entry produces repeated delays.
- Bolt does not recover automatically.
- UI responsiveness is restored only after several seconds.

---

## Edge Cases

Consider valid but unusual conditions such as:

- Single-character input
- Rapid consecutive characters
- Long text input
- Continuous typing without pauses
- Single large paste
- Repeated focus/unfocus cycles
- Text entry immediately after navigation
- Text entry immediately after returning from another application
- Text entry after waiting several seconds before focus
- Different editable fields
- Online state
- Offline state

The purpose is not to test every possible combination, but to identify conditions that materially change the behavior.

---

## Measurements

When a responsiveness issue is observed, record:

- Triggering action
- Text field involved
- Input method
- Approximate freeze duration
- Whether the entire UI or only the text field is affected
- Whether input is preserved
- Whether the application recovers automatically
- Reproduction count

Where practical, measure the delay using a consistent timing method.

---

## Defect Reporting Criteria

Create a defect when the observed behavior is:

- Reproducible
- Clearly different from expected text-entry behavior
- User-visible
- Significant enough to affect normal interaction
- Narrowed to a reasonably specific trigger or condition

The defect report should contain:

- Defect-specific title
- Environment
- Known starting state
- Reproducible steps
- Expected result
- Actual result
- Reproduction rate
- Measured timing where applicable
- Impact
- Severity
- Narrowing performed
- Screenshots
- Short recording where timing or sequence matters
- Application logs when available

---

## Evidence Strategy

Capture evidence that demonstrates the behavior rather than simply documenting that testing occurred.

Potential evidence:

- Screenshot of the affected text field
- Screenshot during the unresponsive state
- Screenshot after recovery showing preserved input
- Short screen recording showing the complete interaction
- Build/version information
- Application logs

For timing-related issues, the recording should clearly show:

`Text insertion → UI becomes unresponsive → recovery → entered text displayed`

---

## Current Finding

During exploration, text insertion was found to cause a repeatable application-wide UI freeze.

Observed conditions:

- The issue occurs across the tested Bolt text fields.
- Clicking/focusing the text field itself does not cause the freeze.
- The freeze begins when text is inserted.
- Individual characters reproduce the delay.
- Continuous typing reproduces the delay.
- `Ctrl + V` paste also reproduces the delay.
- The issue occurs after external application switching.
- The issue also occurs after internal Bolt navigation.
- Waiting before focusing the field does not prevent the behavior.
- The entire Bolt UI becomes unresponsive during the delay.
- The application recovers automatically.
- Entered text is displayed after recovery.

Measured examples:

- `A` → 4.56 seconds
- `B` → 4.64 seconds
- `C` → 4.77 seconds
- `D` → 4.85 seconds
- Continuous typing → approximately 4.67 seconds
- `Ctrl + V` → approximately 4.62 seconds

Initial measured reproduction:

**5/5 attempts**

---

## Investigation Outcome

The investigation narrowed the original observation from:

"Bolt freezes when returning from another application and immediately typing."

to the more specific condition:

**"Inserting text into a focused Bolt text field causes the entire Bolt UI to become unresponsive for approximately 4–5 seconds."**

External application switching is therefore considered a reproducible path, but it is **not required** to trigger the behavior because the issue also occurs during internal Bolt navigation.

---

## Status

**Exploration completed — defect documented as BUG-002.**

Further investigation should focus on retesting the behavior after a fix and verifying that normal text entry remains responsive across the previously affected conditions.
