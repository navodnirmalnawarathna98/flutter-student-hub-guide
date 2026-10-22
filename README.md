# Flutter Student Hub --- A Practical Guide for Higher Diploma Students

A beginner-friendly, step-by-step Flutter project for learning UI
design, widget trees, layouts, navigation, user input, state management,
Provider, and the basics of Riverpod.

> **Learning approach:** Build one small application and improve it
> session by session. Understand each concept before adding the next
> feature.

## Table of Contents

-   [1. Project Overview](#1-project-overview)
-   [2. Learning Outcomes](#2-learning-outcomes)
-   [3. Application Features](#3-application-features)
-   [4. Requirements and Setup](#4-requirements-and-setup)
-   [5. Start with a Clean Flutter
    App](#5-start-with-a-clean-flutter-app)
-   [6. Understand the Widget Tree](#6-understand-the-widget-tree)
-   [7. Build the Home Dashboard](#7-build-the-home-dashboard)
-   [8. Layouts, Constraints, and Responsive
    Design](#8-layouts-constraints-and-responsive-design)
-   [9. Themes, Images, and Fonts](#9-themes-images-and-fonts)
-   [10. Organise the Project into
    Files](#10-organise-the-project-into-files)
-   [11. Navigation and Passing Data](#11-navigation-and-passing-data)
-   [12. User Input and Validation](#12-user-input-and-validation)
-   [13. StatelessWidget, StatefulWidget, and
    setState](#13-statelesswidget-statefulwidget-and-setstate)
-   [14. State Management with
    Provider](#14-state-management-with-provider)
-   [15. Introduction to Riverpod](#15-introduction-to-riverpod)
-   [16. Suggested 10-Session Teaching
    Plan](#16-suggested-10-session-teaching-plan)
-   [17. Student Practical Exercises](#17-student-practical-exercises)
-   [18. Assessment Rubric](#18-assessment-rubric)
-   [19. Common Beginner Problems](#19-common-beginner-problems)
-   [20. Official Documentation](#20-official-documentation)

------------------------------------------------------------------------

## 1. Project Overview

### Project name: Student Hub

Student Hub is a simple educational mobile application. Students can
view a dashboard, browse courses, open course details, enter profile
information, and manage a task list.

We use this one application to learn many Flutter concepts in a
connected and practical way.

### Why use one application?

-   Students learn by building a realistic application.
-   Each lesson adds a new feature to the same project.
-   Students can see how widgets, navigation, and state management work
    together.
-   The project starts small and becomes more complete over time.

## 2. Learning Outcomes

By completing this guide, students should be able to:

-   Explain Flutter widgets and Material Design basics.
-   Read and draw a simple widget tree.
-   Use `Text`, `Container`, `Row`, `Column`, `Image`, buttons, cards,
    and icons.
-   Understand layouts, constraints, and responsive design.
-   Apply themes, text styles, and custom fonts.
-   Accept and validate user input.
-   Navigate between screens and pass data.
-   Explain `StatelessWidget`, `StatefulWidget`, and `setState`.
-   Lift state to a common parent when multiple widgets need the same
    data.
-   Use Provider and `ChangeNotifier` for simple shared state.
-   Explain the basic difference between Provider and Riverpod.
-   Organise Flutter code into screens, widgets, models, and providers.

## 3. Application Features

Build these features gradually:

  -----------------------------------------------------------------------
  Screen                              Features and concepts
  ----------------------------------- -----------------------------------
  Home                                App bar, welcome message, dashboard
                                      cards, icons, theme

  Courses                             Course list, reusable cards,
                                      `ListView`, navigation

  Course Details                      Display information passed from the
                                      selected course

  Tasks                               Add, complete, and remove tasks;
                                      local and shared state

  Profile                             Text fields, keyboard actions,
                                      validation, saved display name

  Navigation                          Bottom navigation, optional drawer,
                                      routes
  -----------------------------------------------------------------------

## 4. Requirements and Setup

Install the following:

-   Flutter SDK
-   Android Studio or Visual Studio Code
-   Android emulator or a supported physical device
-   Git (optional, but recommended)

Check your Flutter installation:

``` bash
flutter doctor
```

Create the project:

``` bash
flutter create student_hub
cd student_hub
flutter run
```

Open the `student_hub` folder in your editor.

> **Tip:** Make sure the default Flutter counter app runs before you
> begin. Fix any setup issues first.

## 5. Start with a Clean Flutter App

Open `lib/main.dart`. Replace its contents with:

``` dart
import 'package:flutter/material.dart';

void main() {
  runApp(const MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Student Hub',
      debugShowCheckedModeBanner: false,
      home: const HomeScreen(),
    );
  }
}

class HomeScreen extends StatelessWidget {
  const HomeScreen({super.key});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('Student Hub'),
      ),
      body: const Center(
        child: Text('Welcome to Student Hub!'),
      ),
    );
  }
}
```

### Understand the code

  -------------------------------------------------------------------------------
  Code                                        Simple explanation
  ------------------------------------------- -----------------------------------
  `import 'package:flutter/material.dart';`   Imports Flutter Material Design
                                              widgets.

  `main()`                                    The starting point of the
                                              application.

  `runApp()`                                  Starts the Flutter app.

  `MyApp`                                     Defines the main application
                                              widget.

  `StatelessWidget`                           A widget that does not manage its
                                              own changing state.

  `build()`                                   Describes the UI that Flutter
                                              should display.

  `MaterialApp`                               Provides app-level configuration,
                                              theme, and navigation support.

  `Scaffold`                                  Provides a standard page structure.

  `AppBar`                                    Displays the top app bar.

  `Center`                                    Centres its child within the
                                              available space.

  `Text`                                      Displays text.
  -------------------------------------------------------------------------------

### Beginner activity

1.  Change the app title.
2.  Change the AppBar title.
3.  Change the welcome message.
4.  Run the app and observe the result.

## 6. Understand the Widget Tree

Flutter UIs are built by placing widgets inside other widgets. This
structure is called a **widget tree**.

The starter app has a simplified structure like this:

``` text
MyApp
└── MaterialApp
    └── HomeScreen
        └── Scaffold
            ├── AppBar
            │   └── Text
            └── Body
                └── Center
                    └── Text
```

Remember:

1.  A widget can contain another widget.
2.  Some widgets accept one `child`.
3.  Other widgets accept multiple `children`.
4.  Layout widgets control the position and size of their children.
5.  The widget tree should be organised so that the UI is easy to
    understand and maintain.

**Try it:** Draw the widget tree for the dashboard you build in the next
section.

## 7. Build the Home Dashboard

Replace the `body` in `HomeScreen` with the following:

``` dart
body: Padding(
  padding: const EdgeInsets.all(16),
  child: Column(
    crossAxisAlignment: CrossAxisAlignment.start,
    children: [
      const Text(
        'Hello, Student!',
        style: TextStyle(
          fontSize: 24,
          fontWeight: FontWeight.bold,
        ),
      ),
      const SizedBox(height: 16),
      const Card(
        child: ListTile(
          leading: Icon(Icons.book),
          title: Text('My Courses'),
          subtitle: Text('View your courses'),
          trailing: Icon(Icons.arrow_forward_ios),
        ),
      ),
      const SizedBox(height: 8),
      const Card(
        child: ListTile(
          leading: Icon(Icons.task_alt),
          title: Text('My Tasks'),
          subtitle: Text('Manage your tasks'),
          trailing: Icon(Icons.arrow_forward_ios),
        ),
      ),
    ],
  ),
),
```

### What have we learned?

-   `Padding` adds space around its child.
-   `Column` arranges children vertically.
-   `crossAxisAlignment` controls horizontal alignment inside a
    `Column`.
-   `SizedBox` creates space between widgets.
-   `Card` presents content in a card-style surface.
-   `ListTile` provides a standard row with leading, title, subtitle,
    and trailing areas.
-   `Icon` displays an icon.
-   `TextStyle` controls text appearance.

### Practice

-   Add a third card for Profile.
-   Change the icons and descriptions.
-   Change the font size of the welcome message.
-   Add a greeting using your own name as sample text.

## 8. Layouts, Constraints, and Responsive Design

### Important layout widgets

  -----------------------------------------------------------------------
  Widget                              Purpose
  ----------------------------------- -----------------------------------
  `Row`                               Places children horizontally.

  `Column`                            Places children vertically.

  `Expanded`                          Makes a child fill available space
                                      along a `Row` or `Column` main
                                      axis.

  `Flexible`                          Lets a child fit within available
                                      space without always forcing it to
                                      fill all of it.

  `Padding`                           Adds space around a child.

  `Container`                         Can provide decoration, padding,
                                      margin, and sizing.

  `Wrap`                              Moves children onto another line
                                      when necessary.

  `ListView`                          Displays a scrollable list.

  `SizedBox`                          Adds fixed space or provides a
                                      fixed size.
  -----------------------------------------------------------------------

### Example: Two dashboard cards in a row

``` dart
Row(
  children: [
    Expanded(
      child: Card(
        child: Padding(
          padding: const EdgeInsets.all(16),
          child: Column(
            children: const [
              Icon(Icons.book, size: 32),
              Text('Courses'),
              Text('4 available'),
            ],
          ),
        ),
      ),
    ),
    const SizedBox(width: 12),
    Expanded(
      child: Card(
        child: Padding(
          padding: const EdgeInsets.all(16),
          child: Column(
            children: const [
              Icon(Icons.task, size: 32),
              Text('Tasks'),
              Text('3 pending'),
            ],
          ),
        ),
      ),
    ),
  ],
)
```

### What are constraints?

In simple English, Flutter passes size limits from parent widgets to
child widgets. Each child must lay itself out within those limits.

Layout errors can happen when a `Row`, `Column`, or another widget does
not have enough space for its content.

### Responsive layout example

Use `LayoutBuilder` when the layout should change according to the space
available:

``` dart
LayoutBuilder(
  builder: (context, constraints) {
    final isWide = constraints.maxWidth >= 600;

    if (isWide) {
      return Row(
        children: [
          Expanded(child: courseCard()),
          Expanded(child: taskCard()),
        ],
      );
    }

    return Column(
      children: [
        courseCard(),
        taskCard(),
      ],
    );
  },
)
```

In this example, `courseCard()` and `taskCard()` represent methods or
widgets that return the relevant cards. Define them before using this
example.

Use `MediaQuery.sizeOf(context)` when you need the screen size. Prefer
flexible layouts instead of giving every widget a fixed width.

### Practice

1.  Show the cards side by side on a wide screen.
2.  Show them vertically on a narrow screen.
3.  Add long text and observe how it wraps.
4.  Test the app on an emulator with different screen sizes.

## 9. Themes, Images, and Fonts

### Set up a consistent theme

A theme helps your screens share the same visual style.

``` dart
MaterialApp(
  title: 'Student Hub',
  debugShowCheckedModeBanner: false,
  theme: ThemeData(
    useMaterial3: true,
    colorScheme: ColorScheme.fromSeed(
      seedColor: Colors.indigo,
    ),
    appBarTheme: const AppBarTheme(
      centerTitle: true,
    ),
  ),
  home: const HomeScreen(),
)
```

### Add an image

1.  Create the folder `assets/images/`.
2.  Add an image, for example `student.jpg`.
3.  Register the folder in `pubspec.yaml`:

``` yaml
flutter:
  uses-material-design: true
  assets:
    - assets/images/
```

4.  Use the image in your widget:

``` dart
Image.asset(
  'assets/images/student.jpg',
  width: 100,
  height: 100,
  fit: BoxFit.cover,
)
```

### Add a custom font

1.  Create `assets/fonts/`.
2.  Place your font files in that folder.
3.  Declare the font family and file paths in `pubspec.yaml`.
4.  Set `fontFamily` in `ThemeData` or a `TextStyle`.

Make sure the font family name matches the name declared in
`pubspec.yaml`.

## 10. Organise the Project into Files

Start with `main.dart` while the application is small. As it grows,
separate screens, widgets, models, and state management code into their
own files.

Recommended structure:

``` text
student_hub/
├── lib/
│   ├── main.dart
│   ├── app.dart
│   ├── models/
│   │   ├── course.dart
│   │   └── task.dart
│   ├── screens/
│   │   ├── home_screen.dart
│   │   ├── courses_screen.dart
│   │   ├── course_details_screen.dart
│   │   ├── tasks_screen.dart
│   │   └── profile_screen.dart
│   ├── widgets/
│   │   ├── course_card.dart
│   │   └── dashboard_card.dart
│   └── providers/
│       └── task_provider.dart
├── assets/
│   ├── images/
│   └── fonts/
└── pubspec.yaml
```

  File or folder   Purpose
  ---------------- ------------------------------------------------------
  `main.dart`      Starts the application.
  `app.dart`       Defines app configuration and theme.
  `models/`        Contains data classes.
  `screens/`       Contains complete pages.
  `widgets/`       Contains reusable UI components.
  `providers/`     Contains shared state management code.
  `assets/`        Contains images, fonts, and other bundled resources.

### Example: Move HomeScreen into its own file

Create `lib/screens/home_screen.dart`:

``` dart
import 'package:flutter/material.dart';

class HomeScreen extends StatelessWidget {
  const HomeScreen({super.key});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('Student Hub'),
      ),
      body: const Center(
        child: Text('Welcome to Student Hub!'),
      ),
    );
  }
}
```

Then update `lib/main.dart`:

``` dart
import 'package:flutter/material.dart';
import 'screens/home_screen.dart';

void main() {
  runApp(const MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      debugShowCheckedModeBanner: false,
      home: const HomeScreen(),
    );
  }
}
```

**Teaching point:** `main.dart` starts the application.
`home_screen.dart` describes the Home screen. This separation makes the
project easier to maintain.

## 11. Navigation and Passing Data

### Navigate to another screen

Import the destination screen, then use `Navigator.push`:

``` dart
ElevatedButton(
  onPressed: () {
    Navigator.push(
      context,
      MaterialPageRoute(
        builder: (context) => const CoursesScreen(),
      ),
    );
  },
  child: const Text('View Courses'),
)
```

Return to the previous screen:

``` dart
Navigator.pop(context);
```

### Create a course model

Create `lib/models/course.dart`:

``` dart
class Course {
  final String title;
  final String description;

  const Course({
    required this.title,
    required this.description,
  });
}
```

### Create the Course Details screen

Create `lib/screens/course_details_screen.dart`:

``` dart
import 'package:flutter/material.dart';
import '../models/course.dart';

class CourseDetailsScreen extends StatelessWidget {
  final Course course;

  const CourseDetailsScreen({
    super.key,
    required this.course,
  });

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: const Text('Course Details')),
      body: Padding(
        padding: const EdgeInsets.all(16),
        child: Column(
          crossAxisAlignment: CrossAxisAlignment.start,
          children: [
            Text(
              course.title,
              style: Theme.of(context).textTheme.headlineSmall,
            ),
            const SizedBox(height: 12),
            Text(course.description),
            ElevatedButton(
              onPressed: () => Navigator.pop(context),
              child: const Text('Back'),
            ),
          ],
        ),
      ),
    );
  }
}
```

### Pass a selected course

``` dart
final course = Course(
  title: 'Mobile App Development',
  description: 'Learn to create mobile applications using Flutter.',
);

Navigator.push(
  context,
  MaterialPageRoute(
    builder: (context) => CourseDetailsScreen(course: course),
  ),
);
```

The `Course` object is passed through the screen constructor.

### Named routes

Named routes are another way to navigate:

``` dart
MaterialApp(
  initialRoute: '/',
  routes: {
    '/': (context) => const HomeScreen(),
    '/courses': (context) => const CoursesScreen(),
    '/profile': (context) => const ProfileScreen(),
  },
)
```

Open a route:

``` dart
Navigator.pushNamed(context, '/courses');
```

### Bottom navigation and drawers

-   Use a `NavigationBar` for primary destinations such as Home,
    Courses, Tasks, and Profile.
-   Store the selected destination index in a `StatefulWidget`.
-   Use `setState` when the selected index changes.
-   Use a `Drawer` for additional destinations such as Settings and
    About.
-   Explain that navigation widgets display destinations, while
    `Navigator` manages the route stack.

For a larger production app with deep links and more complex routing,
introduce a routing package such as `go_router` later.

## 12. User Input and Validation

A profile form can contain a student name, email address, course
selection, and Save button.

### Basic profile screen example

Create `lib/screens/profile_screen.dart`:

``` dart
import 'package:flutter/material.dart';

class ProfileScreen extends StatefulWidget {
  const ProfileScreen({super.key});

  @override
  State<ProfileScreen> createState() => _ProfileScreenState();
}

class _ProfileScreenState extends State<ProfileScreen> {
  final nameController = TextEditingController();
  String savedName = '';

  @override
  void dispose() {
    nameController.dispose();
    super.dispose();
  }

  void saveProfile() {
    final name = nameController.text.trim();

    if (name.isEmpty) {
      ScaffoldMessenger.of(context).showSnackBar(
        const SnackBar(
          content: Text('Please enter your name'),
        ),
      );
      return;
    }

    setState(() {
      savedName = name;
    });

    ScaffoldMessenger.of(context).showSnackBar(
      const SnackBar(content: Text('Profile saved')),
    );
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: const Text('My Profile')),
      body: Padding(
        padding: const EdgeInsets.all(16),
        child: Column(
          children: [
            TextField(
              controller: nameController,
              textInputAction: TextInputAction.done,
              decoration: const InputDecoration(
                labelText: 'Student Name',
                border: OutlineInputBorder(),
              ),
              onSubmitted: (_) => saveProfile(),
            ),
            const SizedBox(height: 16),
            ElevatedButton(
              onPressed: saveProfile,
              child: const Text('Save Profile'),
            ),
            const SizedBox(height: 16),
            Text('Saved Name: $savedName'),
          ],
        ),
      ),
    );
  }
}
```

### Important concepts

-   `TextEditingController` lets you read the text entered by the user.
-   `textInputAction` changes the keyboard action.
-   `onSubmitted` handles keyboard submission.
-   `onPressed` handles a button press.
-   `setState` refreshes the UI when the saved name changes.
-   `dispose()` releases the controller when the screen is removed.

**Note:** This example stores the name only in memory. It does not save
data permanently to a database.

### Further practice

-   Add an email field.
-   Add email validation.
-   Use a `Form` and `TextFormField`.
-   Add a course dropdown.
-   Show an error when required fields are empty.

## 13. StatelessWidget, StatefulWidget, and setState

### StatelessWidget

Use it for a widget that does not manage changing state of its own.

Examples:

-   A course card that displays a title.
-   A logo.
-   A fixed heading.

### StatefulWidget

Use it when a widget needs to manage changing state.

Examples:

-   A task list.
-   A form.
-   A counter.
-   A selected navigation destination.

### What does setState do?

Call `setState` after changing local state so Flutter can rebuild the
relevant widget.

### Example: Task counter

``` dart
class TaskCounter extends StatefulWidget {
  const TaskCounter({super.key});

  @override
  State<TaskCounter> createState() => _TaskCounterState();
}

class _TaskCounterState extends State<TaskCounter> {
  int taskCount = 0;

  @override
  Widget build(BuildContext context) {
    return Column(
      mainAxisSize: MainAxisSize.min,
      children: [
        Text('Total Tasks: $taskCount'),
        ElevatedButton(
          onPressed: () {
            setState(() {
              taskCount++;
            });
          },
          child: const Text('Add Task'),
        ),
      ],
    );
  }
}
```

### Understand the process

1.  `taskCount` starts at `0`.
2.  The user presses Add Task.
3.  The value increases inside `setState`.
4.  Flutter rebuilds the widget.
5.  The new count appears on the screen.

### Lift state between widgets

If Home displays a task count and Tasks displays the list, both screens
need the same data.

**Lifting state up** means moving shared state into a common parent and
passing data and callbacks to child widgets.

Teach this approach first with a small example. When state must be
shared across several screens, introduce Provider.

## 14. State Management with Provider

Provider is a useful next step after `setState`. It helps separate
application data from UI code and share state between widgets.

In Student Hub:

-   Home displays the pending task count.
-   Tasks displays the task list.
-   Students can add, complete, and remove tasks.
-   Both screens update when the shared task data changes.

### Step 1: Install Provider

Run:

``` bash
flutter pub add provider
```

### Step 2: Create the task model

Create `lib/models/task.dart`:

``` dart
class Task {
  final String title;
  bool isCompleted;

  Task({
    required this.title,
    this.isCompleted = false,
  });
}
```

### Step 3: Create TaskProvider

Create `lib/providers/task_provider.dart`:

``` dart
import 'package:flutter/foundation.dart';
import '../models/task.dart';

class TaskProvider extends ChangeNotifier {
  final List<Task> _tasks = [];

  List<Task> get tasks => List.unmodifiable(_tasks);

  int get pendingCount =>
      _tasks.where((task) => !task.isCompleted).length;

  void addTask(String title) {
    if (title.trim().isEmpty) return;

    _tasks.add(Task(title: title.trim()));
    notifyListeners();
  }

  void toggleTask(int index) {
    _tasks[index].isCompleted = !_tasks[index].isCompleted;
    notifyListeners();
  }

  void removeTask(int index) {
    _tasks.removeAt(index);
    notifyListeners();
  }
}
```

### Understand TaskProvider

  -----------------------------------------------------------------------
  Code                                Explanation
  ----------------------------------- -----------------------------------
  `ChangeNotifier`                    Allows the class to notify
                                      listeners when data changes.

  `_tasks`                            Holds the task list privately.

  `tasks`                             Exposes a read-only list view.

  `pendingCount`                      Calculates how many tasks are
                                      incomplete.

  `addTask()`                         Adds a task.

  `toggleTask()`                      Changes a task's completion status.

  `removeTask()`                      Removes a task.

  `notifyListeners()`                 Notifies listening widgets that the
                                      data has changed.
  -----------------------------------------------------------------------

### Step 4: Register Provider

Update `lib/main.dart`:

``` dart
import 'package:flutter/material.dart';
import 'package:provider/provider.dart';

import 'app.dart';
import 'providers/task_provider.dart';

void main() {
  runApp(
    ChangeNotifierProvider(
      create: (_) => TaskProvider(),
      child: const StudentHubApp(),
    ),
  );
}
```

Create `lib/app.dart`:

``` dart
import 'package:flutter/material.dart';
import 'screens/home_screen.dart';

class StudentHubApp extends StatelessWidget {
  const StudentHubApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Student Hub',
      debugShowCheckedModeBanner: false,
      theme: ThemeData(
        useMaterial3: true,
        colorScheme: ColorScheme.fromSeed(
          seedColor: Colors.indigo,
        ),
      ),
      home: const HomeScreen(),
    );
  }
}
```

Now `TaskProvider` is available to descendant widgets.

### Step 5: Display the pending task count

In `home_screen.dart`, add these imports:

``` dart
import 'package:provider/provider.dart';
import '../providers/task_provider.dart';
```

Use a `Consumer` where you want the count to appear:

``` dart
Consumer<TaskProvider>(
  builder: (context, taskProvider, child) {
    return Card(
      child: ListTile(
        leading: const Icon(Icons.task_alt),
        title: const Text('Pending Tasks'),
        trailing: Text(
          '${taskProvider.pendingCount}',
          style: const TextStyle(
            fontSize: 22,
            fontWeight: FontWeight.bold,
          ),
        ),
      ),
    );
  },
)
```

When task data changes and listeners are notified, the count updates
automatically.

### Step 6: Add and display tasks

Inside the `State` class for `TasksScreen`, create a controller:

``` dart
final taskController = TextEditingController();

@override
void dispose() {
  taskController.dispose();
  super.dispose();
}
```

Use this UI pattern inside the screen's `build()` method:

``` dart
Column(
  children: [
    TextField(
      controller: taskController,
      decoration: const InputDecoration(
        labelText: 'Enter a task',
        border: OutlineInputBorder(),
      ),
    ),
    ElevatedButton(
      onPressed: () {
        context.read<TaskProvider>().addTask(
          taskController.text,
        );
        taskController.clear();
      },
      child: const Text('Add Task'),
    ),
    Expanded(
      child: Consumer<TaskProvider>(
        builder: (context, provider, child) {
          return ListView.builder(
            itemCount: provider.tasks.length,
            itemBuilder: (context, index) {
              final task = provider.tasks[index];

              return ListTile(
                title: Text(
                  task.title,
                  style: TextStyle(
                    decoration: task.isCompleted
                        ? TextDecoration.lineThrough
                        : TextDecoration.none,
                  ),
                ),
                leading: Checkbox(
                  value: task.isCompleted,
                  onChanged: (_) {
                    context.read<TaskProvider>().toggleTask(index);
                  },
                ),
                trailing: IconButton(
                  icon: const Icon(Icons.delete),
                  onPressed: () {
                    context.read<TaskProvider>().removeTask(index);
                  },
                ),
              );
            },
          );
        },
      ),
    ),
  ],
)
```

This is the main UI pattern, not a complete screen class. Put the
`Column` inside a `Scaffold` body, and initialise and dispose of the
controller in the screen's `State` class.

### Understand read and Consumer

-   `context.read<TaskProvider>()` accesses the provider without
    subscribing the current widget to updates.
-   `Consumer<TaskProvider>` listens for changes and rebuilds the
    relevant UI.
-   `notifyListeners()` tells listeners that shared state has changed.

> **Important:** Provider manages state; it does not automatically save
> tasks permanently. This example stores tasks in memory. Add local
> storage or a database if tasks must remain after restarting the app.

## 15. Introduction to Riverpod

Teach Riverpod after students understand `setState` and Provider.

  ------------------------------------------------------------------------
  Feature           `setState`        Provider           Riverpod
  ----------------- ----------------- ------------------ -----------------
  Main use          Local widget      Shared application Reactive state
                    state             state              management

  Core idea         Rebuild after     `ChangeNotifier`   Providers and
                    local state       and provider       reactive state
                    changes           access             

  Installation      Included with     External package   External package
                    Flutter                              

  Learning level    Beginner          Beginner to        Intermediate
                                      intermediate       

  Student Hub       Selected tab      Shared task list   Alternative task
  example                                                list
                                                         implementation
  ------------------------------------------------------------------------

Students should first complete the task list with Provider. Then, as an
extension, ask them to implement the same behaviour using Riverpod.

Official guide: <https://riverpod.dev/>

## 16. Suggested 10-Session Teaching Plan

  -----------------------------------------------------------------------
  Session                 Topic                   Expected outcome
  ----------------------- ----------------------- -----------------------
  1                       Flutter setup,          Basic Student Hub
                          `main.dart`,            screen
                          MaterialApp, Scaffold   

  2                       Widgets, widget tree,   Home dashboard
                          Row, Column, cards,     
                          icons                   

  3                       Constraints, responsive Responsive dashboard
                          layouts, themes, fonts, 
                          assets                  

  4                       File organisation and   Multiple screens
                          navigation              

  5                       Passing data, bottom    Navigation and profile
                          navigation, drawers,    form
                          forms                   

  6                       StatelessWidget,        Interactive task list
                          StatefulWidget,         
                          `setState`              

  7                       Lifting state and       Shared local state
                          widget communication    

  8                       Provider and            Shared task list
                          ChangeNotifier          

  9                       Consumer, read,         Improved state
                          Riverpod overview       management

  10                      Integration and         Completed Student Hub
                          practical assessment    demonstration
  -----------------------------------------------------------------------

Adjust the schedule according to your lesson duration and student
progress.

## 17. Student Practical Exercises

Complete these tasks in order:

### Exercise 1 --- Basic UI

Create a Home screen with an AppBar, welcome message, two dashboard
cards, and icons.

### Exercise 2 --- Layouts

Arrange two cards using `Row` and `Expanded`. Test the layout on a
narrow screen.

### Exercise 3 --- Reusable widgets

Create a reusable `DashboardCard` widget that accepts a title, icon, and
description.

### Exercise 4 --- Navigation

Open the Courses screen from Home. Then open Course Details and pass the
selected course object.

### Exercise 5 --- User input

Create a profile form with name and email fields. Validate the name
before displaying the saved details.

### Exercise 6 --- Local state

Create a task list that supports adding, completing, and removing tasks.

### Exercise 7 --- Provider

Move the task list into `TaskProvider`. Display the pending task count
on the Home screen.

### Exercise 8 --- Extension

Add an empty state, task completion indicators, and a consistent theme
across all screens.

## 18. Assessment Rubric

  Assessment area                              Marks
  ---------------------------------------- ---------
  UI design and Material widgets                  20
  Layouts and responsive design                   15
  File organisation and reusable widgets          10
  Navigation and passing data                     15
  User input and validation                       10
  Local state management                          10
  Provider implementation                         15
  Code quality and demonstration                   5
  **Total**                                  **100**

### Suggested submission requirements

Students should submit:

1.  Flutter source code.
2.  A README describing the application and how to run it.
3.  Screenshots of the main screens.
4.  A short explanation of the widget tree.
5.  A demonstration of navigation and state changes.
6.  Answers to questions about Provider and `setState`.

## 19. Common Beginner Problems

  -----------------------------------------------------------------------
  Problem                             What to check
  ----------------------------------- -----------------------------------
  Red error under a widget            Check spelling, brackets, commas,
                                      and imports.

  Screen does not fit                 Check constraints, `Expanded`,
                                      `Flexible`, and scrollable widgets.

  Button does nothing                 Check its callback, such as
                                      `onPressed`.

  UI does not update                  Check whether state changes require
                                      `setState` or provider
                                      notifications.

  Controller warning or leak          Dispose of `TextEditingController`
                                      in the `State` object's `dispose()`
                                      method.

  Provider not found                  Ensure the widget is below the
                                      correct provider in the widget
                                      tree.

  Asset not displayed                 Check the path and `pubspec.yaml`
                                      indentation.

  Import cannot be resolved           Check the file name and relative
                                      import path.

  Task list disappears after restart  The current example uses in-memory
                                      state; add persistence if required.
  -----------------------------------------------------------------------

## 20. Official Documentation

Use these official resources alongside the practical lessons:

-   [Flutter UI documentation](https://docs.flutter.dev/ui)
-   [Flutter layout documentation](https://docs.flutter.dev/ui/layout)
-   [Flutter navigation
    cookbook](https://docs.flutter.dev/cookbook/navigation)
-   [Flutter state
    management](https://docs.flutter.dev/data-and-backend/state-mgmt)
-   [Provider package](https://pub.dev/packages/provider)
-   [Riverpod documentation](https://riverpod.dev/)

------------------------------------------------------------------------

## Final Advice for Students

Do not copy the entire application without understanding it.

For each lesson:

1.  Read the explanation.
2.  Type the code yourself.
3.  Run the app.
4.  Observe the result.
5.  Change one thing and test again.
6.  Complete the practical exercise.
7.  Explain what you learned in your own words.

The goal is not only to make an app that runs. The goal is to understand
how Flutter widgets, layouts, navigation, and state management work
together.
