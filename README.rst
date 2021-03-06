===============================
Evic
===============================

.. image:: https://travis-ci.org/Ban3/python-evic.svg?branch=master
   :target: https://travis-ci.org/Ban3/python-evic

Evic is a USB programmer for devices based on the Joyetech Evic VTC Mini.

Supported devices
---------------------

* Joyetech eVic VTwo*
* Joyetech eVic VTwo mini
* Joyetech evic VTC Mini
* Joyetech eVic VTC Dual*
* Joyetech eVic AIO*
* Joyetech eVic Basic*
* Joyetech eVic Primo*
* Joyetech eVic Primo Mini*
* Joyetech eVic Primo 2.0*
* Joyetech Cuboid
* Joyetech Cuboid Mini
* Joyetech Cuboid 200*
* Joyetech eGrip II*
* Eleaf iStick QC 200W*
* Eleaf iStick TC100W*
* Eleaf iStick TC200W*
* Eleaf iStick Pico
* Eleaf iStick Pico RDTA*
* Eleaf iStick Pico Mega*
* Eleaf iStick Pico Dual*
* Eleaf iStick Power*
* Eleaf ASTER*
* Wismec Presa TC75W
* Wismec Presa TC100W*
* Wismec Reuleaux RX2/3
* Wismec Reuleaux RX200*
* Wismec Reuleaux RX200S*
* Wismec Reuleaux RX75
* Wismec Reuleaux RX300*
* Wismec Reuleaux RXmini*
* Wismec Predator 228
* Vaporflask Classic*
* Vaporflask Lite*
* Vaporflask Stout*
* Beyondvape Centurion*
* Vaponaute La Petit Box*
* Vapor Shark SwitchBox RX*

\*Untested

Tested firmware versions
-----------------------------

* Evic VTC Mini <=3.03
* Presa TC75W 1.02\*
* iStick Pico 1.01
* Binaries built with `evic-sdk <https://github.com/ReservedField/evic-sdk>`_

\*Flashing Presa firmware to a VTC Mini requires changing the hardware version
on some devices. Backup your data flash before flashing!

Installation
-------------

Install from source:
^^^^^^^^^^^^^^^^^^^^^^

Using ``evic-usb`` requires ``cython-hidapi``. You can install it using  ``pip``:

::

    $ pip install hidapi

Building ``cython-hidapi`` requires libusb headers and cython. On Arch Linux they can be obtained from the repositories by installing packages ``libusb`` and ``cython``. Debian based distributions will have packages ``libusb-1.0-0-dev`` and ``cython``.

On Windows you will also need the correct compiler for your Python version. See `this <https://wiki.python.org/moin/WindowsCompilers>`_
page for more information on setting up the compiler.

|

Building python-evic:

::

    $ git clone git://github.com/Ban3/python-evic.git
    $ cd python-evic
    $ python setup.py install


Allowing non-root access to the device
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The file ``udev/99-nuvoton-hid.rules`` contains an example set of rules for setting the device permissions to ``0666``.  Copy the file to the directory ``/etc/udev/rules.d/`` to use it.

Autosync time when device connected
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The file ``scripts/evic-usb-rtc-sync.service`` + ``udev/99-nuvoton-hid.rules`` is a example of how to auto sync time

Usage
-------
See  ``--help`` for more information on a given command.

evic-convert
^^^^^^^^^^^^
``evic-convert`` is a tool to encrypt/decrypt firmware images:

::

    $ evic-convert in.bin -o out.bin

evic-usb
^^^^^^^^^^^^
``evic-usb`` is a tool for interfacing with the device through USB.


Dump device data flash to a file:

::

    $ evic-usb dump-dataflash -o out.bin

Upload an encrypted firmware image to the device:

::

    $ evic-usb upload firmware.bin

Upload an unencrypted firmware image to the device:

::

    $ evic-usb upload -u firmware.bin

Upload a firmware image using data flash from a file:

::

    $ evic-usb upload -d data.bin firmware.bin

Use  ``--no-verify`` to disable verification for APROM or data flash. To disable both:

::

    $ evic-usb upload --no-verify aprom --no-verify dataflash firmware.bin

Reset the device:

::

    $ evic-usb reset

Dump any part of the flash memory (May not work with all firmwares):

::

    $ evic-usb fmc-read -o out.bin -s startaddr -l length

Example to read the parameters flash memory:

::

    $ evic-usb fmc-read -o out.bin -s 122880 -l 4096

Setup date and time of the device to the current time (For firmwares supporting clock display):

::

    $ evic-usb time

Take a screenshot of the device display (May not work with all firmwares):

::

    $ evic-usb screenshot -o outfile.[png|jpg|...]
