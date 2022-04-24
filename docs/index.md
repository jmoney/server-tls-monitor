# Server TLS Monitor

This script pings a server and asks for the certificate.  It then reports some expiration data in json form.  Useful
for monitoring certificate expiration and when a certificate needs to be rotated.

## Inputs

| Name     | Value                                                                                                   |
|----------|---------------------------------------------------------------------------------------------------------|
| Host     | The Host of the server that is to be inspected.                                                         |
| Port     | The Port of the server that is to be inspected. Default is `443`.                                       |
| Protocol | The protocol to use to connect to the server.  Valid options are `tcp` or `postgres`. Default is `tcp`. |

## Output

```json
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "$id": "https://jmoney.dev/server-certificate-monitor/tlsmetrics.schema.json",
  "title": "TlsMetrics",
  "description": "Tls expiration metrics of a certificate hosted on a server.",
  "type": "object",
  "properties": {
    "tls": {
      "description": "Root object. Metric data is hosted under.",
      "type": "object",
      "properties": {
        "days_left": {
          "description": "The number of days left until this certificate expires.",
          "type": "number"
        },
        "issued_days": {
          "description": "The number of days this certificate has been issued for.",
          "type": "number"
        },
        "issued_seconds": {
          "description": "The number of seconds this certificate has been issued for.",
          "type": "number"
        },
        "seconds_left": {
          "description": "The number of seconds left until this certificate expires.",
          "type": "number"
        }
      },
      "required": [ "days_left", "issued_days", "issued_days", "seconds_left" ]
    }
  },
  "required": [ "tls" ]
}
```

## Help

```bash
server-tls-monitor -host example.com
```