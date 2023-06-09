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
* [Google Fonts](https://pub.dev/packages/google_fonts/install)
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
const age = 20;
final val = getMyAge();
```
* The difference between both is that, `const` contains values that are constant at compile-time
* Where as, `final` can be used to store values that are constant, but picked up at run-time 
* Variables that are declared with `final` and `const` can't be re-assigned values obviously
  ```dart
  const String name = 'Asif';
  name = 'YourName' // error
  ```
  * Even though these variables can't be reassigned, they can be mutated in memory (with the help of methods provided by Dart)
    ```dart
    const List<String> names = []
    names.add('Asif') // Works

    names = ['Asif'] // Error
    ```

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
### List
```dart
final List<String> anyList = [];
```
* You need to specify the type of elements that is going to be stored in the list inside angle brackets
* NEVER MAKE A COPY OF LIST LIKE THIS
  ```dart
  newList = oldList
  ```
  * The above code actually creates a pointer to the old list. So both the variables point to the old list.
### map()
```dart
anyList.map((item) => Text(item));
```
* You can use `map()` just like in JS. It returns a new list of all the elements
* You can use the spread operator incase you need to have it as seprate elements instead of a new list
  ```dart
  ...anyList.map((item) => Text(item))
  ```
* The `map()` function returns an `Iterable` which you also can convert it to a list with `.toList()` function


### Map data-type in Dart
* Map is like a Dictionary in python with key value pairs
```dart
var myself = {
  'name': 'Asif',
  'age': 21,
};
``` 
* Here, the data type of the variable is `Map<String, Object>`
* The value of an item in a dictionary can be accessed as follows
  ```dart
  print(myself['name']) // 'Asif'
  ```
### Type Casting
* You can type cast in Dart from one data type to another like this using the `as` keyword
```dart
String as int
```
### Getter Function
* A getter function is a regular function that returns a value. This function is treated like it's a variable
* In Dart, you can create a getter function with the `get` keyword
```dart
// Regular Function
List<String> shuffledAnswers() {
  var ans = List.of(answers);
  ans.shuffle();
  return ans;
}
```
```dart
// Getter Function
List<String> get shuffledAnswers {
  var ans = List.of(answers);
  ans.shuffle();
  return ans;
}
```
* Notice that the parantheses have disappeared
* This function is now treated as a variable (but still as a function internally)
  ```dart
  // Regular function
  print(shuffledAnswers())

  // getter function
  print(shuffledAnswers)
  ```
## Widgets
* 'Icon' to use Icons
* You can wrap widgets with 'Opacity' widget to control the opacity. But has performance overhead, so not recommended
### Container
* _Container_ is a type of widget that is commonly used for layout and styling
* Containers with no children try to be as big as possible unless the incoming constraints are unbounded, in which case they try to be as small as possible.
### Column
* The `Column` widget by default takes up the entire height of the screen
* The width of the Column is the maximum width of the children 
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
### Expanded
* By default, the main (vertical) axis of the column takes up the entire space of the screen and the size of the cross (horizontal) axis is infinity. The size of the cross axis is not size of the screen, but of infinite width
* Similarly, it is the same case with the Row widget
* When you combine Row widget and Column widget, you get this problem of pixels breaking out of the screen
* Using `Expanded` widget solves the problem in this case
```dart
Row(
  children: [
    Expanded(
      Column(
        ....
      )
    )
  ] 
)
```
* Here, the `Column` widget takes up infinite space on the X axis (cross axis) by default. So, the `Expanded` widget tells that, it needs to expand only to the width of the parent widget which is the `Row` widget. As you know the X axis of the row widget takes up only the space available within the screen
* This solves the problem of pixels breaking out of the screen
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
### SingleChildScrollView
```dart
 SizedBox(
  height: 300,
  child: SingleChildScrollView(
    child: Column(
      children: [
        ...
```
* The `SingleChildScrollView` must be wrapped by a widget like `SizedBox`. When content breaks out of the _SizedBox_, it becomes scrollable
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

### Accessing constructor arguments in build() method in StatefulWidgets
* The methods and objects received in the constructor of a Stateful Widget can be accessed via the `widget` object 
* `widget.<obj_name>` gives access to the object
```dart
class QuestionScreen extends StatefulWidget {
  const QuestionScreen({super.key, required this.selectAnswer});

  final void Function(String answer) selectAnswer;

  @override
  State<QuestionScreen> createState() {
    return _QuestionScreenState();
  }
}

class _QuestionScreenState extends State<QuestionScreen> {

  void nextQuestion(String answer) {
    widget.selectAnswer(answer);
  }

  @override
  Widget build(BuildContext context) {
    ...
```
* Here, a function named `selectAnswer()` is received from the constructor
* That function is accessed as `widget.selectAnswer()` in the state class below
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

## Custom Font
* You can add custom font either by downloading a custom font file (.ttf) or using the **google_fonts** package
```dart
// Before
Text(
  'My Text',
  style: TextStyle(
    fontSize: 24,
    fontWeight: FontWeight.bold,
  ),
```
```dart
// After
import 'package:google_fonts/google_fonts.dart';

...

Text(
  'My Text',
  style: GoogleFonts.poppins(
    fontSize: 24,
    fontWeight: FontWeight.bold,
  ),
```
## Icons
* You can use icons with the standalone `Icon` class or use the `.icon()` constructor if you are using it with a button
```dart
// Reset Button
TextButton.icon(
  style: TextButton.styleFrom(
    foregroundColor: Colors.white,
  ),
  icon: const Icon(
    Icons.replay,
  ),
  onPressed: restartQuiz,
  label: const Text('Reset Quiz'),
)
``` 
## Other Notes
* Using `double.infinity` gives you an infinite value that you can use for dimension of an element to take up the maximum size 

## Questions
1. ~~Can you trigger updates to StatefulWidgets from outside the widget?~~ 
1. How do you access arguments received from the constructor in build method for Stateful Widgets  