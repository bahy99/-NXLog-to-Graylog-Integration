# NXLog to Graylog Integration

This repository contains configuration examples and instructions for setting up NXLog to send logs to Graylog.

## Table of Contents
- [Introduction](#introduction)
- [Prerequisites](#prerequisites)
- [Configuration](#configuration)
- [TLS/SSL Setup](#tls-ssl-setup)
- [Graylog Sidecar Management](#graylog-sidecar-management)
- [Contributing](#contributing)

## Introduction

This repository provides guidance on integrating NXLog with Graylog for efficient log management. It includes configurations for various scenarios and platforms.

## Prerequisites

- Installed and configured Graylog server.
- NXLog installed on the target system.
- Basic understanding of log management concepts.

## Configuration

Detailed steps for configuring NXLog and Graylog are provided in the [Configuration Guide](https://docs.nxlog.co/integrate/graylog.html).

### Adding a Windows Host to Graylog

To add a Windows host to Graylog and send logs from that host, follow these steps:

1. **Install NXLog on the Windows Host:**
   - Download and install NXLog on the Windows host from the [NXLog download page](https://nxlog.co/downloads/nxlog-ce?gaconnectorId=87110012-4af8-57bd-41be-76db8c238499&_gl=1*zy0ahl*_ga*MTY0MzgzNTA0OC4xNzA0NzI0MzA2*_ga_M5K1E1X2KD*MTcwNDk3MjMzNC40LjEuMTcwNDk3NDM4NS41OC4wLjA.#nxlog-community-edition).
   - Choose the options that fit your requirements during the installation.

2. **Configure NXLog on the Windows Host:**
   - Open the NXLog configuration file at `C:\Program Files\nxlog\conf\nxlog.conf` in a text editor.
   - Copy and paste the content of the provided configuration example for sending Windows logs over UDP.
   - Replace the placeholder IP address and port with the actual IP address and port of your Graylog server.
     ```xml
     <Extension gelf>
         Module xm_gelf
     </Extension>
     <Input dns_client_logs>
         Module im_etw
         Provider Microsoft-Windows-DNS-Client
     </Input>
     <Output graylog_udp>
         Module om_udp
         Host 192.168.43.29:12201
         OutputType GELF_UDP
     </Output>
     ```

3. **Restart NXLog:**
   - Save the configuration file and restart the NXLog service to apply the changes.

4. **Configure Graylog to Receive Windows Logs:**
   - Log in to the Graylog web interface.
   - Navigate to System > Inputs.
   - Choose an input type suitable for your configuration (e.g., GELF UDP).
   - Click "Launch new input" and configure the input parameters:
     - Choose the Graylog Node or enable the Global option.
     - Enter a friendly name for the input.
     - Specify the IP address and port to listen on.
   - Save the configuration.

5. **Verify Logs in Graylog:**
   - Check the Graylog web interface under System > Inputs to ensure that your new input is active.
   - Go to the Search page to verify that logs from the Windows host are being received. You can filter logs by the input you just created.

**Additional Notes:**
- Ensure that any firewalls on the Windows host or Graylog server allow the necessary traffic.
- Double-check the configuration files for any syntax errors or typos.
- If using TLS/SSL for secure communication, make sure to configure certificates on both the Graylog server and the Windows host accordingly.


## Contributing

Feel free to contribute by submitting issues or pull requests. Your feedback and improvements are highly valued.

