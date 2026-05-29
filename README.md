# Cisco Catalyst 3650 Switch Recovery & Configuration

## Overview
Self-directed lab project involving the recovery and secure configuration of three Cisco Catalyst 3650 Series enterprise switches (WS-C3650-48TS). This project involved diagnosing boot failures, recovering switch access, performing a factory reset, and configuring the switch with secure administrative settings.

## Hardware
- 3x Cisco Catalyst 3650 Series Switches (WS-C3650-48TS)
- USB console cable
- Personal PC running PuTTY

## Problems Diagnosed
- Boot loops on startup
- Stack-member failures
- Missing boot variables
- Corrupted startup configuration

## Recovery Process

### 1. Console Access
Connected to each switch via USB console cable and configured PuTTY with the correct serial COM port settings to access the switch CLI.

### 2. Bootloader Access
Accessed each switch's bootloader prompt (`switch:`) by interrupting the boot process. Used this environment to diagnose the cause of boot failures and missing boot variables.

### 3. Bypassing Corrupted Startup Config
Set the following environment variable to bypass the corrupted startup configurations and regain administrative access on affected switches:

`SWITCH_IGNORE_STARTUP_CFG=1` 

### 4. Factory Reset
Performed a full factory reset on each switch using the following commands:

`write erase`
`delete flash:vlan.dat`
`reload`

### 5. Stack Renumbering
Worked with a total of 3 switches. Two switches were configured as stack members and needed to be renumbered before they could be reused as standalone units. Used the following process to break the stack configuration:

- Identified each switch's stack member number
- Renumbered stack members to prevent them from attempting to rejoin a stack on boot
- Wiped all three switches independently to ensure clean standalone configurations
- Verified each switch booted independently without attempting stack negotiation

### 6. Secure Configuration
After recovery, configured each switch with the following:
- Hostname
- Local admin account
- Enable secret password
- Console authentication
- SSH access with RSA key generation
- VLAN interfaces
- Management IP address

## Concepts Learned
- Cisco IOS CLI navigation
- Switch stacking concepts
- Bootloader environment and recovery procedures
- Difference between startup-config and running-config
- Flash and NVRAM behavior
- Secure switch configuration best practices
- Serial/console administration with PuTTY
