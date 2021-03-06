!SLIDE smbullets small
# Facter

* Facter returns key value pairs named facts
* It is used by Puppet to gather information about the node
* You can also run it on command line to list facts

    <pre>
    $ facter
    augeas => {
      version => "1.12.0"
    }
    disks => {
      vda => {
        size => "10.00 GiB",
        size_bytes => 10737418240,
        vendor => "0x1af4"
      }
    }
    ...
    system_uptime => {
      days => 0,
      hours => 2,
      seconds => 8378,
      uptime => "2:19 hours"
    }
    timezone => UTC
    virtual => kvm
    </pre>

~~~SECTION:handouts~~~

****

Facter returns key value pairs named facts. In older versions these were simple string representations, in newer
versions structured facts are possible, which means a array or hash is returned.

To access such a fact like the disk size in Puppet code use:

    @@@ Puppet
    $facts['disks']['vda']['size']

Or using the older top-scope variables, which are now deprecated:

    @@@ Puppet
    $::disks['vda']['size']

~~~PAGEBREAK~~~

Facter can also be used to display the legacy style. Here all legacy facts shown in the old way as simple strings.

    $ facter --show-legacy
    aio_agent_version => 6.7.2
    architecture => x86_64
    augeas => {
      version => "1.12.0"
    }
    augeasversion => 1.12.0
    bios_release_date => 12/01/2006
    bios_vendor => innotek GmbH
    bios_version => VirtualBox
    ...

The facts are used as Puppet's inventory tool and are generated before requesting a catalog from the master. The master
can use facts in conditionals or templates during catalog compilation but it is impossible to change its values during
a run or change the agents behavior directly on the node based on facts.

Facter includes many different built-in facts and allows to add additional facts in several ways which allows to
provide them by Puppet modules requiring this information.

~~~ENDSECTION~~~
