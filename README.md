# Android Kotlin Code Snippets
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
fun onNumberClick(view: View) {
        val button = view as Button
        currentNumber += button.text
        textViewResult.setText(currentNumber)
    }

    fun onOperationClick(view: View) {
        val button = view as Button
        currentOperator = button.text.toString()
        firstNumber = currentNumber
        currentNumber = ""
    }

    fun onEqualsClick(view: View) {
        val number1 = firstNumber.toDoubleOrNull() ?: return
        val number2 = textViewResult.text.toString().toDoubleOrNull() ?: return

        val result = when (currentOperator) {
            "+" -> number1 + number2
            "-" -> number1 - number2
            "*" -> number1 * number2
            "/" -> number1 / number2
            else -> return
        }

        textViewResult.setText(result.toString())
        currentNumber = result.toString()
    }

    fun onDeleteClick(view: View) {
        currentNumber = ""
        textViewResult.setText("")
    }

    fun onClearClick(view: View) {
        currentNumber = ""
        firstNumber = ""
        textViewResult.setText("")
    }


```



### Project 6: Simple Email Password Login
* [Simple Email Password Login](https://github.com/odukabdulbasit/Simple_Email_Password_Login)

```kotlin

class MainActivity : AppCompatActivity() {

    private lateinit var usernameEditText: EditText
    private lateinit var passwordEditText: EditText
    private lateinit var loginButton: Button

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        usernameEditText = findViewById(R.id.usernameEditText)
        passwordEditText = findViewById(R.id.passwordEditText)
        loginButton = findViewById(R.id.loginButton)

        loginButton.setOnClickListener {
            val username = usernameEditText.text.toString()
            val password = passwordEditText.text.toString()

            if (isValidCredentials(username, password)) {
                // Successful login
                Toast.makeText(this, "Login successful", Toast.LENGTH_SHORT).show()
                // Add your required logic here (e.g., go to the next activity)
            } else {
                // Failed login
                Toast.makeText(this, "Invalid credentials", Toast.LENGTH_SHORT).show()
            }
        }
    }

    private fun isValidCredentials(username: String, password: String): Boolean {
        // Replace this with your actual login validation logic
        val validUsername = "your_username"
        val validPassword = "your_password"
        return username == validUsername && password == validPassword
    }
}


```




