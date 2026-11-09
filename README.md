# Mile Run Tracker setup for GitHub Pages + Google Firebase

This app is designed to run as a static GitHub Pages site while storing all roster and run data in your Google/Firebase account.

## 1) Create a Firebase project

1. Go to https://console.firebase.google.com/
2. Click Add project
3. Give it a name, then complete the setup
4. In Project settings, add a web app
5. Copy the values for:
   - apiKey
   - authDomain
   - projectId
   - storageBucket
   - messagingSenderId
   - appId

## 2) Update the config in the app

Edit `index.html` and replace these values:

```js
const firebaseConfig = {
  apiKey: 'PASTE_YOUR_FIREBASE_API_KEY',
  authDomain: 'YOUR_PROJECT_ID.firebaseapp.com',
  projectId: 'YOUR_PROJECT_ID',
  storageBucket: 'YOUR_PROJECT_ID.appspot.com',
  messagingSenderId: 'PASTE_YOUR_SENDER_ID',
  appId: 'PASTE_YOUR_APP_ID'
};
```

## 3) Enable Google sign-in

In Firebase Console:

1. Go to Authentication
2. Select Sign-in method
3. Enable Google
4. Add your email as an authorized user if needed

## 4) Enable Firestore

1. Go to Firestore Database
2. Create a database in production mode or test mode
3. Choose a region close to you

## 5) Add Firestore security rules

Use something like this to restrict access to signed-in users only:

```js
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /{document=**} {
      allow read, write: if request.auth != null;
    }
  }
}
```

## 6) GitHub Pages setup

1. Push `index.html` to the `main` branch
2. Go to GitHub repository settings
3. Open Pages
4. Set Source to `Deploy from a branch`
5. Select the `main` branch and `/ (root)` folder
6. Save

After a few minutes your site should be available at:

https://YOUR_GITHUB_USERNAME.github.io/YOUR_REPO_NAME/

## 7) Current limitation

This app still uses the same Firestore document layout as the original tracked app, so the fields are:

- `cadets/{id}`
- `results/{runId}_{cadetId}`
- `state/current`
- `state/today`

If you want, I can next help you convert this into a cleaner Google-authenticated app with a sign-in button built directly into the page and a full Firebase configuration checklist for your exact project.
