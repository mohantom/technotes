Flutter
=========


## Install
- Powershell > 5.0
- Git
- flutter for windows[(https://flutter.dev/docs/development/tools/sdk/releases?tab=windows)]
    `flutter doctor`
- Android studio
    add variable "ANDROID_SDK_ROOT"
    `flutter doctor --android-licenses`
- Google USB driver: for test with real device. Android Studio -> Configure -> SDK Manager
- cd to your projects folder
    - `flutter create first_app`
- Android studio
    - AVD Manager, start a device (Pixel 3a)
    - open app, and run (or `fultter run`)

- Visual Studio Code
    - plugins: Flutter, Dart, Material Icon Theme
    - Open first_app folder
    - change `_counter = _counter + 2`
    - `Ctrl + R` to force reload app

    
## Helpful Resources & Links
- Official Flutter Docs: https://flutter.io/docs/
- macOS Setup Guide: https://flutter.io/setup-macos
- Windows Setup Guide: https://flutter.io/setup-windows
- Linux Setup Guide: https://flutter.io/setup-linux
- Visual Studio Code: https://code.visualstudio.com/
- Visual Studio Code Flutter Extension: https://marketplace.visualstudio.com/items?itemName=Dart-Code.flutter
- Android Studio: https://developer.android.com/studio/


## Basics
https://dartpad.dev/
Flutter is all about Widgets

named arguments
```
void main() => runApp(MyApp());

Person({String inputName = 'Tom', @required int age}) {
    this.name = inputName;
    this.age = age;
}

// short form of constructor
Person(this.name = 'Tom', this.age)
```

### stateless widget
```
void main() {
  runApp(MyAppWithState());
}

class MyApp extends StatelessWidget {
  void answerQuestion() {
    print('Answered.');
  }

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
        home: Scaffold(
            appBar: AppBar(
              title: Text('My first app'),
            ),
            body: Column(children: [
              Text('This is the default now'),
              RaisedButton(child: Text('Answer 1'), onPressed: answerQuestion),
              RaisedButton(
                  child: Text('Answer 2'),
                  onPressed: () => print('Answer 2 chosen')),
              RaisedButton(
                  child: Text('Answer 3'),
                  onPressed: () {
                    print('Answer 3 chosen');
                  }),
            ])));
  }
}
```

### stateful widget
```
class MyAppWithState extends StatefulWidget {
  @override
  State<StatefulWidget> createState() {
    return MyAppState();
  }
}

class MyAppState extends State<MyAppWithState> {
  var questionIndex = 0;

  void answerQuestion() {
    setState(() {
      questionIndex += 1;
    });
    print('Answered 1 chosen.');
  }

  @override
  Widget build(BuildContext context) {
    var questions = [
      "What's your favorate color?",
      "What's your favorite animal",
    ];

    return MaterialApp(
        home: Scaffold(
            appBar: AppBar(
              title: Text(questions[questionIndex]),
            ),
            body: Column(children: [
              Text('This is the default now'),
              RaisedButton(child: Text('Answer 1'), onPressed: answerQuestion),
              RaisedButton(
                  child: Text('Answer 2'),
                  onPressed: () => print('Answer 2 chosen')),
              RaisedButton(
                  child: Text('Answer 3'),
                  onPressed: () {
                    print('Answer 3 chosen');
                  }),
            ])));
  }
}
```


### multiple constructor
```
Person.veryOld() {
    this.age = 60;
}
```

### getter
```
String get resultPhrase {
    if (result <= 8) {
        return 'Nice!';
    } else {
        return 'Try again!';
    }
}
```

### date format
pub.dev -> intl 0.15.8
```
Pattern                           Result
 ----------------                  -------
 new DateFormat.yMd()             -> 7/10/1996
 new DateFormat("yMd")            -> 7/10/1996
 new DateFormat.yMMMMd("en_US")   -> July 10, 1996
 new DateFormat.jm()              -> 5:08 PM
 new DateFormat.yMd().add_jm()    -> 7/10/1996 5:08 PM
 new DateFormat.Hm()              -> 17:08 // force 24 hour time
```


### SingleChildScrollingView
ListView.builder() // only load what's visible, good for memory


### Theme
```
return MaterialApp(
    title: Text('My App'),
    theme: ThemeData(
        PrimarySwatch: Colors.purple,
        accentColor: Colors.amber,
    )
)

color: Theme.of(context).primaryColor
```

### Custom fonts
/assets/fonts/...font

### ListTile