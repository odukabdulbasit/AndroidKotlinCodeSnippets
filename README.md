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
buttonShowToast.setOnClickListener {
  showToast("Hello, Toast!")
}


private fun showToast(message: String) {
  Toast.makeText(this, message, Toast.LENGTH_SHORT).show()
}
```





