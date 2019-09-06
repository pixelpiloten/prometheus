# Prometheus helm chart with local storage.
This is a Helm chart for Prometheus that uses local storage instead of volume from a cloud vendor. The helm chart creates a `StorageClass` that uses local storage and also creates the `PersistentVolumes` and `PersistentVolumeClaims` needed.

I created this because i use K3S for some of my Kubernetes setups and I run them on non cloud vendors, so this is perfect for that, On-prem or vendors that dont have cloud volumes.

## Instructions

1. Clone this repo.

2. SSH into the server you plan to deploy Prometheus too.

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