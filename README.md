# Cisco Catalyst 3650 Switch Recovery & Configuration

## Overview
Self-directed lab project involving the recovery and secure configuration of a Cisco Catalyst 3650 Series enterprise switch (WS-C3650-48TS). This project involved diagnosing boot failures, recovering switch access, performing a factory reset, and configuring the switch with secure administrative settings.

## Hardware
- Cisco Catalyst 3650 Series Switch (WS-C3650-48TS)
- USB console cable
- Personal PC running PuTTY

## Problems Diagnosed
- Boot loops on startup
- Stack-member failures
- Missing boot variables
- Corrupted startup configuration

## Recovery Process

### 1. Console Access
Connected to the switch via USB console cable and configured PuTTY with the correct serial COM port settings to access the switch CLI.

### 2. Bootloader Access
Accessed the switch bootloader prompt (`switch:`) by interrupting the boot process. Used this environment to diagnose the cause of boot failures and missing boot variables.

### 3. Bypassing Corrupted Startup Config
Set the following environment variable to bypass the corrupted startup configuration and regain administrative access:

`SWITCH_IGNORE_STARTUP_CFG=1` 

### 4. Factory Reset
Performed a full factory reset using the following commands:

`write erase`
`delete flash:vlan.dat`
`reload`

### 5. Secure Configuration
After recovery, configured the switch with the following:
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