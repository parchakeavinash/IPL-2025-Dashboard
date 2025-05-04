# IPL-2025-Dashboard

## Project Overview:
### Home Page
![image](https://github.com/user-attachments/assets/f05891b3-8a78-4264-8881-2ea90ad479c4)
### Overview page
![image](https://github.com/user-attachments/assets/38534b4d-d23a-45fc-ad6e-21ea817083c8)
### point tabel page
![image](https://github.com/user-attachments/assets/8b010931-a7ee-4a00-8bd7-8c0dd9545dff)
### Squad page
![image](https://github.com/user-attachments/assets/3db891ad-681c-4780-baa0-36eda837ad5b)
![image](https://github.com/user-attachments/assets/c3f87981-48ec-4d60-b03d-1ae2307908c8)
![Uploading image.png…]()

# 🏏 Real-Time IPL Dashboard using CricAPI + Power BI

This project demonstrates how to build a **real-time IPL dashboard** by integrating **CricAPI** for live cricket data and **Power BI** for visualization. Additionally, it features custom **HTML Match Cards** using **DAX + HTML** for a professional, live match UI.

---

## 📦 Data Sources

All data is fetched from [CricAPI](https://cricketdata.org/). Replace `YOURKEY` with your actual API key.

| 🔗 API Purpose       | 🔗 URL |
|----------------------|--------|
| 🟢 Live Match Scores | `https://api.cricapi.com/v1/cricScore?apikey=YOURKEY` |
| 📊 IPL Points Table  | `https://api.cricapi.com/v1/series_points?apikey=YOURKEY&id=d5a498c8-7596-4b93-8ab0-e0efc3345312` |
| 📅 IPL Series Info   | `https://api.cricapi.com/v1/series_info?apikey=YOURKEY&id=d5a498c8-7596-4b93-8ab0-e0efc3345312` |

> 📝 The series ID above is specific to **IPL 2025**.

---

## 🔧 Steps to Load API Data into Power BI

### ✅ Step 1: Get Data from Web  
- Open **Power BI Desktop**
- Go to **Home > Get Data > Web**
- Select the **Basic** option and paste the API URL

### 🔁 Step 2: Convert and Transform JSON  
- Use the **Navigator** pane to explore the JSON
- If it's a list, click **Convert to Table**
- Use **Expand Columns** to flatten nested fields
- Repeat this for each of the 3 APIs

### 🧠 Recommended Query Names
- `LiveScores`
- `PointsTable`
- `MatchSchedule`

---

## 📊 What You Can Build

| Visual Type        | Source API     |
|--------------------|----------------|
| 🔴 Live Match Card | `cricScore`    |
| 📈 Points Table    | `series_points`|
| 🗓️ Match Schedule | `series_info`  |

Add visuals like:
- Cards
- Tables
- Slicers
- Timelines

---

## 🎨 Build Dynamic HTML Match Cards (Power BI)

Create modern, branded match cards using a DAX measure that outputs raw HTML + CSS.

### 🧩 Sample DAX Measure:

```dax
Cards = 
"<!DOCTYPE html>
<html>
<head>
    <style>
        body { font-family: Arial; display: flex; justify-content: center; align-items: center; height: 100vh; }
        .card { background: white; padding: 15px; border-radius: 10px; width: 350px; margin-bottom: 10px; }
        .header { font-size: 14px; color: gray; font-weight: bold; }
        .teams { display: flex; justify-content: space-between; margin: 10px 0; }
        .team { display: flex; align-items: center; font-size: 16px; font-weight: bold; }
        .team img { width: 25px; height: 25px; margin-right: 8px; border-radius: 50%; }
        .score { font-size: 16px; font-weight: bold; color: #444; }
        .status { font-size: 14px; color: gray; margin-top: 5px; }
    </style>
</head>
<body>
    <div class='card'>
        <div class='header'>" & All_Matches_Score[ms] & " • " & All_Matches_Score[matchType] & " • Start: " & FORMAT(All_Matches_Score[dateTimeGMT],"dd-mmm-yy - hh:mmAM/PM") & "</div>
        <div class='teams'>
            <div class='team'>
                <img src='" & All_Matches_Score[t1img] & "'>
                " & All_Matches_Score[t1_SN] & "
            </div>
            <div class='score'>" & All_Matches_Score[t1s] & "</div>
        </div>
        <div class='teams'>
            <div class='team'>
                <img src='" & All_Matches_Score[t2img] & "'>
                " & All_Matches_Score[t2_SN] & "
            </div>
            <div class='score'>" & All_Matches_Score[t2s] & "</div>
        </div>
        <div class='status'>" & All_Matches_Score[status] & "</div>
    </div>
</body>
</html>"
```
### Sample output:
![image](https://github.com/user-attachments/assets/5d626f23-b424-412c-b30d-9f50462f6db6)

✅ Final Tips
🔗 Use valid image URLs for team logos

🙌 Acknowledgments
CricAPI – for real-time cricket data
Power BI – for visualization

🕒 Use FORMAT() for clean date-time display

🔄 Enable Auto-Refresh in Power BI Service

🧩 Use visuals that support raw HTML (e.g., HTML Viewer by OKViz)
