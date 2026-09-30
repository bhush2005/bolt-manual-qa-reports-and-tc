
# Bolt Manual QA Evaluation

Manual QA testing documentation prepared while evaluating
the Bolt desktop application.

## Scope

The documentation demonstrates:

- Exploratory testing
- Test charter creation
- Bug investigation
- Bug reproduction
- Edge-case testing
- Cross-condition narrowing
- Evidence collection
- Severity and impact assessment
- Re-test planning

## Bugs

| ID | Area | Title | Reproduction |
|---|---|---|---|
| BUG-001 | Keyboard Shortcut | Shift + Windows + Backspace does not trigger Reset App | 5/5 |
| BUG-002 | Text Input / UI Responsiveness | Text entry causes Bolt UI to become unresponsive for approximately 4–5 seconds | 5/5 |
| BUG-003 | Onboarding | Onboarding "Simple, or Advanced?" step closes on Next without continuing the onboarding flow | 5/5 |

## Environment

- OS: Windows 11 Home Single Language 25H2
- OS Build: 26200.9457
- Device: ASUS TUF A17
- CPU: AMD Ryzen 7 4800H
- RAM: 8 GB
- GPU: NVIDIA GeForce RTX 3050 4 GB
- Bolt Version: 0.1.162
- Build: `22f4dd5d+457ed915b+a1abb511`
- Edition: Enterprise
- Platform: Desktop
- Installation Type: Fresh installation
- Network: Tested online and offline
