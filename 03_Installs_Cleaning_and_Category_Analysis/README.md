# 03 - Installs Cleaning & Category Analysis

## Goal
To identify which categories have the most installs among paid apps.

## What Happened
The `Installs` column contained non-numeric values such as `"10,000+"` and `"Free"`,
which prevented numerical aggregation from working correctly.

## 🔍 Issue Found
All values in the `Installs` column were stored as strings. Characters like `"+"` 
and `","` made it impossible to sum or sort by install count.

## 🛠️ Fix Applied
Removed `"+"` and `","` characters using `str.replace()`, replaced `"Free"` with 
`"0"`, then converted the column to integer and re-written to SQLite.

## ✅ Result
After cleaning, Family and Game are the top categories by total installs 
among paid apps, followed by Personalization and Photography.