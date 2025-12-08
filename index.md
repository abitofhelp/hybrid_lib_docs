# Hybrid Library Documentation

**Version:** 1.0.0
**Date:** December 08, 2025
**SPDX-License-Identifier:** BSD-3-Clause<br>
**License File:** See the LICENSE file in the project root<br>
**Copyright:** 2025 Michael Gardner, A Bit of Help, Inc.<br>
**Status:** Released

---

## Overview

Shared documentation for hybrid library projects implementing hexagonal architecture patterns with functional error handling in Ada 2022 and Go.

**Key Capabilities:**

- DDD/Clean/Hexagonal architecture demonstration
- Functional error handling via Result monad
- SPARK-compatible design for formal verification
- Embedded-safe patterns (no heap allocation)
- Cross-platform: Linux, macOS, BSD, Windows, Embedded

---

## Quick Navigation

### Getting Started

- **[Quick Start Guide](quick_start.md)** - Installation and first program
- **[Build Profiles](guides/build_profiles.md)** - Configure for different targets

### Formal Documentation

- **[Software Requirements Specification](templates/software_requirements_specification.md)** - Functional and non-functional requirements
- **[Software Design Specification](templates/software_design_specification.md)** - Architecture and detailed design
- **[Software Test Guide](templates/software_test_guide.md)** - Testing strategy and execution

### Developer Guides

- **[All About Our API](guides/all_about_our_api.md)** - Three-package API pattern
- **[Architecture Enforcement](guides/architecture_enforcement.md)** - Layer dependency rules
- **[Error Handling Strategy](guides/error_handling_strategy.md)** - Result monad patterns

---

## Architecture

Hybrid libraries implement a 4-layer hexagonal architecture:

```text
+-----------------------------------------------------------------+
|                          API Layer                               |
|  Library.API (facade) + Library.API.Desktop/Windows/Embedded    |
+----------------------------------+------------------------------+
                                   |
+----------------------------------v------------------------------+
|                      Application Layer                           |
|  Use Cases (operations) + Inbound/Outbound Ports                |
+----------------------------------+------------------------------+
                                   |
+----------------------------------v------------------------------+
|                    Infrastructure Layer                          |
|  I/O Adapters (Desktop, Windows, Embedded) + Platform Ops       |
+----------------------------------+------------------------------+
                                   |
+----------------------------------v------------------------------+
|                       Domain Layer                               |
|  Entities + Value Objects + Result Monad + Error Types          |
+-----------------------------------------------------------------+
```

**Design Principles:**

- Dependencies flow inward (toward Domain)
- Domain layer has zero external dependencies
- Infrastructure implements ports defined in Application
- API provides stable public interface
- Generic I/O plugin pattern enables platform portability

---

## Diagrams

### Language-Agnostic

- [Library Architecture](diagrams/library_architecture.svg)

### Ada Examples

- [API Re-export Pattern (Ada)](diagrams/ada/api_reexport_pattern_ada.svg)
- [Error Handling Flow (Ada)](diagrams/ada/error_handling_flow_ada.svg)
- [Package Structure (Ada)](diagrams/ada/package_structure_ada.svg)
- [Static Dispatch (Ada)](diagrams/ada/static_dispatch_ada.svg)
- [Three Package API (Ada)](diagrams/ada/three_package_api_ada.svg)

### Go Examples

- [API Re-export Pattern (Go)](diagrams/go/api_reexport_pattern_go.svg)
- [Error Handling Flow (Go)](diagrams/go/error_handling_flow_go.svg)
- [Package Structure (Go)](diagrams/go/package_structure_go.svg)
- [Static Dispatch (Go)](diagrams/go/static_dispatch_go.svg)
- [Three Package API (Go)](diagrams/go/three_package_api_go.svg)

---

## Platform Support

| Platform | Status | Notes |
|----------|--------|-------|
| **Linux** | Full | Primary development platform |
| **macOS** | Full | Fully supported |
| **BSD** | Full | Fully supported |
| **Windows** | Full | Windows 11+ |
| **Embedded** | Stub | Custom adapter required |

---

## Need Help?

- Check the [Quick Start Guide](quick_start.md) for common issues
- Review the [Software Test Guide](templates/software_test_guide.md) for testing help
- See [Error Handling Strategy](guides/error_handling_strategy.md) for Result monad usage

---

**License:** BSD-3-Clause
**Copyright:** 2025 Michael Gardner, A Bit of Help, Inc.
