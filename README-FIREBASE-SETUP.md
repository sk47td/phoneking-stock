# PKGC Manager Stock Manager — Firebase setup

The web app is configured for Firebase project `phonekingstock` and manager email `phonekingkd@gmail.com`.

## 1. Authentication
1. Firebase Console → Build → Authentication → Sign-in method → enable **Email/Password**.
2. Create the manager account with `phonekingkd@gmail.com` and your chosen password.
3. Staff accounts can be created directly from PKGC Manager → Staff Management. The app creates the Firebase Authentication user and stores the selected access level.

## 2. Realtime Database
Create Realtime Database in Locked mode, then open **Rules** and replace the rules with `firebase-rules.json` from this package. Publish the rules.

The rules enforce:
- Manager email: full access.
- Staff + `active:true` + `access:'view'`: read-only inventory access.
- Staff + `active:true` + `access:'full'`: read/write inventory access.
- Removed staff (`active:false`): cannot read or write inventory through these rules.
- Staff records can only be changed by the manager.
- Audit history can be read by Manager and Full Access users; new Full Access audit entries must carry the authenticated user's UID.

## 3. 30-day history
PKGC Manager displays audit history from the last 30 days and records the acting user's name/email, action, item, details and timestamp. Manager sessions prune older audit records when history is loaded.

## 4. Staff removal
Removing a staff member sets `active:false`. Their Firebase Authentication account is not deleted by the browser-only app, but the PKGC Manager access is revoked immediately and the Firebase database rules deny inventory access. Previous audit records remain.

## 5. Run the app
Host the folder on a web server such as GitHub Pages, Netlify or Firebase Hosting. Do not open `index.html` directly from `file://`.

## 6. New model recommendations
The dashboard contains a review list of recent India launches as a convenience. It is a seeded list, not a live feed. Verify current local availability before ordering covers.

Never share Firebase passwords, OTPs, recovery codes or service-account private keys.

## IMPORTANT: Full-access staff write fix
The included `firebase-rules.json` explicitly allows authenticated staff accounts to write `/phoneking/data` when their `/phoneking/users/<uid>` record has:
- `role: "staff"`
- `active: true`
- `access: "full"`

Firebase Realtime Database rules are enforced on Firebase's servers; placing the rules file in GitHub does not publish them automatically.

### Publish the rules from Firebase Console
1. Open Firebase Console → Realtime Database → Rules.
2. Replace the existing rules with the contents of `firebase-rules.json`.
3. Click **Publish**.
4. Sign in again as a Full Access staff user and test Add/Edit/Delete.

### Optional Firebase CLI deployment
From this project folder, after installing/logging into the Firebase CLI:
`firebase deploy --only database`

The included `firebase.json` points the CLI to `firebase-rules.json`.
