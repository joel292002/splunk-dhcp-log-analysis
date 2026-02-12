# Splunk DHCP Log Analysis

## Project Description

This project demonstrates how DHCP log data can be ingested and analyzed using Splunk Enterprise. The goal was to explore IP address allocation behavior, examine device request patterns, and perform basic anomaly checks using Splunk's Search Processing Language (SPL).

The dataset consists of sample DHCP traffic logs uploaded into a local Splunk instance for analysis.

---

## Environment

- Splunk Enterprise (local installation)
- Index: main
- Source type: dhcplogs
- Total events: 333
- Time range: Single short time window (approximately one minute)

---

## Data Ingestion

The DHCP log file was uploaded through Splunk’s "Add Data" interface using the Upload option.

Configuration:
- Source type manually defined as `dhcplogs`
- Data indexed into `main`

Data ingestion was verified using:

```
sourcetype=dhcplogs
| stats count
```

Result: 333 events successfully indexed.

---

## Analysis

### 1. Total DHCP Events

```
sourcetype=dhcplogs
| stats count
```

datauploaded1.png

Purpose:
Establish baseline event volume within the dataset.

---

### 2. Most Active Source IP Addresses

```
sourcetype=dhcplogs
| top src_ip
```

Purpose:
Identify client devices generating the highest number of DHCP requests.

---

### 3. Destination IP Allocation Patterns

```
sourcetype=dhcplogs
| top dst_ip
```

Purpose:
Observe which IP addresses were most frequently assigned.

---

### 4. DHCP Activity Per Device

```
sourcetype=dhcplogs
| stats count by src_ip
| sort - count
```

Purpose:
Quantify request frequency per device to detect repeated or abnormal lease behavior.

---

### 5. Time-Based Activity Analysis

```
sourcetype=dhcplogs
| timechart span=1m count
```

Result:
All DHCP events occurred within a single minute, indicating a short burst of network activity rather than susta
