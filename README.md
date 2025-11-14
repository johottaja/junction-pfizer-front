# Migraine Tracker 🧠

A comprehensive mobile application for tracking, predicting, and managing migraine episodes. Built with React Native and Expo, this app provides AI-powered insights to help users understand their migraine patterns and triggers.

## 📋 Table of Contents

- [Features](#features)
- [Technology Stack](#technology-stack)
- [Getting Started](#getting-started)
  - [Prerequisites](#prerequisites)
  - [Installation](#installation)
  - [Running the App](#running-the-app)
- [Project Structure](#project-structure)
- [Development](#development)
  - [Available Scripts](#available-scripts)
  - [Code Style](#code-style)
- [App Features](#app-features)
- [Contributing](#contributing)
- [License](#license)

## ✨ Features

### 🏠 Today Dashboard
- Daily migraine status tracking
- Migraine-free streak counter
- Weekly average statistics
- Recent activity timeline
- Quick action shortcuts

### 🔮 AI Predictions
- Machine learning-powered migraine forecasts
- Risk level indicators (High, Medium, Low)
- Probability percentages for upcoming episodes
- Historical episode statistics
- Pattern analysis and insights

### 📝 Migraine Reporting
- Pain intensity scale (1-10)
- Trigger identification (Stress, Sleep, Weather, Hormones, Food, Light, Noise)
- Symptom tracking (Nausea, Light sensitivity, Sound sensitivity, Aura, Dizziness)
- Episode duration tracking
- Detailed episode logging

### ⚙️ Settings & Preferences
- Push notification controls
- Reminder alert management
- Analytics preferences
- Privacy policy and terms
- App information and support

## 🛠 Technology Stack

- **Framework**: [React Native](https://reactnative.dev/) 0.81.5
- **UI Framework**: [Expo](https://expo.dev/) ~54.0.23
- **Navigation**: [Expo Router](https://docs.expo.dev/router/introduction/) ~6.0.14 (File-based routing)
- **Language**: [TypeScript](https://www.typescriptlang.org/) ~5.9.2
- **State Management**: React Hooks (useState, useEffect)
- **Styling**: StyleSheet API with custom theming
- **Icons**: [Expo Symbols](https://docs.expo.dev/guides/icons/) & SF Symbols
- **Platform Support**: iOS, Android, Web

### Key Dependencies
- `react-navigation` - Navigation components
- `react-native-safe-area-context` - Safe area handling
- `react-native-gesture-handler` - Gesture support
- `react-native-reanimated` - Animations
- `expo-haptics` - Haptic feedback
- `expo-image` - Optimized image component

## 🚀 Getting Started

### Prerequisites

- **Node.js**: Version 18.x or higher
- **npm** or **yarn**: Latest version
- **Expo CLI**: Installed globally (optional but recommended)
- **Mobile Device/Emulator**:
  - For iOS: Xcode with iOS Simulator
  - For Android: Android Studio with Android Emulator
  - Or: Expo Go app on your physical device

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/johottaja/junction-pfizer-front.git
   cd junction-pfizer-front
   ```

2. **Install dependencies**
   ```bash
   npm install
   ```

### Running the App

1. **Start the development server**
   ```bash
   npm start
   # or
   npx expo start
   ```

2. **Run on specific platform**
   ```bash
   # iOS Simulator
   npm run ios
   # or
   npx expo start --ios

   # Android Emulator
   npm run android
   # or
   npx expo start --android

   # Web Browser
   npm run web
   # or
   npx expo start --web
   ```

3. **Using Expo Go** (on physical device)
   - Install Expo Go from [App Store](https://apps.apple.com/app/expo-go/id982107779) or [Google Play](https://play.google.com/store/apps/details?id=host.exp.exponent)
   - Scan the QR code shown in the terminal

## 📁 Project Structure

```
junction-pfizer-front/
├── app/                        # Application screens (file-based routing)
│   ├── (tabs)/                # Tab-based screens
│   │   ├── today.tsx          # Dashboard/Today screen
│   │   ├── prediction.tsx     # AI Predictions screen
│   │   ├── report.tsx         # Migraine reporting screen
│   │   ├── settings.tsx       # Settings screen
│   │   └── _layout.tsx        # Tab navigation layout
│   ├── _layout.tsx            # Root layout
│   └── modal.tsx              # Modal screen example
├── assets/                     # Static assets
│   └── images/                # App icons and images
├── components/                 # Reusable components
│   ├── ui/                    # UI-specific components
│   │   ├── icon-symbol.tsx    # Icon wrapper component
│   │   └── collapsible.tsx    # Collapsible component
│   ├── themed-text.tsx        # Themed text component
│   ├── themed-view.tsx        # Themed view component
│   └── ...                    # Other components
├── constants/                  # App constants
│   └── theme.ts               # Color themes and styles
├── hooks/                      # Custom React hooks
│   └── use-color-scheme.tsx   # Color scheme hook
├── scripts/                    # Utility scripts
├── app.json                   # Expo configuration
├── package.json               # Dependencies and scripts
├── tsconfig.json              # TypeScript configuration
└── README.md                  # This file
```

## 💻 Development

### Available Scripts

```bash
# Start development server
npm start

# Start with cleared cache
npx expo start -c

# Run linter
npm run lint

# Platform-specific commands
npm run ios          # Run on iOS simulator
npm run android      # Run on Android emulator
npm run web          # Run in web browser

# Reset project (use with caution)
npm run reset-project
```

### Code Style

This project uses:
- **ESLint** for code linting (expo configuration)
- **TypeScript** for type safety
- **Prettier** (recommended for code formatting)

Run the linter before committing:
```bash
npm run lint
```

### Theming

The app supports both light and dark modes:
- Theme files are located in `constants/theme.ts`
- Use `useColorScheme()` hook to access current theme
- Wrap text with `<ThemedText>` and views with `<ThemedView>` for automatic theming

## 📱 App Features

### Navigation Structure

The app uses **Expo Router** with file-based routing:
- **Tab Navigation**: Bottom tabs for main screens (Today, Predictions, Report, Settings)
- **Stack Navigation**: For modal overlays and detailed views
- **Deep Linking**: Supports custom URL schemes

### Data Flow (Current Architecture)

Currently using mock data with plans to integrate:
- Local storage (AsyncStorage) for offline data persistence
- Backend API for data synchronization
- Machine learning models for prediction accuracy

### Responsive Design

- **Safe Area Support**: Handles notches and safe areas on all devices
- **Platform-Specific Styles**: Optimized for both iOS and Android
- **Adaptive Layouts**: Responsive to different screen sizes
- **Theme Support**: Light and dark mode

## 🤝 Contributing

Contributions are welcome! Please follow these guidelines:

1. **Fork the repository**
2. **Create a feature branch**
   ```bash
   git checkout -b feature/your-feature-name
   ```
3. **Make your changes**
   - Follow existing code style
   - Add TypeScript types
   - Test on both iOS and Android if possible
4. **Commit your changes**
   ```bash
   git commit -m "Add: your feature description"
   ```
5. **Push to your fork**
   ```bash
   git push origin feature/your-feature-name
   ```
6. **Open a Pull Request**

### Development Guidelines

- Use functional components with hooks
- Maintain type safety with TypeScript
- Follow the existing component structure
- Test on multiple platforms when possible
- Keep styling consistent with the theme system
- Document complex logic with comments

## 📄 License

This project is part of the Junction Pfizer Hackathon.

## 🆘 Support

For issues, questions, or contributions:
- Open an issue on GitHub
- Contact the development team

## 🙏 Acknowledgments

- Built with [Expo](https://expo.dev)
- UI inspired by modern health tracking applications
- Designed for Junction Pfizer Hackathon

---

**Version**: 1.0.0  
**Last Updated**: November 2024
