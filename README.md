# mi-qutic-automx

use [jfqd/mi-qutic.base](https://github.com/jfqd/mi-qutic-base) to create a provisionable image

## description

A qutic automx-image.

## mdata variables

See [mi-qutic-base Readme](https://github.com/jfqd/mi-qutic-base/blob/master/README.md) for a list of usable metadata.

## installation

The following sample can be used to create a zone running a copy of the the automx image.

```
IMAGE_UUID=$(imgadm list | grep 'qutic-automx' | tail -1 | awk '{ print $1 }')
vmadm create << EOF
{
  "brand":      "joyent",
  "image_uuid": "$IMAGE_UUID",
  "alias":      "automx",
  "hostname":   "automx.example.com",
  "dns_domain": "example.com",
  "resolvers": [
    "80.80.80.80",
    "80.80.81.81"
  ],
  "nics": [
    {
      "interface": "net0",
      "nic_tag":   "admin",
      "ip":        "10.10.10.10",
      "gateway":   "10.10.10.1",
      "netmask":   "255.255.255.0"
    }
  ],
  "max_physical_memory": 1024,
  "max_swap":            1024,
  "quota":                 10,
  "cpu_cap":              100,
  "customer_metadata": {
    "admin_authorized_keys": "your-long-key",
    "root_authorized_keys":  "your-long-key",
    "mail_smarthost":        "mail.example.com",
    "mail_auth_user":        "you@example.com",
    "mail_auth_pass":        "smtp-account-password",
    "mail_adminaddr":        "report@example.com",
    "munin_master_allow":    "munin-master.example.com",
    "nagios_allow":          "10.10.10.0/24",
    "server_name":           "automx.example.com",
    "server_alias":          "autoconfig.example.com autodiscover.example.com"
  }
}
EOF
```
