PRODUCTION MANAGEMENT SYSTEM - FIREBASE LIVE SYNC

This version keeps the existing UI and functionality, but replaces cross-device data storage with Firebase Realtime Database.

FILES
- index.html
- style.css
- script.js
- firebase-rules-development.json

IMPORTANT
The current login system is the same custom username/password system as the original site. For this quick live-sync version, Firebase Realtime Database rules need to allow the browser to read/write the shared data. That means the database is NOT secure for a production deployment and passwords are stored in the database.

For a real production/factory deployment, migrate the login to Firebase Authentication and use role-based Realtime Database Security Rules. Firebase recommends Authentication + Security Rules for protecting data.

SETUP
1. Open Firebase Console and create a Firebase project.
2. Add a Web App to the project.
3. Open Realtime Database and create a database.
4. Copy the exact Firebase Web App config from Project settings.
5. Open script.js and replace the values inside firebaseConfig:
   - apiKey
   - authDomain
   - databaseURL
   - projectId
   - storageBucket
   - messagingSenderId
   - appId
   Use the exact databaseURL shown by Firebase; it can vary by database region.
6. Open Realtime Database -> Rules.
7. For initial testing only, paste the contents of firebase-rules-development.json and publish the rules.
8. Open the website on the PC first. The existing local data will be migrated to Firebase if the Firebase database is empty.
9. Open the same GitHub Pages link on the phone or another PC. Both devices will now read/write the same Firebase data and updates will appear live without refreshing.

DEFAULT ACCOUNTS
Admin:
  Username: admin
  Password: admin123
  Department: Admin

Assembly:
  Username: assembly
  Password: 1234
  Department: Assembly

Packing:
  Username: packing
  Password: 1234
  Department: Packing

IMPORTANT DATA BEHAVIOR
- The first device connected to an empty Firebase database uploads its existing local data.
- Once Firebase already contains data, Firebase becomes the source of truth and replaces the browser's local copy.
- localStorage is still kept as a local cache/fallback, but it is no longer the shared database.
- Firebase Realtime Database onValue is used for live updates across devices.

GITHUB PAGES
After configuring script.js, upload/commit all required files to the same GitHub Pages repository:
  index.html
  style.css
  script.js

The Firebase SDK is loaded directly from Google's official gstatic CDN, so no npm or build step is required.
