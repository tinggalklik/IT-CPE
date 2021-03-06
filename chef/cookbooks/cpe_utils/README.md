cpe_utils Cookbook
==================
This cookbook is where we keep all the common function / classes

Usage
-----


#### node.os_greater_than? ####
If the current system's OS X version is greater than the specified version, do something.
```
if node.os_greater_than?('10.10') do
  something
end
```

#### node.os_less_than? ####
If the current system's OS X version is less than the specified version, do something.

```
if node.os_less_than?('10.11') do
  something
end
```

#### node.os_at_least? ####
This functions like a greater than or equal to. In this example, if the machine is 10.11.1 or greater, it will run something.
```
if node.os_at_least?('10.11.1') do
  something
end
```

#### node.os_at_least_or_lower? ####
This functions like a less than or equal to. In this example, if the machine is 10.10.3 or lower, it will run something.
```
if node.os_at_least_or_lower?('10.10.3') do
  something
end
```

#### OS Checks ####

These are to check if a node is a specific OS type

```
node.linux?
node.ubuntu?
node.centos?
node.macosx?
node.windows?
```

These are generally used to scope os-specific features. For instance:
```
if node.macosx?
  osx_profile 'com.company.screensaver.mobileconfig' 
end
```

These can also be used within a resource block via only_if
```
osx_profile 'Install screensaver profile' do
  only_if { node.macosx? }
  profile 'com.company.screensaver.mobileconfig'
end
```

#### node.virtual? ####
This is similar to the OS check functions, except it checks to see if the machine is a virtual machine (guest). This is useful for scoping things like VMWare Tools installs to VMs only.

```
remote_pkg 'VMWareTools' do
  only_if { node.virtual? }
  version '1.1.0'
  checksum '3701fbdc8096756fab077387536535b237e010c45147ea631f7df43e3e4904e0'
  receipt 'com.vmware.tools'
end
```

#### node.munki_installed? ####
Returns true if the item is in munki's managed_installs list.
```
if node.munki_installed?('Firefox') do
  something 
end
```
