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
  utilization: !PeriodicValue
               period: 3600
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
  api_response_delay: !RandomGauss
                      mu: 0.1
                      sigma: 0.01
  resource_boot_time: !RandomGauss
                      mu: 60
                      sigma: 10
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


<!-- .element: style="font-size:45%;" -->
#### `tardis.yml`

```yaml
Plugins:
  SqliteRegistry:
    db_file: drone_registry.db

BatchSystem:
  adapter: FakeBatchSystem
  allocation: 1.0
  utilization: !PeriodicValue
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
  api_response_delay: !RandomGauss
                      mu: 0.1
                      sigma: 0.01
  resource_boot_time: !RandomGauss
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

