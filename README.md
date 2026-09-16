MaanyaOS README
===============

MaanyaOS is a Privacy-First AI Operating System built on a Zero Trust
Architecture, providing a 10-level multi-layer defense system spanning
pre-boot, core protection, and runtime security. MaanyaOS performs the
required UEFI-level hardware initialization and security bootstrapping
to configure the system, then passes control to the next stage of the
boot chain, referred to in MaanyaOS as the payload. Most often, the
primary function of the payload is to boot the operating system layer
and hand off to MaanyaOS's runtime protections.

With the separation of secure hardware initialization and later boot
logic, MaanyaOS is suited to a wide variety of situations. It can be
used for privacy-hardened devices, running trusted operating systems
from flash, loading custom secure bootloaders, or implementing
firmware-level security standards on top of UEFI. This flexibility
allows MaanyaOS systems to include only the protections necessary for
the target deployment, reducing the attack surface and flash space
required.


Source Code
-----------

Source code for MaanyaOS is maintained by the MaanyaOS / NavDrishti
project team.

Development is currently carried out by the Zeus Coders team
(Bhavya Raj Rathi and Kriday Ghosh), with builds and testing performed
inside Oracle VirtualBox during active development.


Payloads
--------

After the basic UEFI initialization and Zero Trust checks have been
performed, any desired "payload" can be started by MaanyaOS — including
a hardened OS runtime, a recovery environment, or a custom secure
bootloader.


Supported Hardware
------------------

MaanyaOS targets UEFI-based systems and is being developed and tested
primarily on virtualized hardware (Oracle VirtualBox) during this
phase of the project, with future hardware-specific support to be
documented as the project matures.


Releases
--------

MaanyaOS does not yet follow a fixed release cadence. Snapshots have
been produced for project milestones, including submission as the
NavDrishti / MaanyaOS Scientific Edition to the Bharatiya Antariksh
Hackathon 2026 (ISRO-themed), and as the winning submission at
DevGathering 2k26.

Please note that early MaanyaOS builds are best considered development
snapshots and do not currently guarantee any sort of extra stability.


Build Requirements and Building MaanyaOS
-----------------------------------------

Building MaanyaOS currently requires a UEFI-capable virtual machine or
compatible hardware, along with the standard toolchain used for UEFI
firmware and OS-layer development. As the project matures, a full list
of build requirements and step-by-step setup instructions will be
published alongside the source.


Copyrights and Licenses
------------------------

### Uncopyrightable files

Consistent with general copyright principles, files in the MaanyaOS
tree that lack the "modicum of creativity" required for copyright
protection — such as empty placeholder files, machine-generated
configuration files, or files containing only version numbers, dates,
or hash values — are treated as public domain and excluded from
MaanyaOS's general license, even where they may be included in a final
build.

### Copyrights

Copyright on MaanyaOS is held by its contributors, currently the Zeus
Coders team (Bhavya Raj Rathi and Kriday Ghosh).

### Licenses

MaanyaOS is licensed under the GNU General Public License (GPL)
Version 2, in keeping with the broader open-firmware ecosystem it
builds upon. Individual files may be licensed under other
GPLv2-compatible licenses where noted. All source files should carry
an SPDX license identifier at the top for clarification.


Credits
-------

The structure and licensing approach of this README were adapted from
the [coreboot](https://www.coreboot.org) project
(<https://review.coreboot.org/coreboot.git>), a Free Software project
for replacing proprietary BIOS/UEFI firmware. MaanyaOS gratefully
acknowledges coreboot and its community for the open-firmware
groundwork and documentation conventions this project draws on.
