Python Guideline
----------------

We follow loosely 
`Google Python Style Guide`_
and
`PEP-8`_. 
If you are new at The Gang, we recommend that you read the `Google Python Style Guide`_ first.
Please refer to the two guidelines for anything not explicitly stated below.

.. contents:: :local:


.. toctree::
   :maxdepth: 2


Linting
~~~~~~~

You must lint your code before committing to the repository. You are going to miss a space or two. 
So, get your editor or linter to do it. For example, in pycharm, the shortcut is ``Command+Alt+L`` or ``Ctrl+Alt+L``.
For jupyter notebook, install `notebook extensions`_ and enable autopep8. Then click the gear icon on your toolbar to format.


**Bad**

.. code-block:: python

    a=a+ b

**Good**

.. code-block:: python

    a = a + b # linting will do this for you


Typing Annotation
~~~~~~~~~~~~~~~~~

It is highly recommend that you document the type of arguments using `mypy`_. This will make your autocomplete life much better.
PyCharm will recognize the typing system and will 

The point here is to help you with auto completion. There is really no need to run mypy type check since the checker is not very good
with contravariant and such.

**Bad**

.. code-block:: python

    def add_number_to_list(lst, number):
        return [x + number for x in lst]

**Good**

.. code-block:: python

    def add_number_to_list(lst: List[float], number: float) -> List[float]:
        return [x + number for x in lst]


Write Test
~~~~~~~~~

At The Gang, the code base for each project tends to be quite big with interworking pieces. Changing one file may affect other people's work.
To make everyone life easier, it is essential to write unit test at least to make sure that it doesn't crash. The recommended tool is `pytest`_. 
Readup how to use it. Or ask your project advisor how to do it.



DocString
~~~~~~~~~

Please use `Google Style Doc String`_. See an example below. Much more readable than RST style. To have pycharm do this automatically
search for ``google`` in pycharm setting, in the python integrated tool change docstring format from rst to Google.


.. code-block:: python
    
    def add_number_to_list(lst: List[float], number: float) -> List[float]:
        """Add number to list
            Args:
                lst (List[float]): list of numbers to be added.
                number (float): number to add.
            
            Returns:
                List[float]. List of added numbers.
        """
        return [x + number for x in lst]


Return Object Instead of Long Tuple
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Being able to return multiple objects and use tuple expansion is great but once you return more than 2 objects you will start questioning yourself
which order you need it tobe. So instead of return a long tuple, return an object instead. We could live with 1 or 2 objects but 3 and more is a No No.

**Bad**

.. code-block:: python

    def summarize(arr: np.ndarray) -> Tuple[float, float, int]:
        return np.average(arr), np.std(arr), len(arr)


**Good**

.. code-block:: python
    
    @dataclass
    class SummarizeResult:
        mean: float
        std: float
        size: int

        def __iter__(self): # Optional just in case you still want to do tuple expansion
            yield mean
            yield std
            yield size

    def summarize(arr: np.ndarray) -> SummarizeResult:
        return SummarizeResult(
            mean = np.average(arr),
            std = np.std(arr),
            size = len(arr)
        )


Use Named Parameter
~~~~~~~~~~~~~~~~~~~

If you need to call a function with a long list of parameters. DO NOT rely on the ordering, someone may change it.
Also it's so hard to figure out which parameter is which. 
Instead, call it with named parameters. For example,

.. code-block:: python
    
    def make_tea(tea_type: str, boba_type: str, boba_number: int, sugar_amount: float) -> Tea:
        pass


**Bad**

.. code-block:: python
    
    make_tea('green', 'coffee', 30, 2.5)


**Good**

.. code-block:: python

    make_tea(tea_type='green',
             boba_type='coffee",
             boba_number=10,
             sugar_amount=3.0)


Class Constructor
~~~~~~~~~~~~~~~~~

It is recommended that you use `dataclass`_ if possible. If you need to use the old style class with :code:`__init__` then
your main constructor must be dumb that means all it does is copy the arguments to :code:`self.xxx`. Then, complicated 
constructor which requires logic should be in an alternative constructor class method. This allows your code to be testable without much 
dependency on other objects.


**Bad, but Tempting**

.. code-block:: python
    
    class MetaData:
        def __init__(self, file: FileObject):
            self.size = file.size
            self.is_file = os.is_file(file) 


**Good**

.. code-block:: python
    
    class MetaData
        def __init__(self, size: int, is_file: bool):
            self.size = size
            self.is_file = is_file

        @classmethod
        def from_file(cls, file: FileObject) -> 'MetaData': 
            # the single quote in the return type is for forward referencing
            return MetaData(size=size, is_file=os.is_file(file))


**Better**

.. code-block:: python

    @dataclass
    class MetaData:
        size: int
        is_file: bool

        @classmethod
        def from_file(cls, file: FileObject) -> 'MetaData':
            return MetaData(size=size, is_file=os.is_file(file))


Variable Naming
~~~~~~~~~~~~~~~

- Use plural for list. Ex: Do use :code:`indices = [1,2,3]` instead of :code:`index = [1,2,3]`.
- DO NOT use camel case for vairable name. Ex: Do use :code:`snake_case` instead of :code:`camelCase`.
- Name the function it so that user know at first glance what it does without having to read doc. 
  Ex: Do use :code:`find_largest_number_less_than(lst, threshold)` instead of :code:`find_number(list, threshold)`

.. _Google Python Style Guide: https://google.github.io/styleguide/pyguide.html
.. _Google Style Doc String: https://sphinxcontrib-napoleon.readthedocs.io/en/latest/example_google.html
.. _PEP-8: https://www.python.org/dev/peps/pep-0008/
.. _dataclass: https://docs.python.org/3/library/dataclasses.html
.. _mypy: https://mypy.readthedocs.io/en/stable/
.. _notebook extensions: https://github.com/ipython-contrib/jupyter_contrib_nbextensions
.. _pytest: https://docs.pytest.org/en/latest/