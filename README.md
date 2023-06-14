# OSISM newstime

New features are listed in the news time even before a release with short examples and background
information. In the process of a release, the details from the newstime are transferred to the
release notes.

* [2023-06-14] In the [cookiecutter](https://github.com/osism/cfg-cookiecutter), new ``nova-compute``
  services were disabled by default and must now be enabled manually after deployment and verification.

* [2023-06-14] The [manager playbooks](https://github.com/osism/ansible-playbooks-manager) are
  now also published on Ansible Galaxy as [osism.manager](https://galaxy.ansible.com/osism/manager).

* [2023-06-14] Preparations for the 5.2.0 release are underway and the first tests of 5.2.0 will
  be completed later this week. It is expected that the release will be released from the end of
  the week.

* [2023-06-14] [Aptly](https://github.com/osism/helm-charts/tree/gh-pages/aptly) mirror setup
  (for deb packages) is now available to be deployed alongside OSISM installations. This requires
  additional infrastructure. Have a look at the [documentation](https://github.com/osism/docs/tree/main/docs/operations/external_services/aptly_external.md)
  for more details.

* [2023-06-12] Bring back colored Ansible output.

* [2023-06-12] From now on, the ``osism-update-manager`` script ignores existing Ansible
  installations on the system and only uses Ansible versions supported by ``osism-update-manager``
  in a virtual Python environment. This avoids recurring conflicts when updating the manager in
  the future. An operator is now free to use any Ansible version for other things on the manager
  without causing problems when updating the manager services.

* [2023-06-12] All Ansible collections and playbooks from OSISM itself has been upgraded to
  Ansible v8.

* [2023-06-12] [Debian 12 (Bookworm) has been released](https://www.debian.org/News/2023/20230610)
  and is now enabled by default in the OpenStack Image Manager.

* [2023-06-12] With the command ``get versions manager`` it is possible to get the
  OSISM version as well as a specific release of a module.

  ```
  $ osism get versions manager
  +---------------+-----------------+------------------+
  | Module        | OSISM version   | Module release   |
  |---------------+-----------------+------------------|
  | osism-ansible | latest          |                  |
  | ceph-ansible  | latest          | pacific          |
  | kolla-ansible | latest          | zed              |
  +---------------+-----------------+------------------+
  ```

* [2023-06-02]  [Garden Linux image](https://github.com/osism/openstack-image-gardenlinux)
  v934.9 is available.

* [2023-06-01] With ``vault`` a new command is available in the OSISM client which will be used to
  control the vault service in the future. Currently, it can be used to set the password for
  Ansible Vault. This way the current approach via ``/opt/configuration/environments/.vault_pass``
  does not have to be used anymore in the future.

  ```
  $ osism vault password set
  Ansible Vault password: ********
  $ osism vault password unset
  ```

* [2023-05-31] Kolla has released the first RC for Antelope (2023.1) and work has started on
  getting it into OSISM.

* [2023-05-31] Validation of sub-environments is now possible with the new ``--environment``
  parameter for the ``validate`` command. This also fixes a problem with the ``validate``
  command that stopped validation of individual service configurations after the introduction
  of sub-environments ([osism/issues#538](https://github.com/osism/python-osism/pull/453)).

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
