# Image Optimizer AMQP - a Magento 2 amqp configuration for image optimizations

> 📖 **Full docs, design notes & production guidance:**
> [brocode.at/modules/module-image-optimizer](https://brocode.at/modules/module-image-optimizer/)
> Part of the BroCode Image Optimizer family for Magento 2.

This module provides a queue configuration for asynchronous image conversions in Magento 2. It is based on the [brocode/module-image-optimizer](https://github.com/brosenberger/module-image-optimizer) and [brocode/module-image-optimizer-queue](https://github.com/brosenberger/module-image-optimizer)

**Goals of this module:**
* Use of Magento 2 RabbitMQ framework and reuse the queue implemention of the base module.

[!["Buy Me A Coffee"](https://www.buymeacoffee.com/assets/img/custom_images/orange_img.png)](https://www.buymeacoffee.com/brosenberger)

## Requirements

- Magento 2.4.x
- Web server: **nginx** (the only server Adobe supports from 2.4.9; nginx 1.30).
  Apache config is included for older installs, but Apache was dropped from
  Magento's tested requirements at 2.4.8-p3 / 2.4.7-p7.
- PHP 8.3 / 8.4 (8.5 on 2.4.9)

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

## Module family

| Module | Purpose |
|---|---|
| [module-image-optimizer](https://github.com/brosenberger/module-image-optimizer) | Base: scan `pub/media`, write modern-format sidecars |
| [module-image-optimizer-webp](https://github.com/brosenberger/module-image-optimizer-webp) | WebP converter |
| [module-image-optimizer-avif](https://github.com/brosenberger/module-image-optimizer-avif) | AVIF converter |
| [module-image-optimizer-queue](https://github.com/brosenberger/module-image-optimizer-queue) | Async conversion via the Magento queue |
| [module-image-optimizer-amqp](https://github.com/brosenberger/module-image-optimizer-amqp) | Async conversion over RabbitMQ/AMQP |

Docs & guides: **[brocode.at](https://brocode.at/modules/module-image-optimizer/)**
