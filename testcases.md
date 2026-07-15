# Test Cases for KAN-3 – Mobile Application Login Functionality

## Jira Context
- **Issue Key:** KAN-3  
- **Summary:** Implement Mobile Application Login Functionalit  
- **Feature:** Mobile application login functionality to allow users to securely authenticate and access the application.

---

## Test Case Suite Overview
- **Total Test Cases:** 22  
- **Primary Focus:** Functional behavior, security of authentication, error handling, and boundary conditions for mobile login.  
- **Audit Reference:** KAN-3-AUDIT-LOGIN-TESTCASE-GENERATION-001

---

## Detailed Test Cases

### KAN-3-TC001 – Verify login screen is presented on application launch for unauthenticated user
- **Test Type:** Functional  
- **Priority:** High  
- **Preconditions:** User is not authenticated; application installed on supported mobile device; network connectivity available.
- **Steps:**
  1. Launch the mobile application.
  2. Observe the initial screen displayed to the user.
- **Expected Result:** The application displays a login mechanism (login screen or button) requiring authentication before accessing main application content.
- **Test Data:** N/A  
- **Traceability:** KAN-3

---

### KAN-3-TC002 – Verify successful login with valid username and password
- **Test Type:** Functional  
- **Priority:** High  
- **Preconditions:** User account exists and is active in the identity provider; backend authentication service is available; user is logged out.
- **Steps:**
  1. Launch the mobile application.
  2. Navigate to the login screen if not shown by default.
  3. Enter a valid username associated with an active account.
  4. Enter the correct password for the username.
  5. Tap the Login/Sign In button.
- **Expected Result:** User is authenticated successfully and granted access to the application main/home screen. No error message is displayed.
- **Test Data:** Valid username and matching valid password  
- **Traceability:** KAN-3

---

### KAN-3-TC003 – Verify access to main application requires authentication
- **Test Type:** Functional  
- **Priority:** High  
- **Preconditions:** User is not authenticated; application installed; backend reachable.
- **Steps:**
  1. Launch the mobile application.
  2. Attempt to navigate directly to main application features without logging in (e.g., via deep link or stored bookmark).
  3. If any shortcut or quick access is provided, tap it before login.
- **Expected Result:** Application requires user to authenticate via login mechanism before granting access to main application features. Unauthenticated user cannot access protected areas.
- **Test Data:** N/A (unauthenticated state)  
- **Traceability:** KAN-3

---

### KAN-3-TC004 – Verify secure transmission of credentials over network (HTTPS/TLS)
- **Test Type:** Validation  
- **Priority:** High  
- **Preconditions:** Test environment with network inspection tools available; application configured to use backend authentication API.
- **Steps:**
  1. Configure a proxy or network sniffer to capture traffic between the mobile application and backend.
  2. Launch the mobile application and navigate to the login screen.
  3. Enter a valid username and password.
  4. Tap the Login/Sign In button.
  5. Inspect the captured network traffic for the login request.
- **Expected Result:** Login request is sent over a secure transport (e.g., HTTPS/TLS). Credentials are not transmitted in plain text over an unencrypted channel.
- **Test Data:** Valid username and password in test environment  
- **Traceability:** KAN-3

---

### KAN-3-TC005 – Verify login with invalid password is rejected
- **Test Type:** Negative  
- **Priority:** High  
- **Preconditions:** User account exists; backend authentication service available; user is logged out.
- **Steps:**
  1. Launch the mobile application.
  2. Navigate to the login screen.
  3. Enter a valid username associated with an active account.
  4. Enter an incorrect password.
  5. Tap the Login/Sign In button.
- **Expected Result:** Authentication fails. User is not granted access to the application. An appropriate generic error indication is shown (exact wording unspecified) and login screen remains available.
- **Test Data:** Valid username with invalid password  
- **Traceability:** KAN-3

---

### KAN-3-TC006 – Verify login with non-existent username is rejected
- **Test Type:** Negative  
- **Priority:** Medium  
- **Preconditions:** Backend authentication service available; test username that does not exist in identity provider.
- **Steps:**
  1. Launch the mobile application.
  2. Navigate to the login screen.
  3. Enter a username that does not exist in the user store.
  4. Enter any password value.
  5. Tap the Login/Sign In button.
- **Expected Result:** Authentication fails. User is not granted access to the application. An appropriate error indication is shown, without revealing whether the username exists.
- **Test Data:** Non-existent username, arbitrary password  
- **Traceability:** KAN-3

---

### KAN-3-TC007 – Verify login fails with empty username and password
- **Test Type:** Negative  
- **Priority:** Medium  
- **Preconditions:** Application installed; user logged out.
- **Steps:**
  1. Launch the mobile application.
  2. Navigate to the login screen.
  3. Leave username field empty.
  4. Leave password field empty.
  5. Tap the Login/Sign In button.
- **Expected Result:** Authentication is not attempted or fails validation. User remains on login screen. Validation feedback is shown that credentials are required (exact text unspecified).
- **Test Data:** Username: empty; Password: empty  
- **Traceability:** KAN-3

---

### KAN-3-TC008 – Verify login validation when username is provided and password left empty
- **Test Type:** Boundary  
- **Priority:** Medium  
- **Preconditions:** Application installed; user logged out.
- **Steps:**
  1. Launch the mobile application.
  2. Navigate to the login screen.
  3. Enter a valid username.
  4. Leave password field empty.
  5. Tap the Login/Sign In button.
- **Expected Result:** Validation fails and user is not authenticated. Feedback indicates password is required (exact wording unspecified).
- **Test Data:** Valid username; Password: empty  
- **Traceability:** KAN-3

---

### KAN-3-TC009 – Verify login validation when password is provided and username left empty
- **Test Type:** Boundary  
- **Priority:** Medium  
- **Preconditions:** Application installed; user logged out.
- **Steps:**
  1. Launch the mobile application.
  2. Navigate to the login screen.
  3. Leave username field empty.
  4. Enter any password.
  5. Tap the Login/Sign In button.
- **Expected Result:** Validation fails and user is not authenticated. Feedback indicates username is required (exact wording unspecified).
- **Test Data:** Username: empty; Password: any value  
- **Traceability:** KAN-3

---

### KAN-3-TC010 – Verify secure storage of credentials (no plain-text password on device)
- **Test Type:** Validation  
- **Priority:** High  
- **Preconditions:** Device with file system access for testing; app installed; valid user account; user logs in successfully.
- **Steps:**
  1. Launch the mobile application and log in with valid credentials.
  2. After successful login, keep application running or place in background.
  3. Use device inspection tools to examine app storage areas (local databases, files, shared preferences/keychain).
  4. Search for stored credentials, especially password, in plain text.
- **Expected Result:** User password is not stored in plain text on the device. Any stored authentication artifacts (tokens, keys) appear to be stored securely according to platform best practices.
- **Test Data:** Valid username/password for test account  
- **Traceability:** KAN-3

---

### KAN-3-TC011 – Verify secure handling of login session token in transit and at rest
- **Test Type:** Validation  
- **Priority:** Medium  
- **Preconditions:** Application integrated with backend returning an authentication token on successful login; test environment with inspection capabilities.
- **Steps:**
  1. Set up network capture for the device.
  2. Launch the mobile application and navigate to the login screen.
  3. Log in with valid credentials.
  4. Capture the authentication response and subsequent requests using the token.
  5. Inspect whether the token is transmitted only over secure channels and not logged or exposed in clear text in local logs accessible to the user.
- **Expected Result:** Authentication token is transmitted only over secure channels and is not exposed in clear text in user-accessible storage or logs.
- **Test Data:** Valid username/password  
- **Traceability:** KAN-3

---

### KAN-3-TC012 – Verify error handling on authentication service network failure during login
- **Test Type:** Edge Case  
- **Priority:** High  
- **Preconditions:** Ability to simulate network outage or backend unavailability; user is logged out.
- **Steps:**
  1. Launch the mobile application.
  2. Navigate to the login screen.
  3. Disable network connectivity or stop the authentication backend service.
  4. Enter valid username and password.
  5. Tap the Login/Sign In button.
- **Expected Result:** Login request fails gracefully. User is not authenticated. Application shows a non-technical error indication about network or server issue (exact text unspecified) and does not crash.
- **Test Data:** Valid username and password; simulated network failure  
- **Traceability:** KAN-3

---

### KAN-3-TC013 – Verify error handling on authentication timeout
- **Test Type:** Edge Case  
- **Priority:** Medium  
- **Preconditions:** Ability to introduce high latency or simulate timeout from backend; user logged out.
- **Steps:**
  1. Configure backend or proxy to delay authentication responses beyond the client timeout threshold.
  2. Launch the mobile application and navigate to login screen.
  3. Enter valid username and password.
  4. Tap the Login/Sign In button.
  5. Observe behavior until timeout occurs.
- **Expected Result:** Application times out the login attempt gracefully, informs the user that the request could not be completed, does not authenticate the user, and allows retry.
- **Test Data:** Valid username and password; simulated high latency/timeout  
- **Traceability:** KAN-3

---

### KAN-3-TC014 – Verify login state persists appropriately when app is sent to background during authentication
- **Test Type:** Edge Case  
- **Priority:** Medium  
- **Preconditions:** User logged out; device capable of multitasking; backend service available.
- **Steps:**
  1. Launch the mobile application and navigate to login screen.
  2. Enter valid username and password.
  3. Tap the Login/Sign In button.
  4. Immediately send the app to background (e.g., press Home or switch apps).
  5. Wait a few seconds, then bring the app back to foreground.
  6. Observe login state and resulting screen.
- **Expected Result:** Application handles background/foreground transition securely. After authentication completes, user is either properly logged in and taken to main screen or required to re-authenticate, depending on design. No inconsistent or insecure state (e.g., partial login with protected data visible) is observed.
- **Test Data:** Valid username and password  
- **Traceability:** KAN-3

---

### KAN-3-TC015 – Verify login fails with credentials containing leading/trailing spaces
- **Test Type:** Boundary  
- **Priority:** Low  
- **Preconditions:** User account exists; backend authentication service available; user logged out.
- **Steps:**
  1. Launch the mobile application.
  2. Navigate to the login screen.
  3. Enter the valid username with leading and trailing spaces.
  4. Enter the correct password with leading and trailing spaces.
  5. Tap the Login/Sign In button.
- **Expected Result:** Behavior follows defined trimming rules (not specified in ticket). For undefined requirements, confirm and document actual behavior: either spaces are trimmed and login succeeds, or treated as part of credentials and login fails. In either case, ensure handling is consistent and does not expose credentials in error messages.
- **Test Data:** Username: '  validUser  '; Password: '  validPassword  '  
- **Traceability:** KAN-3

---

### KAN-3-TC016 – Verify login with maximum allowed length for username and password
- **Test Type:** Boundary  
- **Priority:** Medium  
- **Preconditions:** Defined or assumed max length for username and password in test environment; test accounts created with boundary-length credentials if supported.
- **Steps:**
  1. Determine or assume maximum allowed length for username and password based on system or platform constraints.
  2. Create or identify a user with username at max allowed length and password at max allowed length (if supported).
  3. Launch the mobile application and navigate to login screen.
  4. Enter the boundary-length username.
  5. Enter the boundary-length password.
  6. Tap the Login/Sign In button.
- **Expected Result:** If boundary-length credentials are valid per backend rules, login succeeds and user is granted access. Input fields can handle max length without UI or functional issues.
- **Test Data:** Username and password strings at defined maximum length  
- **Traceability:** KAN-3

---

### KAN-3-TC017 – Verify login rejects credentials exceeding maximum allowed length
- **Test Type:** Boundary  
- **Priority:** Low  
- **Preconditions:** Defined or assumed max length for username and password; ability to input text beyond that length.
- **Steps:**
  1. Launch the mobile application and navigate to login screen.
  2. Attempt to enter username exceeding maximum allowed length.
  3. Attempt to enter password exceeding maximum allowed length.
  4. Tap the Login/Sign In button if extra characters can be entered.
- **Expected Result:** Either additional characters cannot be entered beyond max length, or validation fails and user is not authenticated with clear feedback (exact text unspecified). No buffer overflow or app crash occurs.
- **Test Data:** Username and password strings exceeding maximum allowed length  
- **Traceability:** KAN-3

---

### KAN-3-TC018 – Verify user cannot bypass login via direct API calls from the client
- **Test Type:** Integration  
- **Priority:** High  
- **Preconditions:** Ability to inspect or simulate calls made by the mobile client; user logged out.
- **Steps:**
  1. Launch the mobile application with a proxy that allows inspecting and manipulating API calls.
  2. Attempt to access protected resources APIs without performing a login (e.g., by replaying previously captured calls or constructing calls manually).
  3. Observe server response and client behavior.
- **Expected Result:** Protected resources cannot be accessed without proper authentication token. Server returns unauthorized/forbidden responses and client does not expose protected data.
- **Test Data:** Unauthenticated API calls to protected endpoints  
- **Traceability:** KAN-3

---

### KAN-3-TC019 – Verify logout revokes access and requires re-authentication
- **Test Type:** Integration  
- **Priority:** Medium  
- **Preconditions:** User is logged in successfully; logout feature available in application.
- **Steps:**
  1. Log in to the mobile application with valid credentials.
  2. Navigate to main application screen.
  3. Perform logout action (e.g., tap Logout button).
  4. Attempt to navigate back to main application content.
  5. Attempt to access any protected features.
- **Expected Result:** After logout, user is considered unauthenticated and must log in again to access protected features. Any attempt to access main application content triggers login mechanism.
- **Test Data:** Valid username/password; logged-in session followed by logout  
- **Traceability:** KAN-3

---

### KAN-3-TC020 – Verify multiple rapid login attempts with invalid credentials are handled safely
- **Test Type:** Negative  
- **Priority:** Medium  
- **Preconditions:** User account exists; backend authentication service available.
- **Steps:**
  1. Launch the mobile application and navigate to login screen.
  2. Enter valid username with invalid password.
  3. Tap Login/Sign In.
  4. Repeat invalid login attempt rapidly several times (e.g., 10–20 attempts).
- **Expected Result:** Application handles repeated invalid attempts without crashing or degrading severely. Authentication remains unsuccessful. If any rate limiting or lockout exists, behavior is consistent and does not leak security-sensitive information.
- **Test Data:** Valid username; repeated invalid password attempts  
- **Traceability:** KAN-3

---

### KAN-3-TC021 – Verify behavior when backend returns unexpected error for authentication
- **Test Type:** Edge Case  
- **Priority:** Medium  
- **Preconditions:** Ability to configure backend or mock service to return unexpected error codes (e.g., 5xx, malformed response).
- **Steps:**
  1. Configure authentication backend or mock to return an unexpected server error for login requests.
  2. Launch the mobile application and navigate to login screen.
  3. Enter valid credentials.
  4. Tap Login/Sign In button.
  5. Observe application response.
- **Expected Result:** Application handles unexpected backend errors gracefully, shows generic error indication, does not authenticate the user, and remains stable.
- **Test Data:** Valid username and password; backend configured for error responses  
- **Traceability:** KAN-3

---

### KAN-3-TC022 – Verify that authenticated users are not forced to re-login unnecessarily within active session
- **Test Type:** Functional  
- **Priority:** Low  
- **Preconditions:** User already authenticated; session within normal active period; app running.
- **Steps:**
  1. Log in with valid credentials.
  2. Navigate through various application screens.
  3. Return to home/main screen.
  4. Perform typical user actions for a reasonable period.
  5. Verify that login screen does not reappear without explicit logout or session expiry condition.
- **Expected Result:** User remains authenticated during active session and is not forced to re-login arbitrarily. Access to application features continues seamlessly.
- **Test Data:** Valid username/password; regular navigation  
- **Traceability:** KAN-3
