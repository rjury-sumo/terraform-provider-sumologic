---
layout: "sumologic"
page_title: "SumoLogic: sumologic_local_windows_event_log_source"
description: |-
  Provides a Sumologic Local Windows Event Log Source.
---

# sumologic_local_windows_event_source
Provides a [Sumologic Local Windows Event Log Source][1].

## Example Usage
```hcl
resource "sumologic_installed_collector" "installed_collector" {
  name       = "test-collector"
  category   = "macos/test"
  ephemeral  = true
}

resource "sumologic_local_windows_event_log_source" "local" {
  name             = "windows_system"
  description      = "windows system log"
  category         = "/os/windows/system"
  collector_id     = "${sumologic_installed_collector.installed_collector.id}"
  log_names  = ["System"]
}

  ```

## Argument Reference

The following arguments are supported:

  * `name` - (Required) The name of the local file source. This is required, and has to be unique. Changing this will force recreation the source.
  * `description` - (Optional) The description of the source.
  * `log_names` - List of Windows log types to collect (e.g., Security, Application, System)
  * `render_messages` - When using legacy format, indicates if full event messages are collected
  * `event_format` - 0 for legacy format (XML), 1 for JSON format. Default 0.
  * `event_message` - 0 for complete message, 1 for message title, 2 for metadata only. Required if event_format is 0
  * `deny_list` - Comma-separated list of event IDs to deny
  * `category` - (Optional) The default source category for the source.
  * `fields` - (Optional) Map containing [key/value pairs][2].
  * `denylist` - (Optional) Comma-separated list of valid path expressions from which logs will not be collected.

### See also
  * [Common Source Properties](https://github.com/terraform-providers/terraform-provider-sumologic/tree/master/website#common-source-properties)

## Attributes Reference
The following attributes are exported:

  * `id` - The internal ID of the local file source.

## Import
Local file sources can be imported using the collector and source IDs, e.g.:

```hcl
terraform import sumologic_local_windows_event_source.test 123/456
```

Local file sources can also be imported using the collector name and source name, e.g.:

```hcl
terraform import sumologic_local_windows_event_source.test my-test-collector/my-test-source
```

[1]: https://help.sumologic.com/docs/send-data/installed-collectors/sources/local-windows-event-log-source/
[2]: https://help.sumologic.com/Manage/Fields
[3]: https://help.sumologic.com/docs/send-data/use-json-configure-sources/json-parameters-installed-sources/#local-windows-event-logsource