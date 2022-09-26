### Login to Compute4PUNCH Login Node
#### Set-up oidc-agent

If you are using Compute4PUNCH for the first time and you have not yet used Storage4PUNCH yet, you need to setup OIDC Agent. The OIDC Agent is necessary to use the PUNCH-AAI in combination with command line tools like ssh.

Please, follow the setup procedure "Install OIDC Agent" described in the [Compute4PUNCH Documentation](https://intra.punch4nfdi.de/?md=/docs/TA2/WP2/Compute4PUNCH_Documentation_Users.md)

--

#### Set-up the `oidc-agent` environment

Ensure that `OIDC_SOCK` is defined in this shell by executing

```bash
eval `oidc-agent`
```

Add the `punch-aai` to the `oidc-agent` listening on `$OIDC_SOCKS` by executing

```bash
oidc-add punch-aai
```

You will be asked for the password you have provided during the initial setup.