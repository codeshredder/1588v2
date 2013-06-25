==========================================================
  1588v2 Develop Guide
==========================================================


Authors
==========

`codeshredder <https://github.com/codeshredder>`_ 

Reference
==========

linux kernel: http://www.kernel.org

ptpd: http://ptpd.sourceforge.net/


Table of Contents
=================

::

  0. What is it?
  1. Overview
  2. Host Prepare
  3. Kernel drivers
  4. Ptp protocol
  5. test1
  6. test2
  7. Licensing
  8. Contacts
  
0. What is it?
==============



1. Overview
==============

Host: Ubuntu 12.04 LTS 64bit

PHY: TI DP83640


2. Host Prepare
==============




3. Kernel drivers
==============

kernel config::

   NETWORK_PHY_TIMESTAMPING
   PHYLIB
   Device Drivers ->  PTP clock support  ->  PTP clock support
                                         ->  Driver for the National Semiconductor DP83640 PHYTER
   



4. Ptp protocol
==============

download ptpd-2.2.2.tar.gz from http://ptpd.sourceforge.net/

::

   tar xvf ptpd-2.2.2.tar.gz
   cd ptpd-2.2.2/src
   make


ptpd2 is the target binary.


5. test1
==============

connect two node's eth0 with cable.

clock master::

   ifconfig eth0 192.168.0.1
   ./ptpd2 -G -b eth0 -P


clock slave::

   ifconfig eth0 192.168.0.2
   ./ptpd2 -g -b eth0 -P


check result::

   1) change time in master by "date -s xxxx".
   2) show time in slave to check if slave time is the same as master.

6. test2
==============


7. Licensing
============

This project is licensed under Creative Commons License.

To view a copy of this license, visit [ http://creativecommons.org/licenses/ ].

8. Contacts
===========

codeshredder  : evilforce@gmail.com

