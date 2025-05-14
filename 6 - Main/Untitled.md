Performance

1.       P95 query latency should be kept under 2 s (with P99 under 3 s) for both batch and speed-layer queries.

2.       All full pages, including their visual components, should load within 10 s and should ensure no single component takes over 3 s.

3.       System should support batch workloads of up to 50 GB/day and sustained streaming at around 10 MB/s without backlog.

4.       Must scale horizontally to support at least 100 concurrent active users with accepting some degradation as the load increases.

Reliability

1.       Maintain uptime of at least 95 % per calendar month, recognizing that brief downtimes may occur during development or maintenance.

2.       Must recover from a full cluster failure within one hour, with automated failover.

3.       Must never corrupt or overwrite upstream data sources.

4.       Must provide real-time health dashboards (CPU/RAM/disk I/O, pipeline lag, node status) and alert on threshold breaches.

5.       Should support rolling deployments with zero downtime.

Security

1.       Encrypt all credentials at rest using industry-standard practices and secure network traffic using TLS.

2.       Implement least-privilege policies for user roles so that each role’s permissions are strictly limited to its necessary tasks.

3.       By default, must cancel any query running longer than 25 s by default (Developers may extend to 120 s to troubleshoot long-running analytics).

4.       Maintain audit logs for important events (e.g., authentications, authorizations, data-access, and configuration changes) persistently for at least 6 months (or at least a scalable way that would last 6 months).

Accessibility

1.       Must comply with WCAG 2.1 AA: high-contrast themes, resizable text, keyboard-only navigation.

2.       Must render and function correctly on modern desktop browsers (Chrome, Firefox, Edge, Safari) and mobile browsers on iOS/Android.

3.       Must adapt layouts for tablet and large-screen (TV/monitor kiosk) modes.