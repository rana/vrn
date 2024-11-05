# `vrn` - Variable Integer Compression Library in Rust

A high-performance variable integer compression library implemented in Rust. This library provides efficient encoding and decoding of integers using variable-length compression techniques (VARINT), optimized for space efficiency while maintaining fast access times.

## Overview

`vrn` implements variable-length integer encoding, a compression technique widely used in systems like Protocol Buffers and database engines. The library offers:

- Space-efficient integer compression for both `u32` and `usize` types
- Optimized batch operations for arrays of integers
- Zero-copy decoding capabilities
- Constant-time length calculations
- Zero external dependencies

## Features

- **Variable Length Encoding**: Compresses integers using 7 bits per byte with a continuation bit
- **Flexible Type Support**: Handles both `u32` and `usize` integer types
- **Batch Operations**: Efficient encoding/decoding of integer arrays
- **Memory Safe**: Fully safe Rust implementation with no unsafe code
- **Performance Optimized**: Inline functions and minimal memory allocation
- **Well-Tested**: Comprehensive test suite covering edge cases and common scenarios

## Technical Details

The implementation uses a variable-length encoding scheme where:
- Each byte uses 7 bits for data and 1 bit as a continuation flag
- Small numbers (0-127) require only a single byte
- Larger numbers use multiple bytes, with efficient bit packing
- Maximum encoding length is 4 bytes for u32 and 8 bytes for usize

## API Reference

### Core Functions

```rust
// Single integer operations
pub fn u32_byt_len(v: u32) -> usize
pub fn u32_pck(v: u32, pck: &mut [u8]) -> usize
pub fn u32_unp(pck: &[u8]) -> U32Unp

// Batch operations
pub fn u32s_byt_len(blk: &[u32]) -> usize
pub fn u32s_pck(src: &[u32], dst: &mut [u8])
pub fn u32s_unp(src: &[u8], dst: &mut [u32])

// Similar functions available for usize type
```

### Performance Characteristics

- O(1) length calculation for single integers
- O(n) compression and decompression time
- Space efficiency varies with number magnitude:
  - 1 byte for values 0-127
  - 2 bytes for values 128-16383
  - 3 bytes for values 16384-2097151
  - 4 bytes for values 2097152-268435455

## Use Cases

- Database storage optimization
- Network protocol implementations
- File format compression
- Memory-constrained systems
- High-performance data processing pipelines

## Implementation Notes

The library builds on established variable integer encoding principles while providing a modern, safe Rust implementation. It draws inspiration from:
- Google Protocol Buffers' VARINT encoding
- Stream VByte compression techniques
- Variable-length quantity (VLQ) encoding standards

## Development

The project follows Rust best practices with:
- Documentation comments for all public APIs
- Comprehensive unit tests
- Inline optimizations for performance-critical code
- Clear error handling and type safety

## References

- [Variable-length quantity - Wikipedia](https://en.wikipedia.org/wiki/Variable-length_quantity)
- [Protocol Buffers Encoding](https://developers.google.com/protocol-buffers/docs/encoding)
- [Stream VByte: Breaking New Speed Records for Integer Compression](https://lemire.me/blog/2017/09/27/stream-vbyte-breaking-new-speed-records-for-integer-compression/)

## File Tree
```sh
.
├── Cargo.toml
├── LICENSE
├── README.md
└── src
    └── lib.rs

2 directories, 4 files
```
