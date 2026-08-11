# Changelog

All notable changes to Terminal public schemas are documented here.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project uses [Semantic Versioning](https://semver.org/spec/v2.0.0.html) via git tags.

## [Unreleased]

### Added

- Initial public Kafka Avro schemas mirrored from Terminal's connector wire format.
- Shared types in `kafka/avro/common.avsc`.
- `MessageWrapper` envelope in `kafka/avro/message.avsc`.
- Model schemas: Vehicle, Driver, Device, Group, Trailer, Trip, SafetyEvent, FaultCodeEvent, HOSLog, HOSDailyLog, IFTAVehicleMonth, VehicleLocation, VehicleStatLog, VehicleUtilizationDay.
- Example JSON payloads for Vehicle, Driver, Trip, and VehicleLocation.
