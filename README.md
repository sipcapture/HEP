# HEP
HEP-EEP: Extensible Encapsulation Protocol

This repository serves technical details and documentation for the _EEP_ *(formely HEP)* Encapsulation Protocol.

The Extensible Encapsulation protocol (“EEP”) provides a method to duplicate an IP datagram to a collector by encapsulating the original datagram and its relative header properties (as payload, in form of concatenated
chunks) within a new IP datagram transmitted over UDP/TCP/SCTP connections for remote collection. Encapsulation allows for the original content to be transmitted without altering the original IP datagram and header contents and provides flexible allocation of additional chunks containing additional arbitrary data.

The protocol was originally designed by Alexandr Dubovikov for the [HOMER](http://github.com/sipcapture/homer) [SIPCAPTURE](http://github.com/sipcapture) project and is currently at its third generation (HEP3) and implemented in many leading SIP platforms.

For any inquiry, please contact [support@sipcapture.org](mailto:support@sipcapture.org)

