# SoA-CapstoneProject

Parking Lot Dynamic Pricing Project
Project Overview
This project demonstrates real-time dynamic pricing for parking lots using streaming data and interactive visualization. The solution is implemented entirely in a Jupyter notebook (or Google Colab), leveraging Pathway for data streaming and Bokeh for live plotting.

Project Structure
All code is contained in the notebook.

Key Functions:

baseline_pricing: Implements simple linear pricing based on occupancy.

demand_pricing: Extends baseline logic with additional demand factors.

Data Streaming: Utilizes Pathway to read and stream dataset.csv in real time.

Visualization: Bokeh plots update live via a callback as new data arrives.

Pricing Models
Baseline Model
Formula:

price
=
base_price
+
(
max_price
−
base_price
)
×
(
occupancy
capacity
)
price=base_price+(max_price−base_price)×( 
capacity
occupancy
 )
Defaults:

base_price = $5

max_price = $15

Interpretation:

An empty lot costs $5.

A full lot costs $15.

Demand-Based Model
Extends the baseline model by adding weighted factors:

Occupancy fraction

Queue length (e.g., +$1 per waiting car)

Traffic level

Special day flag (e.g., +$5)

Vehicle type

Effect:

Higher demand (heavy traffic, long queues, special days) increases the price accordingly.

Competitive Model (Optional)
Not fully implemented.

Concept:

Identify nearby lots using latitude/longitude.

Compare prices and adjust: lower if competitors are cheaper, raise if they are higher.

Data Flow
Streaming Simulation:

Uses Pathway’s demo.replay_csv to simulate real-time data from dataset.csv.

Processing:

Each parking update triggers computation of both pricing models.

Results are output and visualized in real time.

Subscription:

pw.io.subscribe reacts to each new row, updating the Bokeh plot.

Visualization Details
Tool: Bokeh with output_notebook() for interactive charts in Colab/Jupyter.

What You’ll See:

A line plot for each parking lot (14 in total).

Blue Line: Baseline Pricing (occupancy only).

Red Line: Demand-Based Pricing (multiple features).

Navigation:

Scroll through vertically stacked plots to analyze trends across all lots.

Customization:

Add more lines for different lots, change colors, or group by lot as needed.

How to Run the Notebook
Ensure dataset.csv is present.

Install required packages:

python
!pip install pathway bokeh pandas numpy
Run notebook cells in order:

Execute imports.

Define pricing functions and the streaming pipeline.

Run the subscription/callback cells.

Visualization:

The Bokeh chart will fill in as the simulated stream runs.

Assumptions & Notes
Numeric mappings are used for traffic and vehicle type.

No synthetic data is generated; only columns from dataset.csv are used.

All lots are handled in one stream; each event is plotted with its own timestamp.

Advanced grouping (e.g., by lot) and more efficient streaming/windowing can be implemented for larger datasets.

Further Work
Competitive Model:

Precompute distances between lots.

Gather and compare nearby lots’ prices (via join in Pathway or preloaded static data).

Scalability:

For very large data, consider more efficient streaming or windowing as shown in Pathway examples.

Where to Place the Visualization Code
After loading and processing the dataset with Pathway and computing the pricing table, insert the provided visualization code block.

This block:

Uses Pathway’s live streaming subscription (pw.io.subscribe).

Automatically routes updates to 14 separate Bokeh plots.

Runs inside Google Colab/Jupyter with output_notebook() enabled.

Plot Legend
Blue Line: Baseline Pricing

Red Line: Demand-Based Pricing

You can scroll through the vertically stacked plots to analyze pricing trends across all parking lots in real time.
