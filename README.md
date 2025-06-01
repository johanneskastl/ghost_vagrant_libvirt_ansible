# ghost_vagrant_libvirt_ansible

This Vagrant setup creates a VM and installs the [Ghost
CMS](https://ghost.org/) on it. It uses a `production` setup, as Ghost calls it.
This means that there is a [Nginx](https://nginx.org/) as reverse proxy as well
as a [MariaDB](https://mariadb.org/) database.

There are multiple branches for different operating systems.

The `main` branch uses AlmaLinux 10. Although that can be changed in the
Vagrantfile, please beware that this will break the Ansible provisioning.

At the time of writing, there are branches for Fedora 41, Fedora 42, openSUSE
Leap 15.6, openSUSE Tumbleweed, Debian12, AlmaLinux9, Ubuntu 22.04 and Ubuntu
24.04.

Due to the fact that Ghost only supports Ubuntu officially and fails to detect
Nginx on other OSes, Ansible does some steps manually, e.g. creating the Nginx
configuration.

## Vagrant

1. You need vagrant obviously. And ansible. And git...
1. In case you do not have the `ansible` package installed, but only the
   `ansible-core` one, you might need to install the collections used by the
   playbooks.

   ```
   ansible-galaxy collection install -r requirements.yml
   ```

1. Fetch the Vagrant box, on this branch this is `fedora/41-cloud-base`, using
   `vagrant box add fedora/41-cloud-base`.
1. Make sure the git submodules are fully working by issuing `git submodule init
   && git submodule update`
1. Run `vagrant up`
1. Open the URL that Ansible printed out at the end of the provisioning. It
   should look something like `http://ghost.192.0.2.13.sslip.io`. You should see
   a default Ghost start page.
1. Open the second URL that Ansible printed out at the end of the provisioning.
   It should look something like `http://ghost.192.0.2.13.sslip.io/ghost/`. This
   will show a sign-up page, where you can set a title and enter your user
   details. Afterwards you are being directed to the administrative section,
   where you can changes themes and do lots of wonderful things.
1. Party!

## Cleaning up

The VM can be torn down after playing around using `vagrant destroy`.

## License

BSD-3-Clause

## Author Information

I am Johannes Kastl, reachable via git@johannes-kastl.de
