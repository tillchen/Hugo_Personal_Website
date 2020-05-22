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

## References

* <https://cnds.jacobs-university.de/courses/cn-2019/>
