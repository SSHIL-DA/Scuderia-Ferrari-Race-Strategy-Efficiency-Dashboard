#  Scuderia Ferrari Performance & Strategic Insights Dashboard

An interactive, multi-page Power BI dashboard designed to analyze Scuderia Ferrari's performance in Formula 1 (2010–Present). Moving beyond simple points accumulation, this report delivers a high-level **Performance & Reliability Audit**, measuring race execution efficiency, driver pace progression, and spatial dominance across global circuits.

---

##  Project Overview & Key Questions

The primary objective of this project is to answer high-level strategic questions for race analysts and executive stakeholders:
1. **Execution Efficiency:** How effectively does the team convert front-row qualifying starts (`Grid <= 3`) into podium finishes (`Position <= 3`)?
2. **Qualifying vs. Race Pace:** Are drivers gaining or losing positions from start to finish?
3. **Reliability Impact:** What proportion of non-finishes are driven by mechanical failures versus on-track incidents?
4. **Geographic Strengths:** Which circuits yield the highest historical points return?

---

##  Key Features & Technical Highlights

* **Data Modeling & Transformation:** Cleaned and structured relational F1 data tables (`Results`, `Races`, `Drivers`, `Constructors`, and `Status`).
* **Custom DAX Measures:** Formulated advanced DAX calculations using `CALCULATE`, `FILTER`, `DIVIDE`, and conditional logic to evaluate conditional KPIs without division-by-zero errors.
* **Dynamic Image UI:** Integrated dynamic **Driver Flags** and **Profile Photos** using image URLs mapped directly within DAX variables.
* **Density & UX Optimization:** Custom-formatted data label placement, overflow text handling, and color palettes matching the official Scuderia Ferrari aesthetic.

---

##  Dashboard Architecture

### Page 1: Overview & Yearly Trajectory
* **Macro Metrics:** Total points, overall race wins, and total podiums.
* **Ferrari Yearly Trajectory (Line Chart):** Year-over-year performance trends tracking points development across seasons.
* **Top 5 Drivers (Bar Chart):** Historical points leaderboard by driver.

### Page 2: Strategic Insights & Race Execution
* **Podium Execution Rate (Gauge Chart):** A conditional KPI measuring conversion rate from top 3 qualifying spots to podium finishes.
* **Average Start vs. Average Finish (Clustered Bar Chart):** Driver pace delta analysis identifying position gain/loss per driver.
* **Reliability Breakdown (Donut Chart):** Categorized distribution of race finishes vs. Mechanical/Incident DNFs.
* **Circuit Performance Mapping (Bubble Map):** Geographic footprint highlighting Ferrari’s strongest circuits globally.

---

##  Key DAX Formula Examples

**Podium Execution Rate (%)**
```dax
Starts in Top 3 = 
CALCULATE(
    COUNT(results[resultId]), 
    results[grid] <= 3 && results[grid] > 0
)

Podium Conversions = 
CALCULATE(
    COUNT(results[resultId]), 
    results[grid] <= 3 && 
    results[grid] > 0 && 
    results[positionOrder] <= 3
)

Podium Execution % = 
DIVIDE([Podium Conversions], [Starts in Top 3], 0)
