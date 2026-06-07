# 📊 Learning Analytics Dashboard: Identifying Student Intervention Thresholds

## 🎯 Project Overview & Objective
Educational institutions track massive volumes of digital footprints through Virtual Learning Environments (VLEs), but this clickstream data is rarely utilized in real-time. This project transforms raw, noisy clickstream interactions (over 10 million rows) into an actionable institutional tool using **Tableau Desktop** and **Advanced Relational Data Modeling**.

Rather than waiting for a student to fail a mid-semester exam or drop out entirely, this dashboard uncovers early **behavioral drop-off windows** and engagement patterns across different course types. This enables academic advisors and student success teams to launch proactive, automated interventions before a student falls behind.

👉 [Click to Explore the Dashboard](https://public.tableau.com/views/E_Learning_Dashboard/LearningAnalyticsDashboardStudentEngagementOULAD?:language=en-US&:sid=&:redirect=auth&:display_count=n&:origin=viz_share_link)

## 🛠️ Data Architecture & Engineering Process
Before building any visual components, significant data structural challenges within the Open University Learning Analytics Dataset (OULAD) had to be architected and resolved to preserve analytical integrity:

### 1. Eliminating the Cartesian Product (Data Multiplicity Glitch)
* **The Challenge:** Directly combining granular daily interaction logs (`studentVle`), student demographics, and course structures initially triggered a massive data-multiplication error. This artificially inflated click counts into the hundreds of millions.
* **The Engineering Fix:** Modeled a strict relational schema inside Tableau's modeling canvas. Instead of a single blunt join, tables were bound across complex, multi-field composite relationship links using `Id Site`, `Code Module`, and `Code Presentation`. This successfully isolated granular dimensions and preserved the true row-level counts.

### 2. User Experience (UX) Translation Layer
* **The Challenge:** The raw database stored course identifiers as cryptic, non-descriptive codes (e.g., Module `BBB`, Module `FFF`). This made the interface completely unreadable for a university advisor.
* **The Engineering Fix:** Implemented clean institutional domain aliases based on metadata characteristics:
  * **Social Sciences / Humanities (`BBB`, `AAA`):** Tagged as *Essay-Based* modules.
  * **STEM (`FFF`, `CCC`):** Tagged as *Applied Science & Laboratory* modules.

---

## 📈 Key Behavioral Insights Discovered

### 📉 The 30-Day "Critical Drop-Off Window" (Humanities)
By analyzing the continuous timeline (normalized to `Day 0` as the official start date of the semester across staggered presentations), a major human behavioral pattern emerged. 
* In massive humanities courses like **`BBB`**, a steep decline in student activity occurs uniformly within the first 30 days.
* **Root Cause Identification:** Cross-referencing the daily activity mix revealed that a sharp, early-semester abandonment of **discussion forums** and **digital textbook reading (`oucontent`)** is the leading behavioral signature of an at-risk student pulling away.

---

## 🎨 Dashboard Architecture & Interactive UX Features

The interface is architected using strict professional visualization layouts to minimize cognitive load and maximize dashboard scannability:

```text
+-----------------------------------------------------------------------------------------+
|  LEARNING ANALYTICS DASHBOARD: Identifying Student Intervention Thresholds               |
+-----------------------------------------------------------------------------------------+
|                                                           | [Filter: Select Course]     |
|   [CHART 1: VLE ENGAGEMENT HEARTBEAT]                     |                             |
|   - Continuous Timeline (Course Days)                     | [Slider: Milestone Day]     |
|   - Interactive Vertical Milestone Reference Line         |                             |
|                                                           | [Legend: Result Status]     |
+-----------------------------------------------------------+-----------------------------+
|                                                                                         |
|   [CHART 2: TOTAL CLICK DISTRIBUTION BY ACTIVITY TYPE]                                  |
|   - Horizontal Bar Chart reflecting Material Mix Dynamics                               |
|   - Two-Tone Professional Color Palette                                                 |
|                                                                                         |
+-----------------------------------------------------------------------------------------+
```

1. **The VLE Engagement Heartbeat (Top):** A macro-level timeline mapping continuous course days. It features an interactive **Course Milestone Slider Parameter** allowing users to glide a vertical reference line across standard academic checkpoints (`Day 30`, `60`, `120`, `180`, `240`) to inspect structural phases dynamically.
2. **Total Click Distribution (Bottom):** A micro-level horizontal bar chart reflecting the exact mix of digital materials students interacted with. It utilizes a clean, desaturated, professional color palette separating baseline interaction from core communicative tools.
3. **Global Synchronization:** All filters are mapped dynamically across separate worksheets. Changing a course module dropdown automatically triggers an instantaneous, synchronized layout update across the heartbeat timeline and the activity bar chart.

---

## 💡 Strategic Institutional Recommendations
Based on the operational insights surfaced by this analytical tool, the following interventions are recommended for university stakeholders:

* **Automated Day-30 Triggers:** Configure the Learning Management System (LMS) to automatically flag students in Humanities modules who display fewer than a defined threshold of forum clicks by Day 30 for immediate academic advisor outreach.
* **Resource Realignment:** Shift instructional design priorities toward creating more engaging, short-form interactive digital materials in modules displaying high early-semester attrition to bridge the initial engagement gap.

