# RSVP – React Native (Expo) + Appwrite Sample

Welcome to **RSVP**, a sample React Native app showcasing authentication, video uploads, and data management using [Expo](https://expo.dev/) and [Appwrite](https://appwrite.io/) on the backend. This project demonstrates how to use Expo Router for navigation, Nativewind (Tailwind CSS in React Native) for styling, and Appwrite for user authentication and file storage.

This project was created for **Edward Washington III** to highlight the ability to build a production-ready, scalable mobile solution. By leveraging Appwrite’s generous free tier—capable of handling up to 75,000 users—this example shows how to implement user signup/login flows, create video posts, manage user profiles, and more.

---

## Table of Contents

1. [Features](#features)  
2. [Tech Stack](#tech-stack)  
3. [Prerequisites](#prerequisites)  
4. [Installation](#installation)  
5. [Project Structure](#project-structure)  
6. [App Configuration & Environment Variables](#app-configuration--environment-variables)  
7. [Available Scripts](#available-scripts)  
8. [Usage & Workflow](#usage--workflow)  
   - [Authentication Flow](#authentication-flow)  
   - [Video Upload Flow](#video-upload-flow)  
   - [Search Functionality](#search-functionality)  
9. [Contributing](#contributing)  
10. [License](#license)  
11. [Contact](#contact)

---

## Features

1. **Authentication**  
   - User sign-up and login (Appwrite-powered).  
   - Persistent session management with Expo Router.

2. **Video Upload**  
   - Pick a video file & thumbnail image via [expo-document-picker](https://docs.expo.dev/versions/latest/sdk/document-picker/).  
   - Store uploaded videos and thumbnails in Appwrite’s storage.  
   - Display videos in a feed using [expo-video](https://docs.expo.dev/versions/latest/sdk/video/).

3. **Home Feed & Trending**  
   - Fetch and display all posts.  
   - Showcase the latest video uploads in a horizontal “Trending” section.

4. **User Profile**  
   - Display user’s personal posts.  
   - Logout functionality.

5. **Search**  
   - Search for videos by title or content prompt via [Appwrite Query](https://appwrite.io/docs/services/database).

6. **Scalable Backend**  
   - Uses Appwrite for up to 75,000 users on the free tier.

7. **Styling with Tailwind (Nativewind)**  
   - Consistent styling with utility classes.

8. **Expo Router Navigation**  
   - `(auth)` folder for sign-up and sign-in pages.  
   - `(tabs)` for bottom tab navigation (home, bookmark, create, profile).  
   - Single-file or folder-based routing with [Expo Router conventions](https://expo.github.io/router/docs).

---

## Tech Stack

- **React Native** (0.76.7) with [Expo](https://docs.expo.dev/)  
- **Appwrite** (authentication, database, file storage)  
- **Nativewind** (Tailwind CSS utility for RN)  
- **Expo Router** (nested routing)  
- **Expo Document Picker** & **Expo Video** (file picking + video component)  
- **React Native Appwrite** (Appwrite client library)

---

## Prerequisites

- **Node.js** (LTS version recommended)
- **Expo CLI** (either installed globally, or via `npx expo`)
- **Appwrite** instance (self-hosted or via [Appwrite Cloud](https://cloud.appwrite.io/))
- Mobile emulator or physical device (Android/iOS) to run the app

---

## Installation

1. **Clone the repository**:
   ```bash
   git clone https://github.com/<your-username>/<your-repo>.git
   cd <your-repo>


## install dependencies

npm install
# or
yarn install

Set up Appwrite:

Create a new Appwrite Project (e.g., “RSVP-Project”).
Note your Project ID, Endpoint, and API keys.
Create a users collection (or rely on Appwrite’s built-in auth).
Create a collection for posts (videos) and configure rules.
Create a storage bucket for video and thumbnail files.
Configure environment variables:
See App Configuration & Environment Variables below for more info.

Start the app:

npm start
# or
yarn start

For Android: npm run android
For iOS: npm run ios
For Web: npm run web

## Project structure

.
├── app
│   ├── (tabs)
│   │   ├── bookmark/         # Bookmark screen
│   │   ├── create/           # Create new video post
│   │   ├── home/             # Main feed screen
│   │   └── profile/          # User profile screen
│   ├── (auth)
│   │   ├── sign-in.jsx       # User login screen
│   │   └── sign-up.jsx       # User registration screen
│   ├── search/[query]/       # Search screen
│   ├── layout.jsx            # Root navigator (fonts + global setup)
│   └── index.jsx             # Welcome screen
├── assets/
│   ├── fonts/                # Custom fonts (Poppins)
│   ├── images/               # App images & icons
│   └── ...
├── components/
│   ├── Loader.jsx            # Loading indicator
│   ├── FormField.jsx         # Custom input field
│   ├── CustomButton.jsx      # Button component
│   └── ...
├── constants/
│   ├── images.js
│   ├── icons.js
│   └── ...
├── context/
│   └── GlobalProvider.jsx    # Global context for user session & state
├── lib/
│   ├── appwrite.js           # Appwrite client config + queries
│   └── useAppwrite.js        # Custom hook for Appwrite data fetching
├── tailwind.config.js        # Tailwind config for Nativewind
├── babel.config.js           # Babel config
├── app.json                  # Expo configuration
├── package.json
└── README.md                 # Project documentation


## App Configuration & Environment Variables
Appwrite Configuration
In lib/appwrite.js, you’ll see placeholders for your Appwrite project endpoint, project ID, and API keys (if applicable). Replace them with your own.

Optional: Use .env for environment variables (not committed to source control). In React Native, consider using packages like react-native-dotenv to manage these variables.

## Expo

Adjust iOS/Android config in app.json if needed.
Current config uses com.rodrigues.rsvp as an example.

Usage & Workflow
Authentication Flow
Welcome Screen (app/index.jsx)

Appears first.
“Continue with Email” button navigates to sign-in.
Sign In (app/(auth)/sign-in.jsx)

Users enter email + password.
Successful login navigates to main tab navigator.
Sign Up (app/(auth)/sign-up.jsx)

Users enter username, email, password.
On success, user is signed in automatically.
Global State

GlobalProvider holds user info + session data.
If user is already logged in, router redirects to /home.
Video Upload Flow
Create Screen (app/(tabs)/create/index.jsx)

Pick a video + thumbnail image with expo-document-picker.
Add an AI prompt (optional).
createVideoPost in lib/appwrite.js handles upload to Appwrite storage + DB record creation.
Home Screen (app/(tabs)/home/index.jsx)

Fetches all posts via Appwrite.
Displays them in a FlatList of VideoCard components.
User Profile (app/(tabs)/profile/index.jsx)

Shows the logged-in user’s own posts.
Includes logout button.
Search Functionality
Search Screen (app/search/[query]/index.jsx)

searchPosts query filters videos by title/content.
Displays matching posts or an empty state if none.
Trending

A horizontal “Latest Videos” section in the home screen.
Fetches the newest posts (getLatestPosts).
Contributing
Contributions are welcome! To contribute:

Fork the project
Create your feature branch: git checkout -b feature/my-new-feature
Commit your changes: git commit -m 'Add some feature'
Push to the branch: git push origin feature/my-new-feature
Open a Pull Request

## Contact
Author: [allahu rodrigues]
Email: [allahu.rodrigues@gmail.com]
Project: RSVP – React Native + Appwrite Sample