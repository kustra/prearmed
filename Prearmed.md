# Prearmed

Prearmed is a heartbeat service around the concept of _reliability in simplicity_. The core idea is that each heartbeat _postpones the alert_ that is scheduled in advance.

It lives entirely in the user's own AWS account. It is serverless, with no idle costs. The alert is a one-time EventBridge Scheduler schedule whose target sends it directly, so none of Prearmed's code runs or polls at alert time. A heartbeat that arrives after the alert has fired re-arms it. Prearmed installs from a CloudFormation template, or by pointing an AI coding agent at the repository.

Jobs send heartbeats over HTTPS. A heartbeat can also carry the job's exit status and output, and one that reports an error alerts at once.

It is free and open source, under Apache-2.0.
