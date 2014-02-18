Alice Context
=============
This context use the [nelmio/alice](https://github.com/nelmio/alice) fixture loading system.

>**Warning** : Alice context is compatible with Alice since **[this commit](https://github.com/nelmio/alice/commit/ae478b9f8abe587c30454b8ad93505642f93a42e)**. For the moment, you have to follow dev-master branch of nelmio/alice.


Configuration
-------------
Edit behat.yml
```yaml
default:
    # ...
    suites:
        default:
            # ...
        contexts:
            - # ...
            - Knp\FriendlyContexts\Context\AliceContext
    extensions:
        # ...
        Knp\FriendlyContexts\Extension:
            alice:
                fixtures:
                    User: path/to/my/user/fixtures.yml
                    Product: path/to/my/product/fixtures.yml
```

Usage
-----
Load a file

```gherkin
@alice(User) @alice(Product)
Feature: My feature
    The feature description
    ...
```

Load all files 

```gherkin
@alice(*)
Feature: My feature
    The feature description
    ...
```

Entity Context
--------------

All imported fixtures can be re-used in the [Entity Context](context-entity.md) for object reference.
```yaml
# user.yml
App\Entity\User:
    user-john:
        firstname: John
        lastname: Doe
    user-admin:
        firstname: Admin
        lastname: Admin
```

```gherkin
@alice(User)
Feature: My feature
    The feature description
    
    Background:
        Given the following products
            | name  | user  |
            | Ball  | John  |
            | Shoes | Admin |
            
    ...
```

Information
-----------

Files will be loaded following the order of files declaration in your behat.yml file. Tag order have no impact.