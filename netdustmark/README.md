# NetDust Mark

**NetDust Mark** is the official benchmarking application for the netdust programming language. It provides a simple and consistent way to measure runtime performance across different netdust engine implementations.

Designed as a native Windows desktop application, NetDust Mark features an intuitive graphical interface for executing benchmark suites, comparing results, and analyzing runtime performance.

## Installation

NetDust Mark can be installed easily using paxon.

`paxon -S netdustmark`

## Features

* Windows GUI built with C# .NET
* Official benchmark suites for the netdust ecosystem
* Consistent and reproducible benchmark execution
* Runtime performance comparison
* Detailed benchmark reports and statistics
* Extensible benchmark architecture

## Runtime Support

### Current

* **NDR (NetDust Runtime)** — Native C++ runtime engine

### Planned

* **Noctura Engine** — Managed C# runtime implementation

Future releases will allow selecting the runtime engine before running benchmarks, making it possible to compare execution speed and performance characteristics between multiple netdust runtimes.

## Purpose

NetDust Mark serves as the reference benchmarking tool for the netdust ecosystem. It is intended for:

* Runtime performance evaluation
* Engine regression testing
* Performance optimization
* Comparing multiple runtime implementations
* Measuring improvements across netdust releases

## Platform

* Windows 10 / Windows 11
* C# (.NET) desktop application
* Native execution powered by the NDR engine
