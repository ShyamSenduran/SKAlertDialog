# SKAlertDialog Example
```dart
import 'package:flutter/material.dart';
import 'package:sk_alert_dialog/sk_alert_dialog.dart';

void main() => runApp(AlertView());

class AlertView extends StatefulWidget {
  @override
  State<StatefulWidget> createState() {
    // TODO: implement createState
    return AlertViewState();
  }
}

class AlertViewState extends State<AlertView> {
  bool isDarkThemeMode = false;
  final emailController = TextEditingController();
  final FocusNode _emailAddressFocus = FocusNode();

  Map<String, bool> checkBoxAry = {
    'Choice One': true,
    'Choice Two': false,
    'Choice Three': true,
    'Choice Four': false,
    'Choice Five': false,
    'Choice Six': false,
    'Choice Seven': false,
    'Choice Eight': false,
  };

  Map<String, int> radioButtonAry = {
    'Choice One': 1,
    'Choice Two': 2,
    'Choice Three': 3,
    'Choice Four': 4,
    'Choice Five': 5,
  };

  var alertTypesAry = [
    {"title": "Simple Alert", "description": "Alert type - info"},
    {"title": "Alert with buttons", "description": "Alert type - buttons"},
    {"title": "Alert with custom buttons", "description": "Alert type - buttons"},
    {"title": "Login Form", "description": "Alert type - loginform"},
    {"title": "Checkbox", "description": "Alert type - checkbox"},
    {"title": "Radiobutton", "description": "Alert type - radiobutton"},
    {"title": "Custom Widget", "description": "Alert type - custom"},
  ];

  @override
  void initState() {
    // TODO: implement initState
    super.initState();
  }

  @override
  Widget build(BuildContext context) {
    // TODO: implement build
    return Scaffold(
      backgroundColor: Theme.of(context).primaryColorLight,
      body: Padding(
        padding: EdgeInsets.only(left: 20, top: 70, right: 20, bottom: 10),
        child: Column(
          crossAxisAlignment: CrossAxisAlignment.start,
          children: <Widget>[
            Row(
              mainAxisAlignment: MainAxisAlignment.spaceBetween,
              children: <Widget>[
                Text('SKAlertDialog',
                    style: GoogleFonts.nunitoSans(
                        fontSize: 35,
                        letterSpacing: .9,
                        fontWeight: FontWeight.bold)),
              ],
            ),
            SizedBox(height: 10),
            Text(
              'Easy to display the alert dialog',
              style: GoogleFonts.nunito(
                  color: const Color(0xFF929794),
                  fontSize: 17,
                  letterSpacing: .5,
                  fontWeight: FontWeight.w500),
            ),
            Expanded(
              child: ListView.builder(
                primary: false,
                scrollDirection: Axis.vertical,
                shrinkWrap: true,
                itemCount: alertTypesAry == null ? 0 : alertTypesAry.length,
                itemBuilder: (BuildContext context, int index) {
                  IconData icon;

                  if (index == 0) {
                    icon = Icons.check_box_outline_blank;
                  } else if (index == 1) {
                    icon = Icons.content_copy;
                  } else if (index == 2) {
                    icon = Icons.people;
                  } else if (index == 3) {
                    icon = Icons.check_box;
                  } else if (index == 4) {
                    icon = Icons.radio_button_checked;
                  } else {
                    icon = Icons.photo_library;
                  }

                  return new GestureDetector(
                    behavior: HitTestBehavior.translucent,
                    onTap: () => _onTileClicked(index),
                    child: AlertCard(
                      title: alertTypesAry[index]['title'],
                      description: alertTypesAry[index]['description'],
                      index: index,
                      iconData: icon,
                    ),
                  );
                },
              ),
            ),
          ],
        ),
      ),
    );
  }

  // Function to be called on click
  void _onTileClicked(int index) {
    if (index == 0) {
      SKAlertDialog.show(
        context: context,
        type: SKAlertType.info,
        title: 'Simple Alert',
        message: 'Hi! Welcome to SKALertDialog',
        onOkBtnTap: (value) {
          print('Okay Button Tapped');
        },
      );
    } else if (index == 1) {
      SKAlertDialog.show(
        context: context,
        type: SKAlertType.buttons,
        title: 'Alert with buttons',
        message: 'Shall we move to next alert?',
        onOkBtnTap: (value) {
          print('Okay Button Tapped');
        },
        onCancelBtnTap: (value) {
          print('Cancel Button Tapped');
        },
      );
    } else if (index == 2) {
      SKAlertDialog.show(
        context: context,
        type: SKAlertType.buttons,
        title: 'Alert with custom buttons',
        message: 'Do you like this package?',
        okBtnText: 'YES',
        okBtnTxtColor: Colors.white,
        okBtnColor: const Color(0xFF3BD459),
        cancelBtnText: 'NO',
        cancelBtnTxtColor: Colors.white,
        cancelBtnColor: const Color(0xFFFF4954),
        onOkBtnTap: (value) {
          print('Okay Button Tapped');
        },
        onCancelBtnTap: (value) {
          print('Cancel Button Tapped');
        },
      );
    } else if (index == 3) {
      SKAlertDialog.show(
        context: context,
        type: SKAlertType.loginform,
        title: 'Login Form',
        okBtnText: 'LOGIN',
        onOkBtnTap: (value) {
          print('Okay Button Tapped');
        },
        onCancelBtnTap: (value) {
          print('Cancel Button Tapped');
        },
        onEmailTextFieldChanged: (value) {
          print('On Email Text Changed $value');
        },
        onPasswordTextFieldChanged: (value) {
          print('On Password Text Changed $value');
        },
      );
    } else if (index == 4) {
      SKAlertDialog.show(
        context: context,
        type: SKAlertType.checkbox,
        checkBoxAry: checkBoxAry,
        title: 'Checkbox',
        onCancelBtnTap: (value) {
          print('Cancel Button Tapped');
        },
        onCheckBoxSelection: (value) {
          print('onCheckBoxSelection $value');
        },
      );
    } else if (index == 5) {
      SKAlertDialog.show(
        context: context,
        type: SKAlertType.radiobutton,
        radioButtonAry: radioButtonAry,
        title: 'Radio Button',
        onCancelBtnTap: (value) {
          print('Cancel Button Tapped');
        },
        onRadioButtonSelection: (value) {
          print('onRadioButtonSelection $value');
        },
      );
    } else if (index == 6) {
      SKAlertDialog.show(
        context: context,
        type: SKAlertType.custom,
        customWidget: customWidget(),
      );
    }
  }

  Widget customWidget() {
    return new Padding(
        padding: EdgeInsets.only(left: 20, right: 20, top: 20, bottom: 20),
        child: Column(
          crossAxisAlignment: CrossAxisAlignment.start,
          children: <Widget>[
            Text(
              'Thank you for reviewing the package',
              style: TextStyle(
                  fontWeight: FontWeight.w400,
                  color: Theme.of(context).primaryColorDark.withOpacity(0.7),
                  fontSize: 20),
            ),
            SizedBox(height: 20),
            Row(
              mainAxisAlignment: MainAxisAlignment.center,
              children: <Widget>[
                FlatButton(
                  color: const Color(0xFF50A1FF),
                  onPressed: () {
                    Navigator.of(context).pop();
                  },
                  child: Text(
                    'The End !',
                    style: TextStyle(
                        fontWeight: FontWeight.w700,
                        color: Colors.white,
                        fontSize: 20),
                  ),
                )
              ],
            ),
          ],
        ));
  }
}

class AlertCard extends StatefulWidget {
  String title;
  String description;
  int index;
  IconData iconData;

  AlertCard({this.title, this.description, this.index, this.iconData});

  @override
  State<StatefulWidget> createState() {
    // TODO: implement createState
    return AlertCardState();
  }
}

class AlertCardState extends State<AlertCard> {
  @override
  Widget build(BuildContext context) {
    // TODO: implement build
    return Container(
      child: Padding(
        padding: EdgeInsets.only(left: 0, right: 0, top: 10, bottom: 0),
        child: Column(
          mainAxisAlignment: MainAxisAlignment.start,
          crossAxisAlignment: CrossAxisAlignment.start,
          children: <Widget>[
            Row(children: <Widget>[
              Column(
                mainAxisAlignment: MainAxisAlignment.center,
                children: <Widget>[
                  Icon(widget.iconData,
                      color:
                          Theme.of(context).primaryColorDark.withOpacity(0.4))
                ],
              ),
              SizedBox(width: 10),
              Expanded(
                child: Container(
                  child: Row(
                    mainAxisAlignment: MainAxisAlignment.spaceBetween,
                    children: <Widget>[
                      Expanded(
                        child: Column(
                          crossAxisAlignment: CrossAxisAlignment.start,
                          children: <Widget>[
                            Text(
                              widget.title,
                              style: GoogleFonts.nunito(
                                  fontSize: 20, fontWeight: FontWeight.w700),
                            ),
                            SizedBox(height: 5),
                            Text(widget.description,
                                style: GoogleFonts.nunito(
                                    fontSize: 15,
                                    fontWeight: FontWeight.w400,
                                    color: const Color(0xFF929794))),
                          ],
                        ),
                      ),
                      Column(
                        mainAxisAlignment: MainAxisAlignment.center,
                        children: <Widget>[
                          Icon(Icons.chevron_right,
                              color: Theme.of(context)
                                  .primaryColorDark
                                  .withOpacity(0.4))
                        ],
                      )
                    ],
                  ),
                ),
              )
            ]),
            SizedBox(height: 4),
            Divider()
          ],
        ),
      ),
    );
  }
}
```
