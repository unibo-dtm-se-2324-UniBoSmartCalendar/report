---
title: User guide
has_children: false
nav_order: 10
---

# User Guide

This section explains how to use **UniBo Smart Calendar** from an end-user perspective. It assumes the application has been correctly deployed and is accessible either online or locally.

## 9.1 Accessing the application

You can access UniBo Smart Calendar in two ways:

### A) Online (deployed)

Open the web application at:

- https://unibosmartcalendar.vercel.app/

### B) Locally (via command line)

To run the application locally, clone the repository, install dependencies, and start the development environment (client + server). After startup, the frontend is available at:

- http://localhost:3000

> Note: details about installation and startup commands are provided in the Deployment / Developer Guide sections.

---

## 9.2 Adding a course timetable (Calendar Settings)

To load your university schedule, you must add at least one timetable from **Calendar Settings**. The application accepts a UniBo timetable URL and automatically converts it into the correct JSON format.

### Step 1 | Open Calendar Settings

Navigate to the **Calendar Settings** page. You will see the section **Add New Timetable** with a field named **Timetable JSON URL** and an **ADD** button.

![Calendar Settings — Add New Timetable](../pictures/add-timetable.png)

### Step 2 — Paste your UniBo timetable URL

Paste the timetable URL of your course into the input field. Any UniBo course timetable link is accepted and will be automatically converted to the correct internal format.

![Calendar Settings — Timetable URL inserted](../pictures/add-tt.png)

### Step 3 — Select Year and Curriculum

Select the additional academic parameters in the **Select Year and Curriculum** section:

- Choose the **Year** (e.g., *2nd year*)
- Choose the **Curriculum** (e.g., *Digital Transformation Management*)

![Calendar Settings — Select Year and Curriculum](../pictures/ad-tt2.png)

### Step 4 — Confirm by clicking ADD

Click **ADD** to register the timetable. The timetable becomes active and is stored in the **Active Timetables** list.

---

## 9.3 Managing active timetables

After adding a timetable, it appears under **Active Timetables**. From here you can:

- **View** the active timetables currently used to build your schedule
- **Edit** timetable settings (when available)
- **Remove** a timetable using the delete icon

---

## 9.4 Viewing the schedule (Calendar view)

1. Open the **Calendar** view.
2. Navigate between weeks using the calendar controls.
3. Events are displayed in the correct time slots based on the active timetables.

---

## 9.5 Filtering the schedule

Use the available filters (e.g., **Course**, **Program/Curriculum**, **Year**) to personalize what you see. When a filter is applied, the calendar updates to display only matching events.

---

## 9.6 Conflicts (overlapping lectures)

If two lectures overlap in time, the application flags them as **conflicts** in the calendar view. This helps you identify timetable clashes immediately.

---

## 9.7 Exporting to ICS and subscription URL feed

UniBo Smart Calendar supports interoperability with external calendar apps:

- **ICS export:** download an `.ics` file and import it into Google Calendar / Outlook / Apple Calendar.
- **Subscription URL feed:** copy the provided URL and subscribe to it from your external calendar app to keep events synchronized.
```

