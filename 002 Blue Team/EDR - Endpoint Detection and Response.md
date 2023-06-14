### What is EDR?

Endpoint detection and response (EDR), also known as endpoint threat detection and response (ETDR), is an integrated endpoint security solution that combines real-time continuous monitoring and collection of endpoint data with rules-based automated response and analysis capabilities.  
(Definition source: mcafee.com)

  
  
**Analysis with EDR**

Some popular EDR solutions used in the workplace: CarbonBlack, SentinelOne, FireEye HX.

**Live Investigation**

In addition, we can click on the “Connect” button and access the machine itself in order to continue our analysis there.

**Containment**

We must isolate a hacked machine from the network. There are important reasons behind this: to be able to stop the attacker’s connection to the inner network and to prevent his movement throughout the inner network.

Therefore the device should be cut off from inner and outer networks until the security gaps are fixed and the device is usable again. We can ensure that isolation happens using the “Containment” feature of EDR solutions. This feature allows the selected device to communicate only with the EDR center. This means that even though the device is isolated from the network we can still continue our analysis.

**Quick Tip**

If you have any kind of IOC such as a file hash, file name, etc. you can perform a search in EDR among all hosts and see if there is a match. For example, let’s say you are sure that a device has been hacked and you have obtained a file with an MD5 hash of “ac596d282e2f9b1501d66fce5a451f00”. You can search for this hash value in EDR and determine whether this file is present or executed on other devices. Therefore you can understand who was affected by this attack.

