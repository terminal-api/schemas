# schemas

Public Avro schemas for Terminal connector deliveries.

This repository is the customer-facing contract for messages published by Terminal's Kafka connector. Pin to a git tag when integrating.

## Kafka

Messages on customer Kafka topics are Avro-encoded `MessageWrapper` records (`kafka/avro/message.avsc`). Each message sets `eventType`, `model`, and exactly one field under `detail`.

| File | Record |
|------|--------|
| `message.avsc` | `MessageWrapper` / `MessageDetail` |
| `common.avsc` | Shared nested types |
| `vehicle.avsc` | `Vehicle` |
| `driver.avsc` | `Driver` |
| `device.avsc` | `Device` |
| `group.avsc` | `Group` |
| `trailer.avsc` | `Trailer` |
| `trip.avsc` | `Trip` |
| `safety-event.avsc` | `SafetyEvent` |
| `fault-code-event.avsc` | `FaultCodeEvent` |
| `hos-log.avsc` | `HOSLog` |
| `hos-daily-log.avsc` | `HOSDailyLog` |
| `ifta-vehicle-month.avsc` | `IFTAVehicleMonth` |
| `vehicle-location.avsc` | `VehicleLocation` |
| `vehicle-stat-log.avsc` | `VehicleStatLog` |
| `vehicle-utilization.avsc` | `VehicleUtilizationDay` |

Namespace for all records: `com.withterminal.api`.

## Versioning

Releases are published as git tags (for example `v0.1.0-beta.1`). See [CHANGELOG.md](CHANGELOG.md).

During beta, minor schema changes may still land; pin to a tag and upgrade deliberately.

## License

Apache License 2.0. See [LICENSE](LICENSE).
