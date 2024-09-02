# Android-Webview
Control Webview Code

**1. Webview Website**

GO TO > KINGSTONSTARCONSULTANTSLIMITED/app/src/main/java/com/totech > Main.java

Copy and paste code from the Main.java to Android Studio

Chnage your 

// Load your URL
        webView.loadUrl("https://example.xyz");

Then you can view the website.


**2. Add Social Media link to your application**
//Add if(url.contains("facebook.com"))
webView.setWebViewClient(new WebViewClient() {
            @Override
            public boolean shouldOverrideUrlLoading(WebView view, String url) {
                if (url != null && (url.startsWith("http://") || url.startsWith("https://"))) {
                    view.loadUrl(url); // Load all URLs in the WebView
                }
                else if (url.contains("m.me")) {
                    view.loadUrl(url);
                    Intent intent = new Intent(Intent.ACTION_VIEW, Uri.parse(url));
                    startActivity(intent);
                }

                return true;
            }
        });
