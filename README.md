Fedora COPR Package Scripts
===============================================================================
https://github.com/pcmoore/copr-pkg_scripts

These scripts help generate patches and SRPMs for use with Fedora's COPR build
system.  At the moment the scripts require customization for each package/COPR
and are only moderately documented; knowledge of git, bash scripting, and the
Fedora COPR build system is likely required to make use of these scripts.
Future releases of these scripts will improve both on the documentation and the
usability of the scripts.

## Setup

Create a Fedora/COPR account if you don't already have one using the URL below:

* https://admin.fedoraproject.org/accounts/user/new

Download the COPR tools on your system:

	dnf install copr-cli

Create a copr-cli access token and place it in ~/.config/copr:

	https://copr.fedorainfracloud.org/api

Clone the GitHub repository into its own directory:

	git clone https://github.com/pcmoore/copr-pkg_scripts.git

Create a new directory, link the scripts, and copy the configuration file:

	mkdir copr-project
	cd copr-project
	ln -s ../copr-pkg_scripts/pcopr_patch .
	ln -s ../copr-pkg_scripts/pcopr_srpm-kernel_fedora .
	cp ../copr-pkg_scripts/pcopr.config .

Clone the upstream project into the new directory and add any remote
repositories that you may need:

	cd copr-project
	git clone <project URL>

Clone the Fedora package repository:

	cd copr-project
	fedpkg clone <package>

Edit the pcopr.config file you copied earlier, all of the configuration options
are documented in the example file:

	cd copr-project
	$EDITOR pcopr.config

## Usage

The usage shown below is for a basic use case that creates a set of patches
from the upstream development repository, applies them to the Fedora package,
and automatically starts a COPR build with the new package.  There are several
additional uses available via command line switches to the scripts used below,
please consult the scripts, and use the '-h' option, for more information.

Generate the patches to be applied to the Fedora package:

	cd copr-project
	./pcopr_patch

Generate a patched Fedora SRPM and submit it to COPR for building:

	cd copr-project
	./pcopr_srpm-kernel_fedora -b

## Reporting Issues and Contributing

Issues can be reported via the GitHub issue tracker and patches can be
submitted as GitHub pull requests.
