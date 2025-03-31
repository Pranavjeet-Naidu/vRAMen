# vRAMen - GPU-Accelerated Hash Table

## Overview

vRAMen is a high-performance GPU-accelerated hash table implementation using CUDA. This project demonstrates how to implement an efficient hash table on the GPU using the linear probing technique for collision resolution. The implementation is optimized for massively parallel processing on NVIDIA GPUs.

## Features

- **Linear Probing Hash Table**: Uses linear probing for collision resolution
- **GPU Acceleration**: Leverages CUDA for parallel hash table operations
- **Key Operations**:
  - Insertion of key-value pairs
  - Lookup by key
  - Deletion of key-value pairs
  - Iteration over non-empty elements
- **Performance Benchmarking**: Compares performance against CPU-based `std::unordered_map`

## Technical Details

### Hash Table Implementation

The implementation uses linear probing, a simple and effective collision resolution strategy:
- When a collision occurs, the algorithm linearly searches for the next available slot
- The hash function used is a 32-bit Murmur3 hash, which provides good distribution
- Empty slots are marked with the special value `0xffffffff`
- Deleted keys remain in the table, but their values are marked as empty

### Performance

The GPU implementation demonstrates significantly higher throughput compared to CPU-based hash tables, especially for large datasets. Performance metrics are displayed during execution, showing:
- Insertion rate (million keys/second)
- Lookup rate (million keys/second)
- Deletion rate (million keys/second)

## Requirements

- NVIDIA GPU with CUDA support
- CUDA Toolkit (compatible with your GPU)
- C++ compiler that supports C++11 or later

## Building and Usage

### Building

```bash
# Navigate to the project directory
cd /path/to/vRAMen/linearprobing

# Build the project
nvcc -o linearprobing main.cpp linearprobing.cu -std=c++11
```

### Running

```bash
# Run the executable
./linearprobing
```

The program will:
1. Generate random key-value pairs
2. Insert them into the GPU hash table
3. Delete a subset of the key-value pairs
4. Benchmark the operations and compare with CPU performance
5. Verify correctness of the implementation

## Output Example

When you run the program, you'll see performance metrics like:

```
Random number generator seed = 1234567890
Initializing keyvalue pairs with random numbers...
Testing insertion/deletion of 67108864/33554432 elements into GPU hash table...
    GPU inserted 4194304 items in 10.123 ms (414.321 million keys/second)
    ...
    GPU delete 4194304 items in 8.765 ms (478.543 million keys/second)
Total time (including memory copies, readback, etc): 320.789 ms (209.123 million keys/second)
Timing std::unordered_map...
Total time for std::unordered_map: 1456.789 ms (46.012 million keys/second)
Success
```

## Implementation Notes

This implementation prioritizes simplicity and performance for demonstration purposes. In a production environment, you might want to consider:
- More sophisticated collision resolution strategies
- Variable-sized keys and values
- Dynamic resizing of the hash table
- Error handling and recovery mechanisms

## License

[Include your license information here]