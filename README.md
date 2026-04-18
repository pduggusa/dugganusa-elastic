# DugganUSA Elastic Integration

**Ingest 1M+ threat indicators into Elasticsearch / OpenSearch. Filebeat or Logstash.**

## Quick Start (Filebeat)

```bash
# Download config
curl -O https://raw.githubusercontent.com/pduggusa/dugganusa-elastic/main/filebeat-dugganusa.yml

# Edit: set your Elasticsearch host and optional API key
vim filebeat-dugganusa.yml

# Run
filebeat -e -c filebeat-dugganusa.yml
```

## Quick Start (Logstash)

```bash
curl -O https://raw.githubusercontent.com/pduggusa/dugganusa-elastic/main/logstash-dugganusa.conf
logstash -f logstash-dugganusa.conf
```

## What It Ingests

- **STIX 2.1 JSON feed** — full indicator objects with type, pattern, confidence, timestamps
- **IP blocklist CSV** — for IP-based correlation
- **Domain blocklist CSV** — for DNS-based correlation

All three polled hourly by default.

## Index Pattern

```
dugganusa-threat-intel-*
```

ILM policy included for automatic rollover.

## Kibana Dashboard

Import the included dashboard:

```bash
curl -X POST "localhost:5601/api/saved_objects/_import" \
  -H "kbn-xsrf: true" \
  --form file=@kibana-dashboard.ndjson
```

## ECS Mapping

Indicators are mapped to ECS Threat fields:
- `threat.feed.name` → "DugganUSA"
- `threat.indicator.provider` → "DugganUSA LLC"
- `threat.indicator.type` → "ipv4-addr" / "domain-name" / etc.

## Free API Key

[analytics.dugganusa.com/stix/register](https://analytics.dugganusa.com/stix/register)

## Part of the DugganUSA Ecosystem

- [VS Code Extension](https://marketplace.visualstudio.com/items?itemName=DugganUSALLC.dugganusa-threat-intel)
- [Splunk TA](https://github.com/pduggusa/dugganusa-splunk)
- [Sentinel Connector](https://github.com/pduggusa/dugganusa-sentinel)
- [CLI Tool](https://github.com/pduggusa/dugganusa-cli)
- [GitHub Action](https://github.com/pduggusa/dugganusa-action)
- [Chrome Extension](https://github.com/pduggusa/dugganusa-chrome)
- [Slack Bot](https://github.com/pduggusa/dugganusa-slack)
- [dugganusa.com](https://www.dugganusa.com)

## License

MIT — [DugganUSA LLC](https://www.dugganusa.com)
