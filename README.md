# traccarKmlFlow
Node-Red Flow to create a KML Network Link of Traccar Client device locations.

![flow](/traccarKmlFlow1.png?raw=true "Node Red Flow")

REQUIREMENTS:

-Node-Red Server

-node-red-dashboard (node)

-Traccar Server

----------------------------

SETUP NODE-RED:

-https://nodered.org/docs/getting-started/

-options include installing node-red on your local PC, a Raspberry Pi or similar single board computer or mini PC, deploying node-red on a cloud server or virtual private server (VPS), Docker Container, or local virtual environment. After installing node-red you should be able to go to the node-red dashboard at http://node-red-ip-address:1880 you may have to open appropriate ports (1880) to allow devices to access the node-red dashboard.

-ensure you install the "node-red-dashboard" node. If not there should be a prompt when you import traccarKmlFlow in Node-Red that there are nodes that need to be installed and will automatically install them for you if you allow. In the event that isnt the case, in Node-Red: Menu (3 horizontal lines) > Manage palette > Install > Search "node-red-dashboard" > Install > Install

-----------------------------

IMPORT .JSON FLOW TO NODE RED:

-in GitHub: click on "traccarKmlFlow.json" > click on the download icon "Download raw file" > note where the "traccarKmlFlow.json" file downloaded to, default is in your Downloads folder

-in Node-Red: click on menu icon (3 horizontal lines top right) > click on "Import" > click on "select a file to import" > go to Downloads folder and click on "traccarKmlFlow.json" > Upload > Import

ALTERNATIVELY..

-you can just copy the whole "traccarKmlFlow.json" code from GitHub and paste it into the Node-Red Import Clipboard.

--------------------------------

SETUP TRACCAR SERVER:

-https://www.traccar.org/download/

-Traccar Server can be hosted on various platforms: Raspberry Pi, Mini PCs, your local PC, Cloud Servers or Virtual Private Servers (VPS), Docker Containers, or Virtual Environments.

--------------------------------

CONFIGURE BOTH HTTP NODES:

-in Node-Red: input your Traccar Server IP address and port (default port is 8082) for both http req nodes

--------------------------------

USING THE TRACCARKMLFLOW:

-network KML link will be: http://node-red-ip-address:1880/traccar.kml

-this can be used with various mapping applications that accept network KMLs such as Google Earth and ATAK.

---------------------------------

HOW THE TRACCARKMLFLOW WORKS:

-the http in node creates the endpoint of http://...traccar.kml, so when a device queues it via KML network link it will then request device and position information from traccar server of all devices. Sort the devices and position information by position ID, join the sorted device and positions, sort the joined array of all devices and positions and then sort them again by attaching the correct device with the correct position information and sending it as a separate payload. The if/else node chooses which icon (shape/color) best suites the status of the device to be placed on the map, additionally the node also starts to consolidate the important information that needs to get put into the KML readable format. The join node gathers all the devices after running through the if/else to then be joined with another join node which helps place the traccar devices into XML Placemark. Add devices to kml node then grabs the XML Placemark payload for all devices and stores them in the appropriate Placemark array. Format payload fixes how its structured by taking away the fact that all the info is in one array element and not an object (I asked too much of array manipulation throughout the flow and this is it coming back to bite me). The XML node parses the data so instead of a json object its in xml tag which turns the whole payload into readable KML. Host kml provides the response of this readable KML.

--------------------------------

TEST / TROUBLESHOOT FLOW:

-http://node-red-ip-address:1880/test.kml

-the test / troubleshoot flow below is for any data manipulation you want to test out to add any styling to icons or remarks etc.

----------------------------------

TROUBLESHOOTING / KNOWN ISSUES:

-in the event the Node-Red service explodes and you lose connection to the Node-Red UI and cant reconnect, you may need to restart your Node-Red service

$ sudo service node-red restart
