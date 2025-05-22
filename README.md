Cairo Traffic Optimization System

Overview

The Cairo Traffic Optimization System is a web-based application designed to enhance urban mobility in Cairo, Egypt, by leveraging advanced graph algorithms and data visualization. Built with Streamlit, it provides tools for infrastructure planning, traffic flow optimization, emergency response routing, public transit scheduling, and real-time traffic signal control. The system integrates datasets on neighborhoods, facilities, roads, traffic flow, and transit demand to deliver actionable insights for city planners and traffic managers.

Key Features





Infrastructure Network Design: Uses Minimum Spanning Tree (MST) algorithms (Kruskal's or Prim's) to design cost-effective road networks, prioritizing high-population areas and critical facilities.



Traffic Flow Optimization: Employs Dijkstra's algorithm with time-dependent modifications to find optimal and alternative routes based on traffic conditions and road quality.



Emergency Response Planning: Utilizes A* search with signal preemption to minimize response times for medical, fire, and police emergencies.



Public Transit Optimization: Applies dynamic programming to optimize metro and bus routes, schedules, and resource allocation, enhancing passenger coverage and efficiency.



Greedy Traffic Signal Control: Implements real-time signal optimization with emergency vehicle preemption to reduce congestion at major intersections.



Interactive Visualizations: Offers maps (Folium), network graphs (Plotly), and charts to visualize routes, traffic patterns, and performance metrics.

Prerequisites

Before running the application, ensure you have the following installed:





Python 3.8+



pip (Python package manager)



A modern web browser (e.g., Chrome, Firefox) for viewing the Streamlit interface.

Installation





Clone the Repository

git clone https:https://github.com/Eyad-Elnakib/Cairo_traffic
cd cairo-traffic-optimization



Create a Virtual Environment (recommended)

python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate



Install DependenciesInstall the required Python packages listed in requirements.txt. If not provided, use the following command to install the core dependencies inferred from the code:

pip install streamlit pandas numpy folium networkx plotly pulp scipy



Prepare Data FilesThe application requires the following datasets (assumed to be in CSV format, based on app.py):





neighborhoods.csv: Contains neighborhood data (ID, Name, Population, X, Y, Type).



facilities.csv: Lists facilities (ID, Name, Type, X, Y).



existing_roads.csv: Details existing roads (FromID, ToID, Distance(km), Current Capacity(vehicles/hour), Condition(1-10)).



potential_roads.csv: Lists potential new roads (FromID, ToID, Distance(km), Estimated Capacity(vehicles/hour), Construction Cost(Million EGP)).



traffic_flow.csv: Provides traffic data (FromID, ToID, Morning Peak(veh/h), Afternoon(veh/h), Evening Peak(veh/h), Night(veh/h)).



metro_lines.csv: Contains metro line data (LineID, Name, Stations(comma-separated IDs), Daily Passengers).



bus_routes.csv: Lists bus routes (RouteID, Stops(comma-separated IDs), Daily Passengers, Buses Assigned).



transit_demand.csv: Details transit demand (FromID, ToID, Daily Passengers).

Place these files in a data/ directory within the project root or update the load_data() function in data_loader.py to point to your data location.

Running the Application





Start the Streamlit ServerRun the main application script (app.py):

streamlit run app.py



Access the ApplicationOpen your web browser and navigate to http://localhost:8501. The Streamlit interface will display the Cairo Traffic Optimization System.

Usage Instructions

The application is organized into six modules, accessible via the sidebar navigation. Below is a guide to using each module.

1. Overview





Purpose: Provides a high-level view of Cairo's traffic system, including geographic distribution, road network, and traffic patterns.



How to Use:





View the interactive map showing neighborhoods, facilities, and roads.



Explore the network graph visualizing connectivity.



Review statistics (e.g., total population, number of roads, facilities).



Analyze the road condition distribution and traffic flow patterns by time of day.

2. Infrastructure Network Design





Purpose: Designs an optimized road network using MST algorithms, balancing connectivity, cost, and priority for populated areas and facilities.



How to Use:





Select the algorithm (Kruskal's or Prim's).



Adjust sliders for Population Weight Factor (0.0–1.0) and Critical Facility Priority (1.0–3.0).



Check Include Potential New Roads and set a Max Budget (in Million EGP).



Click Run MST Analysis to generate the optimized network.



View the resulting map, network metrics (travel time, distance, connectivity), cost analysis, and a table of recommended new roads.

3. Traffic Flow Optimization





Purpose: Finds optimal and alternative routes between two points, considering traffic conditions and road quality.



How to Use:





Select Origin and Destination from the dropdowns (neighborhoods or facilities).



Choose a Time Period (Morning Peak, Afternoon, Evening Peak, Night).



Enable/disable Consider Traffic Conditions and adjust the Congestion Factor (1.0–3.0) if enabled.



Enable/disable Consider Road Quality.



Click Find Optimal Route to display:





A map showing the optimal (blue) and alternative (green) routes.



Metrics for distance and travel time for both routes.



A bar chart comparing traffic levels on each route segment.



Step-by-step directions for both routes.

4. Emergency Response Planning





Purpose: Plans routes for emergency vehicles (medical, fire, police) with signal preemption to minimize response time.



How to Use:





Select Emergency Type (Medical Emergency, Fire, Police).



Choose Emergency Response Origin (facility) and Incident Location (neighborhood).



Select a Time Period.



Adjust Priority Level (1–5) and enable/disable Route Clearing.



Click Find Emergency Route to view:





A map with the emergency route (red) and regular route (orange).



Metrics comparing emergency and regular route times, plus total time saved.



A table detailing signal preemption at intersections.



Step-by-step directions for both routes.



A list of critical intersections for priority.

5. Public Transit Optimization





Purpose: Optimizes public transit routes, schedules, and network design to improve coverage and efficiency.



How to Use:





Route Analysis Tab:





Select Transit Type (Metro, Bus, All) and a specific route.



Choose Optimize For (Passenger Capacity, Travel Time, Resource Efficiency).



For bus routes, adjust Number of Buses.



Click Analyze Route to see the route map, performance metrics, recommended changes, and stop details.



Schedule Optimization Tab:





Select a Transit Line (e.g., M1 - Line 1) and Day Type (Weekday, Weekend, Holiday).



Choose Peak Hours and set Resource Constraint (%).



Click Optimize Schedule to compare current and optimized schedules, with charts and metrics.



Transit Demand Tab:





View a heatmap of transit demand, top demand routes, and coverage statistics.



Explore the transit stop coverage map.



Integrated Network Design Tab:





Set Maximum New Routes and Maximum Budget.



Optionally specify Fleet Availability (e.g., number of buses).



Click Design Integrated Network to see the proposed network map, coverage improvements, cost estimates, and recommendations.

6. Greedy Traffic Signal Control





Purpose: Optimizes traffic signals at major intersections and supports emergency vehicle preemption.



How to Use:





Intersection Analysis Tab:





View a table of major intersections with details (ID, Name, Type, Connecting Roads, Importance Score).



Explore a map highlighting intersection locations.



Signal Optimization Tab:





Select a Time Period.



Enable/disable Emergency Preemption and Adaptive Signal Timing.



Adjust Minimum Intersection Importance.



Click Optimize Traffic Signals to see signal timing results, detailed phase information, and charts for a selected intersection.



Emergency Preemption Tab:





Run signal optimization first.



Select Emergency Type, Emergency Vehicle Origin, Incident Location, and Time Period.



Click Simulate Emergency Response to view the emergency route, response analysis, and preemption details.

Data Requirements

Ensure the datasets are correctly formatted with the expected columns (as described in Installation). Missing or malformed data may cause errors. The data_loader.py module (not provided but referenced in app.py) should handle loading these files.

Troubleshooting





Streamlit not launching: Verify Streamlit is installed (pip install streamlit) and run streamlit run app.py from the project directory.



Data loading errors: Check that all required CSV files are in the data/ directory and match the expected schema.



Visualization issues: Ensure folium and plotly are installed and that your browser supports JavaScript.



Performance issues: For large datasets, consider reducing the number of nodes/edges or optimizing the data preprocessing steps.



Built with ❤️ by the Cairo Traffic Optimization Team
