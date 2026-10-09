# Windows ATT&CK Telemetry Dataset

A normalized Windows event dataset derived from four public Splunk Attack Data recordings. It supports detection and within-trace correlation for three MITRE ATT&CK sub-techniques:

- T1059.001: PowerShell
- T1003.001: LSASS Memory
- T1021.002: SMB/Windows Admin Shares

## Download

[Download attack_scenario.csv](./attack_scenario.csv?raw=true)

The CSV contains 1,275 event records from four independent public test recordings. These recordings come from different dates and hosts. They do not represent one continuous attack or a cross-technique campaign.

## Original sources

The original recordings are published in [Splunk's Attack Data repository](https://github.com/splunk/attack_data).

| Recording | Rows retained | Download |
|---|---:|---|
| PowerShell Sysmon events | 1,185 | [windows-sysmon.log](https://media.githubusercontent.com/media/splunk/attack_data/master/datasets/attack_techniques/T1059.001/encoded_powershell/windows-sysmon.log) |
| LSASS process-access events | 32 | [windows-sysmon_creddump.log](https://media.githubusercontent.com/media/splunk/attack_data/master/datasets/attack_techniques/T1003.001/atomic_red_team/windows-sysmon_creddump.log) |
| SMB share-access events | 55 | [windows-security-xml.log](https://media.githubusercontent.com/media/splunk/attack_data/master/datasets/attack_techniques/T1021.002/atomic_red_team/windows-security-xml.log) |
| SMB service-related Sysmon events | 3 | [smbexec_windows-sysmon.log](https://media.githubusercontent.com/media/splunk/attack_data/master/datasets/attack_techniques/T1021.002/atomic_red_team/smbexec_windows-sysmon.log) |

## Preparation

The preparation script parses the XML recordings and maps their event fields into a shared CSV schema.

The pipeline:

- Retains every input event, without row filtering or deduplication.
- Selects fields needed for detection, correlation and provenance.
- Normalizes timestamps to UTC with millisecond precision without aligning separate recordings onto a shared timeline.
- Removes control characters and surrounding whitespace from text fields.
- Consistently substitutes configured host, address and account identifiers independently of evaluation labels.
- Masks selected identifiers inside text fields.
- Preserves trace identifiers, process GUIDs and parent-process GUIDs so related records can be linked within each recording.

Masking covers configured identifiers and should not be treated as complete anonymization.

## Interpretation

The uneven recording sizes reflect these particular captures, not the real-world frequency of each technique.

Evaluation labels identify selected examples for this project. They are not independently established ground truth and must not be used as detection inputs. Matching an event rule does not by itself prove malicious intent.

## Integrity

SHA-256 of the prepared CSV:

721f40a12a486b08ca886471c6524cf535ca706d61d93d8ab26cf1e579d30646

## Attribution

Splunk's Attack Data project provides the original recordings. This repository provides a normalized derivative for the university project and does not claim authorship of the original logs. Consult the upstream repository for applicable licensing and attribution requirements.
