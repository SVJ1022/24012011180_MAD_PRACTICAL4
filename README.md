# ⏰ Practical-4 --- Android Alarm using Service & BroadcastReceiver

> **Aim:** Create an Android Alarm application by using service &
> BroadcastReceiver.

------------------------------------------------------------------------

## 🎯 Objective

This practical demonstrates the creation of an Android Alarm application
using **Service** and **BroadcastReceiver**.

The application allows the user to:

-   View the current digital time
-   Select an alarm time
-   Create an alarm
-   Cancel an alarm

------------------------------------------------------------------------

## 📋 Practical Requirements

The practical specifies the following development tasks:

1.  Create `MainActivity` according to the given UI design.
2.  Create `AlarmBroadcastReceiver` class.
3.  Create `AlarmService` class.
4.  Add `android.permission.SCHEDULE_EXACT_ALARM` permission in the
    Manifest file.

------------------------------------------------------------------------

## 🧩 Main Components

### 1. MainActivity

`MainActivity` provides the main UI for creating and cancelling an alarm
and displaying the current time.

### 2. AlarmBroadcastReceiver

`AlarmBroadcastReceiver` receives the alarm broadcast when the scheduled
alarm is triggered.

### 3. AlarmService

`AlarmService` is used to perform the service-related operation
associated with the alarm.

### 4. AlarmManager

`AlarmManager` is used to schedule the alarm with the Android system.

### 5. PendingIntent

`PendingIntent` represents the operation that should be performed when
the alarm is triggered.

------------------------------------------------------------------------

## 🕐 TimePickerDialog

A `TimePickerDialog` is used to select the required alarm hour and
minute.

The selected time can then be stored using the `Calendar` class for
scheduling the alarm.

------------------------------------------------------------------------

## 🔄 Alarm Application Flow

``` text
                  MainActivity
                       │
                       ▼
              Select Alarm Time
                       │
                       ▼
               TimePickerDialog
                       │
                       ▼
                    Calendar
                       │
                       ▼
                 AlarmManager
                       │
                       ▼
                 PendingIntent
                       │
                       ▼
            AlarmBroadcastReceiver
                       │
                       ▼
                  AlarmService
                       │
                       ▼
                 Alarm Action
```

------------------------------------------------------------------------

## 🔐 Android Manifest Permission

The practical requires the following permission in the Android Manifest:

``` xml
<uses-permission android:name="android.permission.SCHEDULE_EXACT_ALARM" />
```

------------------------------------------------------------------------

## 🛠️ Development Steps

1.  Create `MainActivity` according to the given UI design.
2.  Create the `AlarmBroadcastReceiver` class.
3.  Create the `AlarmService` class.
4.  Add the required alarm permission in the Manifest file.
5.  Add the digital clock/current time display.
6.  Add the **Create Alarm** button.
7.  Use `TimePickerDialog` to select the alarm time.
8.  Use `Calendar` to prepare the selected time.
9.  Create a `PendingIntent`.
10. Use `AlarmManager` to schedule the alarm.
11. Receive the alarm using `AlarmBroadcastReceiver`.
12. Start the required `AlarmService`.
13. Add the **Cancel Alarm** operation.
14. Test creating and cancelling an alarm.

------------------------------------------------------------------------

## 📚 Concepts Covered

-   `BroadcastReceiver`
-   `Service`
-   `TextClock`
-   `TimePickerDialog`
-   `Calendar`
-   `SimpleDateFormat`
-   `PendingIntent`
-   `AlarmManager`
-   `getSystemService()`
-   `sendBroadcast()`
-   `MediaPlayer`
-   `startService()`
-   `stopService()`
-   `Intent.getStringExtra()`
-   `Intent.putStringExtra()`
-   `MaterialCardView`
-   `SCHEDULE_EXACT_ALARM`

------------------------------------------------------------------------

## 📁 Updated / Added Files

-   MainActivity.kt
-   activity_main.xml
-   AlarmService.kt
-   AlarmBroadcastReceiver.kt
-   clocks.png
-   baseline_alarm_add_24.xml
-   baseline_alarm_off_24.xml

------------------------------------------------------------------------

## ▶️ How to Run

1.  Open the project in **Android Studio**.
2.  Build and run the application.
3.  Verify the current digital clock.
4.  Press **Create Alarm**.
5.  Select the required time using the Time Picker.
6.  Confirm the selected alarm.
7.  Verify the alarm information shown in the application.
8.  Wait for the scheduled alarm or test it with a suitable time.
9.  Use **Cancel Alarm** to cancel the alarm.

------------------------------------------------------------------------

## 🖼️ OUTPUT
<table>
  <tr>
    <td align="center">
      <img width="350" height="600" alt="image" src="https://github.com/user-attachments/assets/5d549e44-67b1-4889-8fb3-967fee55c817" />
    </td>
    <td align="center">
      <img width="350" height="600" alt="image" src="https://github.com/user-attachments/assets/1363b961-12ab-46bd-ab0e-e4a4b237953c" />
    </td>
    </td>
    <td align="center">
      <img width="350" height="600" alt="image" src="https://github.com/user-attachments/assets/4e11612e-f4b3-4b68-a2e3-791826595301" />
    </td>
    </td>
    <td align="center">
      <img width="350" height="600" alt="image" src="https://github.com/user-attachments/assets/816e78d2-3354-45c2-bcb0-103b4ce55369" />
    </td>
  </tr>
  <tr>
    <td align="center"><b>Alarm Main Page</b></td>
    <td align="center"><b>Time Set Dialog Box</b></td>
    <td align="center"><b>New Card After Alarm Set</b></td>
    <td align="center"><b>Alarm Stopped Toast</b></td>
  </tr>
</table>

------------------------------------------------------------------------

## ✅ Result

The Android Alarm application was successfully developed using
**Service, BroadcastReceiver, AlarmManager and PendingIntent** to create
and cancel scheduled alarms.
