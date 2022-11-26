# CustomKeyboardKit
Creating Custom In App Keyboards with SwiftUI has never been easier than with this Swift Package

You can now build a Keyboard with 100% SwiftUI for your SwiftUI or UIKit App!

## Overview
* [Features](#features)
* [Example](#example)
* [Implementation](#implementation)
* [Warranty](#warranty)

## Features
- **Uses Apple's Accelerate framework on Matrix operations and solving of linear systems for increased performance**
- Build the entire keyboard layout in SwiftUI
- Use it in UIKit or SwiftUI
- Use it parallelly to any native keyboard
- Works flawlessly on iOS and iPadOS

## Creating the Keyboard
Simply extend the CustomKeyboard class and provide a static property and use the CustomKeyboardBuilder: 

    extension CustomKeyboard {
        static var yesnt = CustomKeyboardBuilder { textDocumentProxy, submit, playSystemFeedback in
            VStack {
                HStack {
                    Button("Yes!") {
                        textDocumentProxy.insertText("Yes")
                        playSystemFeedback?()
                    }
                    Button("No!") {
                        textDocumentProxy.insertText("No")
                        playSystemFeedback?()
                    }
                }
                Button("Maybe") {
                    textDocumentProxy.insertText("?")
                    playSystemFeedback?()
                }
                Button("Idk") {
                    textDocumentProxy.insertText("Idk")
                    playSystemFeedback?()
                }
                Button("Can you repeat the question?") {
                    playSystemFeedback?()
                    submit?()
                }
            }
            .buttonStyle(.bordered)
            .padding()
        }
    }

## Using my Custom Keyboard in SwiftUI
Once declared, you can use the custom keyboard with the `.customKeyboard(:)` View modifer and using your statically defined property

    struct ContentView: View {
        @State var text: String = ""

        var body: some View {
            VStack {
                Text(text)
                TextField("", text: $text)
                    .customKeyboard(.yesnt)
            }
        }
    }
    
## Using my Custom KEyboard in UIKit
Once declared, you can assign your `CustomKeyboard`'s `keyboardInputView` property to the UITextFields `inputView`.

    override func viewDidLoad() {
        myTextField.inputView = CustomKeyboard.yesnt.keyboardInputView
    }

## Warranty
The code comes with no warranty of any kind. I hope it'll be useful to you (it certainly is to me), but I make no guarantees regarding its functionality or otherwise.

## Special Thanks
Special thanks goes to the user @crayment which made it particularly easy for me with SwiftUI-Introspect to apply the Custom Keyboard to SwiftUI TextFields.

