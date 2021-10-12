# Microsoft DHCP

This integration collects logs and metrics from Microsoft DHCP logs.

## Compatibility

This integration has been made to support the DHCP log format from Windows Server 2008 and later.

### Logs

Ingest logs from Microsoft DHCP Server, by default logged with the filename format:
`%windir%\System32\DHCP\DhcpSrvLog-*.log`

Relevant documentation for Microsoft DHCP can be found on [this]https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd183591(v=ws.10) location.

An example event for `log` looks as following:

```json
{
    "@timestamp": "2001-01-01T01:01:01.000-05:00",
    "agent": {
        "ephemeral_id": "7b80c5f6-3f5b-436f-aab7-ad35bc17cde9",
        "hostname": "docker-fleet-agent",
        "id": "303093f0-28ce-40db-ad0f-05f02e31b666",
        "name": "docker-fleet-agent",
        "type": "filebeat",
        "version": "7.15.0"
    },
    "data_stream": {
        "dataset": "microsoft_dhcp.log",
        "namespace": "ep",
        "type": "logs"
    },
    "ecs": {
        "version": "1.12.0"
    },
    "elastic_agent": {
        "id": "303093f0-28ce-40db-ad0f-05f02e31b666",
        "snapshot": true,
        "version": "7.15.0"
    },
    "event": {
        "agent_id_status": "verified",
        "category": [
            "network"
        ],
        "code": "35",
        "dataset": "microsoft_dhcp.log",
        "ingested": "2021-10-05T12:12:13Z",
        "kind": "event",
        "original": "35,01/01/01,01:01:01,DNS update request failed,192.0.2.1,host.test.com,000000000000,",
        "outcome": "success",
        "timezone": "America/New_York",
        "type": [
            "connection"
        ]
    },
    "host": {
        "domain": "host.test.com",
        "ip": "192.0.2.1",
        "mac": "00-00-00-00-00-00"
    },
    "input": {
        "type": "log"
    },
    "log": {
        "file": {
            "path": "/tmp/service_logs/test-dhcp.log"
        },
        "offset": 646
    },
    "message": "DNS update request failed",
    "tags": [
        "preserve_original_event",
        "forwarded",
        "microsoft_dhcp"
    ]
}
```

**Exported fields**

| Field | Description | Type |
|---|---|---|
| @timestamp | Event timestamp. | date |
| data_stream.dataset | Data stream dataset. | constant_keyword |
| data_stream.namespace | Data stream namespace. | constant_keyword |
| data_stream.type | Data stream type. | constant_keyword |
| ecs.version | ECS version this event conforms to. `ecs.version` is a required field and must exist in all events. When querying across multiple indices -- which may conform to slightly different ECS versions -- this field lets integrations adjust to the schema version of the events. | keyword |
| event.action | The action captured by the event. This describes the information in the event. It is more specific than `event.category`. Examples are `group-add`, `process-started`, `file-created`. The value is normally defined by the implementer. | keyword |
| event.code | Identification code for this event, if one exists. Some event sources use event codes to identify messages unambiguously, regardless of message language or wording adjustments over time. An example of this is the Windows Event ID. | keyword |
| event.dataset | Event dataset | constant_keyword |
| event.ingested | Timestamp when an event arrived in the central data store. This is different from `@timestamp`, which is when the event originally occurred.  It's also different from `event.created`, which is meant to capture the first time an agent saw the event. In normal conditions, assuming no tampering, the timestamps should chronologically look like this: `@timestamp` \< `event.created` \< `event.ingested`. | date |
| event.kind | This is one of four ECS Categorization Fields, and indicates the highest level in the ECS category hierarchy. `event.kind` gives high-level information about what type of information the event contains, without being specific to the contents of the event. For example, values of this field distinguish alert events from metric events. The value of this field can be used to inform how these kinds of events should be handled. They may warrant different retention, different access control, it may also help understand whether the data coming in at a regular interval or not. | keyword |
| event.module | Event module | constant_keyword |
| event.original | Raw text message of entire event. Used to demonstrate log integrity or where the full log message (before splitting it up in multiple parts) may be required, e.g. for reindex. This field is not indexed and doc_values are disabled. It cannot be searched, but it can be retrieved from `_source`. If users wish to override this and index this field, please see `Field data types` in the `Elasticsearch Reference`. | keyword |
| event.timezone | This field should be populated when the event's timestamp does not include timezone information already (e.g. default Syslog timestamps). It's optional otherwise. Acceptable timezone formats are: a canonical ID (e.g. "Europe/Amsterdam"), abbreviated (e.g. "EST") or an HH:mm differential (e.g. "-05:00"). | keyword |
| host.domain | Name of the domain of which the host is a member. For example, on Windows this could be the host's Active Directory domain or NetBIOS domain name. For Linux this could be the domain of the host's LDAP provider. | keyword |
| host.ip | Host ip addresses. | ip |
| host.mac | Host MAC addresses. The notation format from RFC 7042 is suggested: Each octet (that is, 8-bit byte) is represented by two [uppercase] hexadecimal digits giving the value of the octet as an unsigned integer. Successive octets are separated by a hyphen. | keyword |
| input.type |  | keyword |
| log.file.path | Full path to the log file this event came from, including the file name. It should include the drive letter, when appropriate. If the event wasn't read from a log file, do not populate this field. | keyword |
| log.offset |  | long |
| message | For log events the message field contains the log message, optimized for viewing in a log viewer. For structured logs without an original message field, other fields can be concatenated to form a human-readable summary of the event. If multiple messages exist, they can be combined into one message. | match_only_text |
| microsoft.dhcp.correlation_id | The NAP correlation ID related to the client/server transaction. | keyword |
| microsoft.dhcp.dhc_id | The related DHCID (DHC DNS record). | keyword |
| microsoft.dhcp.dns_error_code | DNS error code communicated to client. | keyword |
| microsoft.dhcp.probation_time | The probation time before lease ends on specific IP. | keyword |
| microsoft.dhcp.relay_agent_info | Information about DHCP relay agent used for the DHCP request. | keyword |
| microsoft.dhcp.result | The DHCP result type, for example "NoQuarantine", "Drop Packet" etc. | keyword |
| microsoft.dhcp.transaction_id | The DHCP transaction ID. | keyword |
| microsoft.dhcp.user.hex | Hex representation of the user. | keyword |
| microsoft.dhcp.user.string | String representation of the user. | keyword |
| microsoft.dhcp.vendor.hex | Hex representation of the vendor. | keyword |
| microsoft.dhcp.vendor.string | String representation of the vendor. | keyword |
| tags | List of keywords used to tag each event. | keyword |
| user.name | Short name or login of the user. | keyword |