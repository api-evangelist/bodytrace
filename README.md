# BodyTrace (bodytrace)

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

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
