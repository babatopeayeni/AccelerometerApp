# AccelerometerApp

## Overview  
AccelerometerApp is an Android application that reads real-time accelerometer data, displays it in a grid alongside user-managed entries (e.g., inventory items, events, or weight logs), and optionally sends SMS alerts when configurable thresholds are met. The app’s primary goal is to give users an intuitive, persistent interface for monitoring motion data and custom entries while providing timely notifications.
---

## Requirements & Goals  
- **User Authentication:** Allow new users to register and returning users to log in, with credentials stored in a local SQLite database.  
- **Data Management Shell:** Create a persistent database schema that supports CRUD operations on the core dataset (accelerometer readings or user-defined entries) and on user records.  
- **Grid Display:** Present all database items in a responsive RecyclerView grid for easy viewing, creation, updating, and deletion.  
- **SMS Notifications:** Request `SEND_SMS` permission at runtime and, if granted, send SMS alerts when defined triggers occur. The app must continue to function fully if the user denies SMS permission.  
- **Usability & Maintainability:** Follow best practices—single-responsibility classes, clear naming conventions, in-line comments, and off-UI-thread database operations.

---

## Screens & Features  
1. **Login / Registration Screen**  
   - Fields for username/password  
   - “Register” flow for first-time users  
2. **Main Data Grid Screen**  
   - RecyclerView with GridLayoutManager for entries  
   - FAB or toolbar actions to add, edit, or delete items  
3. **Settings / Alerts Screen**  
   - Toggle to configure SMS alert thresholds  
   - Prompt and explanation for SMS permission  
4. **Permission Dialog**  
   - Runtime request for `SEND_SMS` with rationale  
   - Fallback UI state when permission is denied  

**UI Design Considerations:**  
- Followed Material Design guidelines for consistent typography, spacing, and component behavior.  
- Ensured accessibility by providing content descriptions, focus order, and sufficient color contrast.  
- Early prototyping with low-fidelity wireframes and Android Studio layout previews helped catch usability issues before coding.

---

## Development Approach  
- Adopted an MVVM-inspired structure:  
  - **ViewModels** manage UI state.  
  - **Repository / DatabaseHelper** encapsulate SQLite operations.  
  - **Helper classes** handle SMS and permission logic.  
- Performed database queries and inserts on a background thread (ExecutorService) to keep the UI responsive.  
- Applied clear in-line comments and consistent naming (PascalCase for classes, camelCase for methods/variables).  
- Set up a Continuous Integration pipeline to lint, build, and run unit/UI tests on every commit, enforcing code quality and early regression detection.

---

## Testing Strategy  
- **Unit Tests:** Validated business logic in ViewModels and the DatabaseHelper (e.g., insertItem, deleteItem, getAllItems).  
- **Espresso UI Tests:** Automated core user flows—login/registration, data CRUD on the grid, and permission workflows—to catch regressions.  
- **Manual Emulator Checks:** Verified behavior on API levels 21, 28, and 34 for both granted and denied SMS permissions.  

This rigorous approach uncovered edge cases (e.g., grid refresh after database update, SMS fallback path) and ensured a stable, responsive user experience.

---

## Innovation & Challenges  
Implementing the SMS permission flow with a graceful fallback required innovating on the standard Android template: I wrote a custom rationale dialog that links directly to the app’s settings page if the user permanently denied permission. I also optimized RecyclerView updates with DiffUtil to animate grid changes smoothly after CRUD operations.

---

## Highlighted Component  
The **SMS permission & notification module** best showcases my skills. It demonstrates:  
- Deep understanding of Android’s runtime permission model.  
- Clean separation of concerns (UI prompt vs. SMS dispatch logic).  
- Robust testing of both allowed and denied permission scenarios, ensuring user privacy and uninterrupted core functionality.
