# BUG-003 — Onboarding "Simple, or Advanced?" Step Closes Without Continuing

---

## Environment

### Primary Environment

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

### Comparison Environment

- Browser: Google Chrome
- Interface: Bolt localhost session
- Local Host Observed: `localhost:13018`

---

## Known Starting State

- Bolt was initially installed as a fresh installation.
- Bolt was launched successfully.
- The application was in a state where the reset/setup flow could be initiated.
- No crash or blocking modal was present before beginning the investigation.

The tested flow was initiated using:

`Bolt → Reset App`

---

## Summary

Clicking the `Next →` button on the **"START HERE — Simple, or advanced?"** onboarding screen closes the onboarding interface without continuing to another onboarding step.

The behavior is reproducible with both:

- **Simple** selected
- **Advanced** selected

The behavior was reproduced in:

- Bolt Desktop
- Chrome localhost session

The same behavior was also reproduced after restarting the Bolt application.

After the onboarding interface closes, Bolt remains usable and displays the normal Zen mode screen.

---

# Reproduction Path A — Simple Selected

1. Launch Bolt.
2. Open the `Bolt` menu.
3. Select `Reset App`.
4. When the **"Use Bolt in your browser too"** screen appears, click `Trust it and restart`.
5. Accept the Windows certificate installation/deletion confirmation dialogs by selecting `Yes`.
6. On the **"How will you use Bolt?"** screen, select:
   - `Sign in with Google, Microsoft, or Zoho`
7. Complete the sign-in flow through Google Chrome.
8. When prompted, open the Bolt desktop application.
9. Continue through the setup flow until the **"START HERE — Simple, or advanced?"** onboarding screen appears.
10. Leave **Simple** selected.
11. Click `Next →`.
12. Observe the onboarding interface and resulting application state.

### Actual Result

The onboarding interface disappears.

No subsequent onboarding step is displayed.

The application proceeds to the normal Bolt Zen mode screen and remains usable.

### Reproduction Rate

**5/5 attempts**

---

# Reproduction Path B — Advanced Selected

1. Launch Bolt.
2. Open the `Bolt` menu.
3. Select `Reset App`.
4. When the **"Use Bolt in your browser too"** screen appears, click `Trust it and restart`.
5. Accept the Windows certificate installation/deletion confirmation dialogs by selecting `Yes`.
6. On the **"How will you use Bolt?"** screen, select:
   - `Sign in with Google, Microsoft, or Zoho`
7. Complete the sign-in flow through Google Chrome.
8. When prompted, open the Bolt desktop application.
9. Continue through the setup flow until the **"START HERE — Simple, or advanced?"** onboarding screen appears.
10. Select **Advanced**.
11. Click `Next →`.
12. Observe the onboarding interface and resulting application state.

### Actual Result

The onboarding interface disappears.

No subsequent onboarding step is displayed.

The application proceeds to the normal Bolt Zen mode screen and remains usable.

### Reproduction Rate

**5/5 attempts**

---

# Reproduction Path C — Application Restart

1. Restart the Bolt application.
2. Follow the setup/onboarding flow until the **"START HERE — Simple, or advanced?"** screen is reached.
3. Leave **Simple** selected or select **Advanced**.
4. Click `Next →`.
5. Observe the resulting application state.

### Actual Result

The same behavior occurs:

- The onboarding interface disappears.
- No subsequent onboarding step is displayed.
- Bolt proceeds to the normal Zen mode screen.
- Bolt remains usable.

### Reproduction Rate

**5/5 attempts**

---

# Reproduction Path D — Chrome Localhost Session

1. Open or observe the Bolt localhost session in Google Chrome.
2. Follow the corresponding application flow.
3. Reach the **"START HERE — Simple, or advanced?"** onboarding state.
4. Leave **Simple** selected or select **Advanced**.
5. Click `Next →`.
6. Observe the resulting state.

### Actual Result

The same `Next →` behavior is observed:

- Simple selected → onboarding closes.
- Advanced selected → onboarding closes.
- No subsequent onboarding step is displayed.

The Chrome localhost session follows the corresponding application state as the setup flow is performed in the main Bolt application.

### Reproduction Rate

A separate numerical reproduction count was not recorded for the Chrome localhost session.

---

# Expected Result

After selecting either **Simple** or **Advanced** and clicking `Next →`, Bolt should continue to the next step of the corresponding onboarding flow.

The onboarding sequence should continue through its remaining steps rather than being dismissed before completion.

---

# Actual Result

Clicking `Next →` on the **"START HERE — Simple, or advanced?"** screen closes the onboarding interface without visibly advancing to another onboarding step.

Bolt then displays the normal Zen mode screen and remains usable.

---

# Reproduction Rate

| Condition | Result |
|---|---|
| Simple selected | **5/5** |
| Advanced selected | **5/5** |
| After application restart | **5/5** |
| Bolt Desktop | Reproduced |
| Chrome localhost | Reproduced |

---

# Narrowing Performed

## 1. Selection State

The behavior was tested with both available onboarding selections.

### Simple

`Simple → Next →`

Result: Onboarding closes without advancing.

Reproduced **5/5**.

### Advanced

`Advanced → Next →`

Result:
Onboarding closes without advancing.

Reproduced **5/5**.

This indicates that the observed behavior is not isolated to one of the two available selections.

---

## 2. Application Lifecycle

The behavior was tested after:

- Initial setup following application reset
- Application restart

The same behavior was reproduced after application restart.

Reproduced **5/5** during the tested restart condition.

This indicates that the finding is not limited to the first setup attempt after the initial installation.

---

## 3. Execution Context

The behavior was observed in:

- Bolt Desktop
- Chrome localhost session

Therefore, the current evidence does not support classifying this as a desktop-only issue.

---

## 4. Post-Action Application State

After the onboarding interface closes:

- Bolt remains usable.
- The application does not crash.
- The Zen mode screen appears.
- No data loss was observed.
- No data corruption was observed.

---

# Impact

Users attempting to proceed through the Simple or Advanced onboarding flow are not taken to the next onboarding step after clicking the provided `Next →` control.

Instead, the onboarding interface closes and the user is returned to the normal Bolt application.

This interrupts the intended onboarding sequence, although the core Bolt application remains usable.

---

# Severity

**Medium**

## Severity Rationale

The defect affects the onboarding flow and prevents progression through the remaining onboarding steps from the tested Simple / Advanced screen.

However:

- Bolt does not crash.
- The application remains usable.
- User able to login their account
- The user reaches the normal Zen mode screen.
- No data loss was observed.
- No data corruption was observed.

The observed impact is therefore primarily on the onboarding experience rather than on the availability of the core application.

---

# Workaround

No confirmed method for continuing the remaining onboarding steps was identified during this investigation.

The main Bolt application remains usable after the onboarding interface closes.

---

# Evidence

1. Screen recording
   Below screen recording shows the user onboarding options "Simple, or advance" onboarding Step Closes Without Continuing

   https://github.com/user-attachments/assets/0facd55d-1757-4cb1-92d9-9d2510c966e0

2. Available onboarding selection options
   
   <img width="1920" height="1080" alt="Screenshot (216)" src="https://github.com/user-attachments/assets/41b6efbf-4fb2-413d-a380-d0f36dd28f2e" />
