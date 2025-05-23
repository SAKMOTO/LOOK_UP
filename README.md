# LOOK_UP

![Screenshot](https://i.pinimg.com/564x/29/13/32/291332270f746fdb997843ebed3181a7.jpg)
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
![Screenshot](https://media.geeksforgeeks.org/wp-content/uploads/20250324112934450081/lens-app-design-ui.png)

## Step 5: Creating a model class for storing our data
Navigate to the app > java > {package-name}, Right-click on it, New > Java/Kotlin class and name your class as DataModel and add the below code to it. Comments are added inside the code to understand the code in more detail.
## DataModel File:
```
package org.geeksforgeeks.demo;

public class DataModel {
    private String title;
    private String link;
    private String displayedLink;
    private String snippet;

    // Constructor
    public DataModel(String title, String link, String displayedLink, String snippet) {
        this.title = title;
        this.link = link;
        this.displayedLink = displayedLink;
        this.snippet = snippet;
    }

    // Getters and Setters
    public String getTitle() {
        return title;
    }

    public void setTitle(String title) {
        this.title = title;
    }

    public String getLink() {
        return link;
    }

    public void setLink(String link) {
        this.link = link;
    }

    public String getDisplayedLink() {
        return displayedLink;
    }

    public void setDisplayedLink(String displayedLink) {
        this.displayedLink = displayedLink;
    }

    public String getSnippet() {
        return snippet;
    }

    public void setSnippet(String snippet) {
        this.snippet = snippet;
    }
}
```
## Step 6: Creating a layout file for displaying our RecyclerView items
Navigate to the app > res > layout, Right-click on it, New > Layout Resource File and name it as search_result_rv_item and add the below code to it.
## search_result_rv_item:

```
<?xml version="1.0" encoding="utf-8"?>
<androidx.cardview.widget.CardView
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:background="@color/white"
    android:layout_marginTop="8dp"
    app:cardCornerRadius="8dp">

    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_margin="16dp"
        android:orientation="vertical">

        <!--text view for our title-->
        <TextView
            android:id="@+id/idTVTitle"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:padding="4dp"
            android:text="Title"
            android:textStyle="bold"
            android:textColor="@color/black"
            android:textSize="18sp" />

        <!--text view for our snippet-->
        <TextView
            android:id="@+id/idTVSnippet"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:padding="4dp"
            android:text="Snippet"
            android:textStyle="italic"
            android:textColor="@android:color/darker_gray" />

        <!--text view for our description-->
        <TextView
            android:id="@+id/idTVDescription"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:padding="3dp"
            android:text="Description"
            android:textColor="@android:color/darker_gray" />

    </LinearLayout>

</androidx.cardview.widget.CardView>

```
## Step 7: Creating an adapter class for our RecyclerView
Navigate to the app > java > your app's package name > Right-click on it > New > Java class and name it as Adapter and add the below code to it.

Adapter File:
```
package org.geeksforgeeks.demo;

import android.content.Context;
import android.content.Intent;
import android.net.Uri;
import android.view.LayoutInflater;
import android.view.View;
import android.view.ViewGroup;
import android.widget.TextView;
import androidx.annotation.NonNull;
import androidx.recyclerview.widget.RecyclerView;
import java.util.ArrayList;

public class Adapter extends RecyclerView.Adapter<Adapter.ViewHolder> {

    private final ArrayList<DataModel> list;
    private final Context context;

    public Adapter(ArrayList<DataModel> list, Context context) {
        this.list = list;
        this.context = context;
    }

    @NonNull
    @Override
    public ViewHolder onCreateViewHolder(@NonNull ViewGroup parent, int viewType) {
        View view = LayoutInflater.from(parent.getContext())
                .inflate(R.layout.search_result_rv_item, parent, false);
        return new ViewHolder(view);
    }

    @Override
    public void onBindViewHolder(@NonNull ViewHolder holder, int position) {
        DataModel modal = list.get(position);
        holder.titleTV.setText(modal.getTitle());
        holder.snippetTV.setText(modal.getDisplayedLink());
        holder.descTV.setText(modal.getSnippet());

        // Open link in browser when item is clicked
        holder.itemView.setOnClickListener(v -> {
            Intent intent = new Intent(Intent.ACTION_VIEW, Uri.parse(modal.getLink()));
            context.startActivity(intent);
        });
    }

    @Override
    public int getItemCount() {
        return list.size();
    }

    // ViewHolder to hold item views
    public static class ViewHolder extends RecyclerView.ViewHolder {
        TextView titleTV, descTV, snippetTV;

        public ViewHolder(@NonNull View itemView) {
            super(itemView);
            titleTV = itemView.findViewById(R.id.idTVTitle);
            descTV = itemView.findViewById(R.id.idTVDescription);
            snippetTV = itemView.findViewById(R.id.idTVSnippet);
        }
    }
}
```
## Step 8: Generating your API key
Go to the site https://serpapi.com/search-api and create your account with your Google account. This is a similar process as you signup on GeeksforGeeks. While generating your API key make sure to select the free trial option and proceed further. After going to the site shown above you will get to see the below screen. Simply sign in with your credentials and proceed further.

![Screenshot](https://media.geeksforgeeks.org/wp-content/uploads/20210227102715/Webpnetresizeimage.png)

After proceeding further you have to simply Navigate to the My Account > Dashboard option to open the below screen. On this screen, you will get to see your API key.

![Screenshot](https://media.geeksforgeeks.org/wp-content/uploads/20240730222236/apiss.png)


## Step 9: Working with the MainActivity file
Go to the MainActivity file and refer to the following code. Below is the code for the MainActivity file. Comments are added inside the code to understand the code in more detail.

```
package org.geeksforgeeks.demo;

import android.annotation.SuppressLint;
import android.content.Intent;
import android.graphics.Bitmap;
import android.os.Bundle;
import android.provider.MediaStore;
import android.widget.Toast;
import androidx.activity.result.ActivityResult;
import androidx.activity.result.ActivityResultLauncher;
import androidx.activity.result.contract.ActivityResultContracts;
import androidx.annotation.Nullable;
import androidx.appcompat.app.AppCompatActivity;
import androidx.recyclerview.widget.LinearLayoutManager;
import com.android.volley.Request;
import com.android.volley.toolbox.JsonObjectRequest;
import com.android.volley.toolbox.Volley;
import com.bumptech.glide.Glide;
import com.google.mlkit.vision.common.InputImage;
import com.google.mlkit.vision.label.ImageLabel;
import com.google.mlkit.vision.label.ImageLabeling;
import com.google.mlkit.vision.label.defaults.ImageLabelerOptions;
import org.geeksforgeeks.demo.databinding.ActivityMainBinding;
import org.json.JSONArray;
import org.json.JSONException;
import org.json.JSONObject;
import java.util.ArrayList;

public class MainActivity extends AppCompatActivity {
    private Bitmap imageBitmap;
    private Adapter adapter;
    private ArrayList<DataModel> dataModalArrayList = new ArrayList<>();
    private String title, link, displayedLink, snippet;
    private ActivityResultLauncher<Intent> takeImageLauncher;

    private ActivityMainBinding binding;

    @Override
    protected void onCreate(@Nullable Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        binding = ActivityMainBinding.inflate(getLayoutInflater());
        setContentView(binding.getRoot());

        // Set up RecyclerView
        binding.recyclerView.setLayoutManager(new LinearLayoutManager(this, LinearLayoutManager.VERTICAL, false));
        adapter = new Adapter(dataModalArrayList, this);

        // Button to capture an image
        binding.snap.setOnClickListener(v -> dispatchTakePictureIntent());

        // Button to process image and fetch search results
        binding.getSearchResults.setOnClickListener(v -> processImage());

        // Register image capture activity result launcher
        takeImageLauncher = registerForActivityResult(
                new ActivityResultContracts.StartActivityForResult(),
                this::handleImageCaptureResult
        );
    }

    // Handle image capture result
    private void handleImageCaptureResult(ActivityResult result) {
        if (result.getResultCode() == RESULT_OK) {
            Intent data = result.getData();
            if (data != null && data.getExtras() != null) {
                imageBitmap = (Bitmap) data.getExtras().get("data");
                Glide.with(this).load(imageBitmap).into(binding.image); // Display captured image
            }
        }
    }

    // Process captured image and fetch search results
    private void processImage() {
        dataModalArrayList.clear();

        if (imageBitmap == null) {
            Toast.makeText(this, "No image found. Please capture an image first.", Toast.LENGTH_SHORT).show();
            return;
        }

        InputImage image = InputImage.fromBitmap(imageBitmap, 0);
        ImageLabeling labeler = ImageLabeling.getClient(ImageLabelerOptions.DEFAULT_OPTIONS);

        // Perform image labeling
        labeler.process(image)
                .addOnSuccessListener(labels -> {
                    if (!labels.isEmpty()) {
                        String searchQuery = labels.get(0).getText();
                        Toast.makeText(MainActivity.this, searchQuery, Toast.LENGTH_SHORT).show();
                        searchData(searchQuery);
                    } else {
                        Toast.makeText(MainActivity.this, "No labels detected in the image.", Toast.LENGTH_SHORT).show();
                    }
                })
                .addOnFailureListener(e -> Toast.makeText(MainActivity.this, "Failed to detect image.", Toast.LENGTH_SHORT).show());
    }

    // Perform search query using API
    @SuppressLint("NotifyDataSetChanged")
    private void searchData(String searchQuery) {
        String apiKey = "YOUR_API_KEY";
        String url = "https://serpapi.com/search.json?q=" + searchQuery.trim() +
                "&location=Delhi,India&hl=en&gl=us&google_domain=google.com&api_key=" + apiKey;

        JsonObjectRequest jsonObjectRequest = new JsonObjectRequest(
                Request.Method.GET, url, null,
                response -> {
                    try {
                        JSONArray organicResultsArray = response.getJSONArray("organic_results");
                        for (int i = 0; i < organicResultsArray.length(); i++) {
                            JSONObject organicObj = organicResultsArray.getJSONObject(i);
                            title = organicObj.optString("title", "");
                            link = organicObj.optString("link", "");
                            displayedLink = organicObj.optString("displayed_link", "");
                            snippet = organicObj.optString("snippet", "");

                            dataModalArrayList.add(new DataModel(title, link, displayedLink, snippet));
                        }

                        adapter.notifyDataSetChanged();
                        binding.recyclerView.setAdapter(adapter);
                    } catch (JSONException e) {
                        e.printStackTrace();
                    }
                },
                error -> {
                    error.printStackTrace();
                    Toast.makeText(MainActivity.this, "No result found for the search query.", Toast.LENGTH_SHORT).show();
                });

        Volley.newRequestQueue(this).add(jsonObjectRequest);
    }

    // Launch camera to capture image
    @SuppressLint("QueryPermissionsNeeded")
    private void dispatchTakePictureIntent() {
        Intent takePictureIntent = new Intent(MediaStore.ACTION_IMAGE_CAPTURE);
        if (takePictureIntent.resolveActivity(getPackageManager()) != null) {
            takeImageLauncher.launch(takePictureIntent);
        }
    }
}
```
Now run your app and see the output of the app. Make sure to change your API key before running the app. 
Note: The search results might not be accurate upto an extent.


▶️ [Watch the demo video](https://raw.githubusercontent.com/SAKMOTO/LOOK_UP/main/demo.mp4)




