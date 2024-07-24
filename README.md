### AuthZed Dedicated - Prometheus & Grafana

## Configuring Prometheus to Scrape Metrics from AuthZed Dedicated 

To enable Prometheus to scrape metrics from your permission system, configure the `scrape_config` section in prometheus.yml. 

1. Open `prometheus.yml` in an editor.

2. Add the following `scrape_config` section to your configuration file, replacing the placeholder values with your specific details:

    ```yaml
    scrape_configs:
      - job_name: "exported-metrics-from-[permission-system]"
        metrics_path: /api/v1alpha/metrics
        basic_auth:
          username: "[permission-system]"
          password: "[token]"
        static_configs:
          - targets:
              - "[authzed-dashboard-url]"
    ```

### Required Values


Find this info at `your-authzed-domain.authzed.net/system/[permission-system]/metrics/prometheus` by replacing `[permission-system]` with the name of your permission system or by navigating to the AuthZed Dashbord -> Permission System -> Metrics -> Scrape with Prometheus 


- **job_name**: Replace `[permission-system]` with the name of your permission system. This identifies the job in Prometheus.
  - Example: `job_name: "exported-metrics-from-my-permission-system"`

- **metrics_path**: Set to `/api/v1alpha/metrics`.

- **basic_auth**:
  - **username**: Replace `[permission-system]` with the permission system namep.
    - Example: `username: "my-permission-system"`
  - **password**: Replace `[token]` with the token copied from the AuthZed Dashboard.
    - Example: `password: "doGXlyJdtjZHOdCw486t"`

- **static_configs**:
  - **targets**: Replace `[authzed-dashboard-url]` with the URL of your Authzed Dashboard.

    - Example: `targets: ["https://app.demo.aws.authzed.net"]`

### Example Configuration

Here's an example of a filled-out configuration:

    ```
    scrape_configs:
      - job_name: "exported-metrics-from-my-permission-system"
        metrics_path: /api/v1alpha/metrics
        basic_auth:
          username: "my-permission-system"
          password: "my-secret-token"
        static_configs:
          - targets:
              - "https://app.demo.aws.authzed.net"
    ```


3. Save prometheus.yml 

4. Run `docker compose up`

---

### Results: 


Prometheus running on `localhost:9090`
Grafana running on `localhost:3000`

Check `localhost:9090/targets` for status of AuthZed Dedicated target (reachable via the "Status" –> "Targets" menu option in Prometheus UI as well.) 







