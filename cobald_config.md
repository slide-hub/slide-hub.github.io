### COBalD Configuration
#### Defining Pipelines

```yaml
pipeline:
  - __type__: cobald.controller.linear.LinearController
    low_utilisation: 0.90
    high_allocation: 0.90
    rate: 1
  - __type__: cobald.decorator.limiter.Limiter
    minimum: 1
  - __type__: cobald.decorator.logger.Logger
    name: 'changes'
  - __type__: tardis.resources.poolfactory.create_composite_pool
    configuration: 'tardis.yml'
```
![pipeline](img/pipeline.png)

--

<!-- .element: style="font-size:70%;" -->
### Configure Logging

```yaml
logging:
  version: 1
  root:
      level: DEBUG
      handlers: [console, file]
  formatters:
    precise:
      format: '%(name)s: %(asctime)s %(message)s'
      datefmt: '%Y-%m-%d %H:%M:%S'
  handlers:
    console:
      class: logging.StreamHandler
      formatter: precise
      stream: ext://sys.stdout
    file:
      class: logging.handlers.RotatingFileHandler
      formatter: precise
      filename: tardis.log
      maxBytes: 10485760
      backupCount: 3
```

Parameters are directly passed to [`logging.config.dictConfig`](https://docs.python.org/3.7/library/logging.config.html#logging.config.dictConfig)

--

<!-- .element: style="font-size:50%;" -->
#### `cobald.yml`

```yaml
pipeline:
  - __type__: cobald.controller.linear.LinearController
    low_utilisation: 0.90
    high_allocation: 0.90
    rate: 1
  - __type__: cobald.decorator.limiter.Limiter
    minimum: 1
  - __type__: cobald.decorator.logger.Logger
    name: 'changes'
  - __type__: tardis.resources.poolfactory.create_composite_pool
    configuration: 'tardis.yml'
logging:
  version: 1
  root:
      level: DEBUG
      handlers: [console, file]
  formatters:
    precise:
      format: '%(name)s: %(asctime)s %(message)s'
      datefmt: '%Y-%m-%d %H:%M:%S'
  handlers:
    console:
      class : logging.StreamHandler
      formatter: precise
      stream  : ext://sys.stdout
    file:
      class : logging.handlers.RotatingFileHandler
      formatter: precise
      filename: tardis.log
      maxBytes: 10485760
      backupCount: 3
``` 
