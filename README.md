# rpc-deploy-utility-image

The repo will generate the rpc-deploy-utility-image.  It is a network bootable
LiveOS based on CentOS 7 used for handling provisioning operations for rpc-deploy.

The image contains base tooling for Dell/HP/etc server types and also includes 
[rpc-deploy-utility](https://github.com/rcbops/rpc-deploy-utility) which runs different
playbooks depending on the playbook= flag set on the kernel command line when loading the image.

The image leverages dracut for loading the rootfs and can be loaded via iPXE with the following config:

    kernel http://path.to/vmlinuz
    initrd http://path.to/initrd
    imgargs vmlinuz root=live:http://path.to/rootfs.url nomodeset rd.writable.fsimg rd.shell enforcing=0 BOOTIF=${netX/mac} ip=dhcp playbook=playbook_from_rpc_deploy_utility firmware hpsum_key=key_for_hpsum_access_for_hps role={infra,ceph,haproxy,compute} deploy_host=ip_of_deploy_host initrd=initrd.img
    boot
