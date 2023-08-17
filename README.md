# Android Kotlin Code Snippets
### <ins> Project 1: Hello World! </ins>

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


### <ins> Project 2: Button Click Event </ins>
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



### <ins> Project 3: Handling Text </ins>
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



### <ins> Project 4: Radio Button Group </ins>
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


### <ins> Project 5: Calculator </ins>
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



### <ins> Project 6: Simple Email Password Login </ins>
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


### <ins> Project 7: ListView </ins>
* [ListView](https://github.com/odukabdulbasit/SimpleListView)

```kotlin

// Displaying a List of Items using ListView with ArrayAdapter

val items = arrayOf("Item 1", "Item 2", "Item 3", "Item 4", "Item 5")

val listView: ListView = findViewById(R.id.listView)
val adapter = ArrayAdapter(this, android.R.layout.simple_list_item_1, items)
listView.adapter = adapter


```


### <ins> Project 8: RecyclerView </ins>
* [RecyclerView](https://github.com/odukabdulbasit/RecyclerView)

```kotlin

//ItemModel.kt:
data class ItemModel(val itemName: String)


//ItemAdapter.kt:
import android.view.LayoutInflater
import android.view.View
import android.view.ViewGroup
import android.widget.TextView
import androidx.recyclerview.widget.RecyclerView

class ItemAdapter(private val itemList: List<ItemModel>) : RecyclerView.Adapter<ItemAdapter.ItemViewHolder>() {

    override fun onCreateViewHolder(parent: ViewGroup, viewType: Int): ItemViewHolder {
        val itemView = LayoutInflater.from(parent.context).inflate(R.layout.item_layout, parent, false)
        return ItemViewHolder(itemView)
    }

    override fun onBindViewHolder(holder: ItemViewHolder, position: Int) {
        val item = itemList[position]
        holder.itemNameTextView.text = item.itemName
    }

    override fun getItemCount(): Int = itemList.size

    class ItemViewHolder(itemView: View) : RecyclerView.ViewHolder(itemView) {
        val itemNameTextView: TextView = itemView.findViewById(R.id.itemNameTextView)
    }
}


//MainActivity.kt:
import android.os.Bundle
import androidx.appcompat.app.AppCompatActivity
import androidx.recyclerview.widget.LinearLayoutManager
import androidx.recyclerview.widget.RecyclerView

class MainActivity : AppCompatActivity() {

    private lateinit var recyclerView: RecyclerView
    private lateinit var itemAdapter: ItemAdapter
    private val itemList = mutableListOf<ItemModel>()

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        recyclerView = findViewById(R.id.recyclerView)
        recyclerView.layoutManager = LinearLayoutManager(this)

        // Create sample data
        itemList.add(ItemModel("Item 1"))
        itemList.add(ItemModel("Item 2"))
        itemList.add(ItemModel("Item 3"))

        itemAdapter = ItemAdapter(itemList)
        recyclerView.adapter = itemAdapter
    }
}


```


### <ins> Project 9: ViewPager </ins>
* [ViewPager](https://github.com/odukabdulbasit/ViewPager)

```kotlin

// ViewPager Adapter
class MyPagerAdapter(fragmentManager: FragmentManager) : FragmentPagerAdapter(fragmentManager) {
    private val fragments = listOf(
        FragmentFirst(),
        FragmentSecond(),
        FragmentThird()
    )

    override fun getCount(): Int {
        return fragments.size
    }

    override fun getItem(position: Int): Fragment {
        return fragments[position]
    }
}


// Initialize ViewPager and PagerAdapter in MainActivity.kt
val viewPager: ViewPager = findViewById(R.id.viewPager)
val pagerAdapter = ViewPagerAdapter(supportFragmentManager)
viewPager.adapter = pagerAdapter


```

### <ins> Project 10: WebView </ins>
* [WebView](https://github.com/odukabdulbasit/WebView)

```kotlin
// Manifest
<uses-permission android:name="android.permission.INTERNET" />

// MainActivity.kt
val webView: WebView = findViewById(R.id.webView)
webView.webViewClient = WebViewClient()

        // Load a website
webView.loadUrl("https://Your WebSite")


```


### <ins> Project 11: Open New Activity With Intent </ins>
* [Intent](https://github.com/odukabdulbasit/Intent)

```kotlin
override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        // Find the button in your main activity layout
        findViewById<View>(R.id.btnOpenSecondActivity).setOnClickListener {
            openSecondActivityTextClick(it)
        }
    }

    private fun openSecondActivityTextClick(view: View) {
        // Create an intent to open the new activity
        val intent = Intent(this@MainActivity, MainActivity2::class.java)
        startActivity(intent)
    }


```

