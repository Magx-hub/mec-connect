# mec-connect
A school portal for MagMax Educational Centre using React Native Expo 53+

# To develop a React Native Expo 53+ app with the following features:
  1. Staff Management (fullName, email, classLevel, isActive, createdAt, updatedAt) (CRUD, Count, Search, Pagination)
  2. Staff Attendance Management (checkInTime, checkOutTime, datem remarks, status, teacherId, teacherName, weekNum, workHours, createdAt, updatedAt) (CRUD, Count, Search, Pagination, PDF Export)
  2. Student Management (fullName, classLevel, isActive, createdAt, updatedAt) (CRUD, Count, Search, Pagination, PDF Export)

  app/
├── _layout.js (Root layout with AuthProvider)
├── index.js (Entry point with role-based redirection)
├── login.js (Login screen)
├── unauthorized.js (Unauthorized access screen)
├── (admin)/
│   ├── _layout.js (Admin tabs layout)
│   ├── index.js (Admin dashboard)
│   ├── teachers.js (Teachers management)
│   ├── attendance.js (Attendance management)
│   └── profile.js (Profile screen)
└── (teacher)/
    ├── _layout.js (Teacher tabs layout)
    ├── index.js (Teacher dashboard)
    ├── students.js (Students management)
    ├── assessments.js (Assessments management)
    └── profile.js (Profile screen)


  # Tech
  React Native Expo + expo-router file-based navigation
  Firebase + Firestore + AsyncStorage for offline persistence of all data
  JavaScript
  Check the package.json

  {
  "name": "magx-app",
  "version": "1.0.0",
  "main": "expo-router/entry",
  "description": "MEC Connect",
  "author": "Blakk Systems",
  "license": "MIT",
  "scripts": {
    "start": "expo start",
    "android": "expo start --android",
    "ios": "expo start --ios",
    "web": "expo start --web"
  },
  "dependencies": {
    "@react-native-async-storage/async-storage": "2.1.2",
    "@react-native-community/datetimepicker": "8.4.1",
    "@react-native-picker/picker": "^2.11.1",
    "@react-navigation/native": "^7.1.14",
    "expo": "^53.0.19",
    "expo-constants": "^17.1.7",
    "expo-linking": "^7.1.7",
    "expo-print": "^14.1.4",
    "expo-router": "^5.1.3",
    "expo-sharing": "^13.1.5",
    "expo-splash-screen": "^0.30.10",
    "expo-status-bar": "^2.2.3",
    "firebase": "^11.10.0",
    "nativewind": "^4.1.23",
    "react": "19.0.0",
    "react-dom": "19.0.0",
    "react-native": "0.79.5",
    "react-native-reanimated": "~3.17.4",
    "react-native-safe-area-context": "5.4.0",
    "react-native-screens": "^4.11.1",
    "react-native-web": "^0.20.0"
  },
  "devDependencies": {
    "@babel/core": "^7.20.0",
    "prettier-plugin-tailwindcss": "0.5.11",
    "tailwindcss": "3.4.17"
  },
  "private": true
}


  

🧩 Attendance Management UI Features

collection fields:
checkInTime: "07:00"(string)
checkOutTime: "15:01"(string)
createdAt: July 11, 2025 at 1:56:10 PM UTC(timestamp)
date: "2025-07-04"(string)
remarks: ""(string)
status: "Present"(string)
teacherId: "UTtTjNzdhbVJ0FUxBjFk"(string)
teacherName: "Jennifer Apprey"(string)
updatedAt: July 11, 2025 at 1:56:10 PM UTC(timestamp)
weekNum: 8(number)
workHours: 8.02(number)



1. Header with Navigation
Back button : Allows navigation back to the previous screen.
Title : "Attendance Management"

2. Tab Navigation (Bottom Tabs)
A tab bar lets users switch between three views:

List View : View attendance records
Form View : Add or edit attendance
Report View : Generate reports
Icons used: list-outline, add-circle-outline, bar-chart-outline
Active tab is highlighted visually.

3. List View – Attendance List
Displays list of attendance records using AttendanceList component.
Shows loading state while data is being fetched.
Supports:
Edit : Opens form with pre-filled data.
Delete : Deletes record with confirmation alert.
Pull-to-refresh support (via onRefresh).

4. Form View – Attendance Form
Used to create or edit attendance records.
Includes fields like:
Date
Status (Present, Absent, Late, Half Day)
Work hours
Notes
Teachers can be selected from a dropdown (if editing).
Cancel and Submit buttons.

5. Report View – Attendance Reports
Two types of reports available:

A. Individual Teacher Report
Select teacher via modal dropdown.
Shows stats:
Total records
Present/Absent/Late/Half-day counts
Percentage breakdown
Total and average working hours
Downloadable PDF report for the selected teacher.
B. All Teachers Report
Loads all teachers' attendance data.
Summary per teacher:
Total, present, absent, late, half-day
Attendance rate
Total & average working hours
Button to generate and download a comprehensive PDF report.

6. Modal – Teacher Dropdown Selection
Appears when selecting a teacher for the individual report.
Uses React Native Modal and FlatList.
Lists all teachers.
When selected, updates state and closes modal.

7. PDF Generation & Sharing
Uses Expo’s expo-print and expo-sharing modules.
Generates styled HTML content dynamically.
Converts HTML to PDF and shares it via device options (e.g., email, save, etc.).
Features:
Fully formatted reports (HTML/CSS inside PDF)
Dynamic file names based on date and teacher name
Success/failure alerts

8. UI States & Loading Indicators
Loading states during data fetching:
ActivityIndicator shown while loading all teachers' data.
Empty state handling :
Message displayed if no attendance data exists.

9. Styling & Layout
Responsive layout using ScrollView, View, Text, and TouchableOpacity
Styled cards and grids for reports
Custom colors and spacing
Uses StyleSheet for styling

Feature: -	Description
Header:	Title + back navigation
Tabs:	List / Form / Report
List View:	Display attendance records, edit/delete
Form View:	Create/edit attendance with validation
Report View:	Individual &amp; All Teachers reports
Teacher Selector:	Modal dropdown for selecting teacher
PDF Export:	Shareable PDF reports generated via HTML templates
Loading State:	Activity indicator while data loads
Empty State:	Message if no data found
Responsive Design:	Works on mobile screens
Styled UI:	Cards, grids, icons, colors


+-----------------------------------+
|        AttendanceScreen           |
| (Main Container)                  |
+-----------------------------------+
            |
            v
+-----------------------------------+
|           TabNavigator            |
| - List | Add New | Report        |
+-----------------------------------+
            |
    +-------+--------+
    |                |
    v                v
+----------------+ +------------------+
|   AttendanceList | |  AttendanceForm  |
+----------------+ +------------------+
    |                |
    v                v
+----------------+ +------------------+
|     FlatList     | |     Form Inputs  |
| - Render records | | - Date, Status, |
| - Edit/Delete    | |   Work Hours... |
+----------------+ +------------------+

            |
            v
       +--------------+
       |   ReportTab  |
       +--------------+
            |
    +-------+--------+
    |                |
    v                v
+----------------+ +------------------+
| IndividualReport | | AllTeachersReport|
+----------------+ +------------------+
    |                |
    v                v
+----------------+ +------------------+
| Teacher Dropdown | | Loading Indicator|
| Stats Cards      | | Summary Table    |
| PDF Button       | | PDF Button       |
+----------------+ +------------------+





🔍 Detailed Breakdown of Components
1. AttendanceScreen
Role : Main screen container.
Responsibilities :
Holds tab state (activeTab)
Manages teacher selection
Handles CRUD operations via hooks
Renders appropriate tab content
Displays modal for teacher selection in reports
2. TabNavigator
Role : Navigation bar with three tabs.
Tabs :
List View : Show attendance records
Form View : Add or edit attendance
Report View : Generate reports
UI Elements :
Icons: list-outline, add-circle-outline, bar-chart-outline
Active tab highlighting
3. AttendanceList
Role : Display list of attendance records.
Props :
attendanceRecords: Array of records
loading: Boolean
onEdit: Callback for editing
onDelete: Callback for deletion
onRefresh: Pull-to-refresh handler
Subcomponents:
FlatList : Renders each record
ActivityIndicator : Shows loading state
4. AttendanceForm
Role : Form to add or edit attendance.
Props :
onSubmit: Submit handler
editingRecord: Optional record being edited
onCancel: Cancel button
teachers: For selecting teacher when adding new
Form Fields:
Date Picker
Status Selector (Present, Absent, Late, Half Day)
Work Hours Input
Notes Field
Teacher Dropdown (only when adding)
5. ReportTab
Role : Wrapper for report views.
Switches Between :
Individual Report
All Teachers Report
6. IndividualReport
Role : Displays stats for one selected teacher.
Features :
Teacher dropdown modal
Stats cards: Total, Present, Absent, etc.
Percentage breakdowns
Download PDF button
7. AllTeachersReport
Role : Displays summary for all teachers.
Features :
Teacher-wise stats grid
Attendance rate
Total & average working hours
Download full PDF report
8. TeacherDropdown Modal
Role : Modal picker for selecting a teacher.
Used In :
Individual report screen
Components :
Modal
FlatList of teachers
Close button




📦 State Management
    Local State Used:

activeTab: Controls which tab is displayed
editingRecord: Stores record being edited
teacherId: Current teacher ID
selectedTeacherForReport: Selected teacher in individual report view
reportType: 'individual' or 'all'
allTeachersAttendance: Store attendance data for all teachers
loadingAllData: Loading state for all teachers report
showTeacherDropdown: Controls visibility of teacher selection modal


Data Flow

Firebase Firestore + Offline Persistence
      ↓
Service Layer (attendanceService.js, teacherService.js)
      ↓
Hooks (useAttendance.js, useTeachers.js)
      ↓
AttendanceScreen (state management)
      ↓
Tab Navigator → Selected Tab Content (List / Form / Report)


