A module that makes GstBase.BaseTransform python-compatible
===========================================================

.. image:: https://travis-ci.org/Muges/gstbasetransform.svg?branch=master
    :target: https://travis-ci.org/Muges/gstbasetransform
    :alt: Build Status

``gstbasetransform`` is a module that aims to provide a patched
``GstBase.BaseTransform`` class usable from python.

Source code repository and issue tracker:
   https://github.com/Muges/gstbasetransform/

Python Package Index:
    https://pypi.python.org/pypi/gstbasetransform/

License:
   LGPL 2.1 -- see the file ``LICENSE`` for details.

Installation
------------

``gstbasetransform`` should work with python 2.7 and python 3.4+.

You will first need to install PyGObject_ and python-gst_, as they are not
available on pip. You can then install the latest version of
``gstbasetransform`` with pip::

    pip install gstbasetransform

.. _PyGObject:
    https://pygobject.readthedocs.io/en/latest/getting_started.html

.. _python-gst:
    https://gstreamer.freedesktop.org/modules/gst-python.html

Usage
-----

gstbasetransform provides a subclass of GstBase.BaseTransform_, also called
``BaseTransform``, whose ``do_transform_size`` virtual method has been patched
to be usable in python.

In the original do_transform_size_ virtual method, the ``othersize`` parameter
that represents the size of the output buffer is an ``int``, and is passed by
copy, preventing it from being changed. In ``gstbasetransform.BaseTransform``,
it has been removed, and the size of the output buffer can be set with a return
value of the method.

The signature of the method is::

    do_transform_size(direction, caps, size, othercaps)

and it should return a tuple ``(bool, int)``, where the ``int`` is the size of
the output buffer.

See the ``test_gstbasetransform.py`` file for a basic example.

.. _GstBase.BaseTransform:
    https://lazka.github.io/pgi-docs/index.html#GstBase-1.0/classes/BaseTransform.html#GstBase.BaseTransform

.. _do_transform_size:
    https://lazka.github.io/pgi-docs/index.html#GstBase-1.0/classes/BaseTransform.html#GstBase.BaseTransform.do_transform_size

Credits
-------

Thanks to Dustin Spicuzza for writing pygi-treeview-dnd_, which served as a
base for writing ``gstbasetransform``.

.. _pygi-treeview-dnd:
    https://github.com/virtuald/pygi-treeview-dnd
