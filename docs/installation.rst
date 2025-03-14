.. _installation:

************
Installation
************

This document assumes the developer has a basic understanding of python
packaging, and how to install and manage python on the system executing
Molecule.

Requirements
============

Depending on the driver chosen, you may need to install additional OS packages.
See ``INSTALL.rst``, which is created when initializing a new scenario.

* Python >= 3.6 with :std:doc:`Ansible <ansible:index>` >= 2.8

CentOS 8
--------

.. code-block:: bash

    $ sudo yum install -y gcc python3-pip python3-devel openssl-devel python3-libselinux

Ubuntu 16.x
-----------

.. code-block:: bash

    $ sudo apt-get update
    $ sudo apt-get install -y python3-pip libssl-dev

Pip
===

:std:doc:`pip <pip:usage>` is the only supported installation method.

.. warning::

  Ansible is not listed as a direct dependency of molecule package because
  we only call it as a command line tool. You may want to install it
  using your distribution package installer. If you want to also install a
  compatible  version of ansible, make use of provided ``ansible`` or
  ``ansible-base`` extras:

  .. code-block:: bash

      $ python3 -m pip install "molecule[ansible]"  # or molecule[ansible-base]

Keep in mind that on selinux supporting systems, if you install into a virtual
environment, you may face :gh:`issue <ansible/ansible/issues/34340>` even
if selinux is not enabled or is configured to be permissive.

It is your responsibility to assure that soft dependencies of Ansible are
available on your controller or host machines.

.. warning::

  It is highly recommended that you install molecule in a :std:doc:`virtual
  environment <virtualenv:user_guide>`. This will provide a modern copy of
  `setuptools`_ which is mandatory in order for molecule to be installed
  successfully and function correctly. If you cannot use a virtual environment
  then you can attempt a package upgrade with the following:

  .. code-block:: bash

      $ python3 -m pip install --upgrade --user setuptools

  .. _setuptools: https://pypi.org/project/setuptools/

.. warning::

  Pip v19 series has an :gh:`isolation bug <pypa/pip/issues/6264>` of
  setuptools being exposed to the package build env. That is why it's
  highly recommended to upgrade user setuptools even when using a proper
  virtualenv as shown above.

Requirements
------------

Depending on the driver chosen, you may need to install additional python
packages.  See the driver's documentation or ``INSTALL.rst``, which is created
when initializing a new scenario.

Install
-------

Install Molecule:

.. code-block:: bash

    $ python3 -m pip install --user "molecule[lint]"

Molecule uses the "delegated" driver by default. Other drivers can
be installed seperately from PyPI, such as the molecule-docker driver.
If you would like to use docker as the molecule driver, the installation
command would look like this:

.. code-block:: bash

    $ python3 -m pip install --user "molecule[docker,lint]"

Other drivers, such as ``molecule-podman``, ``molecule-vagrant``,
``molecule-azure`` or ``molecule-hetzner`` are also available.

Installing molecule package also installed its main script ``molecule``,
usually in ``PATH``. Users should know that molecule can also be called as a
python module, using ``python -m molecule ...``. This alternative method has
some benefits:

* allows to explicitly control which python interpreter is used by molecule
* allows molecule installation at user level without even needing to have
  the script in ``PATH``.

.. note::

    We also have a continuous pre-release process which is provided for early
    adoption and feedback purposes only. It is available from
    `test.pypi.org/project/molecule`_ and can be installed like so:

    .. code-block:: bash

        python3 -m pip install \
          --index-url https://test.pypi.org/simple \
          --extra-index-url https://pypi.org/simple \
          molecule==2.21.dev46

    Where ``2.21.dev46`` is the latest available pre-release version.
    Please check the `release history`_ listing for the available releases.

    .. _test.pypi.org/project/molecule: https://test.pypi.org/project/molecule/
    .. _release history: https://test.pypi.org/project/molecule/#history

Docker
======

Molecule is built into a Docker image by the `Toolset`_ project.

Any questions or bugs related to use of Molecule from within a container
should be addressed by the Toolset project.

.. _`Toolset`: https://github.com/ansible-community/toolset

Source
======

Due to the rapid pace of development on this tool, you might want to
install and update a bleeding-edge version of Molecule from Git.

Follow the instructions below to do the initial install and subsequent
updates.

The package distribution that you'll get installed will be autogenerated
and will contain a commit hash information making it easier to refer to
certain unstable version should the need to send a bug report arise.

.. warning::

  Please avoid using ``--editable``/``-e`` `development mode`_ when
  installing Molecule with Pip. This not very well supported and only
  needed when doing development.
  For contributing purposes, you can rely on the tox command line
  interface. Please see :ref:`our testing guide <Testing>` for further
  details.

  .. _`development mode`:
     https://setuptools.readthedocs.io/en/latest\
     /setuptools.html#development-mode

Requirements
------------

CentOS 8
^^^^^^^^

.. code-block:: bash

    $ sudo yum install -y libffi-devel git

Ubuntu 16.x
^^^^^^^^^^^

.. code-block:: bash

    $ sudo apt-get install -y libffi-dev git

Install
-------

.. code-block:: bash

    $ python3 -m pip install -U git+https://github.com/ansible-community/molecule
