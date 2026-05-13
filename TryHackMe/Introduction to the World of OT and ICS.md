---
link: https://tryhackme.com/room/introductiontotheworldofotics
---
## Operational Technology (OT)

**Operational Technology (OT)** is the use of computers to monitor and control physical equipment and processes in the real world.

Such processes could include:

- A generator inside a power plant that spins to create electricity.
- A conveyor belt that moves parts within a manufacturing plant.
- Computers that operate medical equipment such as MRI and CT scanners.
- Safety systems that prevent a train from overturning when taking a curve too fast.
- Building management systems that control elevators, badged door access, HVAC, and lighting.
- Embedded computers in cars control systems such as engine control, Anti-lock Braking Systems (ABS), and Electronic Stability Control (ESC).
## Industrial Control Systems (ICS)

**Industrial Control Systems (ICS)** are a specific type of OT system found in industrial environments.

Industrial environments include:

- Power plants
- Oil refineries
- Steel mills
- Food packaging facilities
- Pharmaceutical manufacturing
- Water treatment plants

Environments such as hospitals and cars are not considered industrial environments. Systems that are used in these environments to monitor and manage physical equipment and processes are only considered OT, not ICS, though you’ll find people often use the term interchangeably.

## Supervisory Control and Data Acquisition (SCADA)

**Supervisory Control and Data Acquisition (SCADA)** is a type of ICS used over a wide-area network to monitor and control remote equipment and processes. Examples of wide-area network connections include 5G cellular connections, microwave radio links, and satellite connections.

SCADA is used to monitor and control equipment in remote environments that can only be reached with WAN technologies, such as:

- Electric substations
- Offshore oil rigs
- Pipeline pumping stations
- Offshore wind farms
- Remote solar farms
# What Does OT Do?

OT monitors and controls physical processes and equipment in the real world.
## Programmable Logic Controllers (PLCs)

OT systems, such as Programmable Logic Controllers (PLCs), the most common type of OT asset deployed today, have both inputs and outputs.
## Inputs

Inputs are pathways that bring data into the PLC from sources such as sensors that monitor conditions in a particular environment. Common types of sensors include, but are not limited to:

- Measure the temperature inside a furnace
- Measure how full an oil storage tank is
- Detect if a dangerous overpressure situation is occurring
- Detect changes in vibration patterns to identify physically failing equipment that needs to be replaced
## Outputs

Outputs are pathways that allow the system to send signals to physical systems in the real world, such as pumps, valves, and motors. I

## Real World Example
For example, if I have a power plant, the plant itself uses ICS to monitor and control the process of generating electricity. At a water treatment facility, ICS would be used to monitor and control the process of making water safe to drink and delivering it to customers.

Think of a PLC as a thermostat for an air conditioner you might have at your home or office. This thermostat has a sensor that continually reads the temperature to determine the room temperature. A PLC is programmed with logic so that if the room temperature exceeds the desired temperature, also referred to as the setpoint, it will send a signal to turn on the air conditioning unit.
In this air conditioning unit, once the thermostat determines that the room has reached the desired temperature, it sends a signal via an output to turn off the air conditioning unit.
# Where Does Cyber Risk Come From in OT/ICS?

Modern OT/ICS environments leverage traditional IT technologies, such as Ethernet, TCP/IP, cloud-based services, and GenAI, to improve performance and efficiency in plants and factories. While these technologies bring significant business advantages to the environment, each also introduces vulnerabilities that attackers and other types of cyber security risks could exploit.

## IT vs. OT Infrastructure Comparison

But it's also important to keep in mind how IT and OT assets, and other infrastructure, are different.

| **Feature**         | **IT Infrastructure**                           | **OT Infrastructure**                                 |
| ------------------- | ----------------------------------------------- | ----------------------------------------------------- |
| Primary Focus       | Managing data and information                   | Managing physical processes and machinery             |
| Top Priority        | Confidentiality                                 | Safety (human & environmental)                        |
| Asset Lifespan      | Short (3 - 5 years). Hardware is often replaced | Long (10 - 30+ years). Legacy systems are very common |
| Patching            | Regular, scheduled updates are standard         | Difficult or rare; requires expensive downtime        |
| Response to Failure | Rebooting is acceptable                         | Rebooting can cause safety issues or physical damages |

OT assets, such as PLCs, are now assigned IP addresses to connect to the OT network and communicate with other systems. For example, a **Human Machine Interface (HMI)** is a graphical interface used by human operators to monitor a physical process, which is in turn controlled by a PLC. The human operator uses the HMI not only to visually monitor how the process is operating, but also to make adjustments, such as in response to an alert.

What type of damage could an attacker do if they gained access to a plant network and accessed an HMI?

Could they:

- Stop power generation to create a blackout?
- Poison water in a water treatment facility?
- Cause systems to physically break down?
- Prevent food from being packaged safely and sent to stores?

**All** of these types of scenarios can happen, and so many others. In fact, the situations listed above are just a small list of the types of OT/ICS cyber security incidents that **have already happened**.

## Cyber Security is a Necessity in OT/ICS

OT/ICS cyber security is necessary to ensure the safety and availability of OT/ICS environments. As the number of cyber-attacks targeting OT/ICS networks (and the connected IT networks) has nearly doubled each year since the [Colonial Pipeline incident](https://www.cisa.gov/news-events/news/attack-colonial-pipeline-what-weve-learned-what-weve-done-over-past-two-years) in 2021, defenders of these specialized environments are woefully underprepared to defend OT against attackers. But it is possible, and it doesn’t have to be hard!
# Differences Between OT & IT Cyber Security

Many OT cyber security professionals might tell you that OT and IT cyber security have **nothing** in common. But that is the furthest thing from the truth. OT and IT cyber security actually have much more in common than they don’t.

What is critical is to understand **where** OT and IT cyber security are different and **how** they are different. Because if you are not aware of those differences, you could get someone hurt or killed, let alone take down a plant in the middle of operations.
## IT Cyber Security

In IT cyber security, the primary requirements are formed by the C-I-A triad.
## OT Cyber Security

In OT cyber security, many say the requirements are reversed, so we now have an A-I-C triad. Unfortunately, this formula leaves out the most important requirement in OT cyber security – physical safety. We must ensure that not only do on-site employees go home safe at the end of the day without getting hurt or killed, but that the general public and the environment surrounding the plant are not harmed as well.

Every action we take to defend OT/ICS networks from cyberattacks focuses first on ensuring physical safety, then on operational availability of the site, the integrity of its data, and, finally, confidentiality. In many OT/ICS environments focused solely on safety and operational availability, OT/ICS networks often lack encryption!
## How IT and OT Cyber Security Compare 

The following table highlights some of the significant differences between IT and OT cyber security.

| Security Task          | IT Environment (Back Office)                                                                         | OT Environment (Factory/Plant)                                                                                                             |
| ---------------------- | ---------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------ |
| Patch Management       | Automatic/Frequent (patches are rolled out almost as soon as they are released)                      | Planned/Rare (patching requires halting production which occurs rarely (e.g., once a year) in scheduled maintenance windows.)              |
| Vulnerability Scanning | Active Scanning (networks can be probed for existing vulnerabilities)                                | Passive Monitoring (active scanning with tools like Nmap and Nessus can cause OT assets to crash)                                          |
| Incident Response      | Isolate & Reboot (If a system is compromised, we wipe it and reinstall)                              | Keep it Running (OT systems cannot simply be isolated or rebooted without introducing safety and operational availability issues)          |
| Network Encryption     | Almost Everything (Almost all network traffic in IT networks is encrypted to ensure confidentiality) | Very Low (Most OT/ICS protocols do not support encryption; while newer protocols do, most plants continue to favor older unencrypted ones) |