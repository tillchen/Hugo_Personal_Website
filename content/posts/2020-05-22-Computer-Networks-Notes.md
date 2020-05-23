+++
draft = false
date = 2020-05-22T18:52:12+02:00
title = "Computer Networks Notes"
description = "Course notes for Computer Networks at Jacobs University Bremen"
tags = ["Computer Science"]
+++

* [Introduction](#introduction)
  * [Internet Concepts and Design Principles](#internet-concepts-and-design-principles)
  * [Structure and Growth of the Internet](#structure-and-growth-of-the-internet)
  * [Internet Programming with Sockets](#internet-programming-with-sockets)
* [Fundamental Concepts](#fundamental-concepts)
  * [Classification and Terminology](#classification-and-terminology)
  * [Communication Channels and Transmission Media](#communication-channels-and-transmission-media)
  * [Media Access Control](#media-access-control)
  * [Transmission Error Detection](#transmission-error-detection)
  * [Sequence Numbers, Acknowledgements, Timer](#sequence-numbers-acknowledgements-timer)
  * [Flow Control and Congestion Control](#flow-control-and-congestion-control)
  * [Layering and the OSI Reference Model](#layering-and-the-osi-reference-model)
* [Local Area Networks](#local-area-networks)
  * [Local Area Networks Overview](#local-area-networks-overview)
  * [Ethernet](#ethernet)
  * [Bridges](#bridges)
  * [Virtual LAN](#virtual-lan)
  * [Port Access Control](#port-access-control)
  * [Wireless LAN](#wireless-lan)
  * [Logical Link Control](#logical-link-control)
* [References](#references)

## Introduction

This is the course notes for Computer Networks at Jacobs University Bremen.

### Internet Concepts and Design Principles

1. Internet Addresses:
    * Leading nulls in IPv6 addresses can be omitted and two consecutive  colons can represent a sequence of nulls:
      * 2001:00db8:0000:0000:0000:0000:0000:0001 can be written as 2001:db8::1
    * IPv6 addresses have 16 bytes (4 x 8 groups); IPv4 addresses have 4 bytes.

2. Autonomous Systems:
    * An AS is a set of routers and networks under the same administration.
    * IP packets are forwarded between ASs by EGP (Exterior Gateway Protocol); within an AS, it's IGP (Interior Gateway Protocol)
    * The Internet is a collection os ASs. There's no central authority.

### Structure and Growth of the Internet

1. Internet Exchange Points (IXPs) are switching hubs where many Internet Service Providers (operating ASs) connect in order to exchange internet traffic.

### Internet Programming with Sockets

1. Sockets are abstract communication endpoints with a rather small number of associated function calls.

2. Connection-less vs connection-oriented communication
    * Connection-oriented communication requires a establishment and a teardown. Most of the Internet traffic is using this.

## Fundamental Concepts

### Classification and Terminology

1. Communication modes:
    * Unicast - 1:1
    * Multicast - 1:n
    * Concast - n:1
    * Multipeer - m:n
    * Anycast - 1: nearest receiver
    * Broadcast - 1: all
    * Geocast - 1: n in a region

2. Communication protocols define the syntax and semantics of messages.

3. Circuit vs packet switching:
    * Circuit switching: create and remove (virtual) circuit (e.g. the telephone network)
    * Packet switching: data is carried in packets (e.g. Internet)

4. Connection-oriented vs connection-less:
    * Connection-oriented: stateful (e.g. fetching a Web page)
    * Connection-less: stateless (e.g. Internet name lookups)

5. Data vs. control vs. management plane:
    * Data plane: forwarding of data (hardware)
    * Control plane: telling the data plane how to forward data (routers and switches)
    * Management plane: configuration and monitoring of data and control planes (may involve humans)

6. Topologies:
    * Star; Ring; Meshed Network; Bus; Line.

### Communication Channels and Transmission Media

1. Signals are in general modified during transmission, leading to transmission errors.

2. Data rate (bit rate) vs bit time:
    * Bit time is the time needed to transmit a single bit (1 microsecond for 1 Mbit/s)

3. Delay is the time needed to transmit a message from the source to the sink. It consists of transmission delay and propagation delay.

    ![transmission vs propagation delay](/images/transmission_propagation_delay.png)

4. Bit error rate is the probability of a bit being changed during transmission.

5. Simple wires can easily experience crosstalk caused by capacitive coupling.

6. Transmission impairments:
    * Attenuation
    * Delay distortion (different frequencies arrive at different time)
    * Noise

### Media Access Control

1. Media access control - shared transmission media require coordinated access to the medium.

2. Frequency division multiplexing (FDM): simultaneous signals in different frequency bands.

3. Wavelength division multiplexing (WDM): different wavelengths at the same time.

4. Time division multiplexing (TDM): signals are assigned to specific time slots.

5. Pure aloha - sends data as soon as data becomes available (not very efficient)

6. Slotted aloha - sends do not send immediately but wait for the beginning of a time slot - (slightly more efficient)

7. Carrier sense multiple access (CSMA) - sense the media whether it's unused before starting a transmission.

8. CSMA with collision detection (CSMA-CD) - terminates the transmission as soon as a collision has been detected (and retries after some random delay).

9. Multiple access with collision avoidance (MACA) - sends RTS (ready to send) and CTS (clear to send)

10. Token passing - a token is a special bit pattern circulating between stations (only the station holding the token is allowed to send data).

### Transmission Error Detection

1. Simple parity bits can be added to code words to detect bit errors.

2. Cyclic redundancy check (CRC) uses polynomials (1101 = $x^3+x^2+1$)
    * Divide the message with the generator, if the remainder is 0, we assume no transmission error. Otherwise, add the remainder to the message to get the real bit sequence.

### Sequence Numbers, Acknowledgements, Timer

1. Errors:
    * Bit errors
    * Loss of complete data frames
    * Duplication of complete data frames
    * Receipt of data frames that were never sent
    * Reordering of data frames during transmission

2. End-to-end flow control - the sender must adapt its speed to the speed of the receiver.

3. Congestion control - the sender must react to congestions.

4. The sender assigns growing sequence numbers to all data frames to deal with the errors above.

5. The receiver sends ACK to handle errors.
    * ACK: positive acknowledgement
    * NACK: negative acknowledgement
    * Stop-and-wait protocol - a frame is only transmitted if the previous frame was acknowledged.

6. A send can also use a timer to retransmit a frame if no ACK has been received in time.

### Flow Control and Congestion Control

1. Flow control - allows the sender to send multiple frames before waiting for ACKs.

2. Sliding window flow control - the size of the window and the speed of the sender must match the buffer capacity of the receiver.
    * For the send: LFS - LAR + 1 <= SWS (last frame sent, last ACK received, send window size)
    * For the receiver: LFA - NFE + 1 <= RWS (last frame acceptable, next frame expected, receive window size)

3. Congestions control is used to adapt the speed of the sender to the speed of the network.

### Layering and the OSI Reference Model

1. Protocol data units (PDUs) are exchanged between peer entities; service data units (SDUs) are exchanged between layers (services).

2. The Open systems interconnection model (OSI model): (layer 7 -> layer 1)
    * Application
    * Presentation - data compression/integrity services etc.
    * Session - security services
    * Transport - communication channels
    * Network - determination of paths
    * Data link - transmission of bit sequences in so called frames
    * Physical - transmission of an unstructured bit stream

## Local Area Networks

### Local Area Networks Overview

1. IEEE 802 addresses (MAC addresses) are 6 octets (48 bits) long.
    * It's usually separated using colons or hyphens (00:D0:59:5C:03:8A)
    * The highest bit indicates whether it's unicast (0) or multicast (1)
    * The broadcast address is FF-FF-FF-FF-FF

### Ethernet

1. Classic Ethernet usd CSMA/CD and shared bus.

2. Today's Ethernet uses a star topology with full duplex links.

### Bridges

1. Source routing bridges - sender routes the frame through the bridged network.

2. Transparent bridges - bridges are transparent to senders and receivers.
    * Look up an entry in the forwarding DB (entry added when a frame is received) and forward the frame to the port.
    * If not matching entry exists, do flooding - forward the frame to all outgoing ports except the port from which the frame was received.

3. Port states:
    * Blocking
    * Listening
    * Learning
    * Forwarding
    * Disabled

4. A bridged LAN has a single broadcast domain - frames sent to this address will be forwarded on all links.

### Virtual LAN

### Port Access Control

### Wireless LAN

### Logical Link Control

## References

* <https://cnds.jacobs-university.de/courses/cn-2019/>
