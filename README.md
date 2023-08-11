# Android Kotlin Gems Projects
### Project 1: Hello World!
* [Hello World!](https://github.com/odukabdulbasit/HelloWorld)

```kotlin
fun helloWorld() {
  Log.i("message", "Hello World!")
}

\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\
Or

<TextView
        android:id="@+id/helloTextView"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Hello World!"
        android:textSize="24sp"
        android:textColor="@android:color/black"/>
```


### Project 2: Button Click Event
* [Button Click Event](https://github.com/odukabdulbasit/ButtonClickEvent)

```kotlin
// Implement Button Click Event and Show Toast Message
val buttonShowToast: Button = findViewById(R.id.buttonShowToast)
buttonShowToast.setOnClickListener {
    showToast("Hello, Toast!")
}

private fun showToast(message: String) {
    Toast.makeText(this, message, Toast.LENGTH_SHORT).show()
}

```



### Project 3: Handling Text
* [Text Handling](https://github.com/odukabdulbasit/TextHandling)

```kotlin
// Handling Text Input with EditText and Displaying it on a TextView

// Find the EditText and Button views from the layout
val editText: EditText = findViewById(R.id.editText)
val buttonShowText: Button = findViewById(R.id.buttonShowText)
val textView: TextView = findViewById(R.id.textView)

// Set an OnClickListener for the "Show Text" button
buttonShowText.setOnClickListener {
    // Retrieve the text entered in the EditText
    val inputText = editText.text.toString()
    
    // Display the entered text on the TextView
    textView.text = "You entered: $inputText"
}

```



### Project 4: Radio Button Group
* [Radio Button Group](https://github.com/odukabdulbasit/RadioButton)

```kotlin
// Using RadioButton and RadioGroup for Selecting Options

// Find the RadioGroup, Button, and TextView views from the layout
val radioGroup: RadioGroup = findViewById(R.id.radioGroup)
val buttonShowSelection: Button = findViewById(R.id.buttonShowSelection)
val textViewSelection: TextView = findViewById(R.id.textViewSelection)

// Set an OnClickListener for the "Show Selection" button
buttonShowSelection.setOnClickListener {
    val selectedOptionId = radioGroup.checkedRadioButtonId
    val selectedRadioButton: RadioButton = findViewById(selectedOptionId)

    val selectedText = selectedRadioButton.text.toString()
    textViewSelection.text = "Selected Option: $selectedText"
}

```


### Project 5: Calculator
* [Calculator](https://github.com/odukabdulbasit/Simple_Calculator)

```kotlin
<!-- ConstraintLayout for Simple Calculator UI -->

<!-- TextView to display result -->
<TextView
    android:id="@+id/textViewResult"
    android:layout_width="0dp"
    android:layout_height="wrap_content"
    android:textSize="24sp"
    android:gravity="end"
    app:layout_constraintTop_toTopOf="parent"
    app:layout_constraintEnd_toEndOf="parent"
    app:layout_constraintStart_toStartOf="parent"
    android:layout_marginTop="16dp"
    android:layout_marginEnd="16dp"
    android:layout_marginStart="16dp"/>

<!-- GridLayout for buttons -->
<GridLayout
    android:layout_width="0dp"
    android:layout_height="0dp"
    android:columnCount="4"
    android:rowCount="5"
    app:layout_constraintTop_toBottomOf="@+id/textViewResult"
    app:layout_constraintBottom_toTopOf="@+id/buttonEquals"
    app:layout_constraintEnd_toEndOf="parent"
    app:layout_constraintStart_toStartOf="parent"
    app:layout_constraintHorizontal_bias="0.5">

    <!-- Number Buttons, Operation Buttons, and Equals Button -->
    <!-- Add your button elements here -->
</GridLayout>


```



