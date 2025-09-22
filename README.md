# RTKA-ML: Recursive Ternary Knowledge Algorithm for Machine Learning - Proof of Concept

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.17137875.svg)](https://doi.org/10.5281/zenodo.17137875)

**Status**: Proof of concept  
**License**: CC BY-NC-SA 4.0 (Research and non-commercial use only)  
**Author**: H. Overman (opsec.ee@pm.me)  

## Project Status

This repository contains a proof-of-concept implementation exploring the application of recursive ternary logic to machine learning. The code demonstrates core concepts but is not production-ready and lacks many features necessary for practical deployment. This implementation serves primarily to validate the theoretical approach and provide a foundation for future research.

## Current Capabilities

The implementation provides basic functionality for ternary logic operations extending Kleene's three-valued logic with arithmetic encodings. A simple tensor system supports multi-dimensional arrays with ternary values and confidence scores. Basic neural network layers implement forward pass computation with ternary weights. Gradient computation enables limited learning through confidence adjustment. Memory pooling reduces allocation overhead in controlled scenarios.

The system can perform simple training tasks on small datasets and demonstrates the mathematical feasibility of the approach. However, performance has not been rigorously benchmarked, and many optimizations remain unimplemented.

## Limitations

This proof of concept has significant limitations that prevent production use. Training is single-threaded with no parallelization support. The implementation supports only dense tensors without sparse representations. No GPU acceleration or distributed computing capabilities exist. The testing framework requires external dependencies not included in the repository. Performance benchmarks are preliminary and unvalidated. Error handling is incomplete with many edge cases unaddressed. The system lacks logging, monitoring, or debugging infrastructure. Model serialization uses a basic binary format without versioning or validation.

## Dependencies

Building this project requires GCC 4.9+ or Clang 3.4+ with C11 support. The math library (-lm) provides standard mathematical functions. POSIX threads (-lpthread) enable atomic operations. Optional AVX2 support requires a compatible processor and compiler flags. The testing framework requires Criterion 2.4+, which must be installed separately.

## Build Instructions

To compile the basic implementation without optimizations:

```bash
gcc -std=c11 -Wall -Wextra -O2 rtka_ml_enhanced_corrected.c -lm -lpthread -o rtka_ml
```

For optimized builds with AVX2 support on compatible systems:

```bash
gcc -std=c11 -Wall -Wextra -O3 -march=native -mavx2 rtka_ml_enhanced_corrected.c -lm -lpthread -o rtka_ml
```

Building tests requires Criterion installation. On Ubuntu/Debian systems:

```bash
sudo apt-get install libcriterion-dev
gcc -std=c11 rtka_ml_test_framework.c rtka_ml_enhanced_corrected.c -lcriterion -lm -lpthread -o test_rtka
```

Note that Criterion may need to be built from source on some systems. Refer to the Criterion documentation for platform-specific installation instructions.

## File Structure

The repository currently contains these core files:

- `rtka_ml_enhanced_corrected.c` - Main implementation with basic ternary operations
- `rtka_base.h` - Header defining core ternary types and operations
- `rtka_ml_test_framework.c` - Test suite skeleton (requires Criterion)
- `README.md` - This documentation

Additional files mentioned in the documentation such as CONTRIBUTING.md, detailed technical documentation, and example applications do not yet exist in the repository.

## Usage

The current implementation provides low-level C functions without high-level interfaces. Basic usage requires understanding the tensor and layer structures:

```c
// Example tensor creation
size_t dims[] = {10, 10};
ternary_tensor_t* tensor = tensor_create(dims, 2);
if (!tensor) {
    // Handle allocation failure
}

// Tensor must be manually destroyed
tensor_destroy(tensor);
```

Complete examples and tutorials are not yet available. The API is subject to change as the project evolves.

## Mathematical Foundation

The system implements Kleene's strong three-valued logic with values encoded as -1 (FALSE), 0 (UNKNOWN/MAYBE), and 1 (TRUE). Logical operations follow standard Kleene truth tables using min for AND and max for OR operations. Confidence propagation uses multiplicative rules for conjunction and inclusion-exclusion for disjunction.

Detailed mathematical analysis and proofs are planned but not yet documented. The current implementation serves as a computational validation of the basic concepts.

## Performance

Preliminary testing suggests memory pooling reduces allocation overhead compared to individual malloc calls. SIMD instructions provide speedup for confidence calculations when AVX2 is available. However, comprehensive benchmarking has not been performed, and performance claims should be considered speculative.

The switch to int8_t storage for ternary values reduces memory usage but may impact computational performance due to type conversions. Real-world performance characteristics remain to be determined through systematic benchmarking.

## Known Issues

The implementation has several known problems requiring attention. Memory management lacks comprehensive leak detection and validation. Concurrent access to shared tensors causes undefined behavior without external synchronization. Numerical stability in gradient computation has not been thoroughly analyzed. The testing framework is incomplete with many test cases unimplemented. Build configuration requires manual compiler flag management without CMake or autotools support.

## Future Work

The project requires substantial development before practical use. Immediate priorities include completing the test suite, implementing proper error handling throughout, and adding basic performance benchmarks. Longer-term goals involve exploring parallelization strategies, investigating sparse tensor representations, and developing higher-level Python bindings.

These goals represent research directions rather than committed development plans. The project may evolve in different directions based on research findings and community feedback.

## Contributing

This project is in early development and not yet ready for external contributions. If you are interested in the research direction, please contact the author directly to discuss collaboration opportunities.

## Contact

For questions about the research or collaboration opportunities:  
H. Overman - opsec.ee@pm.me

Please note this is a research project without support guarantees. Response times may vary.

## Disclaimer

This software is provided as-is without warranties of any kind. It is not suitable for production use and should be considered experimental research code. Users assume all risks associated with its use.

