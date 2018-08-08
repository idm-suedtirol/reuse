# Flight rules for REUSE

#### What are "flight rules"?

A [guide for astronauts](https://www.jsc.nasa.gov/news/columbia/fr_generic.pdf) (now, programmers making software
compliant to the [REUSE Initiative](https://reuse.software/)) about what to do when things go wrong, _or must be
executed with no delay_.

> *Flight Rules* are the hard-earned body of knowledge recorded in manuals that list, step-by-step, what to do if X
> occurs, and why. Essentially, they are extremely detailed, scenario-specific standard operating procedures. [...]

> NASA has been capturing our missteps, disasters and solutions since the early 1960s, when Mercury-era ground teams
> first started gathering "lessons learned" into a compendium that now lists thousands of problematic situations, from
> engine failure to busted hatch handles to computer glitches, and their solutions.

&mdash; Chris Hadfield, *An Astronaut's Guide to Life*.

_ps. Idea taken from the [GIT flight rules](https://github.com/k88hudson/git-flight-rules) project._

----

#### Table of Contents
<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->


- [Licensing](#licensing)
  - [I want to check if my project is REUSE compliant](#i-want-to-check-if-my-project-is-reuse-compliant)
  - [I want to make my GPL-3 project REUSE compliant](#i-want-to-make-my-gpl-3-project-reuse-compliant)
  - [I want to make my multi-license project REUSE compliant](#i-want-to-make-my-multi-license-project-reuse-compliant)
  - [I want to add a comment header to each file](#i-want-to-add-a-comment-header-to-each-file)
  - [I want to define a pattern to associate various files to a license](#i-want-to-define-a-pattern-to-associate-various-files-to-a-license)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

----

## Licensing

### I want to check if my project is REUSE compliant

We use a tool called [reuse](https://reuse.gitlab.io) to see, if the project `my-example` follows the
REUSE recommendations. First, we install it and then we execute it, to see
which files are not compliant to the [REUSE Initiative](https://reuse.software/).

    apt install python3-pygit2
    pip3 install --user fsfe-reuse
    cd my-example
    reuse lint

The result shows a list of files, that do not have licenses associated.

### I want to make my GPL-3 project REUSE compliant

Download the GPL-3 license from https://github.com/spdx/license-list to your project's
source code. Then, add the valid [SPDX license identifier](https://spdx.org/licenses/).

    wget https://raw.githubusercontent.com/spdx/license-list/master/GPL-3.0.txt -O LICENSE
    sed -i "1iValid-License-Identifier: GPL-3.0" LICENSE

From here, you have three possibilities to continue:

  1) [Add a comment header to each file](#i-want-to-add-a-comment-header-to-each-file)
  2) Use a `debian/copyright` file to [associate a license to various files](#i-want-to-define-a-pattern-to-associate-various-files-to-a-license)
  3) Use a combination of both (1) and (2)

In-depth information can be found within the *reuse* [documentation](https://reuse.gitlab.io/) or
[practices](https://reuse.software/practices/2.0/).

### I want to make my multi-license project REUSE compliant

If you have more than one license, create a LICENSES folder and put your license texts there.

    mkdir LICENSES
    wget https://raw.githubusercontent.com/spdx/license-list/master/GPL-3.0.txt -O LICENSES/GPL-3.0.txt
    wget https://raw.githubusercontent.com/spdx/license-list/master/CC-BY-SA-4.0.txt -O LICENSES/CC-BY-SA-4.0.txt

The SPDX identifier is already encoded within the license file name, hence we do not need to add it
to the head of the file itself.

From here, you have three possibilities to continue:

  1) [Add a comment header to each file](#i-want-to-add-a-comment-header-to-each-file)
  2) Use a `debian/copyright` file to [associate a license to various files](#i-want-to-define-a-pattern-to-associate-various-files-to-a-license)
  3) Use a combination of both (1) and (2)

In-depth information can be found within the *reuse* [documentation](https://reuse.gitlab.io/) or
[practices](https://reuse.software/practices/2.0/).

### I want to add a comment header to each file

Add the following lines as comment to each source code file:

    Copyright (C) 2015-2017 Mary Thomas (mary@example.com)
    Copyright (C) 2018 IDM Südtirol - Alto Adige (info@idm-suedtirol.com)

    SPDX-License-Identifier: GPL-3.0

If you use a version control system, like git, you can also use that history to declare copyright
holders, by simply adding a header like this:

    This file is part of the Open Data Hub project. It's copyrighted by
    the contributors recorded in the version control history of the file,
    available from its original location http://git.example.com/odh/filename.c

    SPDX-License-Identifier: GPL-3.0

Optionally, you can also add additional license information, like title, short description, and
warranty information, as follows:

    Open Data Hub - Data Writer for the Open Data Hub

    This program is free software: you can redistribute it and/or modify
    it under the terms of the GNU General Public License as published by
    the Free Software Foundation, either version 3 of the License, or
    (at your option) any later version.

    This program is distributed in the hope that it will be useful,
    but WITHOUT ANY WARRANTY; without even the implied warranty of
    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
    GNU General Public License for more details.

    You should have received a copy of the GNU General Public License
    along with this program (see LICENSE). If not, see
    <http://www.gnu.org/licenses/>.


NB: Do not forget the SPDX identifier at the end. Add multiple `Copyright` lines, if you
have more than one copyright holder over several years.


### I want to define a pattern to associate various files to a license

For this you can use `debian/copyright` files, also if you are not writing software for the Debian
project explicitely.

    mkdir debian
    vim debian/copyright

An example could be as follows:

    Format: https://www.debian.org/doc/packaging-manuals/copyright-format/1.0/
    Upstream-Name: idm-suedtirol/bdp-core
    Upstream-Contact: Open Data Hub Team <info@opendatahub.bz.it>
    Source: https://github.com/idm-suedtirol/bdp-core

    Files: *
    Copyright: 2000-2017 John Doe <jdoe@example.com>
               2018 IDM Südtirol - Alto Adige (info@idm-suedtirol.com)
    License: GPL-2.0-only

    Files: *.md
    Copyright: 2018 IDM Südtirol - Alto Adige (info@idm-suedtirol.com)
    License: CC-BY-SA-4.0

    Files: *.sh
    Copyright: 2018 IDM Südtirol - Alto Adige (info@idm-suedtirol.com)
    License: GPL-3.0-or-later

This means, that per default files are licensed under `GPL-2.0-only`, except for files
ending in `.md`, which are licensed with `CC-BY-SA-4.0`, and all ending with `.sh` as
`GPL-3.0-or-later`. For details on how to write a `debian/copyright` file, see the
[packaging manual](https://www.debian.org/doc/packaging-manuals/copyright-format/1.0/).

