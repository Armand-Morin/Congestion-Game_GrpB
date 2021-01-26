## Congestion Game
Moulon district transport modeling using SUMO traffic simulation software

<a href="https://sumo.dlr.de/docs"><img width=20% src="https://github.com/eclipse/sumo/blob/master/docs/web/docs/images/sumo-logo.svg"></p></a>

## How to use
- Download SUMO https://sumo.dlr.de
- Execute run file

## Area simulated :
![image](https://user-images.githubusercontent.com/72650161/105868306-57872400-5ff6-11eb-9796-d487fb2eb0d1.png)

# Doc:
- [SUMO](https://sumo.dlr.de/docs/Tutorials.html)



# Files explanation:
- Node file (.node.xml)
- Edge file (.edge.xml)
- Edge type file (.type.xml)
- Network from files (.net.xml)
- Route file (.rou.xml)
- Configuration file (.sumo.cfg)
- ....

# Import a Map & Convert from .osm to xml (Sumo) :
1- Open https://www.openstreetmap.or
2- Download file (does not work for big area)
3- Open folder containing osm file
4- Type cmd on the adresse bar and press enter
5- Type :  netconvert --osm-files map.osm -o test.net.xml  #(change the file name "test" before executing)
6- Open NetEdit to personalize the network
7- Load network with Sumo
