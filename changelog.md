1.0.3 (2016-08-10)
------------------

- Fix division by zero in DoctrineStatsCollector::getHydrationTimePercent() and getQueriesTimePercent()

1.0.2 (2016-08-08)
------------------

- Add queries time in Symfony WebProfiler
- Add queries time percent and hydration time percent in Symfony WebProfiler

1.0.1 (2016-08-05)
------------------

- Fix DoctrineEventSubscriber::postLoad() call to addManagedEntity(), only managed entities will trigger this call

1.0.0 (2016-07-21)
------------------

- Add steevanb\DoctrineStats\Doctrine\ORM\EntityManager to overload Doctrine\ORM\Proxy\ProxyFactory
- Add steevanb\DoctrineStats\Doctrine\ORM\Proxy\ProxyFactory to add postLazyLoad event
- Add steevanb\DoctrineStats\EventSubscriber\DoctrineEventSubscriber to collect doctrine statistics
- Add ArrayHydrator, ObjectHydrator, ScalarHydrator, SimpleObjectHydrator and SingleScalarHydrator to ComposerOverloadClass, to add preHydration and postHydration events
- Add Symfony2 and Symfony3 bridge with DoctrineStatsBundle
