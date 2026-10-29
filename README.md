
# Ex No: 1 A : To create a employee details fields and to display the employee details using Firebase Database in Android Studio.

## NAME : SHREYESHKAR SEKAR
## REGISTER NUMBER : 212224220099


## AIM:

To create and display the employee details using Firebase Database in Android Studio.

## EQUIPMENTS REQUIRED:

Android Studio(Min.required Artic Fox)

## ALGORITHM:

Step 1: Open Android Stdio and then click on File -> New -> New project.

Step 2: Then type the Application name as HelloWorld and click Next. 

Step 3: Then select the Minimum SDK as shown below and click Next.

Step 4: Then select the Empty Activity and click Next. Finally click Finish.

Step 5: Design layout in activity_main.xml.

Step 6: Display the employee details in MainActivity file.

Step 7: Save and run the application.

## PROGRAM:
```
/*
Program to print the DatabaseTable using the firebasedatabase”.
Developed by:
Registeration Number : 212224220099

Emp.java : 


package com.example.ex_01_realtimedatabase;

public class Emp {

    String id, name, age, salary;

    public Emp() {
        // Required for Firebase
    }

    public Emp(String id, String name, String age, String salary) {
        this.id = id;
        this.name = name;
        this.age = age;
        this.salary = salary;
    }
}


MainActivity.java : 


package com.example.ex_01_realtimedatabase;

import android.os.Bundle;
import android.widget.*;

import androidx.appcompat.app.AppCompatActivity;

import com.google.firebase.database.*;

import java.util.*;

public class MainActivity extends AppCompatActivity {

    EditText etName, etAge, etSalary;
    Button btnAdd, btnUpdate, btnDelete;
    ListView listView;

    DatabaseReference dbRef;

    ArrayList<String> items = new ArrayList<>();
    ArrayList<String> keys = new ArrayList<>();
    ArrayAdapter<String> adapter;

    String selectedKey = null;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        etName = findViewById(R.id.etName);
        etAge = findViewById(R.id.etAge);
        etSalary = findViewById(R.id.etSalary);

        btnAdd = findViewById(R.id.btnAdd);
        btnUpdate = findViewById(R.id.btnUpdate);
        btnDelete = findViewById(R.id.btnDelete);

        listView = findViewById(R.id.listView);

        dbRef = FirebaseDatabase.getInstance()
                .getReference("Employees");

        adapter = new ArrayAdapter<>(
                this,
                android.R.layout.simple_list_item_1,
                items
        );

        listView.setAdapter(adapter);

        dbRef.addValueEventListener(new ValueEventListener() {

            @Override
            public void onDataChange(DataSnapshot snapshot) {

                items.clear();
                keys.clear();

                for (DataSnapshot d : snapshot.getChildren()) {

                    Emp e = d.getValue(Emp.class);

                    if (e != null) {
                        items.add(
                                e.name + " | " + e.age + " | "
                                        + e.salary
                        );

                        keys.add(d.getKey());
                    }
                }

                adapter.notifyDataSetChanged();
            }

            @Override
            public void onCancelled(DatabaseError error) {
            }
        });

        // Add employee
        btnAdd.setOnClickListener(v -> {

            Emp e = new Emp(
                    etName.getText().toString(),
                    etAge.getText().toString(),
                    etSalary.getText().toString()
            );

            dbRef.push().setValue(e);
            clearFields();
        });

        // Update employee
        btnUpdate.setOnClickListener(v -> {

            if (selectedKey != null) {

                Emp e = new Emp(
                        etName.getText().toString(),
                        etAge.getText().toString(),
                        etSalary.getText().toString()
                );

                dbRef.child(selectedKey).setValue(e);
                clearFields();

            } else {
                Toast.makeText(
                        this,
                        "Select an item first",
                        Toast.LENGTH_SHORT
                ).show();
            }
        });

        // Delete employee
        btnDelete.setOnClickListener(v -> {

            if (selectedKey != null) {

                dbRef.child(selectedKey).removeValue();
                clearFields();

            } else {
                Toast.makeText(
                        this,
                        "Select an item first",
                        Toast.LENGTH_SHORT
                ).show();
            }
        });

        // Select employee from the list
        listView.setOnItemClickListener((p, v, pos, id) -> {

            selectedKey = keys.get(pos);

            dbRef.child(selectedKey).get()
                    .addOnSuccessListener(d -> {

                        Emp e = d.getValue(Emp.class);

                        if (e != null) {
                            etName.setText(e.name);
                            etAge.setText(e.age);
                            etSalary.setText(e.salary);
                        }
                    });
        });
    }

    // Clear input fields
    private void clearFields() {

        etName.setText("");
        etAge.setText("");
        etSalary.setText("");

        selectedKey = null;
    }
}


activity_main.xml :


<?xml version="1.0" encoding="utf-8"?>

<LinearLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:padding="16dp">

    <EditText
        android:id="@+id/etName"
        android:layout_width="match_parent"
        android:layout_height="55dp"
        android:hint="Name" />

    <EditText
        android:id="@+id/etAge"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:hint="Age"
        android:inputType="number" />

    <EditText
        android:id="@+id/etSalary"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:hint="Salary"
        android:inputType="number" />

    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="horizontal">

        <Button
            android:id="@+id/btnAdd"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:text="Add" />

        <Button
            android:id="@+id/btnUpdate"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:text="Update" />

        <Button
            android:id="@+id/btnDelete"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:text="Delete" />

    </LinearLayout>

    <ListView
        android:id="@+id/listView"
        android:layout_width="match_parent"
        android:layout_height="match_parent" />

</LinearLayout>


*/
```

## OUTPUT

<img width="1600" height="958" alt="WhatsApp Image 2026-10-22 at 9 51 04 AM" src="https://github.com/user-attachments/assets/fc09285c-7d54-4e22-b9aa-e0c8f23865f7" />

<img width="1600" height="999" alt="WhatsApp Image 2026-10-22 at 9 51 05 AM" src="https://github.com/user-attachments/assets/00a2f649-4402-47c5-9545-0f1c859906df" />

<img width="1600" height="955" alt="WhatsApp Image 2026-10-22 at 9 51 06 AM" src="https://github.com/user-attachments/assets/947bd5f6-fb1f-4635-a557-633d178dec76" />

<img width="1917" height="1140" alt="image" src="https://github.com/user-attachments/assets/292ae44c-41d8-42bc-a1f0-ecb3b7ba1442" />



## RESULT
Thus a Simple Android Application create a firebase database and to display the employee details using Firbase Real Time Database in Android Studio is developed and executed successfully.
