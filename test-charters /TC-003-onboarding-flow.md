# TC-003 — Onboarding and First-Run Setup Flow

## Feature Area

Onboarding / First-Run Setup / Application Initialization

---

## Charter Mission

Explore the complete Bolt onboarding and first-run setup flow after an application reset and during subsequent application restarts.

The investigation focuses on:

- Reset-to-onboarding flow
- Browser trust and certificate setup
- Initial setup choices
- Authentication flow
- Desktop and browser interaction
- Simple vs Advanced onboarding selection
- `Next →` button behavior
- Progression between onboarding steps
- Application state after onboarding is dismissed
- Onboarding behavior after application restart
- Consistency between Bolt Desktop and the Chrome localhost session

The goal is to determine whether users can successfully progress through the intended onboarding experience and identify any reproducible deviations from the expected flow.

---

## Environment

### Primary Test Environment

- OS: Windows 11 Home Single Language 25H2
- OS Build: `26200.9457`
- Device: ASUS TUF A17
- CPU: AMD Ryzen 7 4800H
- RAM: 8 GB
- GPU: NVIDIA GeForce RTX 3050 4 GB
- Integrated GPU: AMD Radeon Graphics
- Architecture: 64-bit x64
- Bolt Version: `0.1.162`
- Bolt Build: `22f4dd5d+457ed915b+a1abb511`
- Edition: Enterprise
- Platform: Desktop
- Installation Type: Fresh installation
- Network Condition: Online during the tested setup flow

### Additional Test Environment

A browser-based Bolt localhost session was also observed during the setup and authentication flow.

- Browser: Google Chrome
- Interface: Bolt localhost session
- Local Host Observed: `localhost:13018`

The Chrome localhost session was observed to follow the corresponding application state as actions were performed in the main Bolt desktop application.

---

## Starting State

- Bolt was initially installed as a fresh installation.
- Bolt was launched successfully.
- The application was in a state where the reset/setup flow could be initiated.
- No crash or blocking modal was present before beginning the investigation.

The primary investigation was initiated using:

`Bolt → Reset App`

---

# Reset and First-Run Setup Flow

## Step 1 — Reset App

The `Reset App` option was selected from the Bolt application menu.

The application then entered the reset/setup flow.

---

## Step 2 — Browser Trust Setup

The following screen was displayed:

> **Use Bolt in your browser too**

The screen contained a:

> **Trust it and restart**

button.

The `Trust it and restart` action was selected.

---

## Step 3 — Windows Certificate Dialogs

Windows certificate-related confirmation dialogs were presented during the setup process.

The certificate confirmation prompts were accepted by selecting `Yes`.

The observed setup included certificate installation/deletion confirmation dialogs.

These actions were treated as part of the setup sequence required to continue the tested flow.

---

## Step 4 — "How Will You Use Bolt?"

The following setup screen was displayed:

> **How will you use Bolt?**

Three setup paths were available:

1. **Sign in with Google, Microsoft, or Zoho**
2. **Connect to my organization's Bolt server**
3. **Take a guided tour with sample data**

For this investigation, the following option was selected:

> **Sign in with Google, Microsoft, or Zoho**

---

## Step 5 — Authentication Flow

The sign-in flow was initiated from the Bolt application.

The authentication process opened/continued through Google Chrome.

After completing the required sign-in interaction, the user was prompted to open the Bolt desktop application.

The Bolt desktop application was then opened from the authentication flow.

---

## Step 6 — Simple / Advanced Onboarding

After the sign-in and application handoff, the following onboarding screen was reached:

> **START HERE — Simple, or advanced?**

The screen displayed two onboarding choices.

### Simple

> Just type or paste. The essentials only.

The Simple option represents the shorter onboarding path.

### Advanced

> Every scope, prefix, and admin control on screen.

The Advanced option represents the expanded onboarding path.

A:

> **Next →**

button was displayed below the options.

---

# Exploration Areas

## 1. Reset and Application Lifecycle

Explore onboarding behavior:

- Immediately after `Reset App`
- During the initial setup flow
- After completing the setup flow
- After restarting the Bolt application

---

## 2. Setup Flow

Explore the transition between:

- Reset
- Browser trust setup
- Certificate prompts
- "How will you use Bolt?"
- Authentication
- Desktop application handoff
- Simple / Advanced onboarding

---

## 3. Simple / Advanced Selection

Explore the onboarding behavior with:

- Simple selected
- Advanced selected

---

## 4. Next Button

Determine whether clicking `Next →`:

- Advances to the next onboarding step
- Closes the onboarding window
- Returns the user to the normal application
- Produces an error or warning
- Leaves the user on the same onboarding step
- Skips any remaining onboarding steps

---

## 5. Post-Onboarding State

Observe the application state immediately after the onboarding interface is dismissed.

Determine:

- Whether Bolt remains usable
- Which screen is displayed
- Whether another onboarding step appears
- Whether the application crashes or becomes unresponsive

---

## 6. Application Restart

Repeat the relevant onboarding flow after restarting Bolt.

Determine whether the same behavior can be reproduced after an application restart.

---

## 7. Desktop / Browser Consistency

Compare the onboarding behavior between:

- Bolt Desktop
- Chrome localhost session

---

# Happy Path

The expected onboarding experience should allow the user to:

1. Reset or enter the first-run setup flow.
2. Complete the required setup steps.
3. Select the intended Bolt usage mode.
4. Complete authentication where required.
5. Reach the Simple / Advanced onboarding screen.
6. Select either Simple or Advanced.
7. Click `Next →`.
8. Continue to the next onboarding step.
9. Complete the remaining onboarding experience.
10. Reach the normal application after onboarding completion.

---

# Failure Paths

The following paths were explored.

## Failure Path A — Simple Selected

1. Reach the Simple / Advanced onboarding screen.
2. Leave Simple selected.
3. Click `Next →`.
4. Observe the result.

---

## Failure Path B — Advanced Selected

1. Reach the Simple / Advanced onboarding screen.
2. Select Advanced.
3. Click `Next →`.
4. Observe the result.

---

## Failure Path C — Application Restart

1. Restart Bolt.
2. Follow the setup/onboarding flow again.
3. Reach the Simple / Advanced onboarding screen.
4. Repeat the Simple or Advanced path.
5. Observe whether the same behavior occurs.

---

## Failure Path D — Chrome Localhost

1. Observe the Bolt localhost session in Chrome.
2. Follow the corresponding application flow.
3. Reach the Simple / Advanced onboarding state.
4. Repeat the Simple or Advanced selection.
5. Click `Next →`.
6. Observe the result.

---

# Edge Cases and Variables

## Selection State

- Simple selected
- Advanced selected

## Application Lifecycle

- Initial setup after reset
- Application restart

## Execution Context

- Bolt Desktop
- Chrome localhost

## Setup Path

- Sign in with Google, Microsoft, or Zoho

## State Transition

Observe:

- Before clicking `Next →`
- Immediately after clicking `Next →`
- Final application state after the onboarding window closes
- Behavior after application restart

---

# Test Execution and Observations

## Observation 1 — Simple Selected

The Simple option was left selected on the:

> "START HERE — Simple, or advanced?"

screen.

The `Next →` button was clicked.

### Observed Result

The onboarding window disappeared.

The flow did not visibly continue to another onboarding step.

After the onboarding window disappeared, the normal Bolt application remained usable and the Zen mode screen appeared.

### Reproduction

**5/5 attempts**

---

## Observation 2 — Advanced Selected

The Advanced option was selected on the:

> "START HERE — Simple, or advanced?"

screen.

The `Next →` button was clicked.

### Observed Result

The onboarding window disappeared.

The flow did not visibly continue to another onboarding step.

After the onboarding window disappeared, the normal Bolt application remained usable and the Zen mode screen appeared.

### Reproduction

**5/5 attempts**

---

## Observation 3 — Application Restart

The Bolt application was restarted and the setup/onboarding flow was encountered again.

The same onboarding sequence was followed until reaching:

> "START HERE — Simple, or advanced?"

The Simple or Advanced path was then executed again.

### Observed Result

The same `Next →` behavior was reproduced after application restart.

### Reproduction

**5/5 attempts**

---

## Observation 4 — Chrome Localhost Session

The Chrome localhost session was observed during the application flow.

Actions performed in the main Bolt desktop application were reflected in the browser session as the setup process progressed.

The same Simple / Advanced onboarding state was observed in the Chrome session.

The `Next →` behavior was also reproduced there.

### Observed Results

- Simple selected → `Next →` → onboarding closes
- Advanced selected → `Next →` → onboarding closes

Therefore, the observed `Next →` behavior is not currently established as a desktop-only issue.

---

# Narrowing Performed

The following conditions were compared.

| Condition | Result |
|---|---|
| Simple selected → `Next →` | Onboarding closes |
| Advanced selected → `Next →` | Onboarding closes |
| Simple selected | 5/5 reproduced |
| Advanced selected | 5/5 reproduced |
| After application restart | 5/5 reproduced |
| Bolt Desktop | Reproduced |
| Chrome localhost | Reproduced |
| Bolt usable after onboarding closes | Yes |

---

# Investigation Findings

The investigation established the following behavior:

1. The Simple / Advanced onboarding screen can be reached through the tested reset/setup flow.
2. Leaving Simple selected and clicking `Next →` causes the onboarding interface to disappear.
3. Selecting Advanced and clicking `Next →` produces the same result.
4. The behavior was reproduced 5/5 for Simple.
5. The behavior was reproduced 5/5 for Advanced.
6. The same behavior was reproduced after application restart.
7. The same behavior was observed in the Chrome localhost session.
8. After the onboarding interface closes, Bolt remains usable.
9. The Zen mode screen appears after the onboarding interface closes.
10. No crash, data loss, or data corruption was observed during this investigation.

---

# Expected Behavior

After selecting either Simple or Advanced and clicking `Next →`, the user should continue to the next step of the corresponding onboarding flow.

The onboarding process should continue until the configured onboarding steps are completed.

---

# Actual Behavior

Clicking `Next →` on the:

> "START HERE — Simple, or advanced?"

screen closes the onboarding interface without visibly advancing to another onboarding step.

Bolt then displays the normal application Zen mode screen and remains usable.

---

# Current Defect Candidate

## BUG-003

**Onboarding "Simple, or advanced?" step closes on `Next →` without continuing the onboarding flow**

The defect candidate is specifically the behavior of the `Next →` action.

The investigation does not classify the entire onboarding system as broken because the core application remains usable after the onboarding interface closes.

---

# Severity Consideration

## Proposed Severity: Medium

### Rationale

The issue affects the intended onboarding flow and prevents the user from progressing through the remaining onboarding steps from the tested Simple / Advanced screen.

However:

- Bolt does not crash.
- The application remains usable.
- The user reaches the normal Zen mode screen.
- No data loss was observed.
- No data corruption was observed.

Therefore, the observed impact is primarily on the onboarding experience rather than on the availability of the core application.

---

# Workaround

No confirmed method for continuing the remaining onboarding steps was identified during this investigation.

The main Bolt application remains usable after the onboarding interface closes.

---

# Separate Observations Not Classified as BUG-003

The following behaviors were observed during the broader investigation but are not currently combined into BUG-003 unless independently reproduced and narrowed:

- Intermittent visibility of onboarding windows before user interaction
- Windows certificate installation/deletion prompts
- Authentication behavior
- Chrome-to-desktop application handoff
- Any implementation-specific cause of the onboarding behavior

These observations are retained as setup context and are not assumed to share the same root cause.

---

# Scope Boundary

This charter does not establish a technical root cause.

No conclusion is made about whether the behavior is caused by:

- Onboarding navigation logic
- Application state management
- Browser/Desktop synchronization
- Local service behavior
- Authentication state
- UI implementation

Determining the root cause would require additional technical investigation and application logs/source-level analysis.

---
