# PowerWalker NMC NG SNMP Monitoring

This template is designed for the **new generation (NG)** of PowerWalker UPS Network Management Cards (NMC NG). It utilizes the SNMP protocol (v1, v2c, or v3) to monitor critical power parameters, battery health, and system stability.

## 🚀 Overview
The goal of this monitoring solution is to provide early warning signs for potential power failures, battery degradation, or electrical instability in your UPS infrastructure. It covers everything from simple uptime tracking to critical alerts regarding battery runtime and voltage deviations.

## 📊 Monitored Metrics

### 🔋 Battery Health
* **Battery Status**: Tracks the operational state of the battery (triggers alert if status is not "normal").
* **Charge Remaining (%)**: Monitors the percentage of remaining charge with multi-level alerting:
    * 🔴 **High Priority**: Below 11%
    * 🟠 **Average Priority**: Below 25%
    * 🟡 **Warning Priority**: Below 50%
    * 🔵 **Info Priority**: Below 75%
* **Estimated Minutes Remaining**: Monitors how much runtime is left.
    * 💀 **Disaster Priority**: Less than 5 minutes remaining.

### ⚡ Power & Load
* **Input Voltage**: Detects overvoltage conditions (Alerts if voltage > 265V).
* **Output Voltage Stability**: Monitors the stability of the output voltage and alerts on significant deviations.
* **Current Load (%)**: Tracks the UPS load percentage (Alerts if load exceeds 85% to prevent overload).
* **Power Source**: Detects when the UPS switches from mains power to battery power.

### 🖥️ System Information
* **System Uptime**: Tracks how long the management card has been running.

## ⚙️ Configuration (Required Macros)
To use this template, you must configure the following SNMP macros on your Zabbix Host:

| Macro | Description | Default Value |
| :--- | :--- | :--- |
| `{$SNMP_PORT}` | The UDP port for SNMP communication. | `161` |
| `{$SNMP_USERNAME}` | Username for SNMPv3 authentication. | *Leave empty for v1/v2c* |
| `{$SNMP_AUTHPASS}` | Authentication password (for SNMPv3). | *Enter your password* |
| `{$SNMP_PRIVPASS}` | Privacy/Encryption password (for SNMPv3). | *Enter your password* |

## 🛠 Installation
1. **Download**: Download the `template_powerwalker_nmcng_snmp.yaml` file from this directory.
2. **Import**: In your Zabbix Frontend, navigate to **Configuration** -> **Templates**.
3. **Import File**: Click on **Import** and select the downloaded YAML file.
4. **Link Template**: Create or select a Host representing your PowerWalker UPS and link the **"PowerWalker NMC NG SNMP"** template.
5. **Configure Macros**: Update the `{$SNMP_...}` macros as required by your specific network/security configuration.

## 📈 Alert Severity Summary
* 💀 **DISASTER**: Critical battery depletion (< 5 min).
* 🔴 **HIGH**: Battery status abnormal, voltage instability, or extremely low charge (< 10%).
* 🟠 **AVERAGE/WARNING**: Power source change (on battery), high input voltage, or moderate charge drop.
* 🔵 **INFO**: Routine monitoring of charge levels.

---
**Author**: Kordian Dawid
**License**: [MIT License](LICENSE)

_Maintained as part of the [Zabbix Integrations](https://github.com/koda-pub/zabbix-integrations) repository._