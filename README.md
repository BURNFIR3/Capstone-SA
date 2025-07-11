# Capstone-SA

# Project Overview

Dynamic Pricing for Urban Parking Lots is a real time simulation project built using streaming data and basic ML logic to dynamically adjust parking prices across urban locations. The aim is to improve utilization by adjusting prices based on factors like occupancy, queue length, traffic, and special days.

This system mimics a smart pricing engine that adjusts parking rates in response to fluctuating demand and external conditions, all in real time.


# Tech Stack Used
Pandas
Numpy
Pathway
Bokeh
Panel

```mermaid
graph TD
    A[CSV File: Streaming Parking Data] --> B[Pathway Replay CSV]
    B --> C[Parse Timestamp & Group by Day]
    C --> D[Windowed Aggregation (1-day Tumbling Window)]
    D --> E[Apply Smart Pricing Function]
    E --> F[Bokeh Plot via Panel]
    F --> G[Live Dashboard / Output]
```


# Architecture & Workflow Explanation

Input Data (CSV)
  Raw parking data is streamed using Pathway from a CSV file containing fields like:

  Timestamp, Occupancy, Capacity

  QueueLength, TrafficConditionNearby, IsSpecialDay

  Time Parsing & Grouping
  Timestamps are parsed and data is grouped by day using Pathway temporal utilities.

  Windowing
  A tumbling window of 1 day is applied to aggregate key metrics like:

  Maximum Occupancy, Queue Length, Traffic, and more.

  Dynamic Pricing Logic
  A smart pricing function is applied:

price = 10 + 5*(Occupancy/Capacity) + 0.5*QueueLength - 0.3*Traffic + (2 if SpecialDay else 0)

The final price is bounded between $8 and $20.

Visualization
Real-time pricing is visualized using Bokeh (line + dot plot), served via Panel.

Live Simulation
The pipeline runs via pw.run() and displays dynamic price trends per day.


# Additional Documentation

    Data Format
    Ensure your CSV contains:

Timestamp, Occupancy, Capacity, QueueLength, TrafficConditionNearby, IsSpecialDay

Pathway Schema
Must match the data structure exactly.

Customization
You can expand the pricing model to:

    Include VehicleType pricing

    Add rerouting logic

    Implement multi-lot competition
