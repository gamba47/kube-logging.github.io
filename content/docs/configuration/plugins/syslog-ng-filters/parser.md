---
title: Parser
weight: 200
generated_file: true
---

Parser filters can be used to extract key-value pairs from message data. Logging operator currently supports the following parsers:

- [regexp](#regexp)
- [syslog-parser](#syslog)

## Regexp parser {#regexp}

The regexp parser can use regular expressions to parse fields from a message.

{{< highlight yaml >}}
  filters:
  - parser:
      regexp:
        patterns:
        - ".*test_field -> (?<test_field>.*)$"
        prefix: .regexp.
{{</ highlight >}}

For details, see the [documentation of the AxoSyslog syslog-ng distribution](https://axoflow.com/docs/axosyslog-core/chapter-parsers/parser-regexp/).

## Syslog parser {#syslog}

The syslog parser can parse syslog messages. For details, see the [documentation of the AxoSyslog syslog-ng distribution](https://axoflow.com/docs/axosyslog-core/chapter-parsers/parser-syslog/).

{{< highlight yaml >}}
  filters:
  - parser:
      syslog-parser: {}
{{</ highlight >}}

## Configuration
## [Parser](https://axoflow.com/docs/axosyslog-core/chapter-parsers/)

### regexp (*RegexpParser, optional) {#parser-regexp}

Default: -

### syslog-parser (*SyslogParser, optional) {#parser-syslog-parser}

Default: -

### metrics-probe (*MetricsProbe, optional) {#parser-metrics-probe}

Counts the messages that pass through the flow, and creates labeled stats counters based on the fields of the passing messages. For details, see the [documentation of the AxoSyslog syslog-ng distribution](https://axoflow.com/docs/axosyslog-core/chapter-parsers/metrics-probe/).

## [Regexp parser](https://axoflow.com/docs/axosyslog-core/chapter-parsers/parser-regexp/)

### patterns ([]string, required) {#regexp-parser-patterns}

The regular expression patterns that you want to find a match. regexp-parser() supports multiple patterns, and stops the processing at the first successful match. For details, see the [regexp-parser() documentation of the AxoSyslog syslog-ng distribution](https://axoflow.com/docs/axosyslog-core/chapter-parsers/parser-regexp/parser-regexp-options/#patterns).

Default: -

### prefix (string, optional) {#regexp-parser-prefix}

Insert a prefix before the name part of the parsed name-value pairs to help further processing. For details, see the [regexp-parser() documentation of the AxoSyslog syslog-ng distribution](https://axoflow.com/docs/axosyslog-core/chapter-parsers/parser-regexp/parser-regexp-options/#prefix).

Default: -

### template (string, optional) {#regexp-parser-template}

Specify a template of the record fields to match against. For details, see the [regexp-parser() documentation of the AxoSyslog syslog-ng distribution](https://axoflow.com/docs/axosyslog-core/chapter-parsers/parser-regexp/parser-regexp-options/#template).

Default: -

### flags ([]string, optional) {#regexp-parser-flags}

Flags to influence the behavior of the [regexp-parser()](https://axoflow.com/docs/axosyslog-core/chapter-parsers/parser-regexp/parser-regexp-options/). For details, see the [regexp-parser() documentation of the AxoSyslog syslog-ng distribution](https://axoflow.com/docs/axosyslog-core/chapter-parsers/parser-regexp/parser-regexp-options/#flags).

Default: -

## SyslogParser

### flags ([]string, optional) {#syslogparser-flags}

Flags to influence the behavior of the [syslog-parser()](https://axoflow.com/docs/axosyslog-core/chapter-parsers/parser-syslog/parser-syslog-options/). For details, see the [syslog-parser() documentation of the AxoSyslog syslog-ng distribution](https://axoflow.com/docs/axosyslog-core/chapter-parsers/parser-syslog/parser-syslog-options/#flags).

Default: -

## MetricsProbe

Counts the messages that pass through the flow, and creates labeled stats counters based on the fields of the passing messages. For details, see the [documentation of the AxoSyslog syslog-ng distribution](https://axoflow.com/docs/axosyslog-core/chapter-parsers/metrics-probe/).

{{< highlight yaml>}}SyslogNGFlow
apiVersion: logging.banzaicloud.io/v1beta1
kind: SyslogNGFlow
metadata:
  name: flow-mertrics-probe
  namespace: default
spec:
  filters:
    - parser:
        metrics-probe:
          key: "flow_events"
          labels:
            namespace: "${json.kubernetes.namespace_name}"{{< /highlight >}}

### key (string, optional) {#metricsprobe-key}

The name of the counter to create. Note that the value of this option is always prefixed with `syslogng_`, so for example `key("my-custom-key")` becomes `syslogng_my-custom-key`.

Default: -

### labels (ArrowMap, optional) {#metricsprobe-labels}

The labels used to create separate counters, based on the fields of the messages processed by `metrics-probe()`. The keys of the map are the name of the label, and the values are syslog-ng templates. 

Default: -

### level (int, optional) {#metricsprobe-level}

Sets the stats level of the generated metrics (default 0). 

Default: 0
