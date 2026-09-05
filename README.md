# ⏰ Practical-4 — Android Alarm using Service & BroadcastReceiver

> **Aim:** Create an Android Alarm application using **Service** and **BroadcastReceiver**.

---

## 🎯 Objective

This practical implements an Android alarm application in Kotlin. The application allows the user to select an alarm time, schedule the alarm, display the selected alarm in the UI, and cancel the alarm.

The implementation is divided into three important parts:

- `MainActivity` — handles the user interface and alarm scheduling.
- `AlarmBroadcastReceiver` — receives the alarm broadcast and controls the service.
- `AlarmService` — starts and stops the alarm sound using `MediaPlayer`.

The repository also uses `AlarmManager`, `PendingIntent`, `TimePickerDialog`, `Calendar`, Material components and the `SCHEDULE_EXACT_ALARM` permission. citeturn0view0turn5view0turn5view1

---

## 📂 Project Structure

```text
24012011180_MAD_PRACTICAL4/
│
├── app/
│   └── src/
│       ├── main/
│       │   ├── java/
│       │   │   └── com/example/
│       │   │       └── a24012011180_mad_class_practical4/
│       │   │           ├── MainActivity.kt
│       │   │           ├── AlarmBroadcastReceiver.kt
│       │   │           └── AlarmService.kt
│       │   │
│       │   ├── res/
│       │   │   ├── drawable/
│       │   │   ├── layout/
│       │   │   ├── raw/
│       │   │   └── values/
│       │   │
│       │   └── AndroidManifest.xml
│       │
│       └── ...
│
├── gradle/
├── .gitignore
├── build.gradle.kts
├── gradle.properties
├── gradlew
├── gradlew.bat
├── settings.gradle.kts
└── README.md
```

The repository currently contains `MainActivity.kt`, `AlarmBroadcastReceiver.kt`, and `AlarmService.kt` in the application package, with `activity_main.xml` under the layout resources. citeturn4view0turn6view3

---

# 🧩 Main Components

## 1. MainActivity

`MainActivity` is responsible for the alarm UI and the complete scheduling/cancellation flow.

When the Activity is created, it:

- Enables Edge-to-Edge display.
- Loads `activity_main`.
- Applies system-bar insets.
- Finds the alarm TextView and alarm card.
- Initially hides the alarm card.
- Adds a listener to the **Set Alarm** button.
- Adds a listener to the **Cancel Alarm** button. citeturn7view0

### Initial Alarm Card

The project explicitly hides the card until an alarm is successfully scheduled:

```kotlin
cardSetAlarm.visibility = View.GONE
```

After a successful alarm setup, the selected time is displayed and the card becomes visible. citeturn7view0

---

# 🕐 Selecting an Alarm Time

The application uses `TimePickerDialog` to allow the user to select the alarm hour and minute.

```kotlin
val picker = TimePickerDialog(
    this,
    { tp, sHour, sMinute ->
        sendDialogDataToActivity(sHour, sMinute)
    },
    hrs,
    mns,
    false
)

picker.show()
```

The current hour and minute are obtained from `Calendar.getInstance()` and used as the initial values of the picker. citeturn7view0

---

# 📅 Preparing the Alarm Time

After the user selects a time, the application creates a `Calendar` object and sets:

- Current year
- Current month
- Current date
- Selected hour
- Selected minute
- Seconds = `0`

```kotlin
alarmCalendar.set(year, month, day, hour, minute, 0)
```

The resulting time is converted to milliseconds using:

```kotlin
alarmCalendar.timeInMillis
```

This value is passed to the alarm scheduling function. citeturn7view0

---

# ⏱️ AlarmManager & PendingIntent

The project creates a broadcast `PendingIntent` targeting `AlarmBroadcastReceiver`.

```kotlin
val pendingIntent = PendingIntent.getBroadcast(
    applicationContext,
    23245,
    intent,
    PendingIntent.FLAG_IMMUTABLE
)
```

Then `AlarmManager` is obtained from the Android system:

```kotlin
val alarmManager =
    getSystemService(ALARM_SERVICE) as AlarmManager
```

For starting an alarm, the application checks:

```kotlin
alarmManager.canScheduleExactAlarms()
```

and schedules the alarm using:

```kotlin
alarmManager.setExact(
    AlarmManager.RTC_WAKEUP,
    millisTime,
    pendingIntent
)
```

This is the core scheduling logic implemented in the repository. citeturn7view0

---

# 🔐 Exact Alarm Permission

The practical uses:

```xml
<uses-permission
    android:name="android.permission.SCHEDULE_EXACT_ALARM" />
```

If exact alarm scheduling is unavailable, the application displays a message and opens the appropriate system settings screen using `ACTION_REQUEST_SCHEDULE_EXACT_ALARM`. citeturn0view0turn7view0

---

# 📡 AlarmBroadcastReceiver

`AlarmBroadcastReceiver` extends `BroadcastReceiver`.

It reads a String extra named:

```kotlin
SERVICE_KEY = "Service1"
```

The receiver recognises two values:

```kotlin
START_VAL = "start"
STOP_VAL = "stop"
```

When the received value is `start`, the receiver starts `AlarmService`.

When the received value is `stop`, it stops `AlarmService`. citeturn5view0

### Receiver Flow

```text
Alarm Broadcast
      │
      ▼
AlarmBroadcastReceiver
      │
      ├── "start" ──► startService()
      │
      └── "stop"  ──► stopService()
```

---

# 🔊 AlarmService

`AlarmService` extends Android's `Service`.

The service uses:

```kotlin
MediaPlayer.create(this, R.raw.alarm)
```

to load the alarm audio from the application's `res/raw` resources.

When the service starts, it calls:

```kotlin
mp?.start()
```

When the service is destroyed, the media player is stopped:

```kotlin
mp?.stop()
```

The service returns:

```kotlin
START_STICKY
```

from `onStartCommand()`. citeturn5view1

---

# 🔄 Complete Alarm Flow

```text
┌──────────────────┐
│   MainActivity   │
└────────┬─────────┘
         │
         ▼
┌──────────────────┐
│ TimePickerDialog │
└────────┬─────────┘
         │
         ▼
┌──────────────────┐
│     Calendar     │
└────────┬─────────┘
         │
         ▼
┌──────────────────┐
│   AlarmManager   │
└────────┬─────────┘
         │
         ▼
┌──────────────────┐
│   PendingIntent  │
└────────┬─────────┘
         │
         ▼
┌────────────────────────┐
│ AlarmBroadcastReceiver │
└───────────┬────────────┘
            │
            ▼
┌──────────────────┐
│   AlarmService   │
└────────┬─────────┘
         │
         ▼
┌──────────────────┐
│   MediaPlayer    │
│   Alarm Sound    │
└──────────────────┘
```

The repository's implementation follows this architecture through `AlarmManager → PendingIntent → BroadcastReceiver → Service`. citeturn7view0turn5view0turn5view1

---

# ❌ Cancelling the Alarm

The **Cancel Alarm** button calls:

```kotlin
setAlarm(0, AlarmBroadcastReceiver.STOP_VAL)
```

The alarm `PendingIntent` is cancelled using:

```kotlin
alarmManager.cancel(pendingIntent)
```

The receiver is then notified through:

```kotlin
sendBroadcast(intent)
```

and the alarm card is hidden again.

The application also displays:

```text
Alarm is stopped!
```

using a Toast. citeturn7view0

---

# 📚 Concepts Covered

| Concept | Implementation |
|---|---|
| Activity | `MainActivity` |
| BroadcastReceiver | `AlarmBroadcastReceiver` |
| Service | `AlarmService` |
| AlarmManager | Schedules the alarm |
| PendingIntent | Pending broadcast operation |
| TimePickerDialog | Selects alarm time |
| Calendar | Builds scheduled date/time |
| MediaPlayer | Plays alarm sound |
| MaterialCardView | Displays selected alarm |
| MaterialButton | Set/Cancel controls |
| Toast | Displays alarm status |
| Edge-to-Edge | Window configuration |
| Exact Alarm | `setExact()` |
| Manifest Permission | `SCHEDULE_EXACT_ALARM` |

---

# 🛠️ Development Steps

1. Create the Android project.
2. Design the alarm screen in `activity_main.xml`.
3. Create `MainActivity`.
4. Add the Set Alarm and Cancel Alarm controls.
5. Implement `TimePickerDialog`.
6. Store the selected time in `Calendar`.
7. Create a `PendingIntent` for `AlarmBroadcastReceiver`.
8. Obtain `AlarmManager`.
9. Check exact-alarm scheduling permission.
10. Schedule the alarm with `setExact()`.
11. Create `AlarmBroadcastReceiver`.
12. Create `AlarmService`.
13. Load the alarm sound using `MediaPlayer`.
14. Implement alarm cancellation.
15. Test both setting and cancelling the alarm.

---

## ▶️ How to Run

1. Open the project in **Android Studio**.
2. Allow Gradle synchronization to finish.
3. Run the application on an Android device or emulator.
4. Press **Create/Set Alarm**.
5. Select the desired time.
6. Verify that the selected alarm appears in the UI.
7. Allow exact-alarm access if Android requests it.
8. Test the alarm at a suitable time.
9. Press **Cancel Alarm** to stop/cancel it.

---

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

---

## 📁 Important Files

```text
MainActivity.kt
AlarmBroadcastReceiver.kt
AlarmService.kt
activity_main.xml
AndroidManifest.xml
res/raw/alarm
```

The first three Kotlin files are present in the repository's application package. citeturn4view0

---

## ✅ Result

The Android Alarm application was successfully implemented using **AlarmManager, PendingIntent, BroadcastReceiver and Service**, with `MediaPlayer` used to play the alarm sound and a TimePickerDialog used to select the alarm time.
