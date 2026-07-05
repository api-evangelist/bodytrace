# BodyTrace (bodytrace)

BodyTrace makes cellular-connected remote patient monitoring (RPM) devices - blood pressure monitors, body-weight scales, and pulse oximeters - that transmit readings directly over the cellular network with no phone, app, Wi-Fi, or Bluetooth pairing required. Each device encrypts measurements end-to-end and sends them to the BodyTrace platform, which exposes the data to healthcare organizations, EHRs, and RPM programs over a simple HTTP API using HTTP Basic authentication. Consumers can pull device readings (data values) on a polling loop or receive them pushed to a customer-hosted HTTP endpoint. BodyTrace sells to organizations, not individuals; API and device provisioning are arranged through BodyTrace sales.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/bodytrace/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/bodytrace/refs/heads/main/apis.yml)

## Public API status

BodyTrace exposes a **real but gated / partner-facing** HTTP API. There is no open self-serve developer portal - devices and API credentials are arranged with BodyTrace sales. The confirmed, publicly documented surface is the data values pull endpoint (`GET /1/device/{imei}/datavalues`) and the device push-message payload; other logical APIs below are honestly modeled from BodyTrace's IMEI-centric data model and marked as such. No public WebSocket API is documented.

## Tags

- Remote Patient Monitoring
- RPM
- Cellular
- Medical Devices
- Digital Health
- Blood Pressure
- Connected Devices
- IoT

## Timestamps

- **Created:** 2026-07-05
- **Modified:** 2026-07-05

## APIs

### BodyTrace Observations (Data Values) API

Retrieve the latest and historical device readings (data values) for a provisioned device by IMEI - weight, systolic, diastolic, pulse, SpO2, battery voltage, and signal strength - filtered by name and time range. This is the confirmed, documented pull surface at `GET /1/device/{imei}/datavalues`.

- **Human URL:** [https://www.bodytrace.com/medical/](https://www.bodytrace.com/medical/)
- **Base URL:** `https://us.data.bodytrace.com/1`

#### Tags

- Observations
- Data Values
- Readings

#### Properties

- [Documentation](https://www.bodytrace.com/medical/)
- [OpenAPI](openapi/bodytrace-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/bodytrace.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/bodytrace.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### BodyTrace Data Messages API

Retrieve the raw, per-transmission data messages a device has sent - each carrying deviceId, ts (epoch ms), batteryVoltage, rssi/signalStrength, and a values object - for a device by IMEI over a time range. Modeled from BodyTrace's documented device message payload; exact query surface is gated behind account credentials.

- **Human URL:** [https://www.bodytrace.com/medical/](https://www.bodytrace.com/medical/)
- **Base URL:** `https://us.data.bodytrace.com/1`

#### Tags

- Data Messages
- Raw Payloads
- Telemetry

#### Properties

- [Documentation](https://www.bodytrace.com/medical/)
- [OpenAPI](openapi/bodytrace-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)

### BodyTrace Devices API

List the cellular devices in an account and read a single device's status - last seen, battery, signal, and provisioning state - keyed by IMEI. Modeled from BodyTrace's device/IMEI-centric data model; the account-scoped device listing is behind partner credentials.

- **Human URL:** [https://www.bodytrace.com/medical/](https://www.bodytrace.com/medical/)
- **Base URL:** `https://us.data.bodytrace.com/1`

#### Tags

- Devices
- Status
- Fleet

#### Properties

- [Documentation](https://www.bodytrace.com/medical/)
- [OpenAPI](openapi/bodytrace-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)

### BodyTrace Alerts API

Read threshold and connectivity alerts raised for a device - for example a blood-pressure reading outside a configured range or a low-battery / offline condition. Modeled RPM capability; alerting configuration is arranged with BodyTrace and gated behind credentials.

- **Human URL:** [https://www.bodytrace.com/medical/](https://www.bodytrace.com/medical/)
- **Base URL:** `https://us.data.bodytrace.com/1`

#### Tags

- Alerts
- Thresholds
- Notifications

#### Properties

- [Documentation](https://www.bodytrace.com/medical/)
- [OpenAPI](openapi/bodytrace-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)

### BodyTrace Provisioning API

Associate a device (by IMEI) with an account, patient, or program and configure where its measurements are delivered (a pushed HTTP endpoint). Modeled from BodyTrace's documented onboarding flow; provisioning is completed with BodyTrace and gated behind credentials.

- **Human URL:** [https://www.bodytrace.com/medical/](https://www.bodytrace.com/medical/)
- **Base URL:** `https://us.data.bodytrace.com/1`

#### Tags

- Provisioning
- Enrollment
- Registration

#### Properties

- [Documentation](https://www.bodytrace.com/medical/)
- [OpenAPI](openapi/bodytrace-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)

### BodyTrace Measurement Webhook (Push) API

Instead of polling, BodyTrace can push each measurement to a customer HTTP endpoint. The device platform POSTs a JSON body (deviceId, ts, batteryVoltage, rssi, values) to a URL you host, secured with HTTP Basic credentials you define. Confirmed real-time delivery model - the endpoint is hosted by the consumer, not by BodyTrace.

- **Human URL:** [https://www.bodytrace.com/medical/](https://www.bodytrace.com/medical/)
- **Base URL:** `https://your-endpoint.example.com`

#### Tags

- Webhook
- Push
- Data Forwarding

#### Properties

- [Documentation](https://www.bodytrace.com/medical/)
- [OpenAPI](openapi/bodytrace-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)

## Common Properties

- [LinkedIn](https://www.linkedin.com/company/bodytrace)
- [Website](https://www.bodytrace.com)
- [Documentation](https://www.bodytrace.com/medical/)
- [Plans](plans/bodytrace-plans-pricing.yml)
- [Rate Limits](rate-limits/bodytrace-rate-limits.yml)
- [Fin Ops](finops/bodytrace-finops.yml)

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
