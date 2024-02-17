---
title: The Computing-Aware Routing Architecture in Computing-Aware Traffic Steering
abbrev: CAR Architecture
category: info

docname: draft-peng-cats-car-architecture-latest
submissiontype: IETF
number:
date:
consensus: true
v: 3
area: Routing area
workgroup: cats
keyword:
 - User Experience
 - Collaborative Networking
 - Service optimization

author:
 -
    fullname: "Tianhao Peng"
    organization: Beijing Jiaotong University
    email: "th.peng@bjtu.edu.cn"
 -
    fullname: "Yuyin Ma"
    organization: Beijing Jiaotong University
    email: "mayuyin@bjtu.edu.cn"

normative:

informative:


--- abstract

This document proposes a compute-aware routing (CAR) architecture for Computing-Aware Traffic Steering (CATS), designed to support routing systems with compute resource awareness and provide a standardized approach for network devices and services.


--- middle

# Introduction

With the continuous increase of computing resources and the popularity of distributed computing, how to fully utilize these dispersed computing resources to provide better services has become an important challenge.
To address this challenge, Computing-Aware Traffic Steering (CATS) has been proposed.

CATS requires the network to be able to perceive information about computing resources and select appropriate service instances based on the joint indicators of computing and the network, thereby achieving dynamic control of network traffic.
In the implementation of CATS, a key task is to design a message format that can transmit computing resource information.

Therefore, the Computing-Aware Routing (CAR) message format is proposed.

The CAR is a flexible and powerful message transmission method designed to support computing resource-aware routing systems.


# The Computing-Aware Routing Headers (CARH)

```
 0                   1                   2                   3
 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|Version|     Time to Live      |            Length             |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                                                               |
|                       Timestamp (64 bits)                     |
|                                                               |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|  CAI Type[0]  |                 CAI Value[0]                  |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                              ...                              |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|  CAI Type[n]  |                 CAI Value[n]                  |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
```

The CARH contains the following fields:
- Version Number (4-bit): The version number indicates the CARH format version.
- Time to Live (8-bit): Time to Live indicates the effective time of the resource information represented by CARH.
- Length (16-bit): Length of the CARH.
- Timestamp (64-bit): Timestamp for perceiving resource information.
- CAI Type (8-bit): Computing-Aware Info Type (CAI Type) represents a type of computing resource and the order of magnitude corresponding to the specific value of that type of resource. This section corresponds one-to-one with the CAI Value.
- CAI Value (24-bit): Computing-Aware Info Value (CAI Value) represents the specific value of the resource identified by the CAI Type.

# Computing-Aware Info (CAI)

In order to comprehensively evaluate the computing power in the network, CARH needs to introduce a series of dynamic performance indicators to capture real-time changes in computing resources.

These indicators need to cover key performance parameters of network devices during operation, such as CPU Utilization, CPU Frequency, CPU Cores, Memory Utilization, Memory Frequency, Storage Utilization, GPU Memory, GPU Utilization, etc.

In CARH, use Computing-Aware Info (CAI) to carry these key performance parameters.

Computing-Aware Info (CAI) consists of two parts: Computing-Aware Info Type (CAI Type) and Computing-Aware Info Value (CAI Value).

Use the CAI Type field to represent the type of resource being carried, and use the CAI Value field to represent the numerical value and order of magnitude corresponding to the resource being carried.

Here are some definitions of the CAI Type field.

- 0x01 - CPU Utilization: Indicates the percentage of time the CPU processor is executing tasks. The calculation formula is the used CPU time divided by the total CPU time.
- 0x02 - CPU Frequency: Refers to the number of instructions executed by the CPU per second, usually in hertz (Hz).
- 0x03 - CPU Cores: Represents the number of physical cores in the CPU processor. Multi-core processors can execute multiple tasks simultaneously.
- 0x04 - Memory Utilization: Indicates the percentage of system memory in use. The calculation formula uses memory divided by total memory.
- 0x05 - Memory Frequency: Refers to the clock speed of RAM, indicating the amount of data that the memory module can transfer per second.
- 0x06 - Storage Utilization: Indicates the percentage of storage capacity being used in the storage system. The calculation formula uses storage divided by total storage capacity.
- 0x07 - GPU Memory: Refers to the memory on the graphics processing unit (GPU) used to store data required for graphics and computing tasks.
- 0x08 - GPU Utilization: Indicates the percentage of time the GPU processor is performing tasks. The calculation formula is the used GPU time divided by the total GPU time.

# Advanced Info
Dynamic performance indicators can only serve as basic information transmitted in CARH. In fact, based on performance indicator information, some advanced performance indicators can be established according to specific network scenarios.
Advanced info is also a supplementary definition of CAI Type.

## 0xF0 - Composite Performance Score (CPS)

From the perspective of computing power, a computing power weight allocation mechanism can be introduced to assign appropriate weights to different computing power factors.

This mechanism gives appropriate weights to different computing power factors to more accurately reflect their relative importance when calculating comprehensive performance indicators.

For example, in some scenarios, CPU utilization may be more critical, while memory usage may be more important in other scenarios. This can be customized by network administrators according to specific needs, or adjusted through CATS intelligent algorithms for Self-Adaptation.

Therefore, a comprehensive scoring model can be proposed to take into account various computing power factors and generate a comprehensive score.

This score can be a standardized value that reflects the overall computing power status of the system. The formulation of a comprehensive scoring model can combine Data Analysis and network topology features.

## 0xF1 - Network Quality Index (NQI)

From the perspective of network status, a network quality measurement mechanism can be introduced to evaluate network quality.

Network Quality Index (NQI) takes into account several important performance indicators in the network, including latency, packet loss rate, bandwidth utilization, etc.

The goal of NQI is to provide a single metric to measure the overall quality of the network, so that network administrators and system operators can more easily understand the performance of the network and take corresponding measures to optimize the network.

The definition of NQI is based on the weighted average of a series of network performance indicators. Each performance indicator is assigned a weight, which reflects the relative importance of each indicator to network quality. Then, by multiplying the values of each indicator with its corresponding weight and adding all weighted values, a comprehensive score, namely NQI, is obtained.

# Security Considerations

TBD.


# IANA Considerations

This document has no IANA actions.


--- back

# Acknowledgments
{:numbered="false"}

TODO acknowledge.
