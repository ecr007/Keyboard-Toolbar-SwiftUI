# Keyboard Toolbar SwiftUI

```swift
enum FocusedField {
    case int, dec
}

@State private var intNumberString = ""
@State private var decNumberString = ""
@FocusState private var focusedField: FocusedField?
    
var body: some View {
    NavigationStack {
        VStack {
            TextField("Enter Integer Number", text: $intNumberString)
                .focused($focusedField, equals: .int)
                .numbersOnly($intNumberString)
            TextField("Enter Decimal Number", text: $decNumberString)
                .focused($focusedField, equals: .dec)
                .numbersOnly($decNumberString, includeDecimal: true)
            Spacer()
        }
        .navigationTitle("Numbers Only")
        .textFieldStyle(.roundedBorder)
        .frame(width: 200)
        .toolbar {
            ToolbarItem(placement: .keyboard) {
                // To Force Right Position
                Spacer()
            }
            ToolbarItem(placement: .keyboard) {
                Button {
                    focusedField = nil
                } label: {
                    Image(systemName: "keyboard.chevron.compact.down")
                }
            }
        }
        .onAppear {
            // Add Clear option to Field (x)
            UITextField.appearance().clearButtonMode = .whileEditing
        }
    }
}
```
