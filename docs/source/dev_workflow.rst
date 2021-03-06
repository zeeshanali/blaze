==================
Developer Workflow 
==================

Blaze is being developed as an open source project by
`Continuum Analytics`_. This page describes the basic workflow
that development follows, and may be used as a guide for how
to contribute to the project.

.. _Continuum Analytics: http://continuum.io/

For any questions about Blaze and how to get involved, please
email blaze-dev@continuum.io.

GitHub Flow
~~~~~~~~~~~

Source code and issue management are hosted in `this github page`_,
and usage of git roughly follows `GitHub Flow`_. What this means
is that the `master` branch is generally expected to be stable,
with tests passing on all platforms, and features are developed in
descriptively named feature branches and merged via github's
Pull Requests.

.. _this github page: https://github.com/ContinuumIO/blaze
.. _GitHub Flow: http://scottchacon.com/2011/08/31/github-flow.html

The only cases where it's ok to push directly to master are
really minor fixes, or to fix tests that are failing.

Unified Python 2 and 3 Codebase
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Blaze is being developed with one codebase that simultaneously
supports both Python 2 and Python 3. To make this manageable,
just Python 2.6, 2.7, and >= 3.3 are being supported.

To support this, all .py files must begin with a few `__future__`
imports, as follows.::

    from __future__ import absolute_import, division, print_function

Additionally, there is a helper submodule `blaze.py2help` including
a number of utilities to smooth the differences between Python versions.
Please browse the source file to see what is there, and read the
documentation for the `six library`_ for details on this style of
unified codebase.

.. _six library: http://pythonhosted.org/six/

Testing
~~~~~~~

In order to keep the `master` branch functioning with passing tests,
there are two automated testing mechanisms being used. First is
`Travis CI`_, which is configured to automatically build any pull
requests that are made. This provides a smoke test against both
Python 2 and Python 3 before a merge.

.. _Travis CI: https://travis-ci.org/

The Travis tests only run on Linux, but Blaze is supported on Linux,
OS X, and Windows. Internal to Continuum, a `Jenkins`_ server is
running which builds and tests Blaze on 15 different configurations,
versions 2.6, 2.7, and 3.3 for different 32-bit and 64-bit versions
of Linux, OS X, and Windows. That these configurations are all working
should be verified by someone at Continuum after each merge of a
pull request.

Dependencies
~~~~~~~~~~~~

Blaze has a large number of dependencies, some of which are developed
in concert with the blaze repo. For `datashape`, `pykit`, and `dynd-python`,
it is generally expected that the current master branch of all of them
should work together. When a release is made, particular versions of
all the dependencies are fixed.

In the case of `dynd-python`_, its Jenkins build additionally uploads
a conda package to the development channel of `Anaconda`_. As the
`binstar`_ infrastructure gets built out, we expect to transition this
to a repository there which would have daily builds of all these
dependencies and of blaze itself.

.. _dynd-python: https://github.com/ContinuumIO/dynd-python
.. _Anaconda: http://continuum.io/downloads
.. _binstar: https://binstar.org/

