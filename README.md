
ap_wpsr tool
============

The ap_wpsr tool was built to address specific requirements of AP RO verification
that intends to measure SR contents for invariance after signature validation.

The tool leverages the flashrom SPI flash chips database to produce theoretical
mask,value pairs for a given WP configuration (i.e. protection range start and
length) and flash chip part name.

limitations
-----------

There are however some limitations. While the tool is pure logic (no side-effects) and
intended to calculate values with reasonable fidelity there could however be inaccuracies.

These inaccuracies can be the result of any combination of the following factors:

 * Incorrect writeprotoct SR topology data within the database.
 * Duplicate chips or otherwise ambiguous chip identifiers (id or string name).
 * OTP fused values within the SPI flash chip itself.

A precise flash chip name is required to be cited physically on what chip is being worked
with (and not via probing or other inferences). This precise name needs to be mapped to
the corresponding name within the database to produce the tool output products. The
output products *must* be cross-validated with the datasheet to ensure the products are
consistent with expectations and any errors in the database are corrected with a patch
back to the canonical flashrom flashchips database upstream.

usage
-----

An example usage could be `./ap_ro_pcr -n "W25Q128.V" -s 0x40000 -l 0xFC0000`.

src structure
-------------

There are two key parts to the tool `imports/` and `shim/`. The `shim/` directory just
contains enough symbols to allow linking of the `imports/` source taken from upstream
flashrom. The `imports/` contains two key ingredients - the chip database and the
writeprotection calculation code. These should be kept up to date by importing fresh
copies from flashrom.
