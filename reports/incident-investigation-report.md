# Windows Security Log Analysis and Incident Investigation

## 1. Objective

Analyse a synthetic Windows Security event dataset to identify potentially
suspicious authentication activity, construct an event timeline, and document
the investigation findings.

## 2. Scope

This exercise uses fictional training data created for a beginner cybersecurity
home lab. It does not represent an investigation of a real user or attacker.

The analysis focuses on Events 4624, 4625, 4634, and 4672.

## 3. Methodology

1. Reviewed the event records and timestamps.
2. Grouped failed logons by account and source IP address.
3. Compared failed attempts with the subsequent successful logon.
4. Examined session identifiers and related event records.
5. Recorded an initial assessment, limitations, and recommended follow-up actions.

## 4. Key Finding: Repeated Failed Logons Followed by Success

Four Event ID 4625 records for account `j.smith` occurred between
10:14:02 and 10:14:22 on 10 October 2026. All four records used
Logon Type 3 and the documentation-only source IP `192.0.2.50`.

An Event ID 4624 record then showed a successful network logon for the same
account and source IP at 10:15:03. The successful logon occurred 41 seconds
after the final recorded failure.

An Event ID 4634 record at 10:20:00 referenced the same sample Logon ID
as the successful logon.

## 5. Initial Assessment

**Classification: Potentially suspicious; further investigation required.**

Repeated authentication failures followed by a successful logon may be
consistent with password guessing or a brute-force attempt. However, the
available records do not establish that an attacker obtained access. A
legitimate user could also have entered an incorrect password multiple times.

The sequence is a lead for further investigation, not proof of compromise.

## 6. Additional Context

The dataset also contains an Event ID 4624 service logon under the SYSTEM
account, followed by Event ID 4672 with the same sample Logon ID.
This is consistent with privileged Windows activity and is not, by itself,
evidence of malicious behaviour.

## 7. Recommended Follow-up

- Review the logon failure status and substatus in the original event details.
- Check whether the account owner and source device are expected.
- Review surrounding authentication events and other available security logs.
- Check for account lockouts, unexpected access, and subsequent activity.
- Apply the organisation's incident response process if corroborating evidence
  indicates unauthorised access.

## 8. Limitations

- All events in the CSV dataset are fictional and intended for training.
- The source IP `192.0.2.50` is reserved for documentation and examples.
- The dataset is small and does not contain all fields available in native
  Windows Security events.
- No conclusion about a real account, attacker, or security incident can be
  drawn from this exercise.

## 9. Conclusion

The synthetic timeline demonstrates how repeated failed logons followed by
a successful logon can be prioritised for investigation. The correct initial
response is to gather additional evidence before determining whether the
activity is malicious or legitimate.
