# LOOK_UP
Look Up is an Android application that brings the power of visual search to your fingertips. Inspired by the functionality of Google Lens, this app allows users to capture or select an image, scan it using integrated vision tools, and instantly search the web (Google) for relevant information about the object, text, product, or place in the image.
🔍 Look Up – Visual Search Simplified
Snap it. Scan it. Search it.
Unlock the power of visual discovery with Look Up, your smart companion for identifying, exploring, and learning more about the world around you—through your camera lens.

📱 What is Look Up?
Look Up is a powerful Android app that allows users to capture or select an image, and instantly search the web for relevant information using the Google Search API. Whether it’s a product you saw, a place you're curious about, or text you want to understand—Look Up brings visual search to your fingertips.

With a clean UI and intuitive experience, Look Up helps you:

🛍️ Identify products and shop smarter

🗺️ Explore landmarks and places

📖 Translate or recognize text

🎯 Search anything by just taking a picture

🛡️ Not Affiliated with Google – Powered by It
⚠️ Disclaimer:
Look Up is an independently developed application and is not affiliated with, endorsed by, or cloned from Google or Google Lens. It leverages publicly available Google APIs (such as Google Custom Search) to deliver accurate search results in a unique way.

This app was built from scratch to enhance accessibility and creativity using existing public tools.

🌟 Why Use Look Up?
- 📸 Snap a photo and detect objects in real-time.
- 🧠 Image labeling using **Google ML Kit**.
- 🌐 Fetches search results using **SERP API**.
- 🖼️ Beautiful UI with **RecyclerView** to show results.
- 💡 Fast, lightweight, and responsive.
  
🚀 Lightweight and fast

✅ Simple user interface

🔎 Seamless camera integration for instant image search

🔗 Powered by Google APIs for reliable results

🔒 No data stored – your privacy is respected

## ⚙️ Tech Stack

- **Language**: Java
- **ML Framework**: Google ML Kit – Image Labeling
- **Search API**: SerpAPI (https://serpapi.com/)
- **Networking**: Volley
- **Image Loading**: Glide
- **UI**: XML Layouts + View Binding
  
![Logo](C:\Users\moham\Downloads)


## Steps to Implement Look Up in Android

📸 How It Works

## Step 1: Create a New Project
To create a new project in Android Studio please refer to How to Create/Start a New Project in Android Studio.


<br>

![Screenshot](https://media.geeksforgeeks.org/wp-content/uploads/20250324112058953365/lens-app-dir.png)


## Step 2: Adding dependency for language translation and View Binding

Navigate to the app > Gradle Scripts > build.gradle.kts file and add the following dependencies. We have added the dependencies for Firebase ML kit for image labelling, Volley for API Calls and Glide for image loading.


```
dependencies {
    ...
    implementation ("com.google.mlkit:image-labeling:17.0.9")
    implementation ("com.android.volley:volley:1.2.1")
    implementation ("com.github.bumptech.glide:glide:4.16.0")
}

```
Add View Binding support by adding the following code anywhere under the android{} scope
```
buildFeatures {
    viewBinding = true
}
```
## Step 3: Adding permissions to access the Internet in your Android Apps AndroidManifest file

Navigate to the app > AndroidManifest.xml file and add the below code to it.
```
<uses-feature
    android:name="android.hardware.camera"
    android:required="true" />
<uses-permission android:name="android.permission.INTERNET" />
```
## Step 4: Working with activity_main.xml file

Navigate to the app > res > layout > activity_main.xml and add the below code to that file. Below is the code for the activity_main.xml file. 

activity_main.xml:
```
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:background="@color/white"
    tools:context=".MainActivity">

    <ImageView
        android:id="@+id/image"
        android:layout_width="match_parent"
        android:layout_height="300dp"
        android:layout_margin="16dp"
        android:scaleType="centerCrop" />

    <LinearLayout
        android:id="@+id/layoutButtons"
        style="?android:attr/buttonBarStyle"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="horizontal">

        <Button
            android:id="@+id/snap"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_gravity="center"
            android:layout_margin="16dp"
            android:layout_weight="1"
            android:text="Snap"
            android:padding="16dp"
            android:lines="2"
            android:textSize="18sp"
            android:textStyle="bold" />

        <Button
            android:id="@+id/getSearchResults"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_gravity="center"
            android:layout_margin="16dp"
            android:layout_weight="1"
            android:padding="16dp"
            android:lines="2"
            android:text="Get Search Results"
            android:textSize="18sp"
            android:textStyle="bold" />

    </LinearLayout>

    <androidx.recyclerview.widget.RecyclerView
        android:id="@+id/recyclerView"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        tools:listitem="@layout/search_result_rv_item"
        android:layout_margin="16dp"/>

</LinearLayout>
```
## Design UI:
![Screenshot]([https://media.geeksforgeeks.org/wp-content/uploads/20250324112058953365/lens-app-dir.png](https://media.geeksforgeeks.org/wp-content/uploads/20250324112934450081/lens-app-design-ui.png))
