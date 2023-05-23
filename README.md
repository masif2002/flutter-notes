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

## Widgets
* 'Container' is a type of widget that is commonly used for layout and styling