# Settings — Operations Manual

This manual is for operations staff supporting Lobsters users with account settings: profile changes, passwords, notifications, two-factor authentication (2FA), external integrations (Gravatar, Pushover, Mastodon, GitHub), invitations, and account deactivation. All procedures below assume the user is logged in; the entire Settings area requires a logged-in session.

## Where things live

- Main page: **/settings** — profile, security, notifications, mailing list, appearance, external accounts, invitations, deactivation.
- 2FA pages: **/settings/2fa** (start), then enroll → verify screens.
- Mastodon connect starts at **/settings/mastodon_authentication**.

The Settings page subnav links to the user's Public Profile, their Filtered Tags page, and Logout.

## Procedure: update profile or preferences

1. Open **/settings**.
2. Edit the relevant fields. Sections, top to bottom: Public Profile Information; Security Settings; Comment Reply / Comment Mention / Private Message Notification Settings; Submitted Story Comment Settings; Mailing List Settings; Miscellaneous Settings (color scheme, contrast, previews, avatars).
3. Click **Save Account Settings** (there is a save button after the profile section and another at the bottom — both submit the same form).
4. Confirm the "Successfully updated settings." banner.

Operational notes:

- **Username changes are logged**: each rename writes a public moderation-log entry ("changed own username from 'X' to 'Y'"). Warn users expecting anonymity.
- **Email on a disposable-domain blocklist**: the form shows "We don't send email to disposable email domains; change your email address." The user must switch to a non-disposable address to receive mail.
- **Mailing list mode** options: *No e-mails* / *All stories and comments* / *Only stories*. The page displays the user's private list address (`<site>-<token>@<domain>`). If a user reports posts appearing under their account that they didn't make via the website, check whether their list address leaked — mail sent to it posts as them.

## Procedure: password change

1. On **/settings**, under **Security Settings**, have the user fill **Current Password**, **New Password**, **Confirm Password**.
2. Click **Save Account Settings**.

- Error "Your current password was not entered correctly." → the current password is wrong; nothing was saved.
- After a successful change the user's **other sessions are logged out** (session token is rotated). This is expected, not a bug.
- Changing non-password settings does not require the current password.

## Procedure: enable 2FA

1. On **/settings**, next to **Two-Factor Auth**, click **Enroll** (status shows "Disabled" beforehand).
2. Enter the current password, click **Continue**.
3. On the enrollment screen, scan the QR code with a TOTP app (or expand **Reveal Secret** to enter the secret manually).
4. Click **Verify and Enable**, enter the six-digit code from the app, click **Verify and Enable** again.
5. Success banner: "Two-Factor Authentication has been enabled on your account." The Settings page now shows **Enabled** in green.

Failure modes:

- "Your enrollment period timed out." — more than **15 minutes** elapsed since the password confirmation. Restart from step 1.
- "Your TOTP code was invalid, please verify the current code in your TOTP application." — usually device clock drift or reading an old code; retry with a fresh code.
- Enabling 2FA rotates the session token: other devices get signed out. Expected.

## Procedure: disable 2FA

1. On **/settings**, next to **Two-Factor Auth** (showing **Enabled**), click **Disable**.
2. Enter the current password and click **Disable Two-Factor Authentication**.
3. Confirm the banner "Two-Factor Authentication has been disabled."

If the user has lost both their password and TOTP device, this self-service path is unavailable — escalate per your account-recovery process.

## Procedure: Pushover subscription

Precondition: the site must be configured for Pushover; if not, the button is absent and any attempt returns "This site is not configured for Pushover".

1. On **/settings**, under **External Accounts**, click **Subscribe With Pushover**.
2. The user approves the subscription on pushover.net and is returned automatically.
3. Confirm banner: "Your account is now setup for Pushover notifications."
4. The user can now tick the **Receive Pushover Alert** checkboxes in the notification sections.

To stop alerts: click **Manage Pushover Subscription** and unsubscribe at Pushover; on return the banner reads "Your account is no longer setup for Pushover notifications."

Troubleshooting: "No random token present in session/URL" on the callback → the return trip lost its anti-forgery token (stale tab, cookies cleared mid-flow). Have the user redo the subscription in one sitting, same browser.

## Procedure: connect Mastodon

1. On **/settings**, under **External Accounts**, click **Connect** next to Mastodon.
2. Enter the instance as a name or URL (e.g. `mastodon.social`); a profile URL or `@user@instance` handle is also accepted. Click **Continue**.
3. The user authorizes on their instance (only the read-account scope is requested) and returns.
4. Confirm banner: "Linked to Mastodon user @username@instance."

Error reference:

- "Invalid OAuth state" — the state token didn't match (stale tab or replay). Restart the flow.
- "`<instance>` isn't resolving to an IP, check for typos?" — misspelled hostname.
- "App registration failed, is `<instance>` a Mastodon instance?" / "didn't return a client_id and client_secret" / "responded with non-parseable JSON" — the server at that hostname is not a (working) Mastodon instance.
- "`<instance>` isn't a working SSL server" — TLS problem on the instance side.

To unlink: click **Disconnect** next to the linked handle. Banner: "Your Mastodon association has been removed." Revocation on the remote instance is best-effort — if the instance is gone, the local link is still removed.

## Procedure: connect GitHub

1. On **/settings**, under **External Accounts**, click **Connect** next to GitHub (shown only when GitHub integration is configured).
2. Authorize on github.com; the user returns automatically.
3. Confirm banner: "Your account has been linked to GitHub user <username>." The profile row now links to the GitHub account.

To unlink: click **Disconnect**. Banner: "Your GitHub association has been removed." If you also see a notice that GitHub returned an API error on revocation, instruct the user to remove the token themselves at github.com/settings/applications.

"Invalid OAuth state" during connect → restart the flow in the same browser session.

## Procedure: invitations

The **Invite a New User** form is on **/settings**. If the account is not currently allowed to invite, the page displays the reason instead of the form (e.g. restrictions on new or sanctioned accounts). There is no settings-side override; handle exceptions through moderation.

## Procedure: account deactivation

Walk the user through the consequences listed on the page **before** they confirm:

- Profile will show the account as deactivated; login is blocked.
- Reactivation is self-service via password reset.
- Username remains reserved.
- Private messages are deleted (recipients keep their copies); submitted stories are kept; negatively-scored comments are deleted.
- Optional **Disown stories/comments**: all their stories and comments are relisted under "inactive-user".

Steps:

1. On **/settings**, scroll to **Deactivate Account**.
2. Enter the password in **Verify Password**, tick **I am sure** (required), optionally tick **Disown stories/comments**.
3. Click **Yes, Deactivate My Account**.
4. The user is logged out and lands on the homepage with a farewell banner.

Errors: 'You did not check the "I am sure" checkbox.' or "Given password doesn't match account." — fix the corresponding input and resubmit. Every deactivation is recorded in the moderation log (self-initiated, no moderator), including whether content was disowned — useful for audit queries.

## Quick triage table

| User report | Likely cause | First action |
|---|---|---|
| "Settings won't save, asks for password" | New-password field filled, current password wrong/blank | Clear the new-password fields or supply current password |
| "Logged out everywhere after changing password" | Session rotation on password change | Expected behavior; log back in |
| "2FA setup keeps timing out" | >15 min between password confirm and code verify | Redo in one sitting |
| "Pushover boxes don't work" | No Pushover subscription | Subscribe under External Accounts first |
| "Invalid OAuth state" (GitHub/Mastodon) | Stale tab / mismatched state token | Restart the connect flow |
| "Posts appeared under my account from email" | Leaked private mailing-list address | User should treat the address as a credential; investigate source of leak |
