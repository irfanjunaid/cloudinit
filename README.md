# cloudinit

**Note:** The image must have the cloudinit installed for the setup to work.

## cloud-localds -V (return code: 1)
cloud-localds: unrecognized option '--version'
Usage: cloud-localds [ options ] output user-data [meta-data]

   Create a disk for cloud-init to utilize nocloud
```
   options:
     -h | --help             show usage
     -d | --disk-format D    disk format to output. default: raw
                             can be anything supported by qemu-img or
                             tar, tar-seed-local, tar-seed-net
     -H | --hostname    H    set hostname in metadata to H
     -f | --filesystem  F    filesystem format (vfat or iso), default: iso9660
     -i | --interfaces  F    write network interfaces file into metadata
     -N | --network-config F write network config file to local datasource
     -m | --dsmode      M    add 'dsmode' ('local' or 'net') to the metadata
                             default in cloud-init is 'net', meaning network is
                             required.
     -V | --vendor-data F    vendor-data file
     -v | --verbose          increase verbosity
```
Note, --dsmode, --hostname, and --interfaces are incompatible with metadata.

   Example:
```
    * cat my-user-data
      #cloud-config
      password: passw0rd
      chpasswd: { expire: False }
      ssh_pwauth: True
    * echo "instance-id: $(uuidgen || echo i-abcdefg)" > my-meta-data
    * cloud-localds my-seed.img my-user-data my-meta-data
    * kvm -net nic -net user,hostfwd=tcp::2222-:22 \
         -drive file=disk1.img,if=virtio -drive file=my-seed.img,if=virtio
    * ssh -p 2222 ubuntu@localhost
```
cloud-localds --help (return code: 0)
Usage: cloud-localds [ options ] output user-data [meta-data]

   Create a disk for cloud-init to utilize nocloud
```
   options:
     -h | --help             show usage
     -d | --disk-format D    disk format to output. default: raw
                             can be anything supported by qemu-img or
                             tar, tar-seed-local, tar-seed-net
     -H | --hostname    H    set hostname in metadata to H
     -f | --filesystem  F    filesystem format (vfat or iso), default: iso9660
     -i | --interfaces  F    write network interfaces file into metadata
     -N | --network-config F write network config file to local datasource
     -m | --dsmode      M    add 'dsmode' ('local' or 'net') to the metadata
                             default in cloud-init is 'net', meaning network is
                             required.
     -V | --vendor-data F    vendor-data file
     -v | --verbose          increase verbosity
```
   Note, --dsmode, --hostname, and --interfaces are incompatible with metadata.

   Example:
```
    * cat my-user-data
      #cloud-config
      password: passw0rd
      chpasswd: { expire: False }
      ssh_pwauth: True
    * echo "instance-id: $(uuidgen || echo i-abcdefg)" > my-meta-data
    * cloud-localds my-seed.img my-user-data my-meta-data
    * kvm -net nic -net user,hostfwd=tcp::2222-:22 \
         -drive file=disk1.img,if=virtio -drive file=my-seed.img,if=virtio
    * ssh -p 2222 ubuntu@localhost
```
