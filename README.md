# OSISM newstime

New features are listed in the news time even before a release with short examples and background
information. In the process of a release, the details from the newstime are transferred to the
release notes.

* [2023-05-31] A validator for the RGW service is now also available for Ceph.

  ```
  $ osism validate ceph-rgws
  ```

* [2023-05-21] [Kubernetes Cluster API image](https://github.com/osism/k8s-capi-images) v1.27.2
  is available.

* [2023-05-21] The deployment of OpenSearch is currently broken on the rolling tags. A solution is
  being worked on.

* [2023-05-19] Docker Hub can now be used when using Squid as internal proxy.

* [2023-05-19] [Clustershell](https://clustershell.readthedocs.io/en/latest/intro.html) can now
  be used with the OSISM CLI. Only groups are currently supported. Clustershell's groups correspond
  to [Ansible's groups](https://github.com/osism/cfg-generics/tree/main/inventory). The groups are
  updated with the inventory reconciler service when something changes in the inventory.

  ```
  $ osism console --type clush generic
  Enter 'quit' to leave this interactive mode
  Working with nodes: testbed-manager.testbed.osism.xyz,testbed-node-[0-2].testbed.osism.xyz
  clush> uptime
  testbed-manager.testbed.osism.xyz:  18:57:52 up 11:27,  2 users,  load average: 3.90, 1.87, 1.08
  testbed-node-0.testbed.osism.xyz:  18:57:52 up 10:55,  0 users,  load average: 0.56, 0.52, 0.53
  testbed-node-1.testbed.osism.xyz:  18:57:52 up 10:55,  0 users,  load average: 0.38, 0.55, 0.60
  testbed-node-2.testbed.osism.xyz:  18:57:52 up 10:55,  0 users,  load average: 0.50, 0.52, 0.53
  ```

* [2023-05-19] [Kubernetes Cluster API images](https://github.com/osism/k8s-capi-images) from the
  1.27 series are available. Series 1.24 (v1.24.14), 1.25 (v1.25.10) and 1.26 (v1.26.5) have been
  updated.

* [2023-05-17] [scaphandre](https://github.com/hubblo-org/scaphandre), an energy consumption
  metrology agent dedicated to electrical power consumption metrics, can be deployed with
  ``osism.services.scaphandre``. Deployed on all hosts in group ``scaphandre``.

  ``environments/kolla/files/overlays/prometheus/prometheus.yml.d/99-scaphandre.yml``:

  ```
  - job_name: scaphandre
    static_configs:
      - targets:
        - a.b.c.d:9155
    scrape_interval: 5m
  ```
