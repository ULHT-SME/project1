# Project 1

## Project Overview

This midterm project is your opportunity to demonstrate mastery of Flutter development fundamentals by building a complete, functional mobile application with cloud persistence. You will design and implement a multi-screen app that integrates Firebase Firestore for real-time data management, implements proper state management patterns, and showcases clean UI/UX design principles.

## Learning Objectives

By completing this project, you will demonstrate your ability to:

1. **Design and implement** a multi-screen Flutter application with proper navigation architecture
2. **Integrate Firebase Firestore** for cloud-based data persistence with real-time synchronization
3. **Apply state management patterns** using Provider or setState appropriately for different use cases
4. **Implement CRUD operations** (Create, Read, Update, Delete) with proper error handling and validation
5. **Design intuitive user interfaces** following Material Design guidelines and Flutter best practices
6. **Structure a Flutter project** with modular, maintainable code organization (models, services, screens, widgets)
7. **Handle asynchronous operations** gracefully with appropriate loading, success, and error states
8. **Document your work** professionally with clear code comments and project documentation

---

## Project Theme Options

Choose **one** of the following themes for your application, or propose your own:

### Option 1: Personal Notes Application
Build a cloud-synced notes app where users can create, organize, and manage text-based notes.

**Key Features:**
- Create, edit, and delete notes with title and content
- Organize notes by categories or tags
- Search and filter functionality
- Real-time sync across devices via Firestore
- Note timestamps (created/modified dates)

**Example Use Case:** Students taking class notes that sync across phone and tablet

---

### Option 2: Task Manager / Todo Application
Develop a productivity app for managing tasks and tracking completion status.

**Key Features:**
- Create tasks with title, description, due date, and priority
- Mark tasks as complete/incomplete
- Filter by status (all, pending, completed)
- Organize tasks by categories or projects
- Real-time updates to task list

**Example Use Case:** Daily task management for students balancing coursework and personal projects

---

### Option 3: Recipe Collection App
Create a digital cookbook where users can save and organize their favorite recipes.

**Key Features:**
- Add recipes with name, ingredients, instructions, and cooking time
- Categorize by meal type (breakfast, lunch, dinner, dessert)
- Search recipes by name or ingredient
- Mark recipes as favorites
- Display recipe details with formatted instructions

**Example Use Case:** Home cooks organizing family recipes and meal planning

---

### Option 4: Book Library / Reading Tracker
Build a personal library management system for tracking books and reading progress.

**Key Features:**
- Add books with title, author, genre, and pages
- Track reading status (want to read, currently reading, completed)
- Add personal ratings and notes
- Filter and sort by status, author, or rating
- Display reading statistics

**Example Use Case:** Avid readers tracking their reading journey and recommendations

---

### Option 5: Expense Tracker
Develop a personal finance app for monitoring daily expenses and spending patterns.

**Key Features:**
- Log expenses with amount, category, description, and date
- Categorize expenses (food, transport, entertainment, etc.)
- View expense history with date filtering
- Calculate total spending by category or date range
- Visual indicators for spending patterns

**Example Use Case:** Students managing monthly budgets and tracking spending habits

---

### Option 6: Custom Proposal
Have a unique idea? Propose your own project theme!

**Requirements for Custom Proposals:**
- Submit a brief proposal describing your app concept
- Must include clear explanation of CRUD operations specific to your domain
- Must be feasible within the project timeline
- Requires professor approval **before** starting development

---

## Functional Requirements

Your application **must** implement the following core functionality:

### 1. CRUD Operations

Implement complete Create, Read, Update, and Delete functionalities:

- **Create:** Add new items to Firestore with validation
  - Input forms with at least 3 fields
  - Client-side validation (non-empty fields, format checks)
  - Success confirmation to user
  
- **Read:** Display all items from Firestore collection
  - Use StreamBuilder for real-time updates
  - Handle empty state (no items yet)
  - Proper loading indicators
  
- **Update:** Edit existing items
  - Pre-populate form with current data
  - Save changes back to Firestore
  - Confirmation before saving
  
- **Delete:** Remove items from Firestore
  - Confirmation dialog before deletion
  - Handle deletion errors gracefully

### 2. Multi-Screen Architecture 

Your app must have **at least 3 distinct screens**:

- **List/Home Screen:** Display all items from Firestore
  - Use ListView or GridView for data display
  - Navigation to add/detail screens
  - Visual indicators for item status (if applicable)
  
- **Add/Edit Screen:** Form for creating or editing items
  - Reusable form for both create and edit operations
  - Input validation with error messages
  - Clear cancel/save actions
  
- **Detail Screen OR Settings Screen:**
  - **Detail Screen:** View full information about a selected item
  - **Settings Screen:** App settings, about info, or user preferences
  - Proper navigation flow (back button, app bar)

### 3. State Management 

Implement appropriate state management:

- Use **Provider** for app-wide state (recommended) OR
- Use **setState** for local widget state where appropriate
- Demonstrate understanding of when to use each approach
- Properly dispose of resources (controllers, streams)

### 4. Firebase Firestore Integration 

Properly integrate and use Cloud Firestore:

- Initialize Firebase in your app
- Create at least one Firestore collection
- Implement proper data models (Dart classes with fromFirestore/toFirestore)
- Use StreamBuilder for real-time data synchronization
- Handle Firestore errors (network issues, permission errors)
- Use appropriate Firestore queries (orderBy, where, limit)

### 5. User Interface & Experience 

Design a clean, intuitive interface:

- Follow Material Design guidelines
- Consistent theming (colors, typography, spacing)
- Appropriate widgets for each use case
- Responsive layouts that adapt to different screen sizes
- Proper use of loading indicators and error messages
- Smooth navigation transitions

---

## Technical Guidelines

### Required Dependencies

Your `pubspec.yaml` must include:

```yaml
dependencies:
  flutter:
    sdk: flutter
  firebase_core: ^4.2.0
  cloud_firestore: ^6.0.3
  provider: ^6.0.0
  http: ^1.1.0
```

### Project Structure

Organize your code into a clear folder structure:

```
lib/
├── main.dart
├── models/
│   └── your_model.dart
├── services/
│   └── firestore_service.dart
├── providers/
│   └── your_provider.dart (if using Provider)
├── screens/
│   ├── list_screen.dart
│   ├── add_edit_screen.dart
│   └── detail_screen.dart
└── widgets/
    └── custom_widgets.dart (reusable components)
```

### Code Quality Standards

Your code must demonstrate:

- **Proper naming conventions:** descriptive variable and function names
- **Code comments:** explain complex logic, not obvious code
- **Error handling:** try-catch blocks for async operations
- **Input validation:** check user input before Firestore operations
- **Null safety:** properly handle nullable values
- **DRY principle:** avoid code duplication with reusable functions/widgets
- **Consistent formatting:** use `dart format` to auto-format code

### State Management Guidelines

**Use Provider for:**
- Data shared across multiple screens
- Firestore operations (fetch, add, update, delete)
- Global app state (theme, user preferences)

**Use setState for:**
- Local UI state (text field values, checkbox states)
- Widget-specific animations or transitions
- Temporary UI changes that don't affect other screens

### Required Error Handling

Implement proper error handling for:

1. **Network Errors:** Handle when device is offline
2. **Firestore Errors:** Catch and display Firestore operation failures
3. **Validation Errors:** Show user-friendly messages for invalid input
4. **Loading States:** Display loading indicators during async operations
5. **Empty States:** Show helpful messages when no data exists

Example error handling pattern:

```dart
try {
  await FirebaseFirestore.instance
      .collection('items')
      .doc(id)
      .delete();
  // Show success message
} on FirebaseException catch (e) {
  // Show error dialog with user-friendly message
  showErrorDialog(context, 'Failed to delete item: ${e.message}');
} catch (e) {
  // Handle unexpected errors
  showErrorDialog(context, 'An unexpected error occurred');
}
```

---

## External API Integration

Integrate one external public API using HTTP requests to enhance your app.

### Requirements for Bonus Points:

1. Use the `http` package to make GET requests to a public API
2. Parse JSON responses and display data in your UI
3. Handle API errors gracefully (network failures, invalid responses)
4. Document which API you used and why in your README

### Suggested APIs by Project Theme:

- **Notes App:** Use a quotes API to suggest inspirational quotes

| API                 | Endpoint                          | Example                                        |
| ------------------- | --------------------------------- | ---------------------------------------------- |
| **ZenQuotes**       | `https://zenquotes.io/api/random` | Returns 1 random quote                         |
| **Quotable**        | `https://api.quotable.io/random`  | Returns a random quote and author              |
| **Type.fit Quotes** | `https://type.fit/api/quotes`     | Returns a large list of quotes (no key needed) |

- **Task Manager:** Integrate a weather API to display weather for planning outdoor tasks

| API                                      | Endpoint                                                                                     | Notes                       |
| ---------------------------------------- | -------------------------------------------------------------------------------------------- | --------------------------- |
| **Open-Meteo (no key required)**         | `https://api.open-meteo.com/v1/forecast?latitude=52.52&longitude=13.41&current_weather=true` | Replace with actual lat/lon |
| **WeatherAPI (free tier, requires key)** | `https://api.weatherapi.com/v1/current.json?key=YOUR_KEY&q=London`                           | Free 1M calls/month         |
| **wttr.in (simple text or JSON)**        | `https://wttr.in/London?format=j1`                                                           | Very simple and public      |


- **Recipe App:** Use a nutrition or ingredients API (Spoonacular, Edamam)

| API                            | Endpoint                                                                                    | Notes                      |
| ------------------------------ | ------------------------------------------------------------------------------------------- | -------------------------- |
| **TheMealDB**                  | `https://www.themealdb.com/api/json/v1/1/search.php?s=chicken`                              | 100% free, no key required |
| **Edamam (requires free key)** | `https://api.edamam.com/api/recipes/v2?type=public&q=pasta&app_id=YOUR_ID&app_key=YOUR_KEY` | Free 10k calls/month       |
| **Spoonacular (requires key)** | `https://api.spoonacular.com/recipes/random?number=3&apiKey=YOUR_KEY`                       | Free tier available        |


- **Book App:** Use Open Library API or Google Books API to fetch book details

| API                                  | Endpoint                                                            | Example                    |
| ------------------------------------ | ------------------------------------------------------------------- | -------------------------- |
| **Open Library API**                 | `https://openlibrary.org/search.json?q=harry+potter`                | Public and free            |
| **Google Books API**                 | `https://www.googleapis.com/books/v1/volumes?q=flutter+development` | Free tier, no key required |
| **Gutendex API** (Project Gutenberg) | `https://gutendex.com/books?search=tolstoy`                         | Free and simple JSON API   |


- **Expense Tracker:** Use an exchange rate API for currency conversion

| API                                    | Endpoint                                                                | Example                          |
| -------------------------------------- | ----------------------------------------------------------------------- | -------------------------------- |
| **Frankfurter.app**                    | `https://api.frankfurter.app/latest?from=USD&to=EUR`                    | No key, supports many currencies |
| **ExchangeRate.host**                  | `https://api.exchangerate.host/latest?base=USD&symbols=EUR`             | Free and reliable                |
| **CurrencyFreaks (requires free key)** | `https://api.currencyfreaks.com/latest?apikey=YOUR_KEY&symbols=EUR,GBP` | Free tier available              |


### Example API Integration:

```dart
// Example: Fetching a random quote
Future<String> fetchQuote() async {
  final response = await http.get(
    Uri.parse('https://api.quotable.io/random')
  );
  
  if (response.statusCode == 200) {
    final data = jsonDecode(response.body);
    return data['content'];
  } else {
    throw Exception('Failed to load quote');
  }
}
```

---

### Submission Format

1. **Project Folder:** Zip your entire Flutter project
   - Name format: `MidtermProject_YourName_StudentID.zip`
   - Include all source code and README
   - Exclude build folders and generated files

2. Submit in Moodle

3. Include a small report explaining all your screens and functionalities. 

---

## Tips & Best Practices

### Development Workflow

1. **Start Small:** Get basic CRUD working before adding complex features
2. **Test Frequently:** Run your app after each feature to catch bugs early
3. **Commit Often:** Use Git to track changes (optional but highly recommended)
4. **Read Documentation:** Refer to official docs when stuck, not just Stack Overflow

### Common Pitfalls to Avoid

- **Skipping Validation:** Always validate user input before Firestore operations
- **Ignoring Edge Cases:** Test with empty lists, long strings, special characters
- **Poor Error Messages:** Show user-friendly errors, not technical stack traces
- **Hardcoded Values:** Use constants or configuration for repeated values
- **Forgetting Disposal:** Always dispose controllers, listeners, and streams
- **Copying Code Blindly:** Understand every line you write or copy

### Debugging Tips

- Use `print()` statements to track data flow
- Check Flutter DevTools for performance issues
- Review Firestore Console to verify data structure
- Test on multiple devices/emulators (different screen sizes)
- Clear app data and test from fresh install state

---

## Helpful Resources

### FlutterFire Documentation
- [FlutterFire Overview](https://firebase.flutter.dev/)
- [Cloud Firestore](https://firebase.flutter.dev/docs/firestore/overview)
- [Firestore CRUD Operations](https://firebase.flutter.dev/docs/firestore/usage)

### Flutter Official Docs
- [Provider Package](https://pub.dev/packages/provider)
- [Navigation and Routing](https://docs.flutter.dev/development/ui/navigation)
- [Material Design Components](https://docs.flutter.dev/development/ui/widgets/material)
- [Error Handling in Dart](https://dart.dev/guides/language/language-tour#exceptions)

### UI/UX Resources
- [Material Design Guidelines](https://material.io/design)
- [Flutter Widget Catalog](https://docs.flutter.dev/development/ui/widgets)
- [Flutter Layout Cheat Sheet](https://medium.com/flutter-community/flutter-layout-cheat-sheet-5363348d037e)

---

## Final Notes

This project is your opportunity to showcase everything you've learned about Flutter development. Focus on building a functional, well-designed app that you're proud to demo. Good luck, and we look forward to seeing your creative solutions!

**Remember:** A simple app that works perfectly is better than a complex app that crashes. Start with the fundamentals, get them right, then add polish.

---

**Happy Coding! 🚀**
