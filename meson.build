#
# This file is part of the flashrom project.
#
# Copyright (C) 2022 Google Inc.
#
# This program is free software; you can redistribute it and/or modify
# it under the terms of the GNU General Public License as published by
# the Free Software Foundation; either version 2 of the License, or
# (at your option) any later version.
#
# This program is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
# GNU General Public License for more details.
#

project('ap_wpsr', 'c')

libsrc = [
  'imports/flashchips.c',
  'imports/writeprotect.c',
  'imports/writeprotect_ranges.c',
]
inc = include_directories(['imports/include', 'shim/include'])

shim = library('shim', 'shim/flashrom_shim.c', include_directories : inc)

ap_wpsrlib = library('ap_wpsr',
                        libsrc,
                        include_directories : inc,
                        link_with : shim,
                        install : true)

executable('ap_wpsr',
  link_with : [shim, ap_wpsrlib],
  include_directories : inc,
  sources : 'main.c',
)
