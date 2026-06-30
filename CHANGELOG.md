# Changelog

All notable changes to the DugganUSA Elastic Integration are documented here.

## [1.3.0] - 2026-06-30

### Added
- **Feed-efficacy hit reporting (liveness loop)** — new `logstash-dugganusa-report.conf` pipeline. When one of our published indicators matches your traffic, it POSTs the hit to `POST /api/v1/feed/hit` via the logstash `http` output (`consumer_kind: 'elastic'`), closing the Liveness validation axis (`/api/v1/feed-efficacy`). Includes a `translate`-filter example that flags matches off the IP blocklist you already sync.
- **Privacy contract:** the explicit `mapping` in the `http` output is the privacy boundary — only the matched indicator + action/direction/count/ts leave your network, never your source IP, host, user, asset, or the raw event. (The platform also drops any victim-side field server-side.)

## [1.2.1] - 2026-06-30

### Added
- Documented the fourth live validation axis — Liveness (`/api/v1/feed-efficacy`) — alongside novelty, timeliness, and accuracy. Consumers can opt in to report hits via `POST /api/v1/feed/hit` (privacy-preserving — only the matched indicator is sent, never victim data).

### Changed
- Refreshed IOC corpus copy to 1.5M+ IOCs (~1.57M live).
- Reworded the Timeliness validation bullet to point at the live kev-lead ledger instead of a fixed "~31 days ahead" average (the live ledger is the source of truth).

## [1.2.0] - 2026-06-27

### Added
- Documented the three live, no-auth, durable feed-validation endpoints — novelty (`/api/v1/feed-uniqueness`), timeliness (`/api/v1/kev-lead`), and accuracy (`/api/v1/spamhaus-validation`) — for independent detection-engineering verification. Each response carries a `source` field (`live` | `durable` | `baseline`).
- Noted new feed depth: OSV malicious-package feeds (npm + PyPI) and daily GitHub Hunt detections.

### Changed
- **STIX feed is now API-key-enforced.** Removed all "optional API key" / "works without one" copy from the README, `filebeat-dugganusa.yml`, and `logstash-dugganusa.conf`. The `Authorization: Bearer` header is now uncommented and required across the STIX and CSV inputs; anonymous requests return `401` and unregistered keys return `429`.
- Corrected IOC corpus figure to 1.10M+.

## [1.1.0]

- Filebeat (httpjson) and Logstash (http_poller) configs, ECS threat-field mapping, ILM rollover, Kibana dashboard.
