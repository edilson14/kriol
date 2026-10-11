# Changelog

All notable changes to the Kriol compiler are documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/).

## [1.16.1] - 2026-10-11

### Fixed

- Reject records (`molda`) with recursive fields instead of crashing. A field
  whose type is the record being declared, directly or through an array, now
  gets its own diagnostic, and a field of unknown type is no longer added to the
  record, so computing the storage size can no longer recurse forever on
  self-referential or mutually recursive records. ([#14])
- Reject global initializers that read globals declared later, including through
  a function call or mutual recursion. The compiler reports one initialization
  order error per global. ([#19])
- Prefix generated global variables with `kriol.g.`, so a Kriol global can no
  longer clash with a C library or runtime symbol. ([#17])
- Rename the generated source name string to `__kriol.source_name`, keeping it
  out of the user function namespace. ([#18])
- Compute each record storage size once instead of recomputing it per use, and
  saturate the size rather than overflowing on doubling chains. ([#16])

### Changed

- Fail the Windows CI test step when `run_tests.ps1` fails. ([#15])

### Documentation

- Link the four-minute presentation video in the README.

## [1.16.0] - 2026-10-05

### Added

- Write compiler and runtime messages in Portuguese.

### Changed

- Improve test reporting.

## [1.15.0] - 2026-10-05

### Added

- Check program output, runtime errors and wasm runs in the test suite, and
  collect coverage.

### Fixed

- Fill repeated aggregate array elements with a loop.
- Allow `molda` literals inside f-string interpolations.

## [1.14.0] - 2026-10-04

### Added

- Multi-dimensional arrays, and arrays as parameters and return values.
- Write `molda` literals as `Type{field = value}`.

### Changed

- Rename `para` to `kebra`, and allow `pa` without a step.
- Divide like C, truncate reals into integers, and accept numbers in logical
  operators.
- Update the terminology from `Kuale` to `Kualeh`.

### Fixed

- Pass and return `molda` values by address, like arrays.

Releases before 1.14.0 are not covered here. See the
[git history](https://github.com/kriol-lang/kriol/commits/main) and the
[releases page](https://github.com/kriol-lang/kriol/releases).

[#14]: https://github.com/kriol-lang/kriol/pull/14
[#15]: https://github.com/kriol-lang/kriol/pull/15
[#16]: https://github.com/kriol-lang/kriol/pull/16
[#17]: https://github.com/kriol-lang/kriol/pull/17
[#18]: https://github.com/kriol-lang/kriol/pull/18
[#19]: https://github.com/kriol-lang/kriol/pull/19
[1.16.1]: https://github.com/kriol-lang/kriol/compare/v1.16.0-alpha+build2...v1.16.1-alpha+build1
[1.16.0]: https://github.com/kriol-lang/kriol/compare/v1.15.0-alpha+build1...v1.16.0-alpha+build2
[1.15.0]: https://github.com/kriol-lang/kriol/compare/v1.14.0-alpha+build1...v1.15.0-alpha+build1
[1.14.0]: https://github.com/kriol-lang/kriol/compare/v1.13.1-alpha+build1...v1.14.0-alpha+build1
