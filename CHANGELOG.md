# Changelog

All notable changes to the DugganUSA Elastic Integration are documented here.

## [1.2.0] - 2026-06-27

### Added
- Documented the three live, no-auth, durable feed-validation endpoints — novelty (`/api/v1/feed-uniqueness`), timeliness (`/api/v1/kev-lead`), and accuracy (`/api/v1/spamhaus-validation`) — for independent detection-engineering verification. Each response carries a `source` field (`live` | `durable` | `baseline`).
- Noted new feed depth: OSV malicious-package feeds (npm + PyPI) and daily GitHub Hunt detections.

### Changed
- **STIX feed is now API-key-enforced.** Removed all "optional API key" / "works without one" copy from the README, `filebeat-dugganusa.yml`, and `logstash-dugganusa.conf`. The `Authorization: Bearer` header is now uncommented and required across the STIX and CSV inputs; anonymous requests return `401` and unregistered keys return `429`.
- Corrected IOC corpus figure to 1.10M+.

## [1.1.0]

- Filebeat (httpjson) and Logstash (http_poller) configs, ECS threat-field mapping, ILM rollover, Kibana dashboard.
