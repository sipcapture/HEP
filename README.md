<img src="https://camo.githubusercontent.com/cb8c0b32324fa9cd73f7e23a63797b5fb97c4bd0/687474703a2f2f692e696d6775722e636f6d2f466649323851762e706e67" width="150">

# <img src="http://i.imgur.com/RSUlFRa.gif" width="150" alt="HEP">

### HEP-EEP: Extensible Encapsulation Protocol

This repository serves technical documentation for the _EEP_ *(formely HEP)* Encapsulation Protocol.

### Summary:
The Extensible Encapsulation protocol _(“EEP”)_ provides a method to duplicate an IP datagram to a collector by encapsulating the original datagram and its relative header properties _(as payload, in form of concatenated
chunks)_ within a new IP datagram transmitted over UDP/TCP/SCTP connections for remote collection. Encapsulation allows for the original content to be transmitted without altering the original IP datagram and header contents and provides flexible allocation of additional chunks containing additional arbitrary data. The method is NOT designed
or intended for “tunneling” of IP datagrams over network segments, and best serves as vector for passive duplication of packets intended for remote or centralized collection and long term storage and analysis.

### History:
The protocol was originally designed by Alexandr Dubovikov and Roland Hänel for the [HOMER](http://github.com/sipcapture/homer) [SIPCAPTURE](http://github.com/sipcapture) project and is currently at its third generation _(HEPv3)_ 

### Integration:
HEP is natively implemented in many leading SIP platforms:
* [Kamailio](https://github.com/sipcapture/homer/wiki/Examples%3A-Kamailio) 
* [OpenSIPS](https://github.com/sipcapture/homer/wiki/Examples%3A-OpenSIPS)
* [FreeSWTICH](https://github.com/sipcapture/homer/wiki/Examples%3A-FreeSwitch)
* [Asterisk](https://reviewboard.asterisk.org/r/3207/) 
* [RTP:Engine](https://github.com/sipwise/rtpengine) 
*  ... and more!

HEP is also supported by several capture tools:
* [Captagent](http://github.com/sipcapture/captagent)
* [Heplify](https://github.com/sipcapture/heplify)
* [Sipgrep](http://github.com/sipcapture/sipgrep)
* [HEPipe](http://github.com/sipcapture/hepipe)
* [nProbe](http://www.ntop.org/products/netflow/nprobe/)
* [sngrep](https://github.com/irontec/sngrep)
* ... and more!

HEP code examples are available for many languages:
* [C/C++](https://github.com/sipcapture/hep-c)
* [Javascript/Node](https://github.com/sipcapture/hep-js)
* [Java](https://github.com/sipcapture/hep-java)
* [Erlang](https://github.com/sipcapture/hep-erlang)
* [Go](https://github.com/sipcapture/hep-go)
* [Perl](https://github.com/sipcapture/hep-perl)
* [Python](https://github.com/sipcapture/hep-python)



### Support
For any inquiry related to HEP/EEP please contact [support@sipcapture.org](mailto:support@sipcapture.org)

