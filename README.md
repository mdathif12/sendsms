
# Ex.No:3 Design an android application Send SMS using Intent.

## AIM:

To create and design an android application Send SMS using Intent using Android Studio.

## EQUIPMENTS REQUIRED:

Android Studio(Latest Version)

## ALGORITHM:

Step 1: Open Android Stdio and then click on File -> New -> New project.

Step 2: Then type the Application name as smsintent and click Next. 

Step 3: Then select the Minimum SDK as shown below and click Next.

Step 4: Then select the Empty Activity and click Next. Finally click Finish.

Step 5: Design layout in activity_main.xml.

Step 6: Send SMS and Display details give in MainActivity file.

Step 7: Save and run the application.

## PROGRAM:
```
/*
Program to create and design an android application Send SMS using Intent.
Developed by: Mohamed Athif Rahuman J
Registeration Number : 212223220058
*/
```
## MAINACTIVITY.JAVA
```
package com.example.smsintentapp;

import android.content.Intent;
import android.net.Uri;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.EditText;
import android.widget.TextView;
import android.widget.Toast;

import androidx.appcompat.app.AppCompatActivity;

public class MainActivity extends AppCompatActivity {

    private EditText phoneNumberEditText;
    private EditText messageEditText;
    private Button sendButton;
    private TextView statusTextView;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        phoneNumberEditText = findViewById(R.id.phoneNumber);
        messageEditText = findViewById(R.id.message);
        sendButton = findViewById(R.id.sendButton);
        statusTextView = findViewById(R.id.status);

        sendButton.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                sendSMS();
            }
        });
    }

    private void sendSMS() {
        String phoneNumber = phoneNumberEditText.getText().toString().trim();
        String message = messageEditText.getText().toString().trim();

        if (phoneNumber.isEmpty()) {
            Toast.makeText(this, "Please enter a phone number", Toast.LENGTH_SHORT).show();
            return;
        }

        if (message.isEmpty()) {
            Toast.makeText(this, "Please enter a message", Toast.LENGTH_SHORT).show();
            return;
        }

        try {
            Intent intent = new Intent(Intent.ACTION_SENDTO);
            intent.setData(Uri.parse("smsto:" + Uri.encode(phoneNumber))); // encode phone number
            intent.putExtra("sms_body", message);

            if (intent.resolveActivity(getPackageManager()) != null) {
                startActivity(intent);
                statusTextView.setText("Status: SMS intent launched successfully");
                Toast.makeText(this, "Opening SMS app...", Toast.LENGTH_SHORT).show();
            } else {
                statusTextView.setText("Status: No SMS app available");
                Toast.makeText(this, "No SMS app installed", Toast.LENGTH_SHORT).show();
            }
        } catch (Exception e) {
            statusTextView.setText("Status: Error - " + e.getMessage());
            Toast.makeText(this, "Error sending SMS: " + e.getMessage(), Toast.LENGTH_SHORT).show();
        }
    }
}
```
## activity_main.xml
```
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android">
    <!-- Permission to send SMS -->
    <uses-feature
        android:name="android.hardware.telephony"
        android:required="false" />
    <uses-permission android:name="android.permission.SEND_SMS" />

    <application
        android:allowBackup="true"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:theme="@style/Theme.AppCompat.Light.DarkActionBar">
        <activity
            android:name=".MainActivity"
            android:exported="true">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />
                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
    </application>
</manifest>
```
## OUTPUT

<img width="1920" height="1080" alt="int" src="https://github.com/user-attachments/assets/e1d534e4-24c6-4d3f-8b1f-61922fac875c" />

<img width="1920" height="1080" alt="intent" src="https://github.com/user-attachments/assets/ea126b75-2105-4eca-8f13-f7703f520881" />

## RESULT
Thus a Simple Android Application create and design an android application Send SMS using Intent using Android Studio is developed and executed successfully.
