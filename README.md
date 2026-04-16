# Roomies

> A Tinder-style roommate matching app built with Flutter & Firebase

Roomies connects people looking for roommates with house owners listing properties. Renters swipe through profiles to find compatible roommates, while house owners manage their listings and connect with potential tenants — all in one seamless mobile experience.

---

## Features

### For Renters
- **Swipe to Match** — Browse roommate profiles with a Tinder-style card stack. Swipe right to like, left to pass
- **Mutual Matching** — Both users must swipe right for a match to occur
- **Smart Filtering** — Never see the same profile twice; previously swiped users are excluded automatically
- **Detailed Profiles** — View budget range, work/study info, roommate preferences, and multiple photos

### For House Owners
- **Property Listings** — Create detailed house listings with type, price, number of rooms, condition, and location
- **Contact Management** — Share contact info directly with matched renters

### Shared Features
- **Real-time Messaging** — Chat with your matches instantly
- **Online Presence** — See when your matches are active
- **Profile Setup Flows** — Guided multi-step onboarding tailored to each user type
- **House Explorer** — Browse available properties on the Houses tab

---

## Screenshots
<img width="120" alt="image" src="https://github.com/user-attachments/assets/217abe45-fb15-4e5d-95d2-607fcf4b603a" />
<img width="120" alt="image" src="https://github.com/user-attachments/assets/9bc143c7-1706-4f82-b2d9-592f6382cf4b" />
<img width="120" alt="image" src="https://github.com/user-attachments/assets/e4e73354-0863-43d1-9a09-645e77659f70" />
<img width="120" height="1852" alt="image" src="https://github.com/user-attachments/assets/5fa0c848-5d31-4b13-98f9-ab2b61c81629" />
<img width="120" alt="image" src="https://github.com/user-attachments/assets/c60cdaf8-f1af-4803-96f4-fdd887814a31" />
<img width="120" alt="image" src="https://github.com/user-attachments/assets/be354840-f15e-4ba6-949b-9e9f0b41691c" />


---

## Tech Stack

| Layer | Technology |
|---|---|
| Framework | Flutter (Dart) |
| State Management | Provider |
| Authentication | Firebase Auth |
| Database | Cloud Firestore |
| Storage | Firebase Storage |

---

## Architecture

```
lib/
├── main.dart                  # App entry point & routing
├── pages/                     # Screens
│   ├── auth_page.dart         # Login / Sign-up
│   ├── setup_page.dart        # User type selection
│   ├── setup_profile_page.dart # Renter onboarding
│   ├── setup_house_page.dart  # Owner onboarding
│   ├── home_page.dart         # Main tab navigator
│   ├── roomies_page.dart      # Swipe discovery feed
│   ├── matches_page.dart      # Mutual matches list
│   ├── houses_page.dart       # Property listings
│   ├── chat_page.dart         # Direct messaging
│   └── owner_page.dart        # Owner dashboard
├── backend/
│   ├── database.dart          # Firestore service (all DB operations)
│   ├── user_profile_provider.dart
│   ├── current_user_provider.dart
│   ├── matches_provider.dart
│   └── setup_completion_provider.dart
├── models/                    # Data models (User, Message, etc.)
└── widgets/                   # Reusable UI components
```

The app follows an **MVVM-like pattern** using `Provider` for reactive state. Authentication state is tracked via a Firebase stream and routes the user to the appropriate screen (auth → setup → main app) automatically.

---

## How Matching Works

1. User A swipes right on User B → encounter recorded in Firestore
2. User B swipes right on User A → encounter recorded in Firestore
3. The app checks both encounter records — a **match is created only when both users have liked each other**
4. Both users can now message each other in the chat tab

---

## Getting Started

### Prerequisites

- Flutter SDK (`>=2.16.1`)
- A Firebase project with **Authentication**, **Firestore**, and **Storage** enabled

### Setup

```bash
# Clone the repo
git clone https://github.com/your-username/roomies.git
cd roomies

# Install dependencies
flutter pub get

# Add your Firebase config
# iOS: ios/Runner/GoogleService-Info.plist
# Android: android/app/google-services.json

# Run the app
flutter run
```

> Firebase configuration files are not included in this repository. You will need to connect your own Firebase project.

---

## Firestore Data Model

```
users/
└── {userId}/
    ├── name, email, birthdate, ...       # Core fields
    ├── personal_profile/                 # Renter: budget, work, preferences
    ├── house_profile/                    # Owner: property details
    ├── profile_images[]                  # Array of Storage URLs
    ├── encounters/                       # Swipe history
    └── messages/                        # Conversations
```

---

## Contributing

Pull requests are welcome. For major changes, please open an issue first to discuss what you'd like to change.

---

## License

[MIT](LICENSE)
