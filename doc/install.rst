Installation
============

Use Python 3.4 or newer
-----------------------

tracemalloc is now part of Python 3.4 standard library! Nothing to do, enjoy!

.. note::
   Installing pytracemalloc on Python older than 3.4 is much more complex, it
   requires to recompile a patched version of Python. It is worth to try to run
   your application on Python 3.4 rather than trying to compile and install
   manually pytracemalloc on older versions of Python.


Linux packages
--------------

Ubuntu packages for pytracemalloc 1.2: `pytracemalloc 1.0 PPA
<https://launchpad.net/~ionel-mc/+archive/pytracemalloc-1.0>`_ by Ionel
Cristian Maries.


Manual installation
-------------------

First, create the directory ``/opt/tracemalloc``. Example::

    sudo mkdir /opt/tracemalloc
    sudo chown $USER: /opt/tracemalloc

Go into the `/opt/tracemalloc` directory. Then follow these commands to compile a patched Python and install pytracemalloc::

    wget http://www.python.org/ftp/python/2.7.15/Python-2.7.15.tgz
    wget https://pypi.org/packages/source/p/pytracemalloc/pytracemalloc-1.4.tar.gz
    tar -xf Python-2.7.15.tgz
    tar -xf pytracemalloc-1.4.tar.gz
    cd Python-2.7.15
    patch -p1 < ../pytracemalloc-1.4/patches/2.7.15/pep445.patch
    ./configure --enable-unicode=ucs4 --prefix=/opt/tracemalloc/py27
    make
    make install
    cd ../pytracemalloc-1.4
    /opt/tracemalloc/py27/bin/python2.7 setup.py install

You may also run unit tests::

    /opt/tracemalloc/py27/bin/python2.7 test_tracemalloc.py -v

You have now a patched Python 2.7 installed in
``/opt/tracemalloc/py27/bin/python2.7`` with the ``tracemalloc`` module
installed, congrats!

To use modules installed for the system Python, directories of ``sys.path``
should be copied from the system Python to the patched Python. Example of
command to generate an environment variable to use system modules::

    python -c 'import sys; print("PYTHONPATH=%s" % ":".join(filter(bool, sys.path)))'


Patch Python
------------

To install pytracemalloc, you need a modified Python runtime:

* Download Python source code (tarball)
* Uncompress the tarball and enter the newly created directory (ex: Python-2.7.8)
* Apply the patch of your Python version, example::

    patch -p1 < ~/pytracemalloc-1.0/patches/2.7/pep445.patch

* Compile and install Python::

    ./configure --enable-unicode=ucs4 --prefix=/opt/python && make && sudo make install

.. note::

   ``--enable-unicode=ucs4`` uses the wide mode: store Unicode code points in
   32-bit (4 bytes per character). It is the mode used by all Linux
   distributions. Your modified Python will have the same ABI and so you should
   be able to use extension modules of the system.

   ``--enable-unicode=ucs4`` is no more needed with Python 3.3 which always
   uses compact strings: see the PEP 393.

.. note::

   Currently, only patches for Python 2.7 and 3.3 are provided. If you need
   patches for other Python versions, please ask. The code should work on
   Python 2.5-3.3.


Compile and install pytracemalloc
---------------------------------

Dependencies:

* `Python <http://www.python.org>`_ 2.5 - 3.3

`Download pytracemalloc from the Python Cheeseshop (PyPI)
<https://pypi.python.org/pypi/pytracemalloc>`_.

Install pytracemalloc::

    /opt/python/bin/python setup.py install

