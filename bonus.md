### Bonus Pack
#### Configure TARDIS to use SLURM SiteAdapter

```yaml
Sites:
  - name: Emmy
    adapter: Slurm
    quota: 1000
```

--

#### Configure SLURM SiteAdapter

```yaml
Emmy:
  executor: !SSHExecutor
    host: login.gwdg.de
    username: noether
    client_keys:
      - /opt/tardis/ssh/tardis
  StatusUpdate: 2
  MachineTypes:
    - one_day
    - two_days
```

--

#### Configure MachineTypes
```yaml
MachineTypeConfiguration:
    one_day:
      Walltime: '1440'
      Partition: normal
      StartupCommand: 'pilot.sh'
      SubmitOptions:
        short:
          C: "intel"
        long:
          gres: "gpu:2,mic:1"
    two_days:
      Walltime: '2880'
      Partition: normal
      StartupCommand: 'pilot_clean.sh'
      SubmitOptions:
        long:
          gres: "gpu:2,mic:1"
```

---

#### Configure MachineMetaData
```yaml
MachineMetaData:
    one_day:
      Cores: 20
      Memory: 62
      Disk: 480
    twp_days:
      Cores: 20
      Memory: 62
      Disk: 480
```

---
<!-- .element: style="font-size:45%;" -->
#### Entire SLURM SiteAdapter Configuration
```yaml
Sites:
  - name: Emmy
    adapter: Slurm
    quota: 1000

Emmy:
  executor: !SSHExecutor
    host: login.gwdg.de
    username: noether
    client_keys:
      - /opt/tardis/ssh/tardis
  StatusUpdate: 2
  MachineTypes:
    - one_day
    - two_days

MachineTypeConfiguration:
    one_day:
      Walltime: '1440'
      Partition: normal
      StartupCommand: 'pilot.sh'
      SubmitOptions:
        short:
          C: "intel"
        long:
          gres: "gpu:2,mic:1"
    two_days:
      Walltime: '2880'
      Partition: normal
      StartupCommand: 'pilot_clean.sh'
      SubmitOptions:
        long:
          gres: "gpu:2,mic:1"

MachineMetaData:
    one_day:
      Cores: 20
      Memory: 62
      Disk: 480
    twp_days:
      Cores: 20
      Memory: 62
      Disk: 480
```