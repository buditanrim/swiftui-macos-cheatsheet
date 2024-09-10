### Remove TextField focus

Q: How to remove default focus on TextField SwiftUI?

The TextField from SwiftUI focused on itself by default if you use `.focused()`
To remove the default focus when the view appears, set the `.onAppear` modifier and call the DispatchQueue `NSApp.keyWindow?.makeFirstResponder(nil)`
It's basically saying: "I don't want anything in the app to be focused right now."

```swift
var body: some View {
    HStack {
        TextField("Text field", text: $bindingText)
        /// Don't focus on anything
        .onAppear {
            DispatchQueue.main.async {
                NSApp.keyWindow?.makeFirstResponder(nil)
            }
        }
        /// Remove focus after submit (user press enter on the text field)
        .onSubmit {
            DispatchQueue.main.async {
                NSApp.keyWindow?.makeFirstResponder(nil)
            }
        }
    }
}
```

You can also apply the `onAppear` to the HStack in this example. It will remove the focus on the text field.
