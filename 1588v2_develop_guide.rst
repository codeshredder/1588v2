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

testptp: http://lxr.free-electrons.com/source/Documentation/ptp/testptp.c


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

Host: ubuntu 12.04 LTS 64bit

PHY: dp83640


2. Host Prepare
==============




3. Kernel drivers
==============

kernel config::

   Networking support -> Networking options -> Timestamping in PHY devices
   Device Drivers -> Network device support -> PHY Device support and infrastructure
   Device Drivers -> PTP clock support -> PTP clock support
                                       -> Driver for the National Semiconductor DP83640 PHYTER
   

4. Ptp protocol
==============

download ptpd-2.3.1-rc1.tar.gz from http://ptpd.sourceforge.net/

::

   tar xvf ptpd-2.3.1-rc1.tar.gz
   cd ptpd-2.3.1-rc1
   ./configure
   make


ptpd2 in ./src is the target binary.

cross compile

::

   tar xvf ptpd-2.3.1-rc1.tar.gz
   cd ptpd-2.3.1-rc1
   export ac_cv_func_malloc_0_nonnull=yes
   ./configure  --build=i686-pc-linux --host=arm-linux-gnueabi --target=i686-linux  LIBS="-L./lib -lrt -lm"
   make

(copy librt.so libm.so of arm to ./lib)


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

