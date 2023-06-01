# Flutter 
Personalized learning notes for Flutter

## Extensions
```
Flutter | VsCode extension 
```

## Resources
* [Material Design](https://m3.material.io/)
* [Compilation in Dart](https://dart.dev/overview#:~:text=Dart's%20compiler%20technology%20lets%20you,compiler%20for%20producing%20machine%20code)
* [Flutter Widget Catalog](https://docs.flutter.dev/ui/widgets)
## Commands
```
flutter create proj_name
```
* Initialize a flutter project
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
> Hot reload in `main()` does not happen for some reason. But works with the same widget imported from another custom widget

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

### Receiving Arguments in Functions 
```dart
class Dummy extends StatelessWidget {
  const Dummy(String name, {super.key});

  ...
```
  * The constructor function defined above only receives the parameter _name_. It is not assigned to any variable inside the class, so it cannot be accessed anywhere in the widget. Hence, you need to receive arguments from a function as shown below
```dart
class Dummy extends StatelessWidget {
  const Dummy(String name, {super.key}) : myName = name;

  final String myName;

  ...
```
  * Here, we create a variable `myName` and assign the parameter `name` to `myName`. So `myName` would be accessible anywhere inside the widget
  * A shortcut for the same would be this:
  ```dart
  class Dummy extends StatelessWidget {
    const Dummy(this.myName, {super.key});

    final String myName;

    ...
  ```
### Types
* Dart is a type-safe language (like TypeScript)
* Like JS, the root type of a datatype is an 'Object'

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
var age; // not recommended
```
* Dart uses type inference, meaning that it dynamically assigns the type from the value it is assigned
* But, when a variable is declared but not initialized, the variable automatically has a type `dynamic` assigned to it. Instead, we must explicitly declare the variable with the type
    ```dart
    int age;  
    ```
* But, if you specify the type you must assign the value. Or else, we can make the value of the variable optional
    ```dart
    int age = 21;
    // OR
    int age?;
    ```
> Variables can store values of any type and not just limited to Strings and Integers
#### final & const
* You can also create constant variables using `final` and `const` keywords
```dart
final val = fetchVal();
const age = 20;
```
* The difference between both is that, `const` contains values that are constant at compile-time
* Where as, `final` can be used to store values that are constant, but fetched at run-time 

### Instance Variables
```dart
class StyledText extends StatelessWidget {
  const StyledText(this.text, {super.key});

  final String text;

  @override
  Widget build(context) {
    return Text(
      text,
      style: TextStyle(
        color: const Color.fromARGB(255, 255, 255, 255),
        fontSize: size,
      ),
    );
  }
}
```
```dart
...
        child: StyledText('Hello World'),
...
```
* Here, we accept a _text_ variable for our class as part of our constructor
* `this.text` refers to the _text_ variable declared in the class, down below
## Widgets
* 'Container' is a type of widget that is commonly used for layout and styling
* 'Icon' to use Icons
* You can wrap widgets with 'Opacity' widget to control the opacity. But has performance overhead, so not recommended

### Column
* The `Column` widget by default takes up the entire height of the screen
* Even if you wrap the `Column` widget with the `Center` widget, the behaviour remains to be the same
* You can change that by adding an extra property
```dart 
child: Center(
  child: Column(
    mainAxisSize: MainAxisSize.min,
    children: [
    
  ...
```
* Since columns are vertical, _mainAxis_ in columns is the y-axis
* By default, the value for _mainAxisSize_ is `MainAxisSize.max` 
### Buttons
* There are primarily three types of buttons available:  `ElevatedButton`, `OutlinedButton`, `TextButton`
#### Styling Buttons
```dart
 ElevatedButton(
  onPressed: () {},
  style: ElevatedButton.styleFrom(
    padding: const EdgeInsets.only(top: 50),
  ),
  child: const Text('data'),
)
```
* This adds a 50px padding on top to the button
* To add padding on all sides, `EdgeInsets.all()` can be used. Only to add padding on required sides `.only()` is used
### SizedBox
* This widget that can be used as a dummy widget to seperate two elements
```dart
...

child: Column(
  children: [
    // Image.asset( ... )

    const SizedBox(
      height: 50,
    ),
    
    // ElevatedButton( ... )
),

...
```

## Creating a custom widget
### StatelessWidget
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
* To _StatelessWidget_, we must pass a parameter called `key`. So we take in the named argument that is automatically passed by Flutter when we call our constructor of our custom widget, and pass it to our parent class, ie- _StatelessWidget_
* The code can be reduced to even simpler form
    ```dart
    const GradientContainer({super.key});
    ```

### Adding multiple constructors
```dart
class GradientContainer extends StatelessWidget {
  // Getting dynamic color values
  const GradientContainer(this.gradientColors, {super.key});

  // Using preset color values
  GradientContainer.purple({super.key})
      : gradientColors = [  
          Colors.deepPurple,
          Colors.deepPurpleAccent,
        ];

...
```
```dart
// Calling the constructor
        body: GradientContainer.purple(),
...
```

### StatefulWidget
* **_StatefulWidget_** is much like the _StatelessWidget_
* Instead of one class that contains the `build()` method in _StatelessWidget_ we have 2 classes in _StatefulWidget_
* One class that contains the `build()` method and another one that has `createState()` method that creates the state for the widget

```dart
// Actual Widget Class
class Dice extends StatefulWidget {
  // The actual widget remains const. But the constructor of _DiceState is not const (because it maintains the state which may change)
  const Dice({super.key});

  @override
  State<Dice> createState() {
    return _DiceState();
  }
}

// Class that maintains the state of the widget
class _DiceState extends State<Dice> {
  var activeDiceImage = 'assets/images/dice-1.png';

  void rollDice() {
    setState(() {
      activeDiceImage = 'assets/images/dice-5.png';
    });
  }

  @override
  Widget build(context) {
    return Column(
      children: [
        Image.asset( activeDiceImage ),
        ElevatedButton(
          onPressed: rollDice,
          child: const Text('Roll the Dice'),
        )
      ],
    );
  }
}

```
* Here, `setState()` is the method that tells flutter to re-build the widget ie- to re-run the `build()` method (to update the changes)
* Note that the _setState_ method accepts an _anonymous function_ (a function with no name) as an argument. 

### initState() in StatefulWidget
* `initState()` lets you perform some initialization tasks once the object is created
* So `initState()` runs only after the object is created and all the methods & variables in it have been declared
```dart
class _QuizState extends State<Quiz> {
  // 1. Object Created 
  Widget? activeScreen; // 2. Variable Declared

  @override
  void initState() {
    // 3. initState() is executed

    activeScreen = StartScreen(switchScreen);
    super.initState();
  }

  ...
```
## Adding Images
* It is good practice to place images under `assets/images` folder 
* To add images, you need to register them in `pubspec.yaml` first
```yaml
flutter:

  # ....

  assets:
    - assets/images/dice-1.png
    - assets/images/dice-2.png
```
* After registering the images, you can use them with the Image class
```dart
...

child: Image.asset(
      'assets/images/dice-1.png',
      width: 200,
    ),

...
```

## Questions
1. ~~Can you trigger updates to StatefulWidgets from outside the widget?~~ 