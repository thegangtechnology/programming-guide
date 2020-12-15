Data Analysis
-------------

.. contents:: :local:


.. toctree::
   :maxdepth: 2


Getting Started
~~~~~~~~~~~~~~~

Watch these to learn how to collaborate with web developer and communicate with web developer team.
   
   - `Making Python Package <https://youtu.be/X0fAKxrMmDs>`_.
   - `pip install from git <https://youtu.be/DjTsVN0hgAg>`_.

The final product for our data scientist team should be in the form
of pip installable package. The easiest way to do that is to use our
cookie cutter template. `https://github.com/thegangtechnology/python-lib-template <https://github.com/thegangtechnology/python-lib-template>`_.
as shown in the two videos above.


Make Separate Folder for Each Member
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Having jupyter notebook conflict is the last thing you want see when you do git push.
To avoid that make separate notebook folder for each user.

::

    |-notebook
    | |-piti_notebook
    | |-sam_notebook
    |-src
      |-mathy_lib


Put your shared code in library
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

It's ok to try out ideas in the notebook. But this typically leads to an extremely
long notebook. It is recommended that once the code is solid. You should move the
code to inside the package then call the function from the package instead.

Watch `Making Package <https://youtu.be/X0fAKxrMmDs>`_. for how to do that.
