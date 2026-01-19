# SOP for Logrotate

---

## Table of Contents
- [Introduction](#introduction)
- [Purpose](#purpose)
- [Key Features](#key-features)
- [Getting Started](#getting-started)
  - [Pre-requisites](#pre-requisites)
- [Software Overview](#software-overview)
- [System Requirements](#system-requirements)
- [Important Ports](#important-ports)
- [Dependencies](#dependencies)
  - [Run-time Dependency](#run-time-dependency)
  - [Other Dependency](#other-dependency)
- [Logrotate Configuration Structure](#logrotate-configuration-structure)
- [How to Setup and Configure Logrotate](#how-to-setup-and-configure-logrotate)
  - [Install Logrotate](#install-logrotate)
  - [Basic Logrotate Configuration](#basic-logrotate-configuration)
  - [Rotation Frequency](#rotation-frequency)
  - [Retention Policy](#retention-policy)
- [Configuration](#configuration)
- [Maintenance](#maintenance)
- [Monitoring](#monitoring)
- [Disaster Recovery](#disaster-recovery)
- [High Availability](#high-availability)
- [Troubleshooting](#troubleshooting)
- [FAQs](#faqs)
- [Contact Information](#contact-information)
- [References](#references)

---

## Introduction
Logrotate is a Linux utility used to manage log files by automatically rotating, compressing, removing, and mailing log files.  
This SOP defines the standard procedure to configure and manage log rotation using **logrotate**, ensuring optimal disk usage and system stability.

---

## Purpose
The purpose of this SOP is to:
- Prevent log files from consuming excessive disk space
- Automate log rotation and cleanup
- Maintain system performance and reliability
- Define rotation frequency and retention policies

---

## Key Features
- Automatic log rotation
- Compression of old logs
- Configurable retention period
- Supports daily, weekly, monthly rotation
- Post-rotation script execution

---

## Getting Started

### Pre-requisites

| License Type | Description | Commercial Use | Open Source |
|-------------|------------|---------------|------------|
| GPL | Free and open-source utility | Yes | Yes |

---

## Software Overview

| Software | Version |
|--------|---------|
| Logrotate | Latest Stable |

---

## System Requirements

| Requirement | Minimum Recommendation |
|------------|------------------------|
| Processor | Dual-Core |
| RAM | 1 GB or Higher |
| Disk Space | 5 GB or Higher |
| OS Required | Linux (Ubuntu, RHEL, Amazon Linux) |

---

## Important Ports

| Port | Description |
|-----|-------------|
| N/A | Logrotate does not require network ports |

---

## Dependencies

### Run-time Dependency

| Dependency | Version | Description |
|-----------|--------|------------|
| cron | Default | Used to schedule logrotate |

### Other Dependency

| Dependency | Version | Description |
|-----------|--------|------------|
| gzip | Default | Used for log compression |

---

## Logrotate Configuration Structure
Logrotate configuration files are located at:
- `/etc/logrotate.conf` (global configuration)
- `/etc/logrotate.d/` (application-specific configurations)

---

## How to Setup and Configure Logrotate

### Install Logrotate

```
sudo apt update
sudo apt install logrotate -y

```


### Verify installation:

```
logrotate --version
```
## Basic Logrotate Configuration

Example configuration file:

```
/var/log/nginx/*.log {
    daily
    rotate 7
    compress
    missingok
    notifempty
    create 0640 www-data adm
}
```

### Rotation Frequency
Log rotation can be configured as:


* **daily** – Rotate logs every day  
* **weekly** – Rotate logs every week  
* **monthly** – Rotate logs every month  
* **size 100M** – Rotate logs when the file size reaches 100 MB

## Retention Policy

Retention policy defines how many rotated logs to keep:

```bash
rotate 14
```

## Configuration

Configuration involves:

* Defining log file paths
* Setting rotation frequency
* Enabling compression
* Specifying retention count
* Adding post-rotate scripts if required


## Maintenance

Common maintenance commands:

```bash
logrotate -f /etc/logrotate.conf   # Force log rotation
systemctl restart rsyslog          # Restart logging service
```

## Monitoring

To monitor logrotate:

### Check cron logs

```bash
cat /var/log/syslog | grep logrotate
```

### Manually test configuration

```bash
logrotate -d /etc/logrotate.conf
```

## Disaster Recovery

* Backup logrotate configuration files
* Maintain archived logs on external storage
* Restore configuration files if failure occurs:
  * `/etc/logrotate.conf`
  * `/etc/logrotate.d/`

---

## High Availability

* Use centralized logging solutions:
  * ELK
  * CloudWatch
  * Splunk
* Maintain consistent logrotate configurations across servers
* Automate via configuration management tools:
  * Ansible
  * Puppet

## Troubleshooting

| Issue                | Cause             | Solution               |
|---------------------|------------------|------------------------|
| Logs not rotating   | Incorrect config | Validate config syntax |
| Permission denied   | Wrong ownership  | Fix file permissions   |
| Logs not compressed | gzip missing     | Install gzip           |


## Contact Information

| Name  | Email Address      |
|------|--------------------|
| Abhinav Tiwari | abhinav.tiwari.snaatak@mygurukulam.co |



## References

| Link | Description |
|------|------------|
| https://linux.die.net/man/8/logrotate | Official logrotate documentation |
| https://man7.org/linux/man-pages/man8/logrotate.8.html | Logrotate manual page |





