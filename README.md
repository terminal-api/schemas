# schemas

Public Avro schemas for Terminal connector deliveries.

This repository is the customer-facing contract for messages published by Terminal's Kafka connector. Pin to a git tag when integrating.

## Kafka

Messages on customer Kafka topics are raw Avro-encoded `MessageWrapper` records (`kafka/avro/message.avsc`, with no 5-byte Confluent Schema Registry prefix). Each message sets `eventType`, `model`, and exactly one field under `detail`.

Timestamps use Avro's `timestamp-micros` logical type (`long`, Unix epoch microseconds UTC) and calendar dates (`HOSDailyLog.date`, `VehicleUtilizationDay.date`) use Avro's `date` logical type (`int`, days since `1970-01-01`).

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

### Examples

Canonical example payloads for all 14 models (including all 12 `VehicleStatLog` stat types) live under [`kafka/examples/`](kafka/examples/) in both strict Avro JSON (`avro-json/`) and decoded Kafka record JSON (`decoded/`, including `topic`, `key`, and `terminal-*` headers).

## Versioning

Releases are published as git tags (for example `v0.1.0-beta.1`). See [CHANGELOG.md](CHANGELOG.md).

During beta, minor schema changes may still land; pin to a tag and upgrade deliberately.

## License

Apache License 2.0. See [LICENSE](LICENSE).
