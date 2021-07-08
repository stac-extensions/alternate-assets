# Changelog
All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

## [v1.1.0]

### Changed
- No longer reference a STAC version
- Alternate objects are not of type `Asset` but rather `AlternateAsset` which is just a restrictive version of an `Asset`

### Removed
- requirement for alternate (which meant it had to be used in all assets). There are no no required fields

## [v1.0.0]

Initial release

[Unreleased]: <https://github.com/stac-extensions/alternate-assets/compare/v1.1.0...HEAD>
[v1.1.0]: <https://github.com/stac-extensions/alternate-assets/compare/v1.0.0...v1.1.0>
[v1.0.0]: <https://github.com/stac-extensions/alternate-assets/tree/v1.0.0>
