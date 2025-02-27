---
description: The OriginTrail v6 network monitoring system
---

# 👾 Telemetry Hub

The OriginTrail v6 telemetry hub is a system designed to monitor the Decentralized Knowledge Graph network performance and provide feedback on the network activity.&#x20;

### What kind of data does the Telemetry hub collect?

The Telemetry hub aggregates node telemetry measurements - values such as the timestamps and durations of graph queries, inserts, network operations etc as well as errors observed during execution. These measurements are collected by each individual node on the v6 network and submitted to Telemetry hub in the following way:

* by generating measurement data assertions once per hour and publishing them to the DKG&#x20;
* by submitting a log of published assertion IDs to a centralized signalling server, used for double-checking the data pipeline incurs no data loss (potentially due to Telemetry Hub ingestion service or network communication issues)

![Nodes submit telemetry data to the DKG, later ingested by the Telemetry hub. Nodes also submit basic assertion information to a signalling server, used to double-check that all data has been successfully received by the Telemetry Hub](<../.gitbook/assets/ODN v6 diagrams - Page 41 (1).png>)

The telemetry hub then aggregates all information by operation and displays this information via several graphic dashboards. This information is useful for DKG developers when introducing new releases to the network and verifying the correct and efficient operation of the v6 implementation.



![Telemetry dashboard example](../.gitbook/assets/aa.png)

{% hint style="info" %}
Note: no personal data, keys or sensitive information is collected via the Telemetry system.
{% endhint %}

### The dual purpose of the Telemetry hub during OriginTrail v6 Beta&#x20;

The telemetry hub is in essence a Semantic Web3 application collecting and analysing telemetry data on the usage of the DKG, by using the DKG itself for monitoring its **performance**. During the beta however there is one more purpose - testing the DKG **functionalities** in the real-world environment, in order to be able reach of TRL8 and TRL9 (see "[NASA technology readiness levels](https://www.nasa.gov/directorates/heo/scan/engineering/technology/technology\_readiness\_level)").

Therefore it is expected that during beta stages the Telemetry will collect errors, reveal previously undetected issues and problems - all of these are valuable to the OriginTrail Developer community and by running a v6 node you can contribute to the mission [and earn bounty rewards](v6-bounty-program.md)!

### Important notes

{% hint style="warning" %}
You are free to run multiple nodes, and will be rewarded for each of the nodes contributing, however make sure each node uses a different wallet (this is a prerequisite).
{% endhint %}

{% hint style="warning" %}
For each node that you are running, please go to [bounty program website](https://bountyprogram.origintrail.io/) and register wallet of that node (you can preform this step anytime before or after starting your node)
{% endhint %}

### How can you verify your node is submitting data to telemetry?

If you are running an OriginTrail v6 testnet node and want to contribute to the Telemetry system and earn bounty, please make sure to verify the following:

* Check that your node is up to date with the latest v6 node version (check for the latest release [on Github](https://github.com/OriginTrail/ot-node/releases)). We suggest that you turn on autoupdating during the beta stage to make sure your node is updated constantly
* Make sure to check that your nodes are operating properly by checking the node logs
* Make sure that the node operational wallet has enough tokens&#x20;
  * Polygon Mumbai MATIC tokens (from launch stage 1 onwards)
  * Test TRAC tokens (from launch stage 2 onwards) - not applicable yet
* Make sure your node is communicating properly [with the Polygon Mumbai RPC](https://docs.polygon.technology/docs/develop/network-details/network/) endpoints
* Check if your node telemetry plugin has been enabled by using the node API info route (see screenshot below from browser)
  * If you have setup SSL on your node, use https to check
  * If you get _"Access denied"_ message, you need to whitelist yourself by adding your IP address in ipWhitelist array in .origintrail\_noderc file, and then restart your node
  * After starting/restarting, following message in the logs means that telemetry plugin is enabled _"Telemetry hub module initialized successfully, using ot-telemetry-collector package(s)"_

![Example of the response from a node /info API call showing the latest version and if telemetry data is being sent ](<../.gitbook/assets/Screen Shot 2022-03-11 at 10.18.34.png>)

Additionally, check the Debug section in Protocol operations KPIs [Dashboard](https://telemetry.origintrail.io/d/Cs4uPdLnk/telemetry-protocol-operation-kpis) to find your node:

* Find your node wallet address in the table
* Check that the "records\_seen\_by\_signaling\_server" is greater than 0 (the number should be close to 24 as the node should submit one telemetry report assertion every hour)
* Check that the "records\_fetched\_from\_the\_network" is greater than 0. We expect this number to be equal or close to the "records\_seen\_by\_signaling\_server" - a lower number would mean that the assertion data submitted by your node has not been processed by the telemetry hub yet&#x20;
* Check the latest timestamps of submission, particularly the "signaling\_timestamp\_of\_last\_record\_seen" - if this number is not close to the current time (in GMT), that means your node might not be operating properly

{% hint style="info" %}
The Telemetry data received might be lagging behind (not realtime) which is expected. The Telemetry hub data processing pipeline is constantly being tuned in such a way that the network telemetry data can be visualized as close as possible to real-time.
{% endhint %}

{% hint style="info" %}
The bounty scoreboard table is updated daily with points for the previous day.
{% endhint %}

### What should you do if you observe issues?

After checking the above list and not being able to resolve any issues, please contact the developers directly [on Discord](https://discordapp.com/invite/FCgYk2S).

