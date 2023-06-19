A Flutter application that consists of a stateful widget called CounterApp. 

App Includes:

•       The CounterApp should display a counter value and two buttons: "Increment" and "Decrement".

•       Both buttons should be in a Row and have different sizes (responsive).

•       Press the "Increment" button to increase the counter value by 1 and press the "Decrement" button to decrease the counter value by 1. 

•       If the counter value reaches 5, display a dialog box with the message "Counter value is 5!".

•       If the counter value reaches 10, navigate to a new screen called SecondScreen that displays the message "Congratulations! You reached 10!".


![Module 7 live test1](https://github.com/IftikharSikder/Module_7_live_test/assets/101981180/a605986f-38ae-4b4e-8679-69dabe8dda58)
![Module 7 live test2](https://github.com/IftikharSikder/Module_7_live_test/assets/101981180/fcc426bd-d794-4bf3-bb6f-4015c7d91d5a)
![Module 7 live test3](https://github.com/IftikharSikder/Module_7_live_test/assets/101981180/6cbd4539-0fc1-4aaa-874b-0801e4548b31)

Code: --------------------------

import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      debugShowCheckedModeBanner: false,
      title: 'Counter App',
      theme: ThemeData(primarySwatch: Colors.blue),
      home: CounterApp(),
    );
  }
}

class CounterApp extends StatefulWidget {
  @override
  _CounterAppState createState() => _CounterAppState();
}

class _CounterAppState extends State<CounterApp> {
  int _counter = 0;

  void _incrementCounter() {
    setState(() {
      _counter++;
      if (_counter == 5) {
        _showCounterDialog('Counter value is 5!');
      } else if (_counter == 10) {
        Navigator.push(
          context,
          MaterialPageRoute(builder: (context) => SecondScreen()),
        );
      }
    });
  }

  void _decrementCounter() {
    setState(() {
      _counter--;
    });
  }

  void _showCounterDialog(String message) {
    showDialog(
      context: context,
      builder: (BuildContext context) {
        return AlertDialog(
          title: Text('Counter'),
          content: Text(message),
          actions: [
            TextButton(
              onPressed: () {
                Navigator.of(context).pop();
              },
              child: Text('OK'),
            ),
          ],
        );
      },
    );
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('Counter App')),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: <Widget>[
            Text(
              'Counter value:',
              style: TextStyle(fontSize: 24),
            ),
            Text(
              '$_counter',
              style: TextStyle(fontSize: 48, fontWeight: FontWeight.bold),
            ),
            SizedBox(height: 20),
            Row(
              mainAxisAlignment: MainAxisAlignment.center,
              children: <Widget>[
                Expanded(
                  flex: 3, // Incremented flex value to make it 1.5 times shorter
                  child: Padding(
                    padding: EdgeInsets.symmetric(horizontal: 8.0),
                    child: FractionallySizedBox(
                      widthFactor: 0.85,
                      child: ElevatedButton(
                        onPressed: _incrementCounter,
                        style: ElevatedButton.styleFrom(primary: Colors.blue),
                        child: Text('+',style: TextStyle(fontSize: 40),),
                      ),
                    ),
                  ),
                ),
                Expanded(
                  flex: 2,
                  child: Padding(
                    padding: EdgeInsets.symmetric(horizontal: 8.0),
                    child: FractionallySizedBox(
                      widthFactor: 0.67, // Adjusted width factor to make it 1.5 times shorter
                      child: ElevatedButton(
                        onPressed: _decrementCounter,
                        style: ElevatedButton.styleFrom(primary: Colors.red),
                        child: Text('-',style: TextStyle(fontSize: 40),),
                      ),
                    ),
                  ),
                ),
              ],
            ),
          ],
        ),
      ),
    );
  }
}

class SecondScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('Second Screen')),
      body: Center(
        child: Text(
          'Congratulations! You reached 10!',
          style: TextStyle(fontSize: 24),
        ),
      ),
    );
  }
}
