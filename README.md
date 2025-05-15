# 🛡️ SurviveGame Reverse Engineering Task

This project was submitted as part of the **Mobile Security** course.  
The objective was to perform reverse engineering on a given APK and **make it functional** by restoring its missing components and fixing hidden bugs.

---

## 🎯 Task Description

We received an APK file for a game called **SurviveGame**, with the following goal:

> "Find a way to survive and reach your city."

The game requires the player to enter an ID number, and based on internal logic, the game determines a path. If the correct actions are taken, the game will display a toast message with the name of the city the user reached.

Our mission:

- Perform reverse engineering on the APK.
- Restore all missing resources (images, layout files, icons, etc.).
- Fix any bugs or inconsistencies to make the app fully functional.
- Submit the working code to GitHub and show proof of success.

---

## 🔍 Analysis & Reverse Engineering Process

To analyze the APK, I used the online tool:  
🔗 [http://www.javadecompilers.com/apk](http://www.javadecompilers.com/apk)

### Step-by-step process:

1. **Decompiled the APK** to examine its Java source code.
2. **Located the `AndroidManifest.xml`** file to identify the entry-point activity.
3. **Identified main components**:  
   - `Activity_Menu` – for ID entry and starting the game  
   - `Activity_Game` – for the actual gameplay
4. **Imported both activities** into a new Android Studio project.
5. Discovered that many **resources were missing**, including:
   - Layout XML files (`activity_menu.xml`, `activity_game.xml`)
   - Icons and drawable images
   - String resources

---

## 🛠️ Issues Encountered & Fixes Applied

| Problem | Fix |
|--------|-----|
| `AndroidManifest.xml` missing `exported=true` in main activity | ✅ Added `android:exported="true"` to the launcher `<activity>` |
| `targetSdkVersion` was too low (`30`) | ✅ Updated it to `33` for compatibility with latest build tools |
| `url` string was corrupted on copy-paste from the decompiled source | ✅ Manually restored the correct URL string in `strings.xml` |
| Two invalid attributes appeared in `AndroidManifest.xml`: `android:platformBuildVersionCode` and `android:platformBuildVersionName` | ✅ Removed them completely — these are inserted by build tools, not meant for source |
| Missing resources (layouts, drawables) | ✅ Reconstructed layout files based on Java logic and restored placeholders for images |

---

## 🧪 Gameplay Logic Summary

- The user enters an ID (9 digits).
- The app downloads a list of locations (states) from a remote URL.
- Based on the 8th digit of the ID (index 7), it selects one of the cities.
- A sequence of moves (steps) is generated using:  
  `digit % 4` → mapped to arrow buttons.
- If the player presses the correct arrows in order, a toast appears:  
  🏙️ `"Survived in <City>"`

---

📸 *My result:*  
`"Survived in New York"`

<div style="display: flex; justify-content: center; align-items: center;">
  <img src="https://github.com/user-attachments/assets/37c566b4-6666-4167-a491-d83e4b3a9363" width="250" height="400">
</div>

🧭 **My Steps**

- 3 → Down  
- 1 → Right  
- 5 → Right  
- 0 → Left  
- 0 → Left  
- 6 → Up  
- 2 → Up  
- 5 → Right  
- 4 → Left


---

## 🎉 **Have Fun!**  
May you always reach your destination 🚀

---

📌 *Maintained by:* Noa Sharabi  
