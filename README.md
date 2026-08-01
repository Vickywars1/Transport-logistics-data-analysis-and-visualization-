# Voyage Line City Transit — Ridership and Performance Analytics Dashboard

Tools used: Power BI, Power Query, DAX, Data Modeling

Project Overview
Voyage Line City Transit runs a 10 route city bus network served by a 40 bus fleet. This project turns four raw operational tables, covering routes, buses, rider demographics, and individual ridership records, into a two page interactive Power BI dashboard. It lets planning and operations teams monitor ridership, revenue, and demand patterns at both the network level and the individual route level.

Objective
Transit planners need to answer three recurring questions. Where are our riders coming from, who are they, and when do they travel. This dashboard was built to answer all three in one interactive view, and to surface where bus capacity is mismatched with actual demand.

Data and Modeling Approach
The source data was structured as four related tables. Routes, one row per route, with fields like RouteID, RouteName, Start and End Location, Trip Fee, and Scheduled Times. Buses, one row per bus, with BusID, RouteID, Bus Number, and Seating Capacity. Demographics, one row per rider, with RiderID, Age, Gender, and Occupation. Ridership, one row per trip record, with RecordID, BusID, RiderID, Date, Time, and Number of Riders.

Modeling steps included building a star schema style model in Power BI, relating the Ridership fact table to Buses, Routes, and Demographics through BusID, RouteID, and RiderID. Power Query was used to clean and shape the data, and to derive calculated columns for Age Group in 10 year bands, Time Range buckets in six 3 hour windows, and Weekday extracted from the trip date. A Bus Utilization Category measure was built to compare each bus's average riders against its seating capacity and classify it as Underutilized, Properly Utilized, or Overutilized, turning raw headcounts into an operational signal. DAX measures were written for Total Riders, Average Riders per Bus, Total Revenue calculated as the sum of Number of Riders times Trip Fee, Total Trips, Peak and Down Hour of Operation, and a period over period ridership comparison. Interactive slicers for Gender and Route, plus a Top 5 and Bottom 5 buses toggle, let the same report serve both a network wide overview and route level deep dives.

Key Insights

Network performance across all routes. The network carried 6,587 riders across 200 trips, generating an estimated 183.13 thousand dollars in fare revenue, at an average of about 33 riders per bus. Ridership is concentrated on a handful of routes. East West Express at 20 percent and Central Line at 19 percent together account for nearly 40 percent of all riders, while North Circular and South Line trail far behind at 3 percent each, roughly a 7 times gap between the busiest and quietest routes. Five buses, numbers 4, 28, 27, 21, and 38, consistently outperform the fleet, each carrying between 260 and 325 riders, suggesting these routes and time slots are prime candidates for additional capacity.

Rider demographics. The rider base skews slightly female at 35 percent versus male at 32 percent, with a notable 33 percent captured under Other, worth revisiting as a data quality item. Occupation splits fairly evenly across Other at 25 percent, Professional at 24 percent, and Self Employed at 20 percent, with Students at 7 percent and Retirees at 9 percent the smallest segments. The core ridership age band is 30 to 59 years old, making up 43 percent of all riders, with an average rider age of 43, while riders 70 and older are a negligible 2 percent. Each occupation segment has a distinct peak travel hour, for example Retirees peak at 8:50 AM, Professionals at 11:41 AM, and Students, Self Employed, and Other cluster in the evening between 4:55 PM and 11:16 PM, indicating clearly separable commuter versus leisure and off peak travel behavior.

Route level deep dive on Airport Express. Filtered to this single route, it carried 754 riders at 30.16 riders per bus, with demand peaking sharply around 1:34 PM at 56 passengers and dropping to its lowest around 7:50 PM at 15 passengers, a single well defined midday peak rather than the classic AM and PM commuter double peak. Weekday demand is uneven. Saturday at 169 and Tuesday at 148 are the strongest days, while Monday at 41 is the weakest, nearly a 4 times swing across the week, which is unusual for a route named Express and worth investigating for event travel, flight schedules, or work week effects. Of the buses assigned to this route, the Bus Utilization Category split, 3 Properly Utilized, 2 Overutilized, and 2 Underutilized, shows capacity is already imbalanced on a single route, a pattern likely repeated elsewhere in the network. The ridership dataset covers a short one month window from December 2023 to January 2024. The negative 76.6 percent year over year figure shown on the dashboard reflects a period over period comparison across that boundary, 611 riders in the December 2023 slice versus 143 in the January 2024 slice, rather than a full 12 month trend, and should be read as an early signal rather than a confirmed seasonal decline.

Business Recommendations

Rebalance fleet allocation toward high demand routes. East West Express and Central Line together drive about 40 percent of ridership. Shifting spare buses from North Circular and South Line toward these routes, especially during their identified peak windows, could reduce overcrowding without adding fleet cost.

Right size buses per time of day, not just per route. Airport Express's single sharp midday peak at 1:34 PM followed by a steep evening drop off suggests smaller buses or reduced frequency after 6 PM would cut operating cost with minimal service impact.

Investigate the Airport Express weekday swing. A 4 times gap between Saturday and Monday demand warrants a root cause check, such as flight schedules, weekend leisure travel, or fare promotions, before assuming it generalizes to other routes.

Use the Bus Utilization Category as an ongoing operations metric. Rolling this classification out across all routes, not just Airport Express, would give planners a standing early warning signal for reallocating buses before overcrowding or empty running becomes a recurring cost.

Clean up the Other gender category. At 33 percent of riders, Other is nearly as large as the two primary categories combined, which limits how useful gender based segmentation can be. Refining data collection here would sharpen future targeting decisions.

Limitations
The ridership data spans roughly one month, which is enough to establish daily, weekly, and hourly patterns but too short to validate genuine seasonal or year over year trends. Revenue is estimated from trip fee times riders per trip and does not account for discounts, passes, or fare variation by rider type.
