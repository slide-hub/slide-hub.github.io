### TARDIS Configuration
#### Configure Plugins

```yaml
Plugins:
  SqliteRegistry:
    db_file: drone_registry.db
```

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

--

#### Configure Sites

```yaml
Sites:
  - name: Fake
    adapter: FakeSite
    quota: 8000 # CPU core quota
```

--

<!-- .element: style="font-size:90%;" -->
#### Configure each Site

```yaml
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

