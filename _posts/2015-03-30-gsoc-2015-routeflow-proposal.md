---
layout: post
title: "GSoC 2015 RouteFlow Proposal"
modified:
categories: 
excerpt: Here it is my Google Summer of Code proposal for unified end-to-end tests of RouteFlow project for 2015 
tags: [routeflow, test, gsoc]
image:
  feature:
date: 2015-03-30T15:23:06-04:00
image:
  feature: sample-image-4.jpg
---

<section id="table-of-contents" class="toc">
  <header>
    <h3>Overview</h3>
  </header>
<div id="drawer" markdown="1">
*  Auto generated table of contents
{:toc}
</div>
</section><!-- /#table-of-contents -->

Here it is my Google Summer of Code proposal for unified end-to-end tests of RouteFlow project for 2015 

###Executive Summary 	
The purpose of this paper is to propose an automated test suite for RouteFlow (RF) project. RF project has gone through reasonable number of architectural changes since its origin. The unified test project for RF aims to provide a series of tests to ensure that the integrated components of RF function as expected in both development and production environments.  It is expected this project to expedite the project development path by avoiding manual tests. The biggest impact is that developers can make changes in RF components without worrying about breaking the integrity of the whole RF framework. 

###Introduction
The overall objective of this proposal is to ensure that we can cover requirements for unified test project as much possible in advance. 

As part of a developer activity, a typical RT test case scenario would be to set up a proper RT development environment, make component modifications, and verify the expected behavior change in RT while ensuring the integrity and correctness of the RT codebase being modified. For example, in the case of altering RFProtocol specification, not only must the whole RF framework be rebuilt, but the flows in switches must also be flushed and the connection between host be confirmed. 

RF provides virtualized IP routing services for OpenFlow networks.  It is mainly the integration of several interconnected and distributed systems and technologies, each built using different protocols from a variety of organizations as well as its main components developed by RF community. The verification and validation of overall system functionalities of the whole system during development can be viewed as a tedious and challenging task, taking into account possible combination of components and configurations. 

One challenging aspect is RF independency from specific routing engine implementation (i.e. Quagga, XORP, Bird), which entails the use LXC virtualization environment in order to retain multiple instances of routing engines and routing tables simultaneously in isolation, which evidently presents more complexity to the architecture as well as the virtual network connectivity of containers of components in addition to IPC mechanism of them must also be verified.
 
Another challenging aspect is to embed a  portion of test scenarios as an auto-self-test module to the RT platform so end-users can take advantage of auto-self-test, to validate RT configuration regardless of underlying OpenFlow switches or network topology. 


####Related works
GNU AutoTest: Basically is going to be used in integrity test suite. It simplifies tests that depend on text matching it also allow us to easily put a wrapper around each test by using a macro to invoke it. It can also integrated with the project make file to make sure it is invoked as part of built process.  

Mininet: it is a network emulator, which creates a network of virtual hosts, switches, controllers, and links. Mininet hosts run standard Linux network software, and its switches support OpenFlow for highly flexible custom routing and Software-Defined Networking.

####Goals and Objectives 
Currently the RF package includes two shell scripts that automatically configure and run RF components, one illustrating a single network and the other one a network topology with four routers exchanging routes through OSPF routing protocol. The former one instantiates LXC containers representing physical hosts and while the second one employs MiniNet to create a corresponding physical network topology. 

Three main categories of requirements Connectivity tests, Component integrity test, Components integrity test for E2E tests in this proposal are going to be addressed. 


<figure>
    <a href="/images/routeflow.png"><img src="/images/routeflow.png"></a>
    <figcaption><a href="/images/routeflow.png" title="Figure 1">Integrity vs Connectivity Tests</a>.</figcaption>
</figure>


**Connectivity tests**: ensure the connectivity between end-hosts, their corresponding virtual router gateway. 
Throughout the connectivity tests we employ both positive and negative tests by not only testing the connectivity of hosts (positive) but also ensuring that the connection can not be maintained without means of RT. Specifically by disconnecting temporarily these components (negative test) (disconnecting the controller temporarily and flush out all flows switch and running the connectivity test again). This test suit also output related matrix indicating the connectivity state of all end-hosts as an end.
 
**Components integrity test**: this test suite verifies the expected state of RF components and the connectivity between all RF components once they are all properly configured and started by initial scripts. This test suite covers the connectivity between RFVMs and the host management interface. It also verifies of RFClient, Quagga specific processes, specifically, zebra, bgpd, ospfd as well on RFVMs as well as RF-Server, OpenFlow Controller (Ryu, Floodlight, POX, NOX) and RF-Proxy, MongoDB by verifying both status of the running process and expected listening port on that process. This test suite is also responsible to verify expected version of depended components (i.e. MongoDB, Open vSwitch, Linux Kernel, etc)

**Consistency tests**: This test suite is suitable to expedite test cycles by restricting the system under test (SUT) limited to only to hardware or software switches which in case that the automated test of this suite compares and verifies each RFVMs routing table entries and ARP table entries with the corresponding flow entries in the datapath under the test.

####Procedures
*Warm up*: BGP Test rftest3: Just another shell script for RF demonstration just like rftest2 but employing BGP routing protocol instead of OSPF between virtual routers. 

*Integrity Tests*: This test suite is basically a series of shell scripts and python script which are invoked by AutoTest scripts to verify RF components status, listening ports, the connection between RFVMs and the host. This test suite must possibility test anything that might go wrong with deployment of RT framework thus new tests, features must be added to package during this summer project and throughout RT project development. 
 
*Connectivity Test*: This test suite involves development of a Mininet modules and porting older RF tests into Python. In particular Mininet module allows for even more integration between RT framework and Mininet, it also makes the definition of implementation of new test scenarios much easier in future by using both Python scripts and Mininet CLI. 

Mininet Python Module (mininet.rf): this module provides RF specific extension to Mininet main object as new collection and functions:
o	net.rfvms: the collection representing RFVMs objects.  
o	net.addRfvm(): adds a new RFVM to RF controller
o	net.mapSwitchRfvm() as well as supplying Quagga specific configurration to specific RFVMs.
•	Revisited Tests (rftest1.py, rftest2.py, rftest3.py) the same and behavior and functionality of rftest1, rftest2 and rftest3, except that all tests are runnable in Mininet though there will be only a single initial script to configuration and start the main components environment which will be the same main script in Vandervechen branch, projectw.sh). 
•	Once we have needed material constructed needed infrastructure to easily reuse built-in connectivity test features of the Mininet and also implement new a new command to implement positive and negative connectivity tests on end-hosts.  

Consistency Tests: This test suite is a Shell Script making use of AutoTest M4 scripts, which verifies RFVM routing table entries with the switch in the test. 
Self-Tests: Merging and rftest1 and ping.py in projectw.sh 
Documentation: RouteFlow Mininet Module (mininet.rf) API Documentation, user  documentation, instructions on how to run integrity tests, connectivity tests (using Mininet).

In general the only RT component that will be affected is the RF-Test and in the case Vandervechen branch the script file project.sh.

###Timeline and milestones
1.	BGP Test Scenario (rftest3) due on 16 May
2.	MiniNet Python version of rftest1, rftest2, rftest3 due on 30 May
3.	Consistency Tests due on 13 June
4.	Integrity Tests due on 26 June
5.	Consistency Tests due on 11 July
6.	Finalizing and documenting due on 31 July