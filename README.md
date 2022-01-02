Ansible Role: nebula
=========

Ansible role to install [Nebula](https://github.com/slackhq/nebula) Mesh.

Requirements
------------

The requirements are:
- Ansible version >=2.10
- Linux
- Systemd as init system

This role is tested on:
- Ubuntu 20.04 Focal Fossa
- Python 3.10
- Ansible 2.10

Role Variables
--------------

The following variables are available:

| Variable                                      | Default Value                              | Description                                                                                                                                                                              |
|-----------------------------------------------|--------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `nebula_am_lighthouse`                        | `false`                                    | If member is a lighthouse                                                                                                                                                                |
| `nebula_arch`                                 | `amd64`                                    | Architecture to use to build the download URL                                                                                                                                            |
| `nebula_bin_dir`                              | `/usr/local/bin`                           | The directory to install the binaries                                                                                                                                                    |
| `nebula_ca_duration`                          | `175200h` (20 years)                       | The duration of CA                                                                                                                                                                       |
| `nebula_ca_host`                              | `<UNDEFINED>`                              | The inventory_hostname of the host which should be used as CA. If not defined, **exactly 1 play host must have `nebula_is_ca` variable set to true. Required if `nebula_am_lighthouse`** |
| `nebula_ca_name`                              | `Nebula CA Org`                            | The name of the CA                                                                                                                                                                       |
| `nebula_ca_wait_timeout_secs`                 | `120`                                      | Timeout in seconds for members to wait until the CA is ready to issue certificates                                                                                                       |
| `nebula_config_dir`                           | `/etc/nebula`                              | Directory to keep config and certificates                                                                                                                                                |
| `nebula_download_checksum`                    | `<UNDEFINED>`                              | If provided, the checksum will be tested before downloading Nebula from the URL                                                                                                          |
| `nebula_download_dir`                         | `/opt`                                     | The directory to download the tarball                                                                                                                                                    |
| `nebula_download_url`                         | see [defaults/main.yml](defaults/main.yml) | The Nebula download URL                                                                                                                                                                  |
| `nebula_groups`                               | `[]`                                       | Nebula groups of the member                                                                                                                                                              |
| `nebula_ip`                                   | `<UNDEFINED>`                              | The IP required by Nebula. **Needs to contain subnet prefix at the end (e.g. `172.20.0.42/24`). Required**.                                                                              |
| `nebula_is_ca`                                | `false`                                    | If the host is the certificate authority or not. If `nebula_ca_host` is not defined, **exactly 1 play host must have this variable set to true. Required if `nebula_am_lighthouse`**     |
| `nebula_is_member`                            | `true`                                     | If the host should be added to the mesh                                                                                                                                                  |
| `nebula_name`                                 | `"{{ ansible_hostname }}"`                 | Name of the Nebula member                                                                                                                                                                |
| `nebula_routable_ip`                          | `<UNDEFINED>`                              | The routable IP required by Nebula. If undefined, the public IP of the host will be determined and used                                                                                  |
| `nebula_service_name`                         | `nebula`                                   | Name of the systemd service                                                                                                                                                              |
| `nebula_version`                              | `v1.5.2`                                   | Nebula version to use. See git tags [here](https://github.com/slackhq/nebula/releases)                                                                                                   |                                                                                                                                                              |
| `nebula_additional_member_certs_download_dir` | `/tmp`                                     | Local directory to download any additional member certificates                                                                                                                           |
| `nebula_additional_member_certs`              | see [defaults/main.yml](defaults/main.yml) | Dict object of additional member certs with each key being the member name and value being the member configuration. Only used to generate additional certificates on CA                 |
| `nebula_pki_disconnect_invalid`               | `<UNDEFINED>`                              | See Nebula [configuration reference](https://www.defined.net/nebula/config/) and [example config](https://github.com/slackhq/nebula/blob/master/examples/config.yml)                     |
| `nebula_lighthouse_interval`                  | `60`                                       | See Nebula [configuration reference](https://www.defined.net/nebula/config/) and [example config](https://github.com/slackhq/nebula/blob/master/examples/config.yml)                     |
| `nebula_listen_host`                          | `0.0.0.0`                                  | See Nebula [configuration reference](https://www.defined.net/nebula/config/) and [example config](https://github.com/slackhq/nebula/blob/master/examples/config.yml)                     |
| `nebula_listen_port`                          | `4242`                                     | See Nebula [configuration reference](https://www.defined.net/nebula/config/) and [example config](https://github.com/slackhq/nebula/blob/master/examples/config.yml)                     |
| `nebula_listen_batch`                         | `<UNDEFINED>`                              | See Nebula [configuration reference](https://www.defined.net/nebula/config/) and [example config](https://github.com/slackhq/nebula/blob/master/examples/config.yml)                     |
| `nebula_listen_read_buffer`                   | `<UNDEFINED>`                              | See Nebula [configuration reference](https://www.defined.net/nebula/config/) and [example config](https://github.com/slackhq/nebula/blob/master/examples/config.yml)                     |
| `nebula_listen_write_buffer`                  | `<UNDEFINED>`                              | See Nebula [configuration reference](https://www.defined.net/nebula/config/) and [example config](https://github.com/slackhq/nebula/blob/master/examples/config.yml)                     |
| `nebula_punchy_punch`                         | `true`                                     | See Nebula [configuration reference](https://www.defined.net/nebula/config/) and [example config](https://github.com/slackhq/nebula/blob/master/examples/config.yml)                     |
| `nebula_punchy_respond`                       | `<UNDEFINED>`                              | See Nebula [configuration reference](https://www.defined.net/nebula/config/) and [example config](https://github.com/slackhq/nebula/blob/master/examples/config.yml)                     |
| `nebula_punchy_delay`                         | `<UNDEFINED>`                              | See Nebula [configuration reference](https://www.defined.net/nebula/config/) and [example config](https://github.com/slackhq/nebula/blob/master/examples/config.yml)                     |
| `nebula_cipher`                               | `<UNDEFINED>`                              | See Nebula [configuration reference](https://www.defined.net/nebula/config/) and [example config](https://github.com/slackhq/nebula/blob/master/examples/config.yml)                     |
| `nebula_tun_disabled`                         | `false`                                    | See Nebula [configuration reference](https://www.defined.net/nebula/config/) and [example config](https://github.com/slackhq/nebula/blob/master/examples/config.yml)                     |
| `nebula_tun_dev`                              | `nebula1`                                  | See Nebula [configuration reference](https://www.defined.net/nebula/config/) and [example config](https://github.com/slackhq/nebula/blob/master/examples/config.yml)                     |
| `nebula_tun_drop_local_broadcast`             | `false`                                    | See Nebula [configuration reference](https://www.defined.net/nebula/config/) and [example config](https://github.com/slackhq/nebula/blob/master/examples/config.yml)                     |
| `nebula_tun_drop_multicast`                   | `false`                                    | See Nebula [configuration reference](https://www.defined.net/nebula/config/) and [example config](https://github.com/slackhq/nebula/blob/master/examples/config.yml)                     |
| `nebula_tun_tx_queue`                         | `500`                                      | See Nebula [configuration reference](https://www.defined.net/nebula/config/) and [example config](https://github.com/slackhq/nebula/blob/master/examples/config.yml)                     |
| `nebula_tun_mtu`                              | `1300`                                     | See Nebula [configuration reference](https://www.defined.net/nebula/config/) and [example config](https://github.com/slackhq/nebula/blob/master/examples/config.yml)                     |
| `nebula_logging_level`                        | `info`                                     | See Nebula [configuration reference](https://www.defined.net/nebula/config/) and [example config](https://github.com/slackhq/nebula/blob/master/examples/config.yml)                     |
| `nebula_logging_format`                       | `text`                                     | See Nebula [configuration reference](https://www.defined.net/nebula/config/) and [example config](https://github.com/slackhq/nebula/blob/master/examples/config.yml)                     |
| `nebula_logging_disable_timestamp`            | `false`                                    | See Nebula [configuration reference](https://www.defined.net/nebula/config/) and [example config](https://github.com/slackhq/nebula/blob/master/examples/config.yml)                     |
| `nebula_firewall_conntrack_tcp_timeout`       | `12m`                                      | See Nebula [configuration reference](https://www.defined.net/nebula/config/) and [example config](https://github.com/slackhq/nebula/blob/master/examples/config.yml)                     |
| `nebula_firewall_conntrack_udp_timeout`       | `3m`                                       | See Nebula [configuration reference](https://www.defined.net/nebula/config/) and [example config](https://github.com/slackhq/nebula/blob/master/examples/config.yml)                     |
| `nebula_firewall_conntrack_default_timeout`   | `10m`                                      | See Nebula [configuration reference](https://www.defined.net/nebula/config/) and [example config](https://github.com/slackhq/nebula/blob/master/examples/config.yml)                     |
| `nebula_firewall_conntrack_max_connections`   | `100000`                                   | See Nebula [configuration reference](https://www.defined.net/nebula/config/) and [example config](https://github.com/slackhq/nebula/blob/master/examples/config.yml)                     |
| `nebula_firewall_outbound`                    | see [defaults/main.yml](defaults/main.yml) | See Nebula [configuration reference](https://www.defined.net/nebula/config/) and [example config](https://github.com/slackhq/nebula/blob/master/examples/config.yml)                     |
| `nebula_firewall_inbound`                     | see [defaults/main.yml](defaults/main.yml) | See Nebula [configuration reference](https://www.defined.net/nebula/config/) and [example config](https://github.com/slackhq/nebula/blob/master/examples/config.yml)                     |

Example Playbook
----------------

Here's a minimalistic example:

```yaml
- name: Setup Nebula
  hosts: servers
  become: true
  strategy: free
  roles:
    - role: utkuozdemir.nebula
```

See [tests/](tests) directory for a concrete example.
