![Logo](https://github.com/lontivero/Open.Nat/raw/gh-pages/images/logos/128.jpg)

Open.NAT
======

Open.NAT is a lightweight and easy-to-use class library to allow port forwarding in NAT devices that support UPNP (Universal Plug & Play) and/or PMP (Port Mapping Protocol). 


Goals
-----
NATed computers cannot be reached from outside and this is particularly painful for peer-to-peer or friend-to-friend software.
The main goal is to simplify communication amoung computers behind NAT devices that support UPNP and/or PMP providing a clean 
and easy interface to get the external IP address and map ports and helping you to achieve peer-to-peer communication. 

+ Tested with .NET  _YES_
+ Tested with Mono  _YES_

How to use?
-----------
With nuget :
> **Install-Package Open.NAT** 

Go on the [nuget website](https://www.nuget.org/packages/OpenNAT/) for more information.

Example
--------

The simplest scenario:

```c#
var discoverer = new NatDiscoverer();
var device = await discoverer.DiscoverDeviceAsync();
var ip = await device.GetExternalIPAsync();
Console.WriteLine("The external IP Address is: {0} ", ip);
```

The following piece of code shows a common scenario: It starts the discovery process for a NAT-UPNP device and onces discovered it creates a port mapping. If no device is found before ten seconds, it fails with NatDeviceNotFoundException.


```c#
var discoverer = new NatDiscoverer();
var cts = new CancellationTokenSource(10000);
var device = await discoverer.DiscoverDeviceAsync(PortMapper.Upnp, cts);

await device.CreatePortMapAsync(new Mapping(Protocol.Tcp, 1600, 1700, "The mapping name"));
```

For more info please check the [Wiki](https://github.com/lontivero/Open.Nat/wiki)

Documentation
-------------
+ Why Open.NAT? Here you have [ten reasons](https://github.com/lontivero/Open.Nat/wiki/Why-Open.NAT%3F) that make Open.NAT a good candidate for you projects
+ [Visit the Wiki page](https://github.com/lontivero/Open.Nat/wiki)

Development
-----------
Open.NAT is been developed by [Lucas Ontivero](http://geeks.ms/blogs/lontivero) ([@lontivero](http://twitter.com/lontivero)). 
You are welcome to contribute code. You can send code both as a patch or a GitHub pull request. 

Here you can see what are the next features to implement. [Take it a look!](https://trello.com/b/rkHdEm5H/open-nat)
Build Status
------------

[![Build status](https://ci.appveyor.com/api/projects/status/dadcbt26mrlri8cg)](https://ci.appveyor.com/project/lontivero/open-nat)

[![NuGet version](https://badge.fury.io/nu/open.nat.png)](http://badge.fury.io/nu/open.nat)

### Version 2.0.8
* Fixes several defects. #10, #11, #12, #13 and #14

### Version 2.0.0
* Thus version breaks backward compatibility with v1.
* Changes the event-based nature of discovery to an asynchronous one.
* Managed port mapping timelife.

### Version 1.1.0
* Fix for SSDP Location header.
* After this version Open.NAT breaks backward compatibility.

### Version 1.0.19
* Minor changes previous to v2.

### Version 1.0.18
* Discovery timeout raises an event.
* Permanent mappings are created when NAT only supports that kind of mappings.
* Protocol to use in discovery process can be specified.
* Automatic renew port mappings before expiration.
* Add operations timeout after 4 seconds.
* Add parameters validation in Mapping class.
* Fix UnhandledException event was never raised.

### Version 1.0.17
*  Discovery timeout added.
*  Auto release ports opened in the session.
*  Fix NextSearch to use UtcNow (also performance)
*  Fix LocalIP property after add a port.
*  Tracing improvements

### Version 1.0.16
*  Discovery performance and bandwidth improved
*  Tracing improved
*  Cleaner code

