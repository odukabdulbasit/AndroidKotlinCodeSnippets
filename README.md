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


### <ins> Project 12: Basic Stopwatch with Chronometer </ins>
* [Basic Stopwatch with Chronometer](https://github.com/odukabdulbasit/Stopwatch_with_Chronometer)

```kotlin

private var isRunning = false

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        val start_button = findViewById<Button>(R.id.start_button)
        val stop_button = findViewById<Button>(R.id.stop_button)
        val chronometer = findViewById<Chronometer>(R.id.chronometer)

        start_button.setOnClickListener {
            if (!isRunning) {
                chronometer.base = SystemClock.elapsedRealtime()
                chronometer.start()
                isRunning = true
            }
        }

        stop_button.setOnClickListener {
            if (isRunning) {
                chronometer.stop()
                isRunning = false
            }
        }
    }

```


### <ins> Project 13: Custom Dialog with Alert Dialog </ins>
* [Custom Dialog with Alert Dialog](https://github.com/odukabdulbasit/Custom_Dialog_with_AlertDialog)

```kotlin

import android.app.AlertDialog
import android.content.Context
import android.os.Bundle
import android.view.LayoutInflater
import android.view.View
import kotlinx.android.synthetic.main.custom_dialog_layout.view.*

class CustomDialog(context: Context) : AlertDialog(context) {

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)

        val inflater = LayoutInflater.from(context)
        val dialogView = inflater.inflate(R.layout.custom_dialog_layout, null)

        // Customize the dialog view here
        dialogView.dialogTitle.text = "Custom Dialog"
        dialogView.dialogMessage.text = "This is a custom dialog example."

        // Set click listener for buttons
        dialogView.btnCancel.setOnClickListener {
            dismiss()
        }

        dialogView.btnOk.setOnClickListener {
            // Do something when OK button is clicked
            dismiss()
        }

        // Set the custom view to the dialog
        setView(dialogView)
    }
}


// Usage
val customDialog = CustomDialog(this)
customDialog.show()


```


### <ins> Project 14: Progress Bar </ins>
* [Progress Bar](https://github.com/odukabdulbasit/Progress_Bar)

```kotlin

import android.os.Bundle
import android.os.Handler
import android.os.Looper
import androidx.appcompat.app.AppCompatActivity
import kotlinx.android.synthetic.main.activity_main.*

class MainActivity : AppCompatActivity() {

    private lateinit var progressBar: ProgressBar
    private var progressStatus = 0
    private val handler = Handler(Looper.getMainLooper())

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        progressBar = findViewById(R.id.progressBar) // Initialize the ProgressBar

        // Simulate progress updates
        simulateProgress()
    }

    private fun simulateProgress() {
        Thread(Runnable {
            while (progressStatus < 100) {
                progressStatus += 5 // Increment progress
                handler.post {
                    progressBar.progress = progressStatus // Update progress bar
                    if (progressStatus >= 100) {
                        progressBar.visibility = View.GONE // Hide progress bar
                        // Do other actions after loading completes
                    }
                }
                try {
                    Thread.sleep(500) // Simulate some work being done
                } catch (e: InterruptedException) {
                    e.printStackTrace()
                }
            }
        }).start()
    }
}


```


### <ins> Project 15: Quiz App </ins>
* [ Quiz App](https://github.com/odukabdulbasit/Quiz_App)

```kotlin

import android.os.Bundle
import android.widget.Button
import android.widget.RadioButton
import android.widget.RadioGroup
import android.widget.TextView
import androidx.appcompat.app.AppCompatActivity


class MainActivity : AppCompatActivity() {
    private lateinit var questionTextView: TextView
    private lateinit var optionsRadioGroup: RadioGroup
    private lateinit var nextButton: Button

    private val questions = listOf(
        Question("What is the capital of France?", listOf("Berlin", "London", "Paris", "Madrid"), 2),
        Question("Which planet is known as the 'Red Planet'?", listOf("Mars", "Jupiter", "Venus", "Saturn"), 0),
        Question("What is the largest mammal?", listOf("Elephant", "Blue Whale", "Giraffe", "Hippopotamus"), 1)
    )

    private var currentQuestionIndex = 0
    private var score = 0

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        questionTextView = findViewById(R.id.questionTextView)
        optionsRadioGroup = findViewById(R.id.optionsRadioGroup)
        nextButton = findViewById(R.id.nextButton)

        nextButton.setOnClickListener {
            checkAnswer()
            showNextQuestion()
        }

        // Set up a listener for radio button clicks
        optionsRadioGroup.setOnCheckedChangeListener { _, checkedId ->
            // Enable the "Next" button when a radio button is selected
            nextButton.isEnabled = true
        }

        showNextQuestion()
    }

    private fun showNextQuestion() {
        if (currentQuestionIndex < questions.size) {
            val question = questions[currentQuestionIndex]

            questionTextView.text = question.text
            optionsRadioGroup.removeAllViews()

            question.options.forEachIndexed { index, optionText ->
                val radioButton = RadioButton(this)
                radioButton.id = index
                radioButton.text = optionText
                optionsRadioGroup.addView(radioButton)
            }

            nextButton.isEnabled = false
            currentQuestionIndex++
        } else {
            // Quiz completed
            // You can display the final score or any other result here
        }
    }

    private fun checkAnswer() {
        val selectedRadioButtonId = optionsRadioGroup.checkedRadioButtonId
        if (selectedRadioButtonId == questions[currentQuestionIndex - 1].correctAnswerIndex) {
            score++
        }
    }
}

```


### <ins> Project 16: Camera App </ins>
* [Camera App](https://github.com/odukabdulbasit/Camera_App)

```kotlin

<!-- Adding Permissions for Accessing the Camera -->
<uses-permission android:name="android.permission.CAMERA"/>
<uses-feature android:name="android.hardware.camera" android:required="true"/>


// In your activity
private val CAMERA_PERMISSION_REQUEST = 100

// Request camera permission
if (ContextCompat.checkSelfPermission(
        this,
        Manifest.permission.CAMERA
    ) != PackageManager.PERMISSION_GRANTED
) {
    ActivityCompat.requestPermissions(
        this,
        arrayOf(Manifest.permission.CAMERA),
        CAMERA_PERMISSION_REQUEST
    )
}



// Handle permission result
override fun onRequestPermissionsResult(
    requestCode: Int,
    permissions: Array<out String>,
    grantResults: IntArray
) {
    if (requestCode == CAMERA_PERMISSION_REQUEST) {
        if (grantResults.isNotEmpty() && grantResults[0] == PackageManager.PERMISSION_GRANTED) {
            // Permission granted, handle camera access
        } else {
            // Permission denied, handle denied state
        }
    }
}


```

### <ins> Project 17: Date Picker </ins>
* [Date Picker](https://github.com/odukabdulbasit/DatePicker)

```kotlin

import android.app.DatePickerDialog
import android.os.Bundle
import android.widget.Button
import android.widget.TextView
import androidx.appcompat.app.AppCompatActivity
import java.text.SimpleDateFormat
import java.util.*

class MainActivity : AppCompatActivity() {

    private lateinit var selectedDateText: TextView

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        selectedDateText = findViewById(R.id.selectedDateText)
        val pickDateButton: Button = findViewById(R.id.pickDateButton)

        pickDateButton.setOnClickListener {
            showDatePicker()
        }
    }

    private fun showDatePicker() {
        val calendar = Calendar.getInstance()

        val dateListener = DatePickerDialog.OnDateSetListener { _, year, monthOfYear, dayOfMonth ->
            calendar.set(Calendar.YEAR, year)
            calendar.set(Calendar.MONTH, monthOfYear)
            calendar.set(Calendar.DAY_OF_MONTH, dayOfMonth)

            val dateFormat = SimpleDateFormat("yyyy-MM-dd", Locale.getDefault())
            val selectedDate = dateFormat.format(calendar.time)
            selectedDateText.text = "Selected Date: $selectedDate"
        }

        val datePickerDialog = DatePickerDialog(
            this,
            dateListener,
            calendar.get(Calendar.YEAR),
            calendar.get(Calendar.MONTH),
            calendar.get(Calendar.DAY_OF_MONTH)
        )

        datePickerDialog.show()
    }
}

```


### <ins> Project 18: Custom Toolbar with Action </ins>
* [Custom Toolbar with Action](https://github.com/odukabdulbasit/Custom_Toolbar)

```kotlin

import android.os.Bundle
import android.view.Menu
import android.view.MenuItem
import android.widget.Toast
import androidx.appcompat.app.AppCompatActivity
import androidx.appcompat.widget.Toolbar

class MainActivity : AppCompatActivity() {

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        val toolbar = findViewById<Toolbar>(R.id.toolbar)
        setSupportActionBar(toolbar)

        // Customize the Toolbar title and appearance
        supportActionBar?.apply {
            title = "Custom Toolbar"
            setDisplayHomeAsUpEnabled(true)
            setHomeAsUpIndicator(R.drawable.ic_menu) // Replace with your icon
        }

        // Handle the action button click
        toolbar.setOnMenuItemClickListener { menuItem ->
            when (menuItem.itemId) {
                R.id.action_button -> {
                    // Perform your action here
                    Toast.makeText(this, "Action button is clicked!", Toast.LENGTH_LONG).show()
                    true
                }
                else -> false
            }
        }
    }

    override fun onCreateOptionsMenu(menu: Menu?): Boolean {
        menuInflater.inflate(R.menu.menu_main, menu)
        return true
    }

    override fun onOptionsItemSelected(item: MenuItem): Boolean {
        when (item.itemId) {
            android.R.id.home -> {
                // Handle Toolbar's home button click (e.g., navigation drawer toggle)
                Toast.makeText(this, "Home is clicked!", Toast.LENGTH_LONG).show()
                return true
            }
        }
        return super.onOptionsItemSelected(item)
    }
}


```


### <ins> Project 19: Bottom Navigation Bar </ins>
* [Bottom Navigation Bar](https://github.com/odukabdulbasit/Bottom_Navigation_Bar)

```kotlin

import android.os.Bundle
import androidx.appcompat.app.AppCompatActivity
import androidx.fragment.app.Fragment
import com.google.android.material.bottomnavigation.BottomNavigationView

class MainActivity : AppCompatActivity() {

    private lateinit var bottomNavigation: BottomNavigationView

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        bottomNavigation = findViewById(R.id.bottomNavigation)
        bottomNavigation.setOnNavigationItemSelectedListener { menuItem ->
            when (menuItem.itemId) {
                R.id.navigation_home -> replaceFragment(HomeFragment())
                R.id.navigation_dashboard -> replaceFragment(DashboardFragment())
                R.id.navigation_notifications -> replaceFragment(NotificationsFragment())
            }
            true
        }

        // Set the initial fragment
        replaceFragment(HomeFragment())
    }

    private fun replaceFragment(fragment: Fragment) {
        supportFragmentManager.beginTransaction()
            .replace(R.id.container, fragment)
            .commit()
    }
}

```



### <ins> Project 20: Displaying a Snackbar </ins>
* [Displaying a Snackbar](https://github.com/odukabdulbasit/Displaying_Snackbar)

```kotlin

import android.os.Bundle
import androidx.fragment.app.Fragment
import android.view.LayoutInflater
import android.view.View
import android.view.ViewGroup
import android.widget.Button
import com.google.android.material.snackbar.Snackbar


class SnackbarFragment : Fragment() {

    override fun onCreateView(
        inflater: LayoutInflater, container: ViewGroup?,
        savedInstanceState: Bundle?
    ): View? {
        // Inflate the layout for this fragment

        return inflater.inflate(R.layout.fragment_snackbar, container, false)
    }

    override fun onViewCreated(view: View, savedInstanceState: Bundle?) {
        super.onViewCreated(view, savedInstanceState)

        val button = view.findViewById<Button>(R.id.button)

        button.setOnClickListener {
            val message = "This is a Snackbar message"
            val duration = Snackbar.LENGTH_LONG

            val snackbar = Snackbar.make(view, message, duration)
            snackbar.setAction("Dismiss") {
                // Optional: Define action to be taken when the user clicks on the action button
            }

            snackbar.show()
        }
    }

}

```


### <ins> Project 21: Shared Preferences Save and Retrive Data </ins>
* [SharedPreferences](https://github.com/odukabdulbasit/SharedPreferences)

```kotlin

<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />


import android.content.Context
import android.content.SharedPreferences
import androidx.appcompat.app.AppCompatActivity
import android.os.Bundle
import android.widget.Button
import android.widget.EditText
import android.widget.TextView

class MainActivity : AppCompatActivity() {

    private lateinit var sharedPreferences: SharedPreferences
    private lateinit var usernameEditText: EditText
    private lateinit var saveButton: Button
    private lateinit var retrieveButton: Button
    private lateinit var resultTextView: TextView

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        // Initialize SharedPreferences
        sharedPreferences = getSharedPreferences("MyPrefs", Context.MODE_PRIVATE)

        // Initialize UI elements
        usernameEditText = findViewById(R.id.usernameEditText)
        saveButton = findViewById(R.id.saveButton)
        retrieveButton = findViewById(R.id.retrieveButton)
        resultTextView = findViewById(R.id.resultTextView)

        // Save button click listener
        saveButton.setOnClickListener {
            val username = usernameEditText.text.toString()
            saveData("username", username)
            usernameEditText.text.clear()
        }

        // Retrieve button click listener
        retrieveButton.setOnClickListener {
            val savedUsername = getData("username", "")
            resultTextView.text = "Saved username: $savedUsername"
        }
    }

    private fun saveData(key: String, value: String) {
        val editor = sharedPreferences.edit()
        editor.putString(key, value)
        editor.apply()
    }

    private fun getData(key: String, defaultValue: String): String {
        return sharedPreferences.getString(key, defaultValue) ?: defaultValue
    }
}

```


### <ins> Project 22: Animations </ins>
* [Animations](https://github.com/odukabdulbasit/Animations)

```kotlin

<!-- res/anim/fade_in.xml -->
<alpha xmlns:android="http://schemas.android.com/apk/res/android"
    android:interpolator="@android:anim/accelerate_interpolator"
    android:fromAlpha="0.0"
    android:toAlpha="1.0"
    android:duration="1000" />


<!-- res/anim/rotate.xml -->
<rotate xmlns:android="http://schemas.android.com/apk/res/android"
    android:fromDegrees="0"
    android:toDegrees="360"
    android:pivotX="50%"
    android:pivotY="50%"
    android:duration="1000" />


<!-- res/anim/scale.xml -->
<scale xmlns:android="http://schemas.android.com/apk/res/android"
    android:fromXScale="1.0"
    android:toXScale="1.5"
    android:fromYScale="1.0"
    android:toYScale="1.5"
    android:pivotX="50%"
    android:pivotY="50%"
    android:duration="1000"
    android:repeatMode="reverse"
    android:repeatCount="1" />


<!-- res/anim/translate.xml -->
<translate xmlns:android="http://schemas.android.com/apk/res/android"
    android:fromXDelta="0"
    android:toXDelta="200"
    android:duration="1000"
    android:repeatMode="reverse"
    android:repeatCount="1" />





import android.os.Bundle
import android.view.animation.AnimationUtils
import android.widget.Button
import android.widget.ImageView
import androidx.appcompat.app.AppCompatActivity

class MainActivity : AppCompatActivity() {

    private lateinit var imageView: ImageView
    private lateinit var buttonFadeIn: Button
    private lateinit var buttonRotate: Button
    private lateinit var buttonScale: Button
    private lateinit var buttonTranslate: Button

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        imageView = findViewById(R.id.imageView)
        buttonFadeIn = findViewById(R.id.buttonFadeIn)
        buttonRotate = findViewById(R.id.buttonRotate)
        buttonScale = findViewById(R.id.buttonScale)
        buttonTranslate = findViewById(R.id.buttonTranslate)

        val fadeInAnimation = AnimationUtils.loadAnimation(this, R.anim.fade_in)
        val rotateAnimation = AnimationUtils.loadAnimation(this, R.anim.rotate)
        val scaleAnimation = AnimationUtils.loadAnimation(this, R.anim.scale)
        val translateAnimation = AnimationUtils.loadAnimation(this, R.anim.translate)

        buttonFadeIn.setOnClickListener { imageView.startAnimation(fadeInAnimation) }
        buttonRotate.setOnClickListener { imageView.startAnimation(rotateAnimation) }
        buttonScale.setOnClickListener { imageView.startAnimation(scaleAnimation) }
        buttonTranslate.setOnClickListener { imageView.startAnimation(translateAnimation) }
    }
}

```


### <ins> Project 23: Splash Screen with Welcome Animation  </ins>
* [Splash Screen with Welcome Animation](https://github.com/odukabdulbasit/SplashScreen)

```kotlin

import android.content.Intent
import android.os.Bundle
import android.view.animation.AlphaAnimation
import android.view.animation.Animation
import android.view.animation.AnimationSet
import android.view.animation.RotateAnimation
import android.view.animation.TranslateAnimation
import android.widget.TextView
import androidx.appcompat.app.AppCompatActivity

class SplashActivity : AppCompatActivity() {

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)

        // Set the layout for the splash screen
        setContentView(R.layout.activity_splash)

        // Optional: You can perform any initialization tasks here
        val welcomeTextView = findViewById<TextView>(R.id.welcomeTextView)

        // Create a translation animation
        val translateAnimation = TranslateAnimation(0f, 0f, 0f, -100f)
        translateAnimation.duration = 1500 // 1.5 second

        // Create a rotation animation
        val rotateAnimation = RotateAnimation(0f, 360f, Animation.RELATIVE_TO_SELF, 0.5f, Animation.RELATIVE_TO_SELF, 0.5f)
        rotateAnimation.duration = 1500 // 1.5 second

        // Create a fade-out animation
        val fadeOutAnimation = AlphaAnimation(1f, 0f)
        fadeOutAnimation.duration = 2000 // 2 second

        // Combine animations into an AnimationSet
        val animationSet = AnimationSet(true)
        animationSet.addAnimation(translateAnimation)
        animationSet.addAnimation(rotateAnimation)
        animationSet.addAnimation(fadeOutAnimation)

        // Apply animation to the TextView
        welcomeTextView.startAnimation(animationSet)



        // Create a delay using a Handler to transition to the main activity after a certain time
        val handler = android.os.Handler()
        handler.postDelayed({
            // Start the main activity
            val intent = Intent(this@SplashActivity, MainActivity::class.java)
            startActivity(intent)

            // Close the splash activity
            finish()
        }, SPLASH_DELAY) // Set the delay time in milliseconds
    }

    companion object {
        private const val SPLASH_DELAY: Long = 5000 // 5 seconds
    }
}

```


### <ins> Project 24: Async Task  </ins>
* [Async Task](https://github.com/odukabdulbasit/AsyncTask)

```kotlin

import android.os.AsyncTask
import android.os.Bundle
import android.view.View
import androidx.appcompat.app.AppCompatActivity
import com.odukabdulbasit.asynctask.databinding.ActivityMainBinding
import java.lang.ref.WeakReference

class MainActivity : AppCompatActivity() {

    private lateinit var binding: ActivityMainBinding

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)

        binding = ActivityMainBinding.inflate(layoutInflater)
        val view = binding.root
        setContentView(view)

        // Button click event to start the AsyncTask
        binding.startTaskButton.setOnClickListener {
            it.isEnabled = false
            binding.progressBar.visibility = View.VISIBLE
            val task = MyAsyncTask(this)
            task.execute()
        }
    }

    // Define your AsyncTask class
    private class MyAsyncTask(context: MainActivity) : AsyncTask<Void, Void, String>() {

        private val activityReference: WeakReference<MainActivity> = WeakReference(context)

        override fun doInBackground(vararg params: Void?): String {
            // Simulate a background task, e.g., fetching data from a server
            Thread.sleep(5000) // Simulate a delay of 5 seconds
            return "Task completed"
        }

        override fun onPostExecute(result: String) {
            super.onPostExecute(result)
            val activity = activityReference.get()
            activity?.updateUI(result)
        }
    }

    // Update UI after AsyncTask completion
    fun updateUI(result: String) {
        binding.startTaskButton.isEnabled = true
        binding.progressBar.visibility = View.GONE
        binding.resultTextView.text = result
    }
}

```

### <ins> Project 25: Handling orientation changes using onSaveInstanceState </ins>
* [Handling orientation changes using onSaveInstanceState](https://github.com/odukabdulbasit/HandlingOrientationChanges)

```kotlin

import android.os.Bundle
import android.widget.CheckBox
import android.widget.EditText
import androidx.appcompat.app.AppCompatActivity

class MainActivity : AppCompatActivity() {

    private var editTextValue = ""
    private var checkboxChecked = false
    private lateinit var editText: EditText
    private lateinit var checkBox: CheckBox

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        // Initialize your UI components
        // For example, you have an EditText and a CheckBox
        // Assume you have EditText with ID: editText and CheckBox with ID: checkBox

        editText = findViewById(R.id.editText)
        checkBox = findViewById(R.id.checkBox)

        if (savedInstanceState != null) {
            // Restore the saved data from savedInstanceState
            editTextValue = savedInstanceState.getString("editTextValue", "")
            checkboxChecked = savedInstanceState.getBoolean("checkboxChecked", false)
        }

        // Apply the restored values to the UI components
        editText.setText(editTextValue)
        checkBox.isChecked = checkboxChecked

        // Handle other setup tasks
    }

    override fun onSaveInstanceState(outState: Bundle) {
        // Save the state of UI components into the outState Bundle
        outState.putString("editTextValue", editText.text.toString())
        outState.putBoolean("checkboxChecked", checkBox.isChecked)

        super.onSaveInstanceState(outState)
    }
}

```

### <ins> Project 26: Search View </ins>
* [Adding a search functionality with SearchView](https://github.com/odukabdulbasit/SearchView)

```kotlin

import androidx.appcompat.app.AppCompatActivity
import android.os.Bundle
import android.widget.SearchView

class MainActivity : AppCompatActivity() {
    private lateinit var searchView: SearchView

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        searchView = findViewById(R.id.searchView)
        // Configure the SearchView
        searchView.setIconifiedByDefault(false)
        searchView.queryHint = "Search..."

        // Set a query text listener to handle search queries
        searchView.setOnQueryTextListener(object : SearchView.OnQueryTextListener {
            override fun onQueryTextSubmit(query: String?): Boolean {
                // Handle the submitted query (perform search)
                if (!query.isNullOrBlank()) {
                    performSearch(query)
                }
                return true
            }
            override fun onQueryTextChange(newText: String?): Boolean {
                // Handle query text changes (filter results, etc.)
                return true
            }
        })
    }

    private fun performSearch(query: String) {
        // Implement your search logic here
        // You can use this query to filter a list or perform a network request
        // Update your UI with the search results
    }
}

```


### <ins> Project 27: RSS Feed Reader </ins>
* [RSS Feed Reader](https://github.com/odukabdulbasit/RssFeedReader)

```kotlin

import android.os.Bundle
import android.widget.Button
import android.widget.TextView
import androidx.appcompat.app.AppCompatActivity
import kotlinx.coroutines.Dispatchers
import kotlinx.coroutines.GlobalScope
import kotlinx.coroutines.launch
import kotlinx.coroutines.withContext
import io.ktor.client.*
import io.ktor.client.request.*
import io.ktor.client.statement.*
import io.ktor.http.*
import org.w3c.dom.Element
import org.w3c.dom.NodeList
import javax.xml.parsers.DocumentBuilderFactory

class MainActivity : AppCompatActivity() {

    private lateinit var fetchButton : Button
    private lateinit var titleTextView : TextView
    lateinit var descriptionTextView : TextView

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        fetchButton = findViewById(R.id.fetchButton)
        titleTextView = findViewById(R.id.titleTextView)
        descriptionTextView = findViewById(R.id.descriptionTextView)

        val rssFeedUrl = "https://example.com/rss-feed.xml" // Replace with your RSS feed URL

        fetchButton.setOnClickListener {
            fetchAndDisplayRssFeed(rssFeedUrl)
        }
    }

    private fun fetchAndDisplayRssFeed(url: String) {
        GlobalScope.launch(Dispatchers.IO) {
            try {
                val rssFeedItems = fetchRssFeed(url)

                if (rssFeedItems != null && rssFeedItems.length > 0) {
                    val item = rssFeedItems.item(0) as Element // Assuming you want to display the first item

                    val title = item.getElementsByTagName("title").item(0).textContent
                    val description = item.getElementsByTagName("description").item(0).textContent

                    // Update the UI on the main thread
                    withContext(Dispatchers.Main) {
                        titleTextView.text = "Title: $title"
                        descriptionTextView.text = "Description: $description"
                        // Update other TextViews as needed
                    }
                }
            } catch (e: Exception) {
                e.printStackTrace()
            }
        }
    }

    private suspend fun fetchRssFeed(url: String): NodeList? {
        val client = HttpClient()

        val response: HttpResponse = client.get(url) {
            accept(ContentType.Application.Xml)
        }

        val xmlContent = response.readText()

        val documentBuilderFactory = DocumentBuilderFactory.newInstance()
        val documentBuilder = documentBuilderFactory.newDocumentBuilder()
        val document = documentBuilder.parse(xmlContent.byteInputStream())

        return document.documentElement.getElementsByTagName("item")
    }
}

```


### <ins> Project 28: Retrofit </ins>
* [Retrofit](https://github.com/odukabdulbasit/Retrofit)

```kotlin

// Using Retrofit for Making HTTP Requests to a REST API

// Define your Retrofit instance
val retrofit = Retrofit.Builder()
    .baseUrl("https://api.example.com/")
    .addConverterFactory(GsonConverterFactory.create())
    .build()

// Create an interface for your API endpoints
interface MyApiService {
    @GET("posts")
    suspend fun getPosts(): Response<List<Post>>
}

// Create a Retrofit service
val apiService = retrofit.create(MyApiService::class.java)

// Make a network request in a Coroutine
try {
    val response = apiService.getPosts()
    if (response.isSuccessful) {
        val posts = response.body()
        // Handle the fetched data as needed
    } else {
        // Handle error
    }
} catch (e: Exception) {
    e.printStackTrace()
}

```


### <ins> Project 29: Displaying images with Picasso or Glide library </ins>
* [Displaying images with Picasso or Glide library](https://github.com/odukabdulbasit/DinsplayImagefromInternet)

```kotlin

class MainActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        val imageView = findViewById<ImageView>(R.id.imageView)

        // Replace 'image_url' with the actual URL of the image you want to display.
        val imageUrl = "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTGEdz_G8Oj8B21oVav2u1C237PNnifZn68WQ&usqp=CAU"

        // Load and display the image using Picasso
        //Picasso.get().load(imageUrl).into(imageView)

        // Load and display the image using Glide
        Glide.with(this)
            .load(imageUrl)
            .centerCrop() // You can change the transformation as needed
            .placeholder(R.drawable.placeholder_image) // Placeholder image
            .into(imageView)
    }
}

```


### <ins> Project 30: progress notification for long-running tasks </ins>
* [progress notification for long-running tasks](https://github.com/odukabdulbasit/ProgressNotification)

```kotlin

import android.Manifest
import android.app.NotificationChannel
import android.app.NotificationManager
import android.content.Context
import android.content.pm.PackageManager
import android.os.AsyncTask
import android.os.Build
import android.os.Bundle
import android.os.SystemClock
import androidx.appcompat.app.AppCompatActivity
import androidx.core.app.ActivityCompat
import androidx.core.app.NotificationCompat
import androidx.core.app.NotificationManagerCompat

class MainActivity : AppCompatActivity() {

    companion object {
        private const val CHANNEL_ID = "progress_notification_channel"
        private const val NOTIFICATION_ID = 1
    }

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        // Create a notification channel (required for Android Oreo and above)
        createNotificationChannel()

        // Start your long-running task
        MyAsyncTask().execute()
    }

    private fun createNotificationChannel() {
        if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.O) {
            val name = "Progress Notification"
            val descriptionText = "Shows the progress of a long-running task"
            val importance = NotificationManager.IMPORTANCE_LOW
            val channel = NotificationChannel(CHANNEL_ID, name, importance).apply {
                description = descriptionText
            }

            val notificationManager =
                getSystemService(Context.NOTIFICATION_SERVICE) as NotificationManager
            notificationManager.createNotificationChannel(channel)
        }
    }

    inner class MyAsyncTask : AsyncTask<Void, Int, Void>() {

        override fun doInBackground(vararg params: Void?): Void? {
            // Simulate a long-running task
            for (progress in 1..100) {
                SystemClock.sleep(100) // Simulate work being done
                publishProgress(progress) // Update the progress
            }
            return null
        }

        override fun onProgressUpdate(vararg values: Int?) {
            super.onProgressUpdate(*values)

            // Update the progress notification
            val progress = values[0] ?: 0
            updateProgressNotification(progress)
        }

        override fun onPostExecute(result: Void?) {
            super.onPostExecute(result)

            // Remove the progress notification when the task is done
            val notificationManager =
                NotificationManagerCompat.from(this@MainActivity)
            notificationManager.cancel(NOTIFICATION_ID)
        }
    }

    private fun updateProgressNotification(progress: Int) {
        val notificationBuilder = NotificationCompat.Builder(this, CHANNEL_ID)
            .setSmallIcon(R.drawable.ic_notification)
            .setContentTitle("Long Running Task")
            .setContentText("Progress: $progress%")
            .setPriority(NotificationCompat.PRIORITY_LOW)
            .setOnlyAlertOnce(true)
            .setOngoing(true)
            .setProgress(100, progress, false)

        val notificationManager = NotificationManagerCompat.from(this)
        if (ActivityCompat.checkSelfPermission(
                this,
                Manifest.permission.POST_NOTIFICATIONS
            ) != PackageManager.PERMISSION_GRANTED
        ) {
            // TODO: Consider calling
            //    ActivityCompat#requestPermissions
            // here to request the missing permissions, and then overriding
            //   public void onRequestPermissionsResult(int requestCode, String[] permissions,
            //                                          int[] grantResults)
            // to handle the case where the user grants the permission. See the documentation
            // for ActivityCompat#requestPermissions for more details.
            return
        }
        notificationManager.notify(NOTIFICATION_ID, notificationBuilder.build())
    }
}

```


### <ins> Project 31: Custom ListView </ins>
* [Custom ListView](https://github.com/odukabdulbasit/CustomListView)

```kotlin

// MainActivity.kt
class MainActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        val listView = findViewById<ListView>(R.id.listView)

        // Sample data
        val data = listOf("Item 1", "Item 2", "Item 3", "Item 4", "Item 5")

        // Create and set the custom adapter
        val adapter = CustomListAdapter(this, data)
        listView.adapter = adapter

    }
}


// CustomListAdapter
class CustomListAdapter(context: Context, private val data: List<String>) :
    ArrayAdapter<String>(context, R.layout.list_item, data) {

    // ViewHolder pattern for efficient view recycling
    private class ViewHolder {
        internal var textView: TextView? = null
    }

    override fun getView(position: Int, convertView: View?, parent: ViewGroup): View {
        var convertView = convertView
        val holder: ViewHolder

        if (convertView == null) {
            // Inflate the custom list item layout
            val inflater = context.getSystemService(Context.LAYOUT_INFLATER_SERVICE) as LayoutInflater
            convertView = inflater.inflate(R.layout.list_item, null)

            // Initialize the ViewHolder
            holder = ViewHolder()
            holder.textView = convertView.findViewById(R.id.textView) as TextView
            convertView.tag = holder
        } else {
            // Reuse the existing ViewHolder
            holder = convertView.tag as ViewHolder
        }

        // Set the data for the list item
        val item = data[position]
        holder.textView?.text = item

        return convertView!!
    }
}


```


### <ins> Project 32: AlertDialog with a list of items and handling item clicks </ins>
* [AlertDialog with a list of items and handling item clicks](https://github.com/odukabdulbasit/AlertDialogWithList)

```kotlin

import android.app.AlertDialog
import android.os.Bundle
import android.widget.ArrayAdapter
import android.widget.Button
import android.widget.Toast
import androidx.appcompat.app.AppCompatActivity

class MainActivity : AppCompatActivity() {

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        // Sample list of items
        val items = arrayOf("Item 1", "Item 2", "Item 3", "Item 4")

        // Create an ArrayAdapter to populate the list in the AlertDialog
        val adapter = ArrayAdapter(this, android.R.layout.simple_list_item_1, items)

        // Create the AlertDialog
        val alertDialog = AlertDialog.Builder(this)
            .setTitle("Select an Item")
            .setAdapter(adapter) { _, position ->
                // Handle item click
                val selectedItem = items[position]
                Toast.makeText(this, "You selected: $selectedItem", Toast.LENGTH_SHORT).show()
            }
            .setNegativeButton("Cancel") { dialog, _ ->
                // Handle cancel button click
                dialog.dismiss()
            }
            .create()

        // Show the AlertDialog when a button or some UI element is clicked
        val showButton = findViewById<Button>(R.id.show_button) // Replace with your button ID
        showButton.setOnClickListener {
            alertDialog.show()
        }
    }

```


### <ins> Project 33: Custom ProgressBar with CircularProgressDrawable </ins>
* [Custom ProgressBar with CircularProgressDrawable](https://github.com/odukabdulbasit/CustomProgressBar)

```kotlin

// MainActivity.kt
import android.os.Bundle
import android.widget.ImageView
import androidx.appcompat.app.AppCompatActivity
import androidx.core.content.ContextCompat
import androidx.swiperefreshlayout.widget.CircularProgressDrawable

class MainActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        val circularProgressDrawable = CircularProgressDrawable(this)
        circularProgressDrawable.strokeWidth = 10f
        circularProgressDrawable.centerRadius = 50f
        circularProgressDrawable.setColorSchemeColors(ContextCompat.getColor(this, com.google.android.material.R.color.accent_material_light))
        circularProgressDrawable.start()

        val imageView = findViewById<ImageView>(R.id.progressImageView)
        imageView.setImageDrawable(circularProgressDrawable)
    }
}


// circular_progress_drawable.xml
<?xml version="1.0" encoding="utf-8"?>
<layer-list xmlns:android="http://schemas.android.com/apk/res/android">
    <item
        android:id="@android:id/background"
        android:drawable="@drawable/circle_gray" />
    <item
        android:id="@android:id/progress"
        android:drawable="@drawable/circle_progress" />
</layer-list>


// circle_gray
<?xml version="1.0" encoding="utf-8"?>
<shape
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:shape="ring"
    android:useLevel="false"
    android:innerRadiusRatio="2.5"
    android:thicknessRatio="10"
    android:angle="0"
    android:color="#DDDDDD">
</shape>


// circle_progress
<?xml version="1.0" encoding="utf-8"?>
<rotate
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:fromDegrees="0"
    android:toDegrees="360">
    <shape
        android:shape="ring"
        android:useLevel="true"
        android:innerRadiusRatio="2.5"
        android:thicknessRatio="10"
        android:angle="0"
        android:color="#3498db">
    </shape>
</rotate>

```



### <ins> Project 34: Adding a share action to share content from the app </ins>
* [Adding a share action to share content from the app](https://github.com/odukabdulbasit/ShareContent)

```kotlin

import android.content.Intent
import android.os.Bundle
import android.widget.Button
import androidx.appcompat.app.AppCompatActivity

class MainActivity : AppCompatActivity() {

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        val shareButton = findViewById<Button>(R.id.shareButton)

        shareButton.setOnClickListener {
            shareContent("Hello, this is the content to share.")
        }
    }

    private fun shareContent(content: String) {
        val intent = Intent(Intent.ACTION_SEND)
        intent.type = "text/plain"
        intent.putExtra(Intent.EXTRA_TEXT, content)

        // You can also add additional options for the chooser dialog
        val chooserTitle = "Share via"
        val shareIntent = Intent.createChooser(intent, chooserTitle)

        // Verify that the intent will resolve to an activity before starting it
        if (intent.resolveActivity(packageManager) != null) {
            startActivity(shareIntent)
        }
    }
}

```


### <ins> Project 35: Using ConstraintLayout for building responsive layouts </ins>
* [Using ConstraintLayout for building responsive layouts](https://github.com/odukabdulbasit/ResponsiveUi)

```kotlin

<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">

    <!-- Button 1 -->
    <Button
        android:id="@+id/button1"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Button 1"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintEnd_toStartOf="@+id/guideline"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintBottom_toBottomOf="parent" />

    <!-- Guideline to create responsive spacing -->
    <androidx.constraintlayout.widget.Guideline
        android:id="@+id/guideline"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:orientation="vertical"
        app:layout_constraintGuide_percent="0.5" />

    <!-- Button 2 -->
    <Button
        android:id="@+id/button2"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Button 2"
        app:layout_constraintStart_toEndOf="@+id/guideline"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintBottom_toBottomOf="parent" />

</androidx.constraintlayout.widget.ConstraintLayout>

```



### <ins> Project 36: Implementing a Timer with CountDownTimer </ins>
* [CountDownTimer](https://github.com/odukabdulbasit/CountDownTimer)

```kotlin

import android.os.Bundle
import android.os.CountDownTimer
import android.view.View
import android.widget.Button
import android.widget.TextView
import androidx.appcompat.app.AppCompatActivity

class MainActivity : AppCompatActivity() {
    private lateinit var countDownTimer: CountDownTimer
    private var timeLeftInMillis: Long = 60000
    private val countDownInterval: Long = 1000

    private lateinit var startButton : Button
    private lateinit var stopButton : Button
    private lateinit var textViewTimer : TextView

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        startButton = findViewById(R.id.startButton)
        stopButton = findViewById(R.id.stopButton)
        textViewTimer = findViewById(R.id.textViewTimer)

        startButton.setOnClickListener {
            startTimer()
            startButton.visibility = View.GONE
            stopButton.visibility = View.VISIBLE
        }

        stopButton.setOnClickListener {
            stopTimer()
            startButton.visibility = View.VISIBLE
            stopButton.visibility = View.GONE
        }

        updateCountdownUI()
    }

    private fun startTimer() {
        countDownTimer = object : CountDownTimer(timeLeftInMillis, countDownInterval) {
            override fun onTick(millisUntilFinished: Long) {
                timeLeftInMillis = millisUntilFinished
                updateCountdownUI()
            }

            override fun onFinish() {
                // Handle timer finish event here
                startButton.visibility = View.VISIBLE
                stopButton.visibility = View.GONE
                timeLeftInMillis = 60000
                updateCountdownUI()

            }
        }

        countDownTimer.start()
    }

    private fun stopTimer() {
        countDownTimer.cancel()
    }
    
    private fun updateCountdownUI() {
        val minutes = (timeLeftInMillis / 1000) / 60
        val seconds = (timeLeftInMillis / 1000) % 60

        val timeRemainingText = "$minutes:${String.format("%02d", seconds)}"
        textViewTimer.text = timeRemainingText
    }
}

```


### <ins> Project 37: Adding a splash screen with a fade-in animation </ins>
* [Splash Screen with a Fade-in Animation](https://github.com/odukabdulbasit/FadeInSplash)

```kotlin

import android.content.Intent
import androidx.appcompat.app.AppCompatActivity
import android.os.Bundle
import android.os.Handler
import android.widget.ImageView

class SplashScreenActivity : AppCompatActivity() {

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_splash_screen)

        val splashImage = findViewById<ImageView>(R.id.splashImage)
        // Create a fade-in animation
        splashImage.alpha = 0f
        splashImage.animate().alpha(1f).setDuration(FADE_IN_DURATION).start()

        // Create a handler to delay the transition to the main activity
        Handler().postDelayed({
            // Start the main activity
            val intent = Intent(this@SplashScreenActivity, MainActivity::class.java)
            startActivity(intent)
            finish()
        }, SPLASH_TIMEOUT)
    }

    companion object{
        private const val SPLASH_TIMEOUT: Long = 3000 // 3 seconds
        private const val FADE_IN_DURATION: Long = 1500 // 1.5 seconds
    }
}

```
