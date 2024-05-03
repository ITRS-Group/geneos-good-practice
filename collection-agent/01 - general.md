# Collection Agent - Best Practice

## Introduction

The Collection Agent (CA) is a Geneos component that works along with a Netprobe to collect, process and transmit monitoring data to a Gateway.

## Operating Modes

### Managed

In Managed mode the Collection Agent is configured and controlled by a co-located Netprobe.

The configuration is held in a YAML file. There are three ways to drive the configuration:

* Built-in
* Custom
* Managed

Both the Built-in and Custom modes rely on a YAML file stored in the file system and the contents are not accessible or changeable via the Gateway Setup Editor (GSE). These mode can be considered loosely-coupled operating modes.

The Managed mode allows you to edit the YAML contents in the GSE and can be considered a closely-coupled operating mode.

### Unmanaged

In Unmanaged mode the Configuration Agent runs as a standalone process and can be in a different container or on a different system to the Netprobe that it sends data to. The Netprobe has no control over the configuration or the state of the Collection Agent. This can be considered an uncoupled operating mode.

## 