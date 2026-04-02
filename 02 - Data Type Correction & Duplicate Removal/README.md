# 02 - Data Type Correction & Duplicate Removal

## Goal
Identify which genres have the most reviews and find the most popular genre 
among Google Play Store apps.

## What Happened
During the first query attempt, results were not sorted in descending order 
as expected. This triggered a deeper investigation into data quality.

## 🔍 Issues Found

### 1. Wrong Data Type
The `Reviews` column was stored as `object` (string) instead of integer. 
String sorting caused incorrect ordering — for example, '997' appeared 
before '9966' alphabetically.

### 2. Non-Numeric Value
One non-numeric value was found: `'3.0M'`. This was replaced with 
`3000000` before type conversion.

### 3. Duplicate Entries
798 duplicate app entries were detected. For each app, the record with 
the highest review count was retained as the most representative version.

## 🛠️ Fixes Applied
1. Replaced `'3.0M'` with `3000000`
2. Converted `Reviews` column from string to integer
3. Removed duplicates by keeping the highest-reviewed entry per app
4. Re-written the cleaned dataframe to SQLite

## ✅ Result
After cleaning, the top 10 most-reviewed apps are dominated by 
Social and Communication genres, with games like Clash of Clans, 
Subway Surfers, and Clash Royale also appearing in the list.