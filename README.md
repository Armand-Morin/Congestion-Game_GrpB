# Congestion Game   
Moulon district transport modeling using SUMO traffic simulation software

<a href="https://sumo.dlr.de/docs"><img width=20% src="https://github.com/eclipse/sumo/blob/master/docs/web/docs/images/sumo-logo.svg"></p></a>


### How to use
- Download SUMO https://sumo.dlr.de
- Execute run file : sumo-gui -c osm.sumocfg
- run build.bat file to generate some xml files (by default: random trips)
- change inputs and outputs in osm.sumocfg


### DEMO

![osm train1](https://user-images.githubusercontent.com/72650161/106451107-5e92b400-6486-11eb-8bb0-e386dd91efd1.gif)



### Files explanation:

This file is used to launch the simulation
- run.bat

file for netedit
- Node file (.node.xml)
- Edge file (.edge.xml)
- Edge type file (.type.xml)
- Network from files (.net.xml)
- Route file (.rou.xml)


In this file it is necessary to specify the names of the files which will contain the data of the output simulation. It must be done between the input and output tags
- Configuration file (osm.sumocfg)
- Vehicules trips (osm.passenger.trips.xml)
- Bus stops (trips.trips.xml)

pedestrian routes on the network
- osm.pedestrian.trips.xml 


car passengers routes on the network
- osm.passenger.trips.xml


create bus lines that stop at bus stops
- osm_ptlines.xml


create bus stops
- osm_stops.add.xml


inofs about vehicles used 
- vehroutes.xml


This file will create additional output files names: edges.emissions.dump.xml / edges.traffic.dump.xml / lanes.emissions.dump.xml / lanes.traffic.dump.xml
- emissions.xml 


These files contain information on emissions and traffic
- edges.emissions.dump.xml / edges.traffic.dump.xml / lanes.emissions.dump.xml / lanes.traffic.dump.xml


contains information on travel times and waiting times
- time.xml


the following files correspond to additional xml files that represent the real demand of the people who want to go to the different schools and universities of Moulon. 
It is not the same for staff and students
- polytech_studentDemand.add.xml
- polytech_personnelDemand.add.xml
- centrale_personnelDemand.add.xml
- centrale_studentDemand.add.xml
- ens_personnelDemand.add.xml
- ens_studentDemand.add.xml
- iut_personnelDemand.add.xml
- iut_studentDemand.add.xml

### Area simulated : the area of the Moulon plateau (Centralesupelec)
![image](https://user-images.githubusercontent.com/72650161/105868306-57872400-5ff6-11eb-9796-d487fb2eb0d1.png)

### Import a Map & Convert from .osm to xml (Sumo) :
1) Open https://www.openstreetmap.or
2) Download file (does not work for big area)
3) Open folder containing osm file
4) Type cmd on the adresse bar and press enter
5) Type :  netconvert --osm-files map.osm -o test.net.xml  #(change the file name "test" before executing)
6) Open NetEdit to personalize the network
7) Load network with Sumo

###### Other Possibilities
- go to folder Sumo/tools
- type cmd on the adresse bar and press enter
- type python osmWebWizard.py
- select area (check select area)
- generate scenario

### Some Basic outputs

Sumo offers the possibility to view outputs posted on the network:

Average speed of cars on the network. (The redder it is, the faster the cars are on the road). Note that the axis of the N118 is a fast axis.
To get this output run : 
- `python "%SUMO_HOME%\tools\vizualisation\plot_net_speeds.py" -n osm.net.xml --xlim 1000,25000 --edge-width 4 -o C:\Users\Armand\Downloads\network_speeds3.png --minV 0 --maxV 20 --colormap jet`

![vitesse_reseau](https://user-images.githubusercontent.com/72650161/106245493-cf2e9c00-620c-11eb-997d-9381d6ccb606.png)

Location of red lights on the map. Allows you to view areas where there can potentially be traffic jams and high waiting times. For example, it may be interesting for an individual pressed for time not to take this route.

![feux_rouges](https://user-images.githubusercontent.com/72650161/106442537-a9f39500-647b-11eb-93e5-d754b38f677b.png)

Average CO2 emissions on the network. We can notice that some roads ‘those in green are not very polluted because few cars pass there)
To get this output various possibilities you can run one or the other : 
- `python "%SUMO_HOME%\tools\vizualisation\plot_net_dump.py" -v -n osm.net.xml --measures CO2_perVeh,CO2_perVeh   -i edges.emissions.dump.xml,edges.emissions.dump.xml --min-color-value 0 --max-color-value 40 --colormap jet`
- `python "%SUMO_HOME%\tools\vizualisation\plot_net_dump.py" -v -n osm.net.xml --measures CO2_perVeh,CO2_perVeh  --default-width 3 -i lanes.emissions.dump.xml,lanes.emissions.dump.xml --default-width 3  --min-color-value 0 --max-color-value 40 --colormap jet`
- `python "%SUMO_HOME%\tools\vizualisation\plot_net_dump.py" -v -n osm.net.xml --measures CO2_normed,CO2_normed  --default-width 10 -i lanes.emissions.dump.xml,lanes.emissions.dump.xml --default-width 2 --min-color-value 0 --max-color-value 40 --colormap #0:#00c000,.25:#408040,.5:#808080,.75:#804040,1:#c00000 --default-color #606060`
- `python "%SUMO_HOME%\tools\vizualisation\plot_net_dump.py" -v -n osm.net.xml --measures CO2_normed,CO2_normed  --default-width 10 -i lanes.emissions.dump.xml,lanes.emissions.dump.xml --default-width 2 --min-color-value 0 --max-color-value 40 --colormap #0:#00c000,.25:#408040,.5:#808080,.75:#804040,1:#c00000 --default-color #606060`
- `python "%SUMO_HOME%\tools\vizualisation\plot_net_dump.py" -v -n osm.net.xml --measures CO2_perVeh,CO2_perVeh  --default-width 3 -i edges.emissions.dump.xml,edges.emissions.dump.xml --default-width 50  --min-color-value 0 --max-color-value 40 --colormap #0:#00c000,.25:#408040,.5:#808080,.75:#804040,1:#c00000 --default-color #606060`
![CO2](https://user-images.githubusercontent.com/72650161/106442598-bed02880-647b-11eb-8ce3-2894abfa5b8e.png)

Average Nox emissions on the network
To get this output various possibilities you can run one or the other : 
- `python "%SUMO_HOME%\tools\vizualisation\plot_net_dump.py" -v -n osm.net.xml --measures NOx_normed,NOx_normed  --default-width 10 -i edges.emissions.dump.xml,edges.emissions.dump.xml --default-width 1  --min-color-value 0 --max-color-value 40 --colormap #0:#00c000,.25:#408040,.5:#808080,.75:#804040,1:#c00000 --default-color #606060`
- `python "%SUMO_HOME%\tools\vizualisation\plot_net_dump.py" -v -n osm.net.xml --measures NOx_normed,NOx_normed  --default-width 10 -i lanes.emissions.dump.xml,lanes.emissions.dump.xml --default-width 2 --min-color-value 0 --max-color-value 40 --colormap #0:#00c000,.25:#408040,.5:#808080,.75:#804040,1:#c00000 --default-color #606060`
- `python "%SUMO_HOME%\tools\vizualisation\plot_net_dump.py" -v -n osm.net.xml --measures NOx_normed,NOx_normed  --default-width 3 -i edges.emissions.dump.xml,edges.emissions.dump.xml --default-width 2  --min-color-value 0 --max-color-value 40 --colormap jet`
- `python "%SUMO_HOME%\tools\vizualisation\plot_net_dump.py" -v -n osm.net.xml --measures NOx_normed,NOx_normed  --default-width 10 -i lanes.emissions.dump.xml,lanes.emissions.dump.xml --default-width 2 --min-color-value 0 --max-color-value 40 --colormap #0:#00c000,.25:#408040,.5:#808080,.75:#804040,1:#c00000 --default-color #606060`

![edges emissions_NOx_normed](https://user-images.githubusercontent.com/72650161/106442749-f048f400-647b-11eb-9e8f-f5ee34589247.png)

Congestion with real demand and offer 
To get this output run : 
![NOX_real_demand](https://user-images.githubusercontent.com/72650161/106442837-0fe01c80-647c-11eb-8a97-5055e188dc6e.png)


### Results:
Graph showing the quantity of vehicles running on the network as a function of time. Note that there is a peak in the number of cars between 8.15am and 8.45am, which corresponds well to the high demand on the road network during this rush hour period. (The simulation starts at 8 a.m.)
To get this file run :
- `python "%SUMO_HOME%\tools\plot_summary.py" -i time.xml -o summary_running.png --xtime1 --ygrid --ylabel "running vehicles [#]" --xlabel "time" --title "running vehicles over time" --adjust .14,.1` 

![time repartition](https://user-images.githubusercontent.com/72650161/106441773-c04d2100-647a-11eb-8a52-82e3ca2ee8ad.png)

This graph represents the histogram of the distribution of the travel times of individuals on the Moulon network. We notice that most individuals make a journey of less than 6 minutes which shows that the journey is rather fluid on the Moulon.
To get this file run : 
- `python "%SUMO_HOME%\tools\plot_tripinfo_distributions.py" -i true.xml -o tripinfo_distribution_duration.png -v -m duration --minV 0 --maxV 3600 --bins 10 --xticks 0,3601,360,14 --xlabel "duration [s]" --ylabel "number [#]" --title "duration distribution" --yticks 14 --xlabelsize 14 --ylabelsize 14 --titlesize 16 -l mon,tue-thu,fri,sat,sun --adjust .14,.1 --xlim 0,3600`

![tripduration](https://user-images.githubusercontent.com/72650161/106441804-cc38e300-647a-11eb-8845-b4ec38a4e537.png)


### Resources used:
- [SUMO DOC](https://sumo.dlr.de/docs)
- [SUMO TUTORIALS](https://sumo.dlr.de/docs/Tutorials.html)


