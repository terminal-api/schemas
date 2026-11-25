# Kafka Example Payloads

Canonical sample messages for all 14 Common Models in [`kafka/avro/`](../avro), including all 12 `VehicleStatLog` stat types. Every example is validated against `com.withterminal.api.MessageWrapper` (`kafka/avro/message.avsc`).

## Directory Structure

- [`avro-json/`](avro-json/) — Strict **Apache Avro JSON encoding** of the `MessageWrapper` value (including Avro union branch wrappers such as `{"double": 88.5}` and `{"com.withterminal.api.VehicleStatLog": {...}}`). Suitable for Avro `JsonDecoder` / `avro-tools fromjson`.
- [`decoded/`](decoded/) — Human-readable **Kafka record JSON** showing `topic`, `key`, `headers`, and the decoded `MessageWrapper` `value` (without Avro union wrappers) for inspecting field names, nesting, and units.

## Wire-Format & Type Notes

- **Raw Avro binary value:** Terminal's Kafka connector serializes `com.withterminal.api.MessageWrapper` directly as standard Avro binary (there is **no** 5-byte Confluent Schema Registry magic byte + schema ID prefix).
- **Timestamps (`timestamp-micros`):** All timestamp fields (`timestamp`, `locatedAt`, `observedAt`, `startedAt`, `endedAt`, `createdAt`, `updatedAt`, `metadata.addedAt`, `metadata.modifiedAt`, `metadata.deletedAt`, etc.) use Avro's `timestamp-micros` logical type (`long`, microseconds since Unix epoch UTC). Avro readers with logical-type conversions decode these to native timestamp/`Instant`/`datetime` values.
- **Calendar dates (`date`):** `HOSDailyLog.date` and `VehicleUtilizationDay.date` use Avro's `date` logical type (`int`, days since `1970-01-01`). `IFTAVehicleMonth.month` is a `YYYY-MM` string.
- **Kafka headers (`terminal-*`):** Every record includes UTF-8 headers `terminal-application-id`, `terminal-connection-id`, `terminal-model`, `terminal-provider` (when present), and `terminal-event-time` (an **ISO 8601 UTC string**, set on models with an event time).
- **Event type (`eventType`):** Emitted as `"INSERT"` or `"MODIFY"` (uppercase) on the wire; compare case-insensitively in consumers.
- **Raw provider data (`raw`):** `null` unless `includeRaw: true` is enabled on the topic. See [`vehicle-stat-log/engine_coolant_temperature_with_raw.json`](decoded/vehicle-stat-log/engine_coolant_temperature_with_raw.json) for an example with `raw` populated.

## `VehicleStatLog` Stat Types

Each `VehicleStatLog` message sets `type` and populates only the matching value attribute (all other value attributes are `null`):

| `type` | Populated Field | Units / Values | Example |
| --- | --- | --- | --- |
| `battery_voltage` | `voltage` | Volts (V) | [`battery_voltage.json`](decoded/vehicle-stat-log/battery_voltage.json) |
| `coolant_percentage` | `percentage` | Percentage (0–100) | [`coolant_percentage.json`](decoded/vehicle-stat-log/coolant_percentage.json) |
| `engine_coolant_temperature` | `temperature` | Celsius (°C) | [`engine_coolant_temperature.json`](decoded/vehicle-stat-log/engine_coolant_temperature.json) |
| `engine_oil_percentage` | `percentage` | Percentage (0–100) | [`engine_oil_percentage.json`](decoded/vehicle-stat-log/engine_oil_percentage.json) |
| `engine_oil_pressure` | `pressure` | PSI | [`engine_oil_pressure.json`](decoded/vehicle-stat-log/engine_oil_pressure.json) |
| `engine_oil_temperature` | `temperature` | Celsius (°C) | [`engine_oil_temperature.json`](decoded/vehicle-stat-log/engine_oil_temperature.json) |
| `engine_rpm` | `rpm` | RPM | [`engine_rpm.json`](decoded/vehicle-stat-log/engine_rpm.json) |
| `engine_runtime` | `duration` | Milliseconds (ms) | [`engine_runtime.json`](decoded/vehicle-stat-log/engine_runtime.json) |
| `engine_state` | `state` | `"on"`, `"off"`, `"idle"` | [`engine_state.json`](decoded/vehicle-stat-log/engine_state.json) |
| `fuel_level` | `fuelPercentage` | Percentage (0–100) | [`fuel_level.json`](decoded/vehicle-stat-log/fuel_level.json) |
| `odometer` | `odometer` | Kilometers (km) | [`odometer.json`](decoded/vehicle-stat-log/odometer.json) |
| `total_fuel_consumption` | `fuelConsumed` | Liters (L) | [`total_fuel_consumption.json`](decoded/vehicle-stat-log/total_fuel_consumption.json) |
