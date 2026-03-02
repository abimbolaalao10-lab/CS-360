# CS 360 Mobile App Development Portfolio

## Event Tracker App

This repository contains my completed Event Tracker mobile application, developed as part of CS 360 - Mobile Architecture and Programming at Southern New Hampshire University.

---

## Project Summary

### Requirements and Goals

The Event Tracker app was designed to help users organize and manage their important events in one centralized location. The primary user need was a simple, reliable way to track events (such as meetings, birthdays, conferences, and appointments) without the complexity of full-featured calendar applications.

**Key Requirements:**
- Secure user authentication system with login and account creation
- Persistent storage of events using SQLite database
- Full CRUD operations (Create, Read, Update, Delete) for event management
- Optional SMS notifications for upcoming event reminders
- Clean, intuitive user interface with logical navigation flow

The app addresses the needs of busy professionals, students, and anyone who requires a straightforward tool to stay organized and never miss important dates.

---

## Screens and Features

### User-Centered UI Design

The app consists of three main screens, each designed with specific user needs in mind:

**1. Login Screen:**
- Simple username and password fields
- Password field configured to obscure text for security
- Clear "Login" and "Create New Account" buttons
- Validates input before processing to prevent errors

**2. SMS Permission Screen:**
- Clear explanation of why SMS permission is requested
- "Allow" and "Not Now" options giving users control
- Continues to function fully even if permission is denied
- Professional, non-intrusive design

**3. Events Grid Screen:**
- Header row with clear column labels (Event Name, Date, Action)
- Scrollable grid displaying all user events
- "Edit" and "Delete" buttons on each row for easy management
- Bottom form section for adding new events
- Immediate visual feedback for all actions

### Design Success Factors

My UI designs kept users in mind through:
- **Visual Hierarchy:** Most important actions (Add Event, Save) use prominent green buttons
- **Consistency:** Same color scheme and button styles across all screens
- **Feedback:** Toast messages confirm every action (login success, event saved, etc.)
- **Simplicity:** No unnecessary features or clutter—focused on core functionality
- **Touch Targets:** All buttons meet the 48dp minimum size for easy tapping
- **Logical Flow:** Users progress naturally from login → permission → events

The designs were successful because they prioritized user goals over aesthetic complexity, making the app immediately understandable without requiring instructions.

---

## Coding Approach

### Techniques and Strategies

**1. Database-First Design:**
I began by creating the DatabaseHelper class with clear separation between user operations and event operations. This modular approach made it easy to test database functionality independently before connecting it to the UI.

**2. Incremental Development:**
Rather than trying to build everything at once, I implemented features in stages:
- First: Database structure and basic CRUD operations
- Second: Login functionality with authentication
- Third: Events display and management
- Fourth: SMS permissions and notifications

**3. Code Reusability:**
I created helper methods (like `addEventRow()` in EventsActivity) that could be called multiple times rather than duplicating code. This made the codebase more maintainable.

**4. Comprehensive Commenting:**
I added inline comments explaining the purpose of each method and important logic decisions, making the code easier to understand and modify later.

**5. Proper Resource Management:**
I ensured database connections were properly opened and closed, and used SharedPreferences for persistent data like user IDs.

### Future Application

These strategies can be applied to any software development project:
- **Modular design** makes debugging easier and allows team collaboration
- **Incremental development** reduces risk and allows for testing at each stage
- **Clear documentation** helps both current and future developers understand the code
- **Proper lifecycle management** prevents memory leaks and crashes

---

## Testing Process

### Testing Methodology

I employed multiple testing approaches to ensure code functionality:

**1. Unit Testing During Development:**
- Tested database operations individually (add user, retrieve events, etc.)
- Used Log statements to verify data was being stored correctly
- Checked SharedPreferences values to ensure user sessions persisted

**2. UI Testing:**
- Tested on physical Android device (real-world conditions)
- Verified all buttons triggered correct actions
- Ensured text input validation worked properly
- Confirmed password field obscured text

**3. Lifecycle Testing:**
- Closed and reopened app to verify data persistence
- Tested navigation between activities
- Verified user stayed logged in after app restart

**4. Permission Testing:**
- Tested both "Allow" and "Deny" scenarios for SMS permission
- Confirmed app continued functioning when permission was denied
- Verified permission status was saved correctly

**5. Edge Case Testing:**
- Attempted to login with incorrect credentials
- Tried to create account with existing username
- Attempted to save events with empty fields
- Tested deleting and editing multiple events

### Importance and Revelations

This testing process is critical because it:
- **Prevents user frustration** by catching bugs before release
- **Validates assumptions** about how users will interact with the app
- **Identifies edge cases** developers might not have considered
- **Ensures data integrity** and prevents data loss

Key revelations from testing:
- Initial implementation had issues with event persistence after app closure (fixed by properly closing database connections)
- Permission denial needed better handling to avoid confusing users
- Input validation was crucial to prevent empty database entries
- Testing on a physical device revealed touch target size issues not apparent in emulator

---

## Innovation and Problem-Solving

### Overcoming Development Challenges

**Challenge 1: Dynamic Event Display**

The most significant challenge was dynamically creating and displaying event rows from the database. The initial UI design had static sample rows, but I needed to generate rows programmatically based on database content.

**Solution:** I created the `addEventRow()` method that programmatically builds LinearLayout rows with TextViews and Buttons, applies proper styling and layout parameters, and adds click listeners for edit/delete functionality. This approach allowed unlimited events to be displayed without modifying the XML layout.

**Challenge 2: User Data Isolation**

Ensuring each user only saw their own events required careful database design with foreign keys and proper query filtering.

**Solution:** I implemented a foreign key relationship between the events table and users table, stored the current user ID in SharedPreferences after login, and filtered all database queries by user ID. This ensured complete data isolation between accounts.

**Challenge 3: Permission Handling Without Breaking App**

SMS permission could be denied, but the app needed to continue functioning normally.

**Solution:** I wrapped SMS functionality in permission checks, saved permission status to SharedPreferences, and implemented graceful degradation where the app simply skips notification logic if permission is denied. The `checkUpcomingEvents()` method returns early if SMS is not enabled.

---

## Demonstrated Knowledge and Skills

### Strongest Component: Database Integration

I am particularly proud of the **DatabaseHelper class and its integration with the UI**, as it demonstrates several key competencies:

**1. Database Design Expertise:**
- Properly structured tables with primary keys, foreign keys, and appropriate data types
- Implemented referential integrity between users and events tables
- Used SQLite best practices for Android development

**2. Clean Architecture:**
- Separated database logic from UI code
- Created reusable methods with clear parameters and return types
- Followed single responsibility principle—each method does one thing well

**3. Full CRUD Implementation:**
- **Create:** `addUser()` and `addEvent()` methods with validation
- **Read:** `getUserEvents()` returns filtered, sorted results
- **Update:** `updateEvent()` modifies existing records
- **Delete:** `deleteEvent()` removes records with confirmation

**4. Error Handling:**
- All database methods return meaningful values (-1 for failure, row count for success)
- Proper cursor management to prevent memory leaks
- Try-catch would be added in production for additional safety

**5. User Experience:**
- Database operations are fast and responsive
- Data persists correctly across app sessions
- No data loss even when app is force-closed

This component showcases my ability to design robust backend systems, implement industry-standard database patterns, and integrate complex functionality into a user-friendly interface—skills that are directly transferable to professional software development roles.

---

## Technologies Used

- **Language:** Java
- **IDE:** Android Studio
- **Database:** SQLite
- **Minimum SDK:** API 24 (Android 7.0)
- **Target SDK:** API 36 (Android 15.0)
- **Key Android Components:**
  - Activities and Intents
  - SQLiteOpenHelper
  - SharedPreferences
  - Runtime Permissions (SMS)
  - UI Components (LinearLayout, ConstraintLayout, ScrollView)

---

## Repository Contents

- **EventTracker.zip** - Complete Android Studio project with full source code
- **(Optional) LaunchPlan.docx** - Detailed plan for app distribution and monetization

---

## Future Enhancements

Planned features for Version 2.0:
- Google Calendar integration
- Recurring events
- Event categories with color coding
- Cloud sync across devices
- Export events to CSV

---

*Developed as part of CS 360 - Mobile Architecture and Programming*  
*Southern New Hampshire University*  

This repository contains my completed Event Tracker app (ZIP file) and a comprehensive README with reflections on the development process, design decisions, testing methodology, and demonstrated skills.
