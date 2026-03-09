# Ex.No:5 Develop a simple application for proximity sensor using Sensor Manager in android studio.


## AIM:

To develop a sensor application for proximity sensor using sensor manager in Android Studio.

## EQUIPMENTS REQUIRED:

Android Studio(Min.required Giraffe)

## ALGORITHM:

Step 1: Open Android Stdio and then click on File -> New -> New project.

Step 2: Then type the Application name as proximitysensor and click Next. 

Step 3: Then select the Minimum SDK as shown below and click Next.

Step 4: Then select the Empty Activity and click Next. Finally click Finish.

Step 5: Design layout in activity_main.xml.

Step 6: Display process of proximitysensor in android mobile devices.

Step 7: Save and run the application.

## PROGRAM:
```
/*
Program to print the process of proximitysensor in android mobile devices”.
Developed by: TAMIZHSELVAN B
Registeration Number : 212223230225
*/
```

### Main Activity :

```
package com.example.proximitysensor;

import android.content.Context;
import android.graphics.Color;
import android.hardware.Sensor;
import android.hardware.SensorEvent;
import android.hardware.SensorEventListener;
import android.hardware.SensorManager;
import android.os.Bundle;
import android.widget.TextView;
import android.widget.Toast;

import androidx.appcompat.app.AppCompatActivity;

public class MainActivity extends AppCompatActivity implements SensorEventListener {

    private SensorManager sensorManager;
    private Sensor proximitySensor;
    private TextView tvStatus, tvDistance;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        // Initialize UI elements
        tvStatus = findViewById(R.id.tvStatus);
        tvDistance = findViewById(R.id.tvDistance);
        TextView tvMaxRange = findViewById(R.id.tvMaxRange);
        TextView tvSensorAvailable = findViewById(R.id.tvSensorAvailable);

        // Initialize Sensor Manager
        sensorManager = (SensorManager) getSystemService(Context.SENSOR_SERVICE);
        if (sensorManager != null) {
            proximitySensor = sensorManager.getDefaultSensor(Sensor.TYPE_PROXIMITY);
        }

        if (proximitySensor == null) {
            tvStatus.setText("---");
            tvSensorAvailable.setText(R.string.tvSensorNotAvailable);
            tvSensorAvailable.setTextColor(Color.RED);
            Toast.makeText(this, "Proximity Sensor not found!", Toast.LENGTH_SHORT).show();
        } else {
            tvMaxRange.setText(getString(R.string.tvMaxRange, proximitySensor.getMaximumRange()));
            tvSensorAvailable.setText(R.string.tvSensorAvailable);
        }
    }

    @Override
    protected void onResume() {
        super.onResume();
        if (proximitySensor != null) {
            sensorManager.registerListener(this, proximitySensor, SensorManager.SENSOR_DELAY_NORMAL);
        }
    }

    @Override
    protected void onPause() {
        super.onPause();
        if (proximitySensor != null) {
            sensorManager.unregisterListener(this);
        }
    }

    @Override
    public void onSensorChanged(SensorEvent event) {
        if (event.sensor.getType() == Sensor.TYPE_PROXIMITY) {
            float distance = event.values[0];
            tvDistance.setText(getString(R.string.tvDistance, distance));

            if (distance < proximitySensor.getMaximumRange()) {
                // Near
                tvStatus.setText(R.string.tvStatusNear);
                tvStatus.setTextColor(Color.RED);
            } else {
                // Far
                tvStatus.setText(R.string.tvStatusFar);
                tvStatus.setTextColor(Color.YELLOW);
            }
        }
    }

    @Override
    public void onAccuracyChanged(Sensor sensor, int accuracy) {
        // No implementation needed
    }
}


```

### Activity_Main.xml :

```
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:id="@+id/main"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:gravity="center"
    android:padding="20dp"
    android:background="#121212">

    <TextView
        android:id="@+id/tvTitle"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="@string/tvTitle"
        android:textSize="28sp"
        android:textColor="#4CAF50"
        android:textStyle="bold"
        android:layout_marginBottom="40dp"/>

    <LinearLayout
        android:layout_width="200dp"
        android:layout_height="200dp"
        android:gravity="center"
        android:background="@drawable/circle_background"
        android:layout_marginBottom="30dp">

        <TextView
            android:id="@+id/tvStatus"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="@string/tvStatusFar"
            android:textSize="24sp"
            android:textColor="#FFFFFF"
            android:textStyle="bold" />
    </LinearLayout>

    <TextView
        android:id="@+id/tvDistance"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="@string/tvDistance"
        android:textColor="#FFFFFF"
        android:textSize="16sp"
        android:layout_marginBottom="10dp" />

    <TextView
        android:id="@+id/tvMaxRange"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="@string/tvMaxRange"
        android:textColor="#FFFFFF"
        android:textSize="14sp"
        android:layout_marginBottom="20dp" />

    <TextView
        android:id="@+id/tvSensorAvailable"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="@string/tvSensorAvailable"
        android:textColor="#888888"
        android:textSize="12sp" />

</LinearLayout>


```

## OUTPUT

<img width="1918" height="1023" alt="image" src="https://github.com/user-attachments/assets/289afbe4-a17c-4604-980d-07e223b4dacd" />

![exp5_1](https://github.com/user-attachments/assets/a18a23ab-2261-484a-a662-3d9b4c27d188)

![exp5_2](https://github.com/user-attachments/assets/91f9e3c1-8811-4652-8398-85fda7ab7b4b)



## RESULT
Thus a Simple Android Application to display the details of proximity sensor using sensor manager in Android Studio is developed and executed successfully.
