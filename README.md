
# Ex.No:4 Create Your Own Content Providers to get Contacts details.


## AIM:

To create your own content providers to get contacts details using Android Studio.

## EQUIPMENTS REQUIRED:

Android Studio(Min. required Artic Fox)

## ALGORITHM:

Step 1: Open Android Stdio and then click on File -> New -> New project.

Step 2: Then type the Application name as “ex.no.3″ and click Next. 

Step 3: Then select the Minimum SDK as shown below and click Next.

Step 4: Then select the Empty Activity and click Next. Finally click Finish.

Step 5: Design layout in activity_main.xml.

Step 6: Get contacts details and Display details give in MainActivity file.

Step 7: Save and run the application.

## PROGRAM:
```
/*
Program to print the text create your own content providers to get contacts details.
Developed by:Vikaskumar M
Registeration Number : 212224220122
*/
```
## MainActivity.java
```java
package com.example.exp_04;

import android.Manifest;
import android.content.pm.PackageManager;
import android.database.Cursor;
import android.os.Bundle;
import android.provider.ContactsContract;
import android.widget.ArrayAdapter;
import android.widget.Button;
import android.widget.ListView;
import android.widget.Toast;
import android.content.ContentResolver;
import androidx.appcompat.app.AppCompatActivity;
import androidx.core.app.ActivityCompat;
import androidx.core.content.ContextCompat;
import java.util.ArrayList;

public class MainActivity extends AppCompatActivity {

    Button btnLoad;
    ListView listView;
    ArrayList<String> contacts;
    ArrayAdapter<String> adapter;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        btnLoad = findViewById(R.id.btnLoad);
        listView = findViewById(R.id.listView);

        contacts = new ArrayList<>();

        adapter = new ArrayAdapter<>(
                this,
                android.R.layout.simple_list_item_1,
                contacts
        );

        listView.setAdapter(adapter);

        btnLoad.setOnClickListener(v -> {
            if (ContextCompat.checkSelfPermission(
                    this,
                    Manifest.permission.READ_CONTACTS)
                    != PackageManager.PERMISSION_GRANTED) {

                ActivityCompat.requestPermissions(
                        this,
                        new String[]{Manifest.permission.READ_CONTACTS},
                        100
                );

            } else {
                loadContacts();
            }
        });
    }

    private void loadContacts() {

        contacts.clear();

        ContentResolver resolver = getContentResolver();

        Cursor cursor = resolver.query(
                ContactsContract.CommonDataKinds.Phone.CONTENT_URI,
                null,
                null,
                null,
                ContactsContract.CommonDataKinds.Phone.DISPLAY_NAME
        );

        if (cursor != null) {

            int nameIndex = cursor.getColumnIndex(
                    ContactsContract.CommonDataKinds.Phone.DISPLAY_NAME);

            int numberIndex = cursor.getColumnIndex(
                    ContactsContract.CommonDataKinds.Phone.NUMBER);

            while (cursor.moveToNext()) {

                String name = cursor.getString(nameIndex);
                String number = cursor.getString(numberIndex);

                contacts.add(name + "\n" + number);
            }

            cursor.close();
        }

        adapter.notifyDataSetChanged();

        Toast.makeText(this,
                "Contacts Loaded: " + contacts.size(),
                Toast.LENGTH_SHORT).show();
    }

    @Override
    public void onRequestPermissionsResult(
            int requestCode,
            String[] permissions,
            int[] grantResults) {

        super.onRequestPermissionsResult(
                requestCode, permissions, grantResults);

        if (requestCode == 100 &&
                grantResults.length > 0 &&
                grantResults[0] == PackageManager.PERMISSION_GRANTED) {

            loadContacts();

        } else {
            Toast.makeText(this,
                    "Permission Denied",
                    Toast.LENGTH_SHORT).show();
        }
    }
}

```
## activity_main.xml
```java
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:padding="20dp"
    android:background="#F2F3FA">

    <TextView
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="My Contacts"
        android:textSize="28sp"
        android:textStyle="bold"
        android:textColor="#FFFFFF"
        android:gravity="center"
        android:padding="25dp"
        android:background="#5146E5"/>

    <Button
        android:id="@+id/btnLoad"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Load Contacts"
        android:textAllCaps="false"
        android:textSize="16sp"
        android:layout_marginTop="20dp"
        android:backgroundTint="#5146E5"/>

    <ListView
        android:id="@+id/listView"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:layout_marginTop="15dp"
        android:divider="#D5D5E0"
        android:dividerHeight="1dp"/>

</LinearLayout>

```
## AndroidManifest.xml
```java
<uses-permission android:name="android.permission.READ_CONTACTS"/>
```

## OUTPUT

<img width="1316" height="727" alt="Screenshot 2026-11-25 230955" src="https://github.com/user-attachments/assets/e63d58d5-1683-4b0d-a256-53fe2ae8323f" />

<img width="1325" height="734" alt="Screenshot 2026-11-25 231802" src="https://github.com/user-attachments/assets/47df13ae-8c50-4a79-ae51-d84566a7faa1" />

<img width="294" height="587" alt="Screenshot 2026-11-25 231005" src="https://github.com/user-attachments/assets/4553d87c-7ede-444a-a5d9-df530472838c" />
<img width="298" height="591" alt="Screenshot 2026-11-25 231810" src="https://github.com/user-attachments/assets/ca74a8ab-3be6-4ba2-a7db-881583e60369" />

## RESULT
Thus a Simple Android Application create your own content providers to get contacts details using Android Studio is developed and executed successfully.
