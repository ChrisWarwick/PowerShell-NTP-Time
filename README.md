


PowerShell-NTP-Time
====
PowerShell Module to read NTP time from a specified NTP Server

Chris Warwick, @cjwarwickps, September 2015.

This module contains a single PS Function 'Get-NtpTime' which sends an NTP request to a specified NTP server and
decodes the returned raw NTP packet. The function will connect to pool.ntp.org if no server is specified.

I originally wrote this script to check NTP responses from Windows Domain Controllers - but it works with 
any NTP server.  See rfc-1305: http://www.faqs.org/rfcs/rfc1305.html

Refer to the PowerShell help and additional background information included in the module for further details.

Inline Help
----
````
.PARAMETER Server
    The NTP Server to contact.  Uses pool.ntp.org by default.
.PARAMETER MaxOffset
    The maximum acceptable offset between the local clock and the NTP Server, in milliseconds.
    The script will throw an exception if the time difference exceeds this value (on the assumption
    that the returned time may be incorrect).  Default = 10000 (10s).
.PARAMETER NoDns
    (Switch) If specified do not attempt to resolve Version 3 Secondary Server ReferenceIdentifiers.
.EXAMPLE
    Get-NtpTime uk.pool.ntp.org
    Gets time from the specified server.
.EXAMPLE
    Get-NtpTime | fl *
    Get time from default server (pool.ntp.org) and displays all output object attributes.
.EXAMPLE
    Get-NtpTime DC01.company.org
    Get time from a domain controller.
````


Sample Usage
----
````
 PS:\> Get-NtpTime


 NtpServer           : pool.ntp.org
 NtpTime             : 21/09/2015 12:17:26
 OffsetSeconds       : -0.009
 NtpVersionNumber    : 3
 Mode_text           : server
 Stratum             : 2
 ReferenceIdentifier : 195.66.241.2 <ntp0.linx.net>



 PS:\> Get-NtpTime -Server uk.pool.ntp.org | Format-List *


 NtpServer           : uk.pool.ntp.org
 NtpTime             : 21/09/2015 12:18:23
 Offset              : -18.845458984375
 OffsetSeconds       : -0.019
 Delay               : 22.98193359375
 t1ms                : 3588751103158.74
 t2ms                : 3588751103151.39
 t3ms                : 3588751103151.43
 t4ms                : 3588751103181.77
 t1                  : 21/09/2015 12:18:23
 t2                  : 21/09/2015 12:18:23
 t3                  : 21/09/2015 12:18:23
 t4                  : 21/09/2015 12:18:23
 LI                  : 0
 LI_text             : no warning
 NtpVersionNumber    : 3
 Mode                : 4
 Mode_text           : server
 Stratum             : 2
 Stratum_text        : secondary reference (via NTP or SNTP)
 PollIntervalRaw     : 0
 PollInterval        : 00:00:01
 Precision           : -23
 PrecisionSeconds    : 1.19209289550781E-07
 ReferenceIdentifier : 195.66.241.2 <ntp0.linx.net>
 RootDelay           : 0.003143310546875
 RootDispersion      : 0.02679443359375
 Raw                 : {28, 2, 0, 233, 0, 0, 0, 206, 0, 0, 6, 220, 195, 66, 241, 2, 213, 231, 252, 27...}
 ````
 
 Version History:
 ---
 V1.1 (This version)
  - Updated help to reflect usage against domain controllers
  - Removed default display format code from script and replaced with format.ps1xml file

 V1.0 (Initial PowerShell Gallery version)
  - Copy with updates from original script
 
 V0.9 (Initial Technet ScriptCenter version)

 V0.1-0.8 Dev versions
