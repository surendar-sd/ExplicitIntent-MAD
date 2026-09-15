# Ex.No:4 To create a two screens , first screen will take one number input from user. After click on Factorial button, second screen will open and it should display factorial of the same number using Explicit Intents.


## AIM:

To create a two screens , first screen will take one number input from user. After click on Factorial button, second screen will open and it should display factorial of the same number using Explicit Intents.


## EQUIPMENTS REQUIRED:

Latest Version Android Studio

## ALGORITHM:

Step 1: Open Android Studio and select File → New → New Project.

Step 2: Enter the application name as ExplicitIntent and click Next.

Step 3: Select the required Minimum SDK and click Next.

Step 4: Select Empty Activity and click Finish.

Step 5: Design the first screen in activity_main.xml with a TextView, EditText, and Button.

Step 6: Create a second Activity, MainActivity2, along with its layout file activity_main2.xml.

Step 7: Design the second screen in activity_main2.xml.

Step 8: Register MainActivity2 in the AndroidManifest.xml file.

Step 9: In MainActivity.java, create an explicit Intent to navigate from MainActivity to MainActivity2.

Step 10: In MainActivity2.java, create an explicit Intent to navigate back to MainActivity.

Step 11: Set the onClick methods for the buttons in the respective XML layouts.

Step 12: Save and run the application.

## PROGRAM:
```
/*
Program to print the text “ExplicitIntent”.
Developed by:S.R.AMIRITHA
Registeration Number :212224220009
*/
```

## MainActivity.java
```
package com.example.explicitintent;

import android.content.Intent;
import android.os.Bundle;
import android.view.View;

import androidx.activity.EdgeToEdge;
import androidx.appcompat.app.AppCompatActivity;
import androidx.core.graphics.Insets;
import androidx.core.view.ViewCompat;
import androidx.core.view.WindowInsetsCompat;

import android.widget.EditText;
import android.widget.Toast;
import java.math.BigInteger;

public class MainActivity extends AppCompatActivity {

    EditText numberInput;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        numberInput = findViewById(R.id.numberInput);
    }

    public void newsScreen(View view) {
        String input = numberInput.getText().toString();
        if (input.isEmpty()) {
            Toast.makeText(this, "Please enter a number", Toast.LENGTH_SHORT).show();
            return;
        }

        try {
            int n = Integer.parseInt(input);
            if (n < 0) {
                Toast.makeText(this, "Please enter a non-negative number", Toast.LENGTH_SHORT).show();
                return;
            }
            BigInteger factorial = calculateFactorial(n);

            Intent i = new Intent(MainActivity.this, MainActivity1.class);
            i.putExtra("RESULT", factorial.toString());
            startActivity(i);
        } catch (NumberFormatException e) {
            Toast.makeText(this, "Invalid number", Toast.LENGTH_SHORT).show();
        }
    }

    private BigInteger calculateFactorial(int n) {
        BigInteger result = BigInteger.ONE;
        for (int i = 2; i <= n; i++) {
            result = result.multiply(BigInteger.valueOf(i));
        }
        return result;
    }
}
```
## MainActivity1.java
```
package com.example.Explicit_intent;

import androidx.appcompat.app.AppCompatActivity;
import android.content.Intent;
import android.os.Bundle;
import android.view.View;

import com.example.explicitintent.MainActivity;
import com.example.explicitintent.R;

import android.widget.TextView;

public class MainActivity1 extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main1);

        TextView resultTextView = findViewById(R.id.resultTextView);
        String result = getIntent().getStringExtra("RESULT");

        if (result != null) {
            resultTextView.setText(result);
        }
    }

    public void homeScreen(View view) {
        Intent i = new Intent(MainActivity1.this, MainActivity.class);
        startActivity(i);
    }
}
```
## activity_main.xml
```
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/main"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">

    <TextView
        android:id="@+id/textView"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Factorial Calculator"
        android:textSize="24sp"
        android:textStyle="bold"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.498"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.15" />

    <EditText
        android:id="@+id/numberInput"
        android:layout_width="200dp"
        android:layout_height="wrap_content"
        android:ems="10"
        android:hint="Enter a number"
        android:inputType="number"
        android:textAlignment="center"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@+id/textView"
        app:layout_constraintVertical_bias="0.15" />

    <Button
        android:id="@+id/button"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Calculate Factorial"
        android:onClick="newsScreen"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.497"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@+id/numberInput"
        app:layout_constraintVertical_bias="0.2" />
</androidx.constraintlayout.widget.ConstraintLayout>
```
## activity_main1.xml
```
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    <TextView
        android:id="@+id/textView2"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="The result is:"
        android:textSize="22sp"
        android:textStyle="bold"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.464"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.2" />

    <TextView
        android:id="@+id/resultTextView"
        android:layout_width="0dp"
        android:layout_height="wrap_content"
        android:layout_marginStart="32dp"
        android:layout_marginEnd="32dp"
        android:text="0"
        android:textAlignment="center"
        android:textSize="18sp"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@+id/textView2"
        android:layout_marginTop="16dp" />

    <Button
        android:id="@+id/button2"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Calculate Another"
        android:onClick="homeScreen"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.468"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@+id/resultTextView"
        app:layout_constraintVertical_bias="0.3" />
</androidx.constraintlayout.widget.ConstraintLayout>
```


## OUTPUT

<img width="1740" height="1077" alt="Screenshot 2026-08-21 093503" src="https://github.com/user-attachments/assets/6ff2ae78-55b1-4e9d-9773-368008443726" />

<img width="943" height="560" alt="Screenshot 2026-08-21 094533" src="https://github.com/user-attachments/assets/40145057-94e4-46d2-a853-dd90b6416e4e" />


## RESULT
Thus a Simple Android Application create a Explicit Intents using Android Studio is developed and executed successfully.


