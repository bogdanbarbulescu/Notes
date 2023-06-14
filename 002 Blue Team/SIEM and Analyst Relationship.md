### What is SIEM?
#siem

Security information and event management (SIEM), is a security solution that provides the real time logging of events in an environment. The actual purpose for event logging is to detect security threats.

In general, SIEM products have a number of features. The ones that interest us most as SOC analysts are: they filter the data that they collect and create alerts for any suspicious events.

Example of an alert: If someone on a Windows operating system attempts to enter 20 incorrect passwords in 10 seconds, this is suspicious activity, it is not likely that someone who forgot their password would try to re-enter their password so many times in such a short period. This is why we create a SIEM rule/filter, to determine such activities that exceed the threshold values. Due to this SIEM rule an alert will be created if such a situation occurs.

Some popular SIEM solutions: **IBM QRadar, ArcSight ESM, FortiSIEM, Splunk** etc.

As we mentioned above, alerts are created by data that is passed through filters. The alerts are primarily analyzed by a SOC analyst. This is exactly where a SOC analyst’s duty in the security operations center begins. Fundamentally, he must decide whether this created alert is a real threat or a false alarm.

To better understand, let’s return to the “Monitoring” page, as you see below there are various alerts on the SIEM interface. As a SOC analyst we should analyze the details related to these alerts with the help of other SOC products (such as EDR, Log Management, Threat Intelligence Feed, etc.) and lastly we should determine whether or not they are real threats.