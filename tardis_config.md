### TARDIS Configuration
#### Configure Plugins

```yaml
Plugins:
  SqliteRegistry:
    db_file: drone_registry.db
```

> Using drone registry as persistent storage of states is recommended!

More plugins can be found in the [TARDIS Documentation](https://cobald-tardis.readthedocs.io/en/latest/plugins/plugins.html)

--

#### Configure Batch System

```yaml
BatchSystem:
  adapter: FakeBatchSystem
  allocation: 1.0
  utilization: !TardisPeriodicValue
               period: 600
               amplitude: 0.5
               offset: 0.5
               phase: 0.
  machine_status: Available
```

More batch system adapters can be found in the [TARDIS Documentation](https://cobald-tardis.readthedocs.io/en/latest/adapters/batchsystem.html) 

--

#### Configure Sites

```yaml
Sites: # List of sites to use
  - name: Fake
    adapter: FakeSite
    quota: 8000 # CPU core quota
```

More site adapters can be found in the [TARDIS Documentation](https://cobald-tardis.readthedocs.io/en/latest/adapters/site.html) 

--

<!-- .element: style="font-size:80%;" -->
#### Configure each Site

```yaml
Fake: 
  # Configuration of the site adapter
  api_response_delay: !TardisRandomGauss
                      mu: 0.1
                      sigma: 0.01
  resource_boot_time: !TardisRandomGauss
                      mu: 10
                      sigma: 1
  MachineTypes:
    - m1.infinity # List of machine types
  MachineTypeConfiguration:
    m1.infinity: # Configuration of each machine type
  MachineMetaData:
    m1.infinity: # Meta-data used for internal accounting
      Cores: 8
      Memory: 16
      Disk: 160
```

--


<!-- .element: style="font-size:80%;" -->
## Enable TARDIS Configuration

The `TARDIS` configuration is part of `COBalD` configuration:
* Add a `tardis` MappingNode to the `cobald.yml`
* Add `tardis` configuration to this MappingNode

```yaml
<COBalD configuration>
tardis:
  <TARDIS configuration>
```

--

<!-- .element: style="font-size:45%;" -->
#### tardis MappingNode

```yaml
tardis:
  Plugins:
    SqliteRegistry:
      db_file: drone_registry.db
  
  BatchSystem:
    adapter: FakeBatchSystem
    allocation: 1.0
    utilization: !TardisPeriodicValue
                 period: 3600
                 amplitude: 0.5
                 offset: 0.5
                 phase: 0.
    machine_status: Available
  
  Sites:
    - name: Fake
      adapter: FakeSite
      quota: 8000 # CPU core quota
  
  Fake:
    api_response_delay: !TardisRandomGauss
                        mu: 0.1
                        sigma: 0.01
    resource_boot_time: !TardisRandomGauss
                        mu: 60
                        sigma: 10
    MachineTypes:
      - m1.infinity
    MachineTypeConfiguration:
      m1.infinity:
    MachineMetaData:
      m1.infinity:
        Cores: 8
        Memory: 16
        Disk: 160
```

--

<!-- .element: style="font-size:45%;" -->
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
tardis:
  Plugins:
    SqliteRegistry:
      db_file: drone_registry.db
  
  BatchSystem:
    adapter: FakeBatchSystem
    allocation: 1.0
    utilization: !TardisPeriodicValue
                 period: 3600
                 amplitude: 0.5
                 offset: 0.5
                 phase: 0.
    machine_status: Available
  
  Sites:
    - name: Fake
      adapter: FakeSite
      quota: 8000 # CPU core quota
  
  Fake:
    api_response_delay: !TardisRandomGauss
                        mu: 0.1
                        sigma: 0.01
    resource_boot_time: !TardisRandomGauss
                        mu: 60
                        sigma: 10
    MachineTypes:
      - m1.infinity
    MachineTypeConfiguration:
      m1.infinity:
    MachineMetaData:
      m1.infinity:
        Cores: 8
        Memory: 16
        Disk: 160
```
