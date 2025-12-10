# Hybrid_Lib_Ada Documentation

**Version:** 2.0.0<br>
**Date:** December 09, 2025<br>
**SPDX-License-Identifier:** BSD-3-Clause<br>
**License File:** See the LICENSE file in the project root<br>
**Copyright:** © 2025 Michael Gardner, A Bit of Help, Inc.<br>
**Status:** Released

---

## Overview

Documentation for Hybrid_Lib_Ada - a professional Ada 2022 library demonstrating hybrid DDD/Clean/Hexagonal architecture with functional error handling.

**Key Capabilities:**

- 4-layer hexagonal architecture (Domain, Application, Infrastructure, API)
- Functional error handling via Result monad (no exceptions)
- Three-package API pattern for flexible dependency injection
- Generic I/O plugin pattern for platform portability
- Embedded-safe design (no heap allocation, bounded types)
- SPARK-compatible for formal verification
- Cross-platform: Linux, macOS, Windows, Embedded

---

## Quick Navigation

### Getting Started

- **[Quick Start Guide](quick_start.md)** - Installation and first program
- **[Build Profiles](guides/build_profiles.md)** - Configure for different targets

### Formal Documentation

- **[Software Requirements Specification](formal/software_requirements_specification.md)** - Functional and non-functional requirements
- **[Software Design Specification](formal/software_design_specification.md)** - Architecture and detailed design
- **[Software Test Guide](formal/software_test_guide.md)** - Testing strategy and execution

### Developer Guides

- **[All About Our API](guides/all_about_our_api.md)** - Three-package API pattern
- **[Architecture Enforcement](guides/architecture_enforcement.md)** - Layer dependency rules
- **[Error Handling Strategy](guides/error_handling_strategy.md)** - Result monad patterns

---

## Architecture

Hybrid_Lib_Ada implements a 4-layer hexagonal architecture:

```text
+-----------------------------------------------------------------+
|                          API Layer                               |
|  Hybrid_Lib_Ada.API (facade) + API.Desktop + API.Operations    |
+----------------------------------+------------------------------+
                                   |
+----------------------------------v------------------------------+
|                      Application Layer                           |
|  Use Cases (Greet) + Inbound/Outbound Ports + Commands          |
+----------------------------------+------------------------------+
                                   |
+----------------------------------v------------------------------+
|                    Infrastructure Layer                          |
|  Adapters (Console_Writer) + Platform Implementations           |
+----------------------------------+------------------------------+
                                   |
+----------------------------------v------------------------------+
|                       Domain Layer                               |
|  Value Objects (Person) + Result Monad + Error Types            |
+-----------------------------------------------------------------+
```

**Design Principles:**

- Dependencies flow inward (toward Domain)
- Domain layer has zero external dependencies
- Infrastructure implements ports defined in Application
- API provides stable public interface via three-package pattern
- Generic I/O plugin pattern enables platform portability
- Static dispatch via generics (zero runtime overhead)

---

## API Operations

Hybrid_Lib_Ada exposes operations through a three-package API pattern:

| Operation | Description | Input | Output |
|-----------|-------------|-------|--------|
| `Greet` | Generate greeting for a person | `Greet_Command` | `Unit_Result.Result` |

**Usage Example:**

```ada
with Hybrid_Lib_Ada.API;

procedure Example is
   use Hybrid_Lib_Ada.API;
   Cmd : constant Greet_Command := Create_Greet_Command ("Alice");
   Result : constant Unit_Result.Result := Greet (Cmd);
begin
   if Unit_Result.Is_Ok (Result) then
      -- Success - greeting written to console
   end if;
end Example;
```

---

## Diagrams

- [Library Architecture](diagrams/library_architecture.svg)
- [API Re-export Pattern](diagrams/ada/api_reexport_pattern_ada.svg)
- [Error Handling Flow](diagrams/ada/error_handling_flow_ada.svg)
- [Package Structure](diagrams/ada/package_structure_ada.svg)
- [Static Dispatch](diagrams/ada/static_dispatch_ada.svg)
- [Three Package API](diagrams/ada/three_package_api_ada.svg)

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
- Review the [Software Test Guide](formal/software_test_guide.md) for testing help
- See [Error Handling Strategy](guides/error_handling_strategy.md) for Result monad usage

---

**License:** BSD-3-Clause
**Copyright:** 2025 Michael Gardner, A Bit of Help, Inc.
