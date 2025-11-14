# Contributing to Migraine Tracker

Thank you for your interest in contributing to the Migraine Tracker application! This document provides guidelines and instructions for contributing to the project.

## Table of Contents

- [Code of Conduct](#code-of-conduct)
- [Getting Started](#getting-started)
- [Development Workflow](#development-workflow)
- [Coding Standards](#coding-standards)
- [Commit Guidelines](#commit-guidelines)
- [Pull Request Process](#pull-request-process)
- [Testing Guidelines](#testing-guidelines)
- [Documentation](#documentation)
- [Issue Reporting](#issue-reporting)

## Code of Conduct

### Our Pledge

We are committed to providing a welcoming and inclusive environment for all contributors, regardless of experience level, gender, gender identity and expression, sexual orientation, disability, personal appearance, body size, race, ethnicity, age, religion, or nationality.

### Our Standards

**Positive behavior includes:**
- Being respectful and inclusive
- Welcoming differing viewpoints
- Accepting constructive criticism gracefully
- Focusing on what's best for the community
- Showing empathy towards others

**Unacceptable behavior includes:**
- Harassment or discriminatory language
- Trolling or insulting comments
- Personal or political attacks
- Publishing others' private information
- Other conduct that could be considered inappropriate

## Getting Started

### Prerequisites

Before contributing, ensure you have:

1. **Node.js** (version 18.x or higher)
2. **npm** or **yarn**
3. **Git**
4. **Code editor** (VS Code recommended)
5. **Expo CLI** (optional but recommended)
6. **iOS/Android development environment** (for native testing)

### Setting Up Your Development Environment

1. **Fork the repository**
   - Visit https://github.com/johottaja/junction-pfizer-front
   - Click the "Fork" button in the top right

2. **Clone your fork**
   ```bash
   git clone https://github.com/YOUR_USERNAME/junction-pfizer-front.git
   cd junction-pfizer-front
   ```

3. **Add upstream remote**
   ```bash
   git remote add upstream https://github.com/johottaja/junction-pfizer-front.git
   ```

4. **Install dependencies**
   ```bash
   npm install
   ```

5. **Start the development server**
   ```bash
   npm start
   ```

### VS Code Setup (Recommended)

Install these extensions:
- **ESLint** - Code linting
- **Prettier** - Code formatting
- **React Native Tools** - React Native development
- **TypeScript + React** - TypeScript support
- **Expo Tools** - Expo development support

## Development Workflow

### 1. Create a Feature Branch

Always create a new branch for your changes:

```bash
git checkout -b feature/your-feature-name
# or
git checkout -b fix/your-bug-fix
```

**Branch naming conventions:**
- `feature/` - New features
- `fix/` - Bug fixes
- `docs/` - Documentation updates
- `refactor/` - Code refactoring
- `test/` - Adding or updating tests
- `chore/` - Maintenance tasks

### 2. Make Your Changes

- Write clean, readable code
- Follow existing code patterns
- Add comments for complex logic
- Update documentation as needed
- Test your changes thoroughly

### 3. Keep Your Branch Updated

Regularly sync with the upstream repository:

```bash
git fetch upstream
git rebase upstream/main
```

### 4. Run Tests and Linting

Before committing, ensure your code passes all checks:

```bash
# Run linter
npm run lint

# Fix linting issues automatically
npm run lint -- --fix

# Run tests (when available)
npm test
```

## Coding Standards

### TypeScript Guidelines

1. **Always use TypeScript types**
   ```typescript
   // Good ✓
   interface Episode {
     id: string;
     intensity: number;
   }
   
   const episode: Episode = { id: '123', intensity: 7 };
   
   // Bad ✗
   const episode = { id: '123', intensity: 7 };
   ```

2. **Avoid `any` type**
   ```typescript
   // Good ✓
   const data: Episode[] = [];
   
   // Bad ✗
   const data: any = [];
   ```

3. **Use interfaces for objects**
   ```typescript
   // Good ✓
   interface Props {
     title: string;
     onPress: () => void;
   }
   
   // Acceptable for simple types
   type Status = 'active' | 'inactive';
   ```

### React/React Native Guidelines

1. **Use functional components**
   ```typescript
   // Good ✓
   const MyComponent = () => {
     return <View />;
   };
   
   // Avoid class components
   class MyComponent extends React.Component { }
   ```

2. **Use hooks properly**
   ```typescript
   // Good ✓
   const [state, setState] = useState(initialValue);
   
   useEffect(() => {
     // Effect logic
     return () => {
       // Cleanup
     };
   }, [dependencies]);
   ```

3. **Memoize expensive operations**
   ```typescript
   const expensiveValue = useMemo(() => {
     return computeExpensiveValue(data);
   }, [data]);
   
   const handleCallback = useCallback(() => {
     doSomething(param);
   }, [param]);
   ```

### Styling Guidelines

1. **Use StyleSheet.create**
   ```typescript
   const styles = StyleSheet.create({
     container: {
       flex: 1,
       padding: 20,
     },
   });
   ```

2. **Use theme system**
   ```typescript
   const colorScheme = useColorScheme();
   const theme = Colors[colorScheme ?? 'light'];
   
   <View style={{ backgroundColor: theme.background }} />
   ```

3. **Platform-specific styles**
   ```typescript
   const styles = StyleSheet.create({
     shadow: {
       ...Platform.select({
         ios: {
           shadowColor: '#000',
           shadowOffset: { width: 0, height: 2 },
           shadowOpacity: 0.1,
           shadowRadius: 8,
         },
         android: {
           elevation: 2,
         },
       }),
     },
   });
   ```

### File Organization

```typescript
// 1. React and React Native imports
import React, { useState, useEffect } from 'react';
import { View, Text, StyleSheet } from 'react-native';

// 2. Third-party library imports
import { SafeAreaView } from 'react-native-safe-area-context';

// 3. Local component imports
import { ThemedText } from '@/components/themed-text';
import { ThemedView } from '@/components/themed-view';

// 4. Constants and utilities
import { Colors } from '@/constants/theme';
import { useColorScheme } from '@/hooks/use-color-scheme';

// 5. Type definitions
interface Props {
  title: string;
}

// 6. Component definition
export default function MyComponent({ title }: Props) {
  // Component logic
}

// 7. Styles
const styles = StyleSheet.create({
  // Style definitions
});
```

### Naming Conventions

- **Components**: PascalCase (`ThemedText`, `IconSymbol`)
- **Files**: kebab-case or camelCase (`themed-text.tsx`, `useColorScheme.tsx`)
- **Functions**: camelCase (`handlePress`, `fetchData`)
- **Constants**: UPPER_SNAKE_CASE (`API_BASE_URL`, `MAX_RETRIES`)
- **Interfaces/Types**: PascalCase (`Episode`, `UserStats`)

## Commit Guidelines

### Commit Message Format

Follow the conventional commits specification:

```
<type>(<scope>): <subject>

<body>

<footer>
```

**Types:**
- `feat` - New feature
- `fix` - Bug fix
- `docs` - Documentation changes
- `style` - Code style changes (formatting, etc.)
- `refactor` - Code refactoring
- `test` - Adding or updating tests
- `chore` - Maintenance tasks

**Examples:**

```bash
feat(report): add duration tracking to migraine reports

Added a duration field to the report form allowing users to track
how long their migraine episodes last.

Closes #123
```

```bash
fix(predictions): correct probability calculation

The prediction probability was being calculated incorrectly,
leading to inaccurate risk assessments.

Fixes #456
```

```bash
docs(readme): update installation instructions

Updated the README with clearer installation steps and
added troubleshooting section.
```

### Commit Best Practices

1. **Make atomic commits** - One logical change per commit
2. **Write descriptive messages** - Explain what and why, not how
3. **Reference issues** - Include issue numbers when applicable
4. **Keep commits small** - Easier to review and revert if needed

## Pull Request Process

### Before Submitting

1. ✅ Code follows style guidelines
2. ✅ All tests pass
3. ✅ Linting passes without errors
4. ✅ Documentation is updated
5. ✅ Commit messages follow conventions
6. ✅ Branch is up-to-date with main

### Submitting a Pull Request

1. **Push your branch**
   ```bash
   git push origin feature/your-feature-name
   ```

2. **Create pull request**
   - Go to the repository on GitHub
   - Click "New Pull Request"
   - Select your branch
   - Fill in the PR template

3. **PR Title Format**
   ```
   feat: Add episode duration tracking
   fix: Correct prediction probability calculation
   docs: Update API documentation
   ```

4. **PR Description Template**
   ```markdown
   ## Description
   Brief description of changes
   
   ## Type of Change
   - [ ] Bug fix
   - [ ] New feature
   - [ ] Documentation update
   - [ ] Code refactoring
   
   ## Testing
   - [ ] Tested on iOS
   - [ ] Tested on Android
   - [ ] Tested on Web
   
   ## Screenshots (if applicable)
   Add screenshots here
   
   ## Related Issues
   Closes #123
   ```

### Review Process

1. At least one maintainer review required
2. All CI checks must pass
3. Address review comments
4. Maintain professional discussion
5. Be patient - reviews may take time

### After Approval

- Maintainers will merge your PR
- Your branch will be deleted
- Changes will be deployed in next release

## Testing Guidelines

### Manual Testing

Before submitting, test your changes on:

1. **iOS Simulator/Device**
2. **Android Emulator/Device**
3. **Web Browser** (if applicable)

### Test Different Scenarios

- ✅ Light and dark themes
- ✅ Different screen sizes
- ✅ Edge cases and error states
- ✅ Accessibility features
- ✅ Performance with large datasets

### Future: Automated Testing

When test infrastructure is added:

```typescript
// Example test structure
describe('ReportScreen', () => {
  it('should render correctly', () => {
    // Test implementation
  });
  
  it('should validate intensity selection', () => {
    // Test implementation
  });
});
```

## Documentation

### Code Documentation

1. **Add JSDoc comments for complex functions**
   ```typescript
   /**
    * Calculates the risk level based on prediction probability
    * @param probability - Percentage probability (0-100)
    * @returns Risk level: 'low', 'medium', or 'high'
    */
   function calculateRisk(probability: number): 'low' | 'medium' | 'high' {
     // Implementation
   }
   ```

2. **Comment complex logic**
   ```typescript
   // Calculate streak by finding consecutive days without migraines
   const streak = episodes.reduce((acc, episode) => {
     // Implementation with explanation
   }, 0);
   ```

### Documentation Updates

Update relevant documentation when:
- Adding new features
- Changing APIs or interfaces
- Modifying project structure
- Adding dependencies
- Changing build/deployment process

## Issue Reporting

### Before Creating an Issue

1. **Search existing issues** - Your issue may already exist
2. **Check documentation** - The answer might be documented
3. **Try latest version** - Bug might be fixed

### Creating a Good Issue

**Bug Reports should include:**
- Clear, descriptive title
- Steps to reproduce
- Expected behavior
- Actual behavior
- Screenshots/videos
- Environment details (OS, device, app version)
- Error messages/logs

**Feature Requests should include:**
- Clear description of the feature
- Use case and benefits
- Proposed implementation (optional)
- Alternative solutions considered

### Issue Templates

**Bug Report:**
```markdown
## Description
Brief description of the bug

## Steps to Reproduce
1. Go to '...'
2. Click on '...'
3. Scroll down to '...'
4. See error

## Expected Behavior
What should happen

## Actual Behavior
What actually happens

## Screenshots
Add screenshots here

## Environment
- OS: [iOS/Android/Web]
- Device: [iPhone 14, Pixel 7, etc.]
- App Version: [1.0.0]
```

**Feature Request:**
```markdown
## Feature Description
Brief description of the feature

## Problem It Solves
What problem does this solve?

## Proposed Solution
How should it work?

## Alternatives Considered
What other solutions did you consider?
```

## Getting Help

- **Documentation**: Check README.md and ARCHITECTURE.md
- **Issues**: Search existing issues or create new one
- **Discussions**: Use GitHub Discussions for questions
- **Email**: Contact the maintainers

## Recognition

Contributors will be:
- Listed in CONTRIBUTORS.md
- Credited in release notes
- Thanked in the community

## License

By contributing, you agree that your contributions will be licensed under the same license as the project.

---

Thank you for contributing to Migraine Tracker! 🙏

