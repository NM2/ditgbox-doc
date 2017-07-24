# DITGBox Manual

## Introduction

DITGBox is a high-speed platform for traffic generation and performance measurement over a wide range of protocols and applications.
It can craft packets at L3/4, statistically controlling inter-time and size of packets. It can directly generate at L7 with full stack traversal or it can replay real traffic traces.
DITGBox accurately measures the performance of the whole traffic and/or the detailed performance experienced by single, specific flows.
It can act as a simple (open loop) packet generator or it can work towards the same or other DITGBoxes.
DITGBox is controlled via an easy-to-use web GUI and through a RESTful API.

## Login

Once the product has been activated the user will be automatically redirected to the “Login Page” that shows:
two input boxes for username and password, a “Login” button to confirm the credentials and a “Recovery” button to start the password reset procedure or to bring the product to the factory configuration.

![login-page](images/login_page.png?style=centerme)

In case the user forgets the password he can retrieve it by clicking the “Recovery” button. This operation is allowed only if the user is able to reach the box at the recovery address “http://172.17.71.1” through the “admin” port by configuring his host with the 172.17.71.2/30 IP address. 
The recovery page also allows to perform the factory reset of the product.

## Generation

After successfully logging in, the “Generation” screen will be shown. This is the section of the WebUI where the user can configure and run traffic generation experiments.


![generation-section](images/generation_section.png?style=centerme)

A Dashboard with network stats will be shown. For each data port the received and transmitted byte volume is reported and these values will be updated in real time while generating traffic.
On the bottom of the Dashboard there is an icon to shutdown DITGBox and another one to restart it.
On the  top of the Generation page the name, speed and status of the Control Port and data ports are reported. A green label means the port is enabled, while a red one means it is disabled. Only enabled data ports can be selected for generating/receiving traffic. Under each of the port icons there’s a lightbulb that when clicked will make the led of the corresponding Ethernet port blink.
In order to configure an experiment the user has to select a data port by clicking on its icon. After doing that the “Traffic Settings” for the selected data port will be shown.


### Traffic Settings

The “Traffic Settings” section allows to customize a new traffic generation experiment, save a preset of the experiment or load a previously saved preset.
The “Generation mode” button lets the user select the kind of traffic experiments the product supports. Generation modes are dependent on the license currently installed with your DITGBox appliance.
The “Meter” drop-down menu allows to choose if the metrics computed by DITGBox will be one-way or round-trip.
When a data port has been selected to generate traffic, the user will see a flow profile associated with it. On the left side of each flow profile he can then see/edit its name, status and number of replicas. On the right side there are buttons to add a new flow profile, clone or delete the current one.
For each traffic flow profile the user can configure settings shown in 5 tabs:
Application Layer, Transport Layer, Network Layer, Destination and Timing Options.


![traffic-settings](images/traffic_settings.png?style=centerme)

#### Application Layer

The “Application Layer” tab allows the user to choose a stochastic profile for the generated traffic. Each stochastic profile has its own specific settings. For example, if the VoIP profile is selected the user will be able to choose the codec type used for the traffic generation.
The “Custom” profile allows to fully customize the generated traffic. By selecting this profile the user is able to set the following parameters:
payload size distribution, inter-departure time distribution, required throughput, payload size of the packets, packet rate, payload content and seed to initialize the random generator used for distributions.
The required throughput, the payload size and the packet rate are interdependent. Clicking on the lock icon above one of these parameters locks the parameter and allows to edit the remaining two.


![custom-profile](images/custom_generation_profile.png?style=centerme)

#### Transport Layer
The “Transport Layer” tab allows the user to choose TCP or UDP as the transport layer protocol and the source and destination ports.


![transport-layer](images/transport_layer.png?style=centerme)

#### Network Layer
The “Network Layer” tab allows to choose the IP version, the source and destination IP addresses with netmask, the “Time To Live” and “Type of Service” values.


![network-layer](images/network_layer.png?style=centerme)

#### Destination
The “Destination” tab allows to decide who is going to receive the traffic generated during the experiment. Two kinds of destination can be chosen:
*loopback* when the destination data port belongs to the same box that generates traffic or *remote box* when the destination data port belongs to a remote box to which the origin box is connected. In order to be able to choose a remote data port, a remote box has to be added first (see Remote Configuration).


![traffic-settings-destination-loopback](images/traffic_settings_destination_loopback.png?style=centerme)



![traffic-settings-destination-remote_box](images/traffic_settings_destination_remote_box.png?style=centerme)

#### Timing Options
The “Timing Options” tab allows to set an initial delay for the traffic generation and the time duration of the traffic generation. The latter can be set to *auto* to specify an amount of time after which the generation automatically stops, or *manual* to be able to stop the generation manually.


![traffic-settings-timing-options](images/traffic_settings_timing_options.png?style=centerme)


### Traffic Generation
The “Traffic Generation” section shows the current status of the traffic generation on top along with buttons to stop or abort the generation and a table reporting the elapsed time of the experiment and the computed metrics for both the Sender and the Receiver data ports. The rows of this table can be expanded/collapsed by clicking the arrow icons to the right of the data port names.


![traffic-generation-running-experiment](images/traffic_generation_running_experiment.png?style=centerme)

While an experiment is running you can click on the “Detailed Stats” button to show real-time graphs of the computed metrics.


![traffic-generation-real-time-detailed-stats](images/traffic_generation_real_time_detailed_stats.png?style=centerme)

When stopping an experiment 3 buttons will appear below the Traffic Generation table:
clicking on the “Detailed stats” button will show graphs of the computed metrics both for the sender and receiver data ports;
“Save results” allows to save the results of the experiment on the box to be later analysed (see Traffic Generation Results);
“Discard results” will remove the results gathered during the experiment.


![traffic-generation-end-of-experiment](images/traffic_generation_end_of_experiment.png?style=centerme)

## File Manager

The “File Manager” section allows to manage all the files stored on the box and to upload new ones. It is composed of 6 subsections, each for a specific type of file:
Presets, Traffic Generation Results, PCAP Traces, Payloads Content, Packet Size Distributions and IDT Distributions.

### Presets

A preset is a file that stores the complete configuration of an experiment. It can be used to load an experiment profile without having to configure it from the WebUI every time the user wants to run it. The “Presets” section shows a list of all the presets currently saved on the box.


![file-manager-presets](images/file_manager_presets.png?style=centerme)

On this screen, by clicking a button to the right of the presets list, the user can rename the preset file, download it on your computer, delete it permanently from the box, see a preview of its content or load it as a new experiment.


![file-manager-presets-upload](images/file_manager_presets_upload.png?style=centerme)



### Traffic Generation Results

The “Traffic Generation Results” section lists all the results of the experiments that have been saved on the box.

![file-manager-traffic-generation-results](images/file_manager_traffic_generation_results.png?style=centerme)

By clicking on one of the traffic generation results a complete report of it will be shown.
On the top of this report users can see the name of the experiment, the date of its execution and buttons to rename it, export it to a file that can be saved locally or delete it.
The report shows the complete configuration of the experiment and all the involved data ports and flow profiles.


![file-manager-traffic-generation-results-expanded-1](images/file_manager_traffic_generation_results_expanded_1.png?style=centerme)

On the bottom of the report, a table with the computed metrics is shown along with graphs for each metric.


![file-manager-traffic-generation-results-expanded-2](images/file_manager_traffic_generation_results_expanded_2.png?style=centerme)

The graphs can be customized to show only the data actually needed. In particular, users can
add a line to the graph by dragging one of the blue squares in the table and dropping it on one of the graphs,
remove a line from the graph by clicking on the x of one of the labels listed on the bottom of the graph
or hide a graph by clicking on the minus sign on the top-right of it.


![file-manager-traffic-generation-results-expanded-3](images/file_manager_traffic_generation_results_expanded_3.png?style=centerme)

### PCAP Traces

The “PCAP Traces” section lists all the PCAP traces currently stored on the box.


![file-manager-pcap-traces](images/file_manager_pcap_traces.png?style=centerme)

From this view users can rename, download, delete or see a preview of each of the saved PCAP traces. Furthermore they can upload a new PCAP trace by clicking the “Upload file” button.


![file-manager-pcap-traces-upload](images/file_manager_pcap_traces_upload.png?style=centerme)

### Payload Contents

The “Payload Contents” section lists all payload content files saved on the box. A payload content file can be used as custom payload for packets generated during an experiment (see Application Layer Settings).
An example of a payload content file containing an HTTP GET request is shown below.

![file-manager-payload-contents](images/file_manager_payload_contents.png?style=centerme)

### Packet Size Distributions

A Packet Size Distribution file stores a list of packet sizes (expressed in bytes) used during traffic generation. Each line of a Packet Size Distribution file has one positive integer only. During the execution of an experiment the generation engine will read this file sequentially to set the payload size of the next packet to be sent.
An example of a Packet Size Distribution file is shown below.


![file-manager-packet-size-distribution](images/file_manager_packet_size_distribution.png?style=centerme)

### IDT Distributions

An Inter-Departure Time Distribution file stores a list of inter-departure times (expressed in milliseconds) used during traffic generation. Each line of an Inter-Departure Time Distribution file has one positive integer only. During the execution of an experiment the generation engine will read this file sequentially to set the inter-departure time between consecutive packets.
An example of an Inter-Departure Distribution file is shown below.


![file-manager-idt-distribution](images/file_manager_idt_distribution.png?style=centerme)

## Settings
The “Settings” section allows you to manage the box and network configuration, enable the remote assistance component, download and send the current box configuration, contact us through email and upgrade the components of the product.


![settings](images/settings.png?style=centerme)

### Box Configuration

The “Box Configuration” section allows you to change the administrator password, the name of the box and its date, time and timezone.
If you want to change the administrator password just click the “Change administrator password” button and the following screen will appear.


![settings-modify-administrator-password](images/settings_modify_administrator_password.png?style=centerme)


In order to change time, date, and timezone just click on the gear icon to the right of the current time and date shown in the “Box Configuration” section.
When changing the date, time or timezone of the box the following screen will appear.


![settings-date-time-configuration](images/settings_date_time_configuration.png?style=centerme)

Here the user can decide if:
- the time and date have to be automatically updated by synchronizing with a remote NTP server or with a remote box. After selecting the machine you want the product to sync with, you have to click on the black arrow icon above the name of the syncing machine;
- the time and date have to be manually set.

### Network Configuration

The “Network Configuration” section allows to configure the network settings of the current box and to add remote boxes.
In the “Local Configuration” subsection the user can see all the network settings of the local box.
Here it is possible to:
- edit the Web Management IP address and netmask;
- edit the Control Port IP address and netmask;
- edit the Control TCP Port;
- edit the default gateway IP address;
- edit the DNS server IP address;
- edit the default IP network prefixes and netmasks of the data ports;
- see the current routing table.

Furthermore the user can check if the box is able to connect to the Internet.


![settings-network-configuration-local-configuration](images/settings_network_configuration_local_configuration.png?style=centerme)

The “Remote Configuration” subsection allows to add a new remote box and see the list of the currently saved remote boxes. To the right of each saved remote box you will have buttons to edit the remote box name and control IP address, remove the remote box, update the status of the remote box ports and see the remote box data ports configuration.
When the background color of the control IP address of a remote box is green it means that the local box is able to contact the remote box and this remote box can be selected as receiver for an experiment.


![settings-network-configuration-remote-configuration](images/settings_network_configuration_remote_configuration.png?style=centerme)

### Troubleshooting

The “Troubleshooting” section provides services the user can use if he needs help.
In particular if the local box is able to connect to the Internet, the Remote Assistance switch will be visible. Turning on the Remote Assistance service allows NM2 to analyse remotely the behavior of the product, diagnose and solve possible problems.
If a user experiences any problem and he needs support he can also download the current configuration of the box and send it to us.


![settings-troubleshooting](images/settings_troubleshooting.png?style=centerme)

### Upgrade

In future NM2 may release upgrades to one or several components of DITGBox. In order to install an upgrade package the user just has to click on the “Select an upgrade package” button.


![settings-upgrade](images/settings_upgrade.png?style=centerme)

After doing that a modal window will appear showing the changelog for the upgrade and asking for a valid activation key. After typing the key and clicking the “Install” button the user just has to wait for the upgrade package to be installed. He will be informed by the system when the installation has completed.


![settings-upgrade-package](images/settings_upgrade_package.png?style=centerme)

## About
The “About” section reports useful information such as:
NM2 company and website addresses;
the product version, the serial number, and the activation key of the local box;
the version of each component installed on the box;
license info such as the expiration date;
the list of all the features currently enabled on the local box;
the limits imposed by the license;
the list of the RFCs the current version of the product is compliant with
(the list depends on the license installed on the box);
license information for third party components used in DITGBox.
