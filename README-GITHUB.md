# PKGC Manager

GitHub Pages-ready PWA for mobile cover and universal glass stock management.

## Publish
1. Create a GitHub repository.
2. Upload **all files and folders in this package** to the repository root.
3. In GitHub: **Settings → Pages → Deploy from a branch → main → / (root)**.
4. Open the HTTPS GitHub Pages URL on Android Chrome.
5. Use Chrome's **Install app / Add to Home screen** option.

## Firebase
Firebase configuration is already included in `firebase-config.js` and the existing app uses Firebase Authentication + Realtime Database. Keep your Firebase Realtime Database rules enabled; client-side UI restrictions are not a security boundary.

## PWA
- App name: PKGC Manager
- Short name: PKGC
- Display: standalone
- Orientation: portrait
- Theme: #f97316
- Background: #f3f4f6
- Service worker: `service-worker.js`
- Icons: `icons/icon-192.png`, `icons/icon-512.png`

Firebase/Google external requests are intentionally not intercepted by the service worker so live authentication and cloud synchronization continue to use the network.
