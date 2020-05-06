Version Control
----------------
Every project at The Gang requires multiple team members to collaborate.  Therefore, we must create a good procedure for working together effortlessly.

.. toctree::
   :maxdepth: 2

Basics
~~~~~~

It is best to understand the underlying working of git. Watch `this <https://www.youtube.com/watch?v=2sjqTHE0zok>`_. Do not think of git as a set of magical command.
It will come back and bite you later.

Main Branches
~~~~~~~~~~~~~
Every project at The Gang will have the following branches

master
  Production-ready code. The branch will be used for user acceptance testing.

.. _dev:

dev
  The main development branch where everyone will be branching from

release/{semver_versioning_number}
  Production-ready code on branch with `semver <https://semver.org/>`_ versioning. Thus, allow easy analysis of production code and revert if needed.

Branching Strategy
~~~~~~~~~~~~~~~~~~
The developer shall create a new branch each time he/she will develop a story or task. The newly created branch shall be created from the :ref:`dev<dev>` branch.

The branch name shall follow the following rule:
:: 
    {creator_nickname}/{feature/fix/test}/{short-description}

For example:
::
    o/feature/create-user-profile

**Branches are intended to be short-lived.** The ability to frequently merge code is critical to avoiding costly merge conflict. 


Merging Strategy
~~~~~~~~~~~~~~~~
The developer shall create a Pull/Merge request to the :ref:`dev<dev>`. branch. The branch shall be deleted once the merge request has been approved. The developer must also assign the merge request responsibility to the person who received `Code Review`_ responsibility for that particular project.

The person who was assigned as a code reviewer for a particular project shall regularly check for merge requests. 

Code Review
~~~~~~~~~~~
Every project will consist of at least one code reviewer. His/her task is to review the merge request and make sure that the developer follows the standard set by The Gang.