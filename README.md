# Multilevel Cache Simulator

A C++-based multilevel cache simulator that models L1 and L2 caches and evaluates memory access patterns using a trace file.

## Overview

This project simulates a two-level cache hierarchy consisting of an L1 cache and an L2 cache. It processes read and write memory requests from an input trace and models cache hits, misses, and data movement between cache levels and main memory.

The simulator supports configurable cache sizes, block sizes, and associativity.

## Features

- Two-level cache hierarchy: L1 and L2
- Configurable cache size, block size, and associativity
- Direct-mapped, set-associative, and fully associative cache configurations
- Read and write memory operations
- Write-back policy
- Write-no-allocate policy for write misses
- Round-robin replacement policy
- Non-inclusive cache organization
- Memory access trace processing

## Project Structure

```text
Multilevel-Cache-Simulator/
├── cachesimulator.cpp
├── cacheconfig.txt
├── trace.txt
├── README.md
└── traceout.txt   (optional output file)
```

## Cache Configuration

The simulator reads cache parameters from `cacheconfig.txt`.

The configuration file contains the parameters for L1 and L2 caches in the following order:

```text
L1:
8
1
16
L2:
16
4
32
```

The parameters represent:

- **Block size:** Size of each cache block in bytes.
- **Associativity:** `1` indicates a direct-mapped cache; a positive value greater than `1` indicates a set-associative cache. Use `0` for a fully associative cache if supported by the implementation.
- **Cache size:** Cache capacity in KB.

For the example above:

| Parameter | L1 Cache | L2 Cache |
|---|---:|---:|
| Block size | 8 bytes | 16 bytes |
| Associativity | Direct-mapped | 4-way set-associative |
| Capacity | 16 KB | 32 KB |

Keep the configuration file in the same directory as the simulator executable when running the program.

## Input Trace

The simulator reads memory-access requests from `trace.txt`.

Each trace entry represents a read (`R`) or write (`W`) operation followed by a memory address in hexadecimal format.

Example:

```text
R 00000010
W 00000020
R 00000010
W 00000040
```

The simulator processes the requests in order and uses them to determine cache hits, misses, and data transfers.

## Cache Behavior

### Read Miss

When the requested data is not found in L1, the simulator checks L2. If the data is not found there, it must be fetched from main memory.

### Write Hit

For a write hit, the simulator updates the cached data according to the write-back policy.

### Write Miss

The simulator uses a write-no-allocate policy for write misses, meaning the missed data is not automatically loaded into the cache.

### Replacement Policy

When a cache set needs space for a new block, the simulator uses round-robin replacement.

### Cache Inclusion

The simulator uses a non-inclusive cache organization, meaning L1 blocks are not required to also exist in L2.

## How to Compile and Run

Make sure a C++ compiler such as GCC or MinGW is installed.

Open a terminal in the project directory.

### Compile

```bash
g++ cachesimulator.cpp -o cachesimulator
```

### Run

On Windows PowerShell:

```powershell
.\cachesimulator.exe
```

On Linux or macOS, if the executable is named `cachesimulator`:

```bash
./cachesimulator
```

Ensure that `cacheconfig.txt` and `trace.txt` are in the locations expected by the program. The output depends on how the simulator writes its results.

## Testing

To test the simulator:

1. Run it with the supplied configuration and trace files.
2. Try read and write operations that access the same address repeatedly.
3. Test accesses to different addresses to observe cache misses and replacements.
4. Modify cache size, block size, or associativity and compare the results.
5. Check the generated output, if the program produces an output file such as `traceout.txt`.

## Learning Outcomes

This project helps develop an understanding of:

- Cache memory hierarchy
- Cache hits and misses
- Cache block size and associativity
- Cache replacement policies
- Write-back and write-no-allocate policies
- Memory access traces
- The relationship between cache configuration and performance

## Future Improvements

- Add cache hit-rate and miss-rate statistics.
- Compare different replacement policies.
- Support more cache configurations.
- Add automated test cases.
- Compare the performance of different L1 and L2 configurations.

## Technologies Used

- C++
- Cache memory architecture
- File handling and trace-based simulation
