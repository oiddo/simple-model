Customizing the fields on your model
====================================

Models are used to manage business logic, data and rules of applications.
Data is represented by model classes and its fields. The easiest way to
define fields using simple model is by using `type hints`_ syntax:

.. code-block:: python

    from decimal import Decimal

    from simple_model import Model


    class Category(Model):
        name: str
        is_active: bool = False


    class Product(Model):
        title: str
        description: str
        category: Category
        price: Decimal
        is_active: bool = False


In the example above we create two models ``Category`` with ``name``
and ``is_active`` fields and ``Product`` with ``title``, ``description`` and
other fields.

simple model will automtically create custom initializers (``__init__`` methods
or constructors) that receives all the specified fields as parameters.
To create model instances just do the following:


.. code-block:: python

    category = Category(
        name='clothing',
        is_active=True,
    )
    product = Product(
        title='Pants',
        description='Pants are great',
        category=category,
        price=80,
        is_active=True,
    )


As shown in the models above it is possible to can easily customize field types
by defining the class attributes using `type hints`_. It is also possible to
provide a default value for each field by setting values on each field on the
model class.


**Note:**

    Attributes and methods that starts with "__" (dunder) are considered private
    and not included in model.

    For a better understanding, check this `python underscore convention`_ link.


Defining fields without explicit types
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

If you don't want to enforce types on your fields it is possible to use
``typing.Any`` as  a field type. This way simple model will ignore any type-related
feature on the declared model:

.. code-block:: python

    from typing import Any

    from simple_model import Model


    class Bag(Model):
        name: Any
        brand: Any
        items: Any


Validating data on your model
=============================

TBD

Allowing empty values on field validation
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

TBD


Converting models to dict
=========================

To convert model to dict you should use `to_dict()`

.. code-block:: python

    from simple_model import Model
    from simple_model.converters import to_dict

    class Category(Model):
        name: str
        is_active: bool = False

    category = Category(
        name='clothing',
        is_active=True,
    )

    to_dict(category)


You can convert models instances to dictionary using the method `.as_dict()`, you must run `.validate()` before conversion.
This way is more recommended because you don't need to import `to_dict` to convert the instance

.. code-block:: python

    from simple_model import Model


    class Category(Model):
        name: str
        is_active: bool = False

    category = Category(
        name='clothing',
        is_active=True,
    )

    category.validate()
    category.as_dict()


Creating models instances and classes from dicts
================================================

TBD


Model inheritance
=================

TBD

Field conversion and customizing model initialization
=====================================================

TBD (``__post_init__``)


Building models and model classes dynamically
=============================================

TBD


FAQ
===

TBD


.. _`type hints`: https://www.python.org/dev/peps/pep-0484/#type-definition-syntax
.. _`python underscore convention`: https://dbader.org/blog/meaning-of-underscores-in-python
