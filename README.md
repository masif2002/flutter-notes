# Flutter 
Personalized learning notes for Flutter

## Extensions
```
Flutter | A VsCode extension 
```

## Resources
* [Material Design](https://m3.material.io/)

## Commands
```
flutter create proj_name
```
* Initialise a flutter project
```
flutter run 
```
* To run the flutter project. You can also use 'Run without Debugging' option in VsCode

# Notes
## About
* Flutter is an Open Source project by Google. 
* Flutter supports Google's Material Design 
* `pubspec.yaml` file contains the list of dependencies and third party packages. It is probably similar to `package.json` file in web frameworks

## Hot Reload
* Dart uses Just-In-Time (JIT) compilation which helps us perform hot reload. 
* Hot reload works by injecting updated source code files into the running Dart Virtual Machine (VM).
> More on that, [here](https://dart.dev/overview#:~:text=Dart's%20compiler%20technology%20lets%20you,compiler%20for%20producing%20machine%20code)

## main()
* Like, C and C ++, dart calls the `main()` function by default. So, the application's workflow starts from the `main()` function
* Usually, the `runApp()` function (from Flutter) comes within the `main()` function 
* So, the entrypoint of a Flutter application is the `main()` function from `lib/main.dart`

## Widget
* Widget is the building block of Flutter. You nest widgets and have a widget tree for your app (like a DOM tree for web (: )
* `MaterialApp()` is usually your root widget. It is used as a base for bringing in _Material Design_ to your app

> List of widgets from Flutter: [Flutter Widget Catalog](https://docs.flutter.dev/ui/widgets)

## Dart Syntax
### Named Arguments
```dart
void subtract({num1, num2}) {
    num2 - num1 
}

void calculator() {
    subtract(num1: 3, num2: 10)
}
```
* Here, the named arguments are defined inside curly braces
* Positional arguments are **required** and cannot be skipped whereas named arguments are optional to be passed in to a function
* However this behavior can be changed

#### Reqiured Named argument
```dart
void subtract({num1, required num2}) {
    num2 - num1
}
```
* Adding the `required` keyword makes _num2_ a required named argument

#### Optional Positional argument
```dart
void subtract([a], b) {
    b - a
}
```
* Positional arguments in square brackets become optional 
____
* You can use both, positional and named arguments as parameters in the same function

### Types
* Dart is a type-safe language (like TypeScript)
* Like JS, the root type of a datatype is an 'Object'``

```dart
void add(int num1, int num2) {
   num1 + num2 
}
```
* Here, we've added the type for the arguments that the function must accept. Incase, any datatype other than integer is passed, then Dart will throw an error

### Variables
* You can create variables with the `var` keyword in Dart
```dart
var name = 'Mohamed Asif';
var age; // cannot do
```
* Dart uses type inference, meaning that it dynamically assigns the type from the value it is assigned
* But, when a variable is declared but not initialized, we must explicitly declare it with the type
    ```dart
    int age; // error 
    ```
    * But, if you specify the type you must assign the value. Instead, we can make the value of the variable optional
    ```dart
    int age = 21;
    // OR
    int age?;
    ```
## Widgets
* 'Container' is a type of widget that is commonly used for layout and styling

## Creating a custom widget
```dart
import 'package:flutter/material.dart';

void main() {
  runApp(
    MaterialApp(
      home: Scaffold(
        body: MyWidget(),
      ),
    ),
  );
}

class MyWidget extends StatelessWidget {
  @override
  Widget build(context) {
    return const Center(
        child: Text(
          'Hello World',
          style: TextStyle(
            fontSize: 48,
          ),
        ),
      );
  }
}
```
* We create a new widget called _MyWidget_ that extends _StatelessWidget_
* When extending _StatelessWidget_, we need to override the build method provided by _StatelessWidget_. When Flutter comes across our widget in the code while compiling the app, it builds the widget returned from the build() method
* _context_ is a parameter provided by Flutter when it creates the widget
* **Widget** is the return type of our _build_ method
* Note that when we use our widget, we have the parantheses after the name of our widget. This is because we are actually invoking the constructor of our widget (inherited constructor in this case)

### Adding custom constructor to our widget
```dart
class GradientContainer extends StatelessWidget {
  const GradientContainer({myKey}): super(key: myKey);

...
```  
* To _StatelessWidget_, we must pass a parameter called key. So we take in the named parameter that is automatically created by Flutter when we call our constructor of our custom widget, and pass it to our parent class, ie- _StatelessWidget_
* The code can be reduced to even simpler form
    ```dart
    const GradientContainer({super.key});
    ```