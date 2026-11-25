# Changelog

All notable changes to Terminal public schemas are documented here.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project uses [Semantic Versioning](https://semver.org/spec/v2.0.0.html) via git tags.

## [Unreleased]

### Added

- Canonical Kafka example payloads under `kafka/examples/` (`avro-json/` and `decoded/`) for all 14 models, including all 12 `VehicleStatLog` stat types and an `includeRaw: true` example.

## [0.1.0-beta.1] - 2026-08-11

### Added

- Initial public Kafka Avro schemas mirrored from Terminal's connector wire format.
- Shared types in `kafka/avro/common.avsc`.
- `MessageWrapper` envelope in `kafka/avro/message.avsc`.
- Model schemas: Vehicle, Driver, Device, Group, Trailer, Trip, SafetyEvent, FaultCodeEvent, HOSLog, HOSDailyLog, IFTAVehicleMonth, VehicleLocation, VehicleStatLog, VehicleUtilizationDay.
