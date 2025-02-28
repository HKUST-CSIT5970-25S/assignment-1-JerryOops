[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/IAASVEAZ)
# CSIT5970 Assignment-1: EC2 Measurement (2 questions, 4 marks)

### Deadline: 11:59PM, Feb, 28, Friday

---

### Name: ZHANG, Jiaqi
### Student Id: 21071753
### Email: jzhangkd@connect.ust.hk

---

## Question 1: Measure the EC2 CPU and Memory performance

1. (1 mark) Report the name of measurement tool used in your measurements (you are free to choose *any* open source measurement software as long as it can measure CPU and memory performance). Please describe your configuration of the measurement tool, and explain why you set such a value for each parameter. Explain what the values obtained from measurement results represent (e.g., the value of your measurement result can be the execution time for a scientific computing task, a score given by the measurement tools or something else).

    > **Tool**: Phoronix Test Suite
    >
    > Configuration of CPU Performance
    >
    > - **Command**: `phoronix-test-suite run pts/compress-7zip`
    > - **Result**: Compression Rating & Decompression Rating 
    >   - **Explanation**: Compression Rating & Decompression Rating represent the system's efficiency in compressing and decompressing data, measured in MIPS (Million Instructions Per Second), where higher values indicate better performance.
    >
    > Configuration of Memory Performance
    >
    > - **Command**: `phoronix-test-suite run pts/ramspeed`
    > - **Parameter**:
    >   - **Type**: 6 (Test All Options - Copy, Scale, Add, Triad, Average)
    >   - **Benchmark**: 3 (Test All Options - Integer, Floating Point)
    >   - **Explanation**: To test all the possible options and achieve maximum coverage.
    > - **Result**: Integer Benchmark & Floating Point Benchmark
    >   - **Explanation**: Integer Benchmark & Floating Point Benchmark measure the system's ability to handle integer and floating-point operations, respectively, with higher values indicating faster processing speeds.

2. (1 mark) Run your measurement tool on general purpose `t2.micro`, `t2.medium`, and `c5d.large` Linux instances, respectively, and find the performance differences among these instances. Launch all the instances in the **US East (N. Virginia)** region. Does the performance of EC2 instances increase commensurate with the increase of the number of vCPUs and memory resource?

    In order to answer this question, you need to complete the following table by filling out blanks with the measurement results corresponding to each instance type.

    | Size        | CPU performance | Memory performance |
    | ----------- | --------------- | ------------------ |
    | `t2.micro` | Compression: 4184 MIPS, Decompression: 3170 MIPS | Integer Average: 10571.23 MB/s, Float Average: 11023.87 MB/s |
    | `t2.medium`  | Compression: 10001 MIPS, Decompression: 5977 MIPS | Integer Average: 19260.55 MB/s, Float Average: 11087.16 MB/s |
    | `c5d.large` | Compression: 7856 MIPS, Decompression: 5184 MIPS | Integer Average: 14023.67 MB/s, Float Average: 13610.85 MB/s |

    > Region: US East (N. Virginia). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI.

## Question 2: Measure the EC2 Network performance

1. (1 mark) The metrics of network performance include **TCP bandwidth** and **round-trip time (RTT)**. Within the same region, what network performance is experienced between instances of the same type and different types? In order to answer this question, you need to complete the following table.

    | Type                      | TCP b/w (Mbps) | RTT (ms) |
    | ------------------------- | -------------- | -------- |
    | `t3.medium` - `t3.medium` | 4125 Mbps      | 0.201 ms |
    | `m5.large` - `m5.large`   | 5006 Mbps      | 0.162 ms |
    | `c5n.large` - `c5n.large` | 5077 Mbps      | 0.133 ms |
    | `t3.medium` - `c5n.large` | 2433 Mbps      | 0.644 ms |
    | `m5.large` - `c5n.large`  | 4972 Mbps      | 0.123 ms |
    | `m5.large` - `t3.medium`  | 2423 Mbps      | 0.562 ms |

    > Region: US East (N. Virginia). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI. Note: Use private IP address when using iPerf within the same region. You'll need iPerf for measuring TCP bandwidth and Ping for measuring Round-Trip time.

2. (1 mark) What about the network performance for instances deployed in different regions? In order to answer this question, you need to complete the following table.

    | Connection                | TCP b/w (Mbps) | RTT (ms) |
    | ------------------------- | -------------- | -------- |
    | N. Virginia - Oregon      | 32.5 Mbps      | 63.1 ms  |
    | N. Virginia - N. Virginia | 4921 Mbps      | 0.122 ms |
    | Oregon - Oregon           | 4962 Mbps      | 0.209 ms |

    > Region: US East (N. Virginia), US West (Oregon). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI. All instances are `c5.large`. Note: Use public IP address when using iPerf within the same region.
