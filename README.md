[![version](https://img.shields.io/badge/version-1.3.4-green.svg)](https://github.com/huttopia/doctrine-stats/tree/1.3.4)
[![doctrine](https://img.shields.io/badge/doctrine/orm-^2.4.8-blue.svg)](http://www.doctrine-project.org)
[![php](https://img.shields.io/badge/php-^5.4.6%20||%20^7.0-blue.svg)](http://www.php.net)
![Lines](https://img.shields.io/badge/code%20lines-2153-green.svg)
[![SensionLabsInsight](https://img.shields.io/badge/SensionLabsInsight-platinum-brightgreen.svg)](https://insight.sensiolabs.com/projects/884a7b62-bb7a-41dc-8198-6d2bb0694795/analyses/28)

### doctrine-stats

Add important Doctrine statistics :
* count managed entities
* count lazy loaded entities
* hydration time by hydrator and query
* group queries by query string, show differents parameters used by same query string
* count different query string used

[Changelog](changelog.md)

### Installation

```bash
composer require --dev "huttopia/doctrine-stats": "^1.3.4"
```

If you want to add hydration time to your statistics :

```json
# composer.json
{
    "require-dev": {
        "steevanb/composer-overload-class": "^1.1"
    },
    "autoload": {
        "psr-4": {
            "ComposerOverloadClass\\": "var/cache/ComposerOverloadClass"
        }
    },
    "scripts": {
        "pre-autoload-dump": "steevanb\\ComposerOverloadClass\\OverloadClass::overload"
    },
    "extra": {
        "composer-overload-cache-dir": "var/cache",
        "composer-overload-class-dev": {
            "Doctrine\\ORM\\Internal\\Hydration\\ArrayHydrator": {
                "original-file": "vendor/doctrine/orm/lib/Doctrine/ORM/Internal/Hydration/ArrayHydrator.php",
                "overload-file": "vendor/steevanb/doctrine-stats/ComposerOverloadClass/Doctrine/ORM/Internal/ArrayHydrator.php"
            },
            "Doctrine\\ORM\\Internal\\Hydration\\ObjectHydrator": {
                "original-file": "vendor/doctrine/orm/lib/Doctrine/ORM/Internal/Hydration/ObjectHydrator.php",
                "overload-file": "vendor/steevanb/doctrine-stats/ComposerOverloadClass/Doctrine/ORM/Internal/ObjectHydrator.php"
            },
            "Doctrine\\ORM\\Internal\\Hydration\\ScalarHydrator": {
                "original-file": "vendor/doctrine/orm/lib/Doctrine/ORM/Internal/Hydration/ScalarHydrator.php",
                "overload-file": "vendor/steevanb/doctrine-stats/ComposerOverloadClass/Doctrine/ORM/Internal/ScalarHydrator.php"
            },
            "Doctrine\\ORM\\Internal\\Hydration\\SimpleObjectHydrator": {
                "original-file": "vendor/doctrine/orm/lib/Doctrine/ORM/Internal/Hydration/SimpleObjectHydrator.php",
                "overload-file": "vendor/steevanb/doctrine-stats/ComposerOverloadClass/Doctrine/ORM/Internal/SimpleObjectHydrator.php"
            },
            "Doctrine\\ORM\\Internal\\Hydration\\SingleScalarHydrator": {
                "original-file": "vendor/doctrine/orm/lib/Doctrine/ORM/Internal/Hydration/SingleScalarHydrator.php",
                "overload-file": "vendor/steevanb/doctrine-stats/ComposerOverloadClass/Doctrine/ORM/Internal/SingleScalarHydrator.php"
            }
        }
    }
}
```
```bash
composer update huttopia/composer-overload-class
```

### Symfony 2.x, 3.x and 4.x integration

Read Installation paragraph before.

#### Symfony 5.x

```php
### config/bundles.php
return [
    // ...
    \steevanb\DoctrineStats\Bridge\DoctrineStatsBundle\DoctrineStatsBundle::class => ['dev' => true]
];
```

If you want to add lazy loaded entities to your statistics :

```yml
### config/services.yaml
parameters:
    doctrine.orm.entity_manager.class: steevanb\DoctrineStats\Doctrine\ORM\EntityManager
```

### Manual integration

To retrieve statistics, you need to register steevanb\DoctrineStats\EventSubscriber\DoctrineEventSubscriber in your event manager.

If you want to add lazy loaded entities to your statistics, you need to overload default EntityManager, with steevanb\DoctrineStats\Doctrine\ORM\EntityManager.

### Screenshots

![Symfony profiler](symfony_profiler.jpg)

![Symfony profiler panel](symfony_profiler_panel.jpg)
