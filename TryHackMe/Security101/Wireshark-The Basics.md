---
tags:
  - recon
  - tool
  - gui
  - network
link: https://tryhackme.com/room/wiresharkthebasics
prerequisites:
  - "[[Networking Concepts]]"
  - "[[Networking Core Protocols]]"
  - "[[Networking Essentials]]"
  - "[[Networking Secure Protocols]]"
---
# Overview
- Detecting and troubleshooting network problems, such as network load failure points and congestion.
- Detecting security anomalies, such as rogue hosts, abnormal port usage, and suspicious traffic.
- Investigating and learning protocol details, such as response codes and payload data.

[Wireshark Documentation](https://www.wireshark.org/docs/)

> [!NOTE] Note
> Wireshark is not an Intrusion Detection System (IDS). It only allows analysts to discover and investigate the packets in depth. It also doesn't modify packets; it reads them. Hence, detecting any anomaly or network problem highly relies on the analyst's knowledge and investigation skills.

Along with quick packet information, Wireshark also colour packets in order of different conditions and the protocol to spot anomalies and protocols in captures quickly.You can create custom colour rules to spot events of interest by using display filters.
![Default colouring rules](Pasted%20image%2020260130071227.png)
Wireshark has two types of packet colouring methods: temporary rules that are only available during a program session and permanent rules that are saved under the preference file (profile) and available for the next program session.

# [Packet Dissection](https://github.com/boundary/wireshark/blob/master/doc/README.dissector)
Packet dissection is also known as protocol dissection, which investigates packet details by decoding available protocols and fields.
You can click on a packet in the packet list pane to open its details (double-click will open details in a new window). Packets consist of 5 to 7 layers based on the OSI model. Each time you click a detail, it will highlight the corresponding part in the packet bytes pane.
![Packet dissection by layers in OSI model](Pasted%20image%2020260130073128.png)
We can see seven distinct layers to the packet: `frame/packet`,`source [MAC]`,`source [IP]`,`protocol`,`protocol errors`, `application protocol`, and `application data`.
- The Frame (Layer 1):This will show you what frame/packet you are looking at and details specific to the Physical layer of the OSI model.
- Source [MAC] (Layer 2):This will show you the source and destination MAC Addresses; from the Data Link layer of the OSI model.
- Source [IP] (Layer 3):This will show you the source and destination IPv4 Addresses; from the Network layer of the OSI model.
- Protocol (Layer 4):This will show you details of the protocol used (UDP/TCP) and source and destination ports; from the Transport layer of the OSI model.
- Protocol Errors:This continuation of the 4th layer shows specific segments from TCP that needed to be reassembled.
- Application Protocol (Layer 5):This will show details specific to the protocol used, such as HTTP, FTP,  and SMB. From the Application layer of the OSI model.
- Application Data: This extension of the 5th layer can show the application-specific data.

# Packet Navigation
## Packet Numbers
Wireshark calculates the number of investigated packets and assigns a unique number for each packet. This helps the analysis process for big captures and makes it easy to go back to a specific point of an event.
![Frame numbers as same as packet numbers](Pasted%20image%2020260130074329.png)
Packet numbers do not only help to count the total number of packets or make it easier to find/investigate specific packets. This feature not only navigates between packets up and down; it also provides in-frame packet tracking and finds the next packet in the particular part of the conversation.
## Go to Packet
Packet numbers do not only help to count the total number of packets or make it easier to find/investigate specific packets. This feature not only navigates between packets up and down; it also provides in-frame packet tracking and finds the next packet in the particular part of the conversation. You can use the **"Go"** menu and toolbar to view specific packets.
## Find Packets
There are two crucial points in finding packets. The first is knowing the input type. This functionality accepts four types of inputs (Display filter, Hex, String and Regex). String and regex searches are the most commonly used search types. Searches are case insensitive, but you can set the case sensitivity in your search by clicking the checkbox.

The second point is choosing the search field. You can conduct searches in the three panes (packet list, packet details, and packet bytes), and it is important to know the available information in each pane to find the event of interest. For example, if you try to find the information available in the packet details pane and conduct the search in the packet list pane, Wireshark won't find it even if it exists.
## Mark Packets
You can find/point to a specific packet for further investigation by marking it. It helps analysts point to an event of interest or export particular packets from the capture. You can use the **"Edit"** or the **"right-click"** menu to mark/unmark packets.
Marked packets will be shown in black regardless of the original colour representing the connection type. Note that marked packet information is renewed every file session, so marked packets will be lost after closing the capture file.
## Packet Comments
Similar to packet marking, commenting is another helpful feature for analysts. You can add comments for particular packets that will help the further investigation or remind and point out important/suspicious points for other layer analysts. Unlike packet marking, the comments can stay within the capture file until the operator removes them.
## Export Packets
As Wireshark is not an IDS, so sometimes, it is necessary to separate specific packages from the file and dig deeper to resolve an incident. This functionality helps analysts share the only suspicious packages (decided scope). Thus redundant information is not included in the analysis process.
![Export options in the File Ribbon tab](Pasted%20image%2020260130082216.png)
You can export a range of packets , thus filtering all the noise, making analysis much easier.
## Export Objects/Bytes
Wireshark can extract files transferred through the wire. For a security analyst, it is vital to discover shared files and save them for further investigation. Exporting objects are available only for selected protocol's streams (DICOM, HTTP, IMF, SMB and TFTP).
## Expert Info
Wireshark also detects specific states of protocols to help analysts easily spot possible anomalies and problems. Note that these are only suggestions, and there is always a chance of having false positives/negatives

| Severity  | Colour | Info                                                    |
| --------- | ------ | ------------------------------------------------------- |
| **Chat**  | **Blue**   | Information on usual workflow                           |
| **Note**  | **Cyan**   | Notable events like application error codes             |
| **Warn**  | **Yellow** | Warnings like unusual error coeds or problem statements |
| **Error** | **Red**    | Problems like malformed packets                         |

# Packet Filtering
Wireshark has a powerful filter engine that helps analysts to narrow down the traffic and focus on the event of interest. 
Wireshark has two types of filtering approaches: capture and display filters. Capture filters are used for **"capturing"** only the packets valid for the used filter. Display filters are used for **"viewing"** the packets valid for the used filter. 
Filters are specific queries designed for protocols available in Wireshark's official protocol reference. While the filters are only the option to investigate the event of interest, there are two different ways to filter traffic and remove the noise from the capture file. The first one uses queries, and the second uses the right-click menu.
Wireshark provides a powerful GUI, and there is a golden rule for analysts who don't want to write queries for basic tasks.

> [!quote] If you can click on it, you can filter and copy it.
## Apply as Filter
This is the most basic way of filtering traffic. While investigating a capture file, you can click on the field you want to filter and use the "right-click menu" or **"Analyse** **--> Apply as Filter"** menu to filter the specific value. Note that the number of total and displayed packets are always shown on the status bar.
## Conversation Filter
When you use the "Apply as a Filter" option, you will filter only a single entity of the packet. This option is a good way of investigating a particular value in packets. However, suppose you want to investigate a specific packet number and all linked packets by focusing on IP addresses and port numbers. In that case, the "Conversation Filter" option helps you view only the related packets and hide the rest of the packets easily. You can use the"right-click menu" or "**Analyse --> Conversation Filter**" menu to filter conversations.
## Colourise Conversation
This option is similar to the "Conversation Filter" with one difference. It highlights the linked packets without applying a display filter and decreasing the number of viewed packets. This option works with the "Colouring Rules" option ad changes the packet colours without considering the previously applied colour rule. You can use the "right-click menu" or **"View --> Colourise Conversation"** menu to colourise a linked packet in a single click. Note that you can use the **"View --> Colourise Conversation --> Reset Colourisation"** menu to undo this operation.
## Prepare as Filter
Similar to "Apply as Filter", this option helps analysts create display filters using the "right-click" menu. However, unlike the previous one, this model doesn't apply the filters after the choice. It adds the required query to the pane and waits for the execution command (enter) or another chosen filtering option by using the **".. and/or.."** from the "right-click menu".
## Apply as Column
By default, the packet list pane provides basic information about each packet. You can use the "right-click menu" or "**Analyse --> Apply as Column**" menu to add columns to the packet list pane. Once you click on a value and apply it as a column, it will be visible on the packet list pane. This function helps analysts examine the appearance of a specific value/field across the available packets in the capture file. You can enable/disable the columns shown in the packet list pane by clicking on the top of the packet list pane.
## Follow Stream
Following the protocol, streams help analysts recreate the application-level data and understand the event of interest. You can literary follow the order of request and response of any protocol especially in case of HTTP. It is also possible to view the unencrypted protocol data like usernames, passwords and other transferred data.
You can use the"right-click menu" or **"Analyse** **--> Follow TCP/UDP/HTTP Stream"** menu to follow traffic streams. Streams are shown in a separate dialogue box; packets originating from the server are highlighted with blue, and those originating from the client are highlighted with red.
## Simple Display Filter Queries
**Filter By Protocol Name or Port**
There are two basic ways to filter based on a specific protocol: by protocol name and by protocol port number.

To filter by **protocol name**, simply type in the protocol name and hit enter or click on the arrow button at the right hand side of the display filter bar. The GIF below shows an example of how to filter for http traffic. You can similarly filter for other protocols using keywords like `arp`, `dhcp`, `ftp`, `smtp`, `pop`, `imap`, and more.
![Filter by protocol name](Pasted%20image%2020260130102133.png)

To filter by **protocol port number**, you can use the structure `tcp.port == <port number>` or `udp.port == <port number>`. For example, if you want to see only http packets, you would use the filter "tcp.port == 80" and then hit enter.

![Filer by port number](Pasted%20image%2020260130105723.png)

