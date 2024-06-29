# Image Optimizer AMQP - a Magento 2 amqp configuration for image optimizations

This module provides a queue configuration for asynchronous image conversions in Magento 2. It is based on the [brocode/module-image-optimizer](https://github.com/brosenberger/module-image-optimizer) and [brocode/module-image-optimizer-queue](https://github.com/brosenberger/module-image-optimizer)

**Goals of this module:**
* Use of Magento 2 RabbitMQ framework and reuse the queue implemention of the base module.

[!["Buy Me A Coffee"](https://www.buymeacoffee.com/assets/img/custom_images/orange_img.png)](https://www.buymeacoffee.com/brosenberger)

## Installation

```
composer require brocode/module-image-optimizer-amqp
bin/magento module:enable BroCode_ImageAmqpOptimizer
bin/magento setup:upgrade
```

## Configuration

Basically nothing has to be configured and should run out of the box if RabbitMQ is already up and running.

Any image needed to be converted is scanned with a cron job from the base module and published to the configured queue instead of a direct conversion.

To consume any conversion event published, you can manually start the queue consumer via the Magento CLI:

```
bin/magento queue:consumers:start BroCodeImageConversionConsumer
```

Consider using supervisor or any other process manager to keep the consumer running.
