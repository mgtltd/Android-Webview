# Android-Webview
Control Webview Code

<h1>Create New Project</h1>

Create a new pj:
![Screenshot 2025-06-17 at 3 39 14 PM](https://github.com/user-attachments/assets/269772fd-54da-43a0-950a-5203b99413f3)


![Screenshot 2025-06-17 at 3 40 04 PM](https://github.com/user-attachments/assets/92b2cb58-c537-4092-aae7-f98e9871e351)

<h1>User permission</h1>

Then find out the AndroidManifest.xml to setup the pressmission

![Screenshot 2025-06-17 at 3 45 43 PM](https://github.com/user-attachments/assets/dd3b1b89-fd99-4524-8dd6-b768e3bc5bf4)

paste the source code:

```
<uses-permission android:name="android.permission.INTERNET"/>
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE"/>
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
<uses-permission android:name="android.permission. ACTION_MANAGE_ALL_FILES_ACCESS_PERMISSION"/>
```

<h1>MainActivity Source code</h1>

After that search MainActivity.java 
![Screenshot 2025-06-17 at 3 47 02 PM](https://github.com/user-attachments/assets/0b2b2907-05b6-4380-b302-a4a18434d9e2)

then paste the source code



**Remark: change your package name**
**MainActivity.java**

```
package example.com
import android.annotation.SuppressLint;
import android.app.Activity;
import android.content.Intent;
import android.net.Uri;
import android.os.Bundle;
import android.webkit.ValueCallback;
import android.webkit.WebChromeClient;
import android.webkit.WebSettings;
import android.webkit.WebView;
import android.webkit.WebViewClient;
import androidx.annotation.Nullable;
import androidx.appcompat.app.AppCompatActivity;

public class MainActivity extends AppCompatActivity {

    private WebView webView;
    private ValueCallback<Uri[]> filePathCallback;
    private final int FILE_CHOOSER_REQUEST_CODE = 1;

    @SuppressLint({"SetJavaScriptEnabled", "MissingInflatedId"})
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        webView = findViewById(R.id.webView);
        webView.setWebViewClient(new WebViewClient() {
            @Override
            public boolean shouldOverrideUrlLoading(WebView view, String url) {
                if (url != null && (url.startsWith("http://") || url.startsWith("https://"))) {
                    view.loadUrl(url); // Load all URLs in the WebView
                }
                if (url.contains("m.me")) {
                    view.loadUrl(url);
                    Intent intent = new Intent(Intent.ACTION_VIEW, Uri.parse(url));
                    startActivity(intent);
                }
                if (url.contains("facebook")) { //load fb page link
                    view.loadUrl(url);
                    Intent intent = new Intent(Intent.ACTION_VIEW, Uri.parse(url));
                    startActivity(intent);
                }
                if (url.contains("instagram")) { //load instagram link
                    view.loadUrl(url);
                    Intent intent = new Intent(Intent.ACTION_VIEW, Uri.parse(url));
                    startActivity(intent);
                }
                if (url.contains("whatsapp")) { //load whatsapp link
                    view.loadUrl(url);
                    Intent intent = new Intent(Intent.ACTION_VIEW, Uri.parse(url));
                    startActivity(intent);
                }
                if (url.contains("https://cdn.botpress.cloud")) { //load whatsapp link
                    view.loadUrl(url);
                    Intent intent = new Intent(Intent.ACTION_VIEW, Uri.parse(url));
                    startActivity(intent);
                }

                return true;
            }
        });
        WebSettings webSettings = webView.getSettings();
        webSettings.setJavaScriptEnabled(true);

        webView.setWebChromeClient(new WebChromeClient() {
            @Override
            public boolean onShowFileChooser(WebView webView, ValueCallback<Uri[]> filePathCallback, FileChooserParams fileChooserParams) {
                MainActivity.this.filePathCallback = filePathCallback;
                openFilePicker();
                return true;
            }
        });

        // Load your URL
        webView.loadUrl("https://kgod.shop");
    }

    private void openFilePicker() {
        Intent intent = new Intent(Intent.ACTION_GET_CONTENT);
        intent.addCategory(Intent.CATEGORY_OPENABLE);
        intent.setType("*/*");
        startActivityForResult(intent, FILE_CHOOSER_REQUEST_CODE);
    }

    @Override
    protected void onActivityResult(int requestCode, int resultCode, @Nullable Intent data) {
        super.onActivityResult(requestCode, resultCode, data);

        if (requestCode == FILE_CHOOSER_REQUEST_CODE) {
            if (resultCode == Activity.RESULT_OK && data != null) {
                if (filePathCallback != null) {
                    filePathCallback.onReceiveValue(new Uri[]{data.getData()});
                    filePathCallback = null;
                }
            }
        }
    }

    @Override
    public void onBackPressed() {
        if (webView.canGoBack()) {
            webView.goBack();
        } else {
            super.onBackPressed();
        }
    }
}
```
<h1>WebVView Layout</h1>
Then go to **layout** folder 
<img width="397" alt="Screenshot 2025-06-17 at 3 50 09 PM" src="https://github.com/user-attachments/assets/8447fc92-d529-46f3-9735-e2b14d37fb0b" />

paste your source code to **activity_main.xml**

<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">
    <WebView
        android:id="@+id/webView"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        />

</RelativeLayout>

<h1> Add Mobile application logo</h1>
Find out the mipmap folder
<img width="369" alt="Screenshot 2025-06-17 at 4 04 00 PM" src="https://github.com/user-attachments/assets/4db511cd-7d15-4a83-8385-98a3dcbccf8f" />

Then rightclick on mipmap folder 

![Screenshot 2025-06-17 at 4 07 26 PM](https://github.com/user-attachments/assets/8ffd96d7-ddee-4452-a7a9-6c4baf9ec751)

Select **Image Asset** add company logo to the path

<img width="968" alt="Screenshot 2025-06-17 at 4 12 07 PM" src="https://github.com/user-attachments/assets/652b42a0-2f0e-4232-a36e-24adc81d7a22" />

Change the bg color on Background Layer then click "NEXT"

<img width="971" alt="Screenshot 2025-06-17 at 4 12 55 PM" src="https://github.com/user-attachments/assets/e37336b9-dd34-4260-8512-8c170634f844" />


The result:

![Screenshot 2025-06-17 at 4 15 21 PM](https://github.com/user-attachments/assets/7b19d303-3e9d-414e-8a7a-c34b18214dce)

<h1>Pulish your mobile app using aab format</h1>

![Screenshot 2025-06-17 at 4 18 04 PM](https://github.com/user-attachments/assets/8f0f9b11-4cc5-450a-90d2-46d8dcf29e7c)

![Screenshot 2025-06-17 at 4 18 25 PM](https://github.com/user-attachments/assets/10a51930-af89-45be-90ec-8632b2841c53)

![Screenshot 2025-06-17 at 4 19 13 PM](https://github.com/user-attachments/assets/433aaaf9-16b3-41a1-97c0-4a2b50ec2c8b)

![Screenshot 2025-06-17 at 4 20 28 PM](https://github.com/user-attachments/assets/ab09ce7f-e3a6-4d49-a444-137a922e29cc)

![Screenshot 2025-06-17 at 4 20 52 PM](https://github.com/user-attachments/assets/f57c37c2-545f-43ad-a398-ef1013ac7b6c)

![Screenshot 2025-06-17 at 4 21 01 PM](https://github.com/user-attachments/assets/274083cc-b1a7-4e57-a31f-a9f74e5ada2f)


Then publish aab file to samsung store

View this document follow the step to publish your mobile application
https://drive.google.com/file/d/14wdE1axhFj2VGrgcDP-IdtSzR_eFB-nJ/view?usp=sharing











