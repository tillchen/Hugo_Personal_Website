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

### Media Access Control

### Transmission Error Detection

### Sequence Numbers, Acknowledgements, Timer

### Flow Control and Congestion Control

### Layering and the OSI Reference Model

## References

* <https://cnds.jacobs-university.de/courses/cn-2019/>
