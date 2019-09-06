# Prometheus / Grafana helm chart with local storage.
This is a Helm chart for Prometheus and Grafana that uses local storage instead of volume from a cloud vendor. The helm chart creates a `StorageClass` that uses local storage and also creates the `PersistentVolumes` and `PersistentVolumeClaims` needed.

I created this because i use K3S for some of my Kubernetes setups and I run them on non cloud vendors, so this is perfect for that, On-prem or vendors that dont have cloud volumes.

## Instructions

1. Clone this repo.

2. SSH into the server you plan to deploy Prometheus & Grafana too.

3. Create the directories needed, paths for this can be changed to whatever you supply in `values.yaml`.

    ```bash
    $ mkdir -p /myvolumes/prometheus/alertmanager
    ```
    ```bash
    $ mkdir -p /myvolumes/prometheus/pushgateway
    ```
    ```bash
    $ mkdir -p /myvolumes/prometheus/server
    ```

4. Deploy the helm chart.

    ```bash
    $ helm install --name pixelpiloten_prometheus . -f values.yaml
    ```

5. Create a port-forward to the Grafana Service, port 8080 can be whatever port you want.

    ```bash
    $ kubectl -n monitoring port-forward svc/grafana 8080:80
    ```

6. Now you can access the Grafana web GUI in your browser.

    ```bash
    http://127.0.0.1:8080
    ```