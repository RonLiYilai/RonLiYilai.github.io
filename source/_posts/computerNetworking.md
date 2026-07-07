---
title: Computer Networking
date: 2026-07-06
tags:
hide: true
description: Computer Networking Course Note
---
计算机网络

# 1. Introduction

## Internet

hosts = end systems

communication links

packet switches: routers and switches

protocols define format, order of messages sent and received

## Network Edge

hosts: clients and servers

# 2. Application Layer

application architectures

- client-server

  server:

  - always-on host
  - permanent IP address

  clients:

  - static/dynamic IP addresses
- peer-to-peer

## Electronic Mail

- User agents
- Mail servers
- Simple Mail Transfer Protocol

mail access protocol

- POP
- IMAP
- HTTP

## DNS

Domain Name System

- distributed database

  storing resource records

  - format(name, value, type, ttl)

# 3. Transport Layer

UDP

Internet checksum (weak protection)

1. add two 16-bit integers
2. most significant bit add to the result
3. complement

TCP congestion control

# 4. Network layer

BGP

eBGP, iBGP

## Intra-AS Routing

* RIP: Routing Information Protocol
* OSPF: Open Shortest Path First
* IGRP: Interrior Gateway Routing Protocol

## Inter-AS Routing

# 5. Link Layer
