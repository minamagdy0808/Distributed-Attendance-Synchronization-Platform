# Distributed Attendance Synchronization Platform

## Overview

A distributed attendance data collection and synchronization platform designed to centralize employee attendance records from multiple branch locations into a unified PostgreSQL database.

The system integrates with biometric attendance devices over TCP/IP, automatically collecting employee check-in and check-out logs and synchronizing them to a centralized server for workforce monitoring, reporting, and analytics.

The platform supports both direct device connectivity and distributed edge collectors, enabling reliable operation even in branches located behind CGNAT or private ISP networks.

---

# Business Problem

Organizations with multiple branches often struggle to:

* Consolidate attendance records from different locations.
* Monitor employee attendance in real time.
* Eliminate manual attendance collection processes.
* Prevent duplicate attendance records.
* Handle network restrictions such as CGNAT and dynamic IP addresses.
* Maintain a centralized attendance database across geographically distributed offices.

This platform solves these challenges through automated synchronization and centralized data management.

---

# Solution Architecture

The platform follows a distributed synchronization model consisting of:

### Centralized Infrastructure

* PostgreSQL database
* Synchronization services
* Branch management
* Attendance processing
* Scheduling engine

### Branch Infrastructure

Each branch can operate using one of two connectivity models:

#### Model 1: Direct Remote Collection

The centralized scheduler directly connects to attendance devices using:

* TCP/IP communication
* DDNS
* Port forwarding

The scheduler periodically retrieves new attendance records from remote devices.

#### Model 2: Edge Collector Deployment

For branches behind:

* CGNAT
* Restricted firewalls
* Private ISP networks

A lightweight Docker collector is deployed locally inside the branch network.

The collector:

* Connects to attendance devices locally
* Reads attendance logs
* Filters already synchronized records
* Pushes new attendance events to the centralized PostgreSQL server

This architecture removes the requirement for:

* Static IP addresses
* Public IP addresses
* Port forwarding
* DDNS configuration

---

# Key Features

## Multi-Branch Attendance Management

* Centralized attendance repository
* Unlimited branch support
* Branch-specific synchronization configurations

## Automated Data Collection

* Scheduled synchronization jobs
* Fully automated attendance retrieval
* Background processing

## Incremental Synchronization

* Fetches only new attendance records
* Avoids duplicate data collection
* Optimized network utilization

## Hybrid Connectivity Architecture

Supports both:

* Direct remote machine access
* Distributed edge collectors

## Dockerized Deployment

* Easy installation
* Consistent environments
* Simplified maintenance

## Reliable Data Processing

* Synchronization metadata tracking
* Fault-tolerant attendance collection
* Automatic retry mechanisms

---

# Core Components

## Scheduler Service

Responsible for:

* Triggering synchronization jobs
* Managing branch schedules
* Monitoring synchronization status

## Branch Connector Module

Responsible for:

* TCP/IP communication
* Device authentication
* Network connection management

## Attendance Fetcher Module

Responsible for:

* Reading attendance logs
* Parsing device records
* Incremental synchronization logic

## Edge Collector Service

Responsible for:

* Local device communication
* Attendance extraction
* Data forwarding to centralized infrastructure

## PostgreSQL Database

Stores:

* Employees
* Branches
* Attendance records
* Synchronization metadata
* Device configurations

---

# Technology Stack

## Backend

* Python 3

## Database

* PostgreSQL

## Infrastructure

* Docker
* Docker Compose

## Networking

* TCP/IP
* DDNS
* Port Forwarding
* Local Network Collectors

## Scheduling

* Background Scheduler Services

---

# Synchronization Workflow

## Direct Collection Mode

1. Scheduler triggers synchronization task.
2. Connector establishes TCP/IP connection.
3. Attendance logs are retrieved.
4. Duplicate prevention logic validates records.
5. New records are stored in PostgreSQL.
6. Synchronization state is updated.

## Edge Collector Mode

1. Edge Collector runs inside branch network.
2. Collector connects locally to attendance machine.
3. Attendance records are extracted.
4. Previously synchronized records are ignored.
5. New records are transmitted to centralized server.
6. PostgreSQL stores attendance data.
7. Synchronization metadata is updated.

---

# Deployment Architecture

Docker Containers:

### Centralized Server

#### Application Container

* Business logic
* Synchronization services
* Branch management

#### Scheduler Container

* Automated synchronization jobs
* Monitoring tasks

#### PostgreSQL Container

* Centralized attendance database

### Branch Collector (Optional)

#### Edge Collector Container

* Local attendance machine integration
* Attendance forwarding service

---

# Benefits

* Centralized workforce attendance management
* Automated attendance synchronization
* Elimination of duplicate records
* Reduced operational workload
* Support for CGNAT environments
* No dependency on static IP addresses
* Scalable multi-branch architecture
* Containerized deployment for simplified operations




