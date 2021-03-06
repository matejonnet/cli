# Bacon
Bacon is a new Java CLI for PNC 2.0 combining features of old PNC, DA CLI and PiG tooling.

---
# Reporting an issue
To report an issue, please use the internal JIRA instance. The Github issues usage is now deprecated, and will be closed in the future.

# Common Usages
Compile:
```bash
mvn clean install
```

Run:
```bash
java -jar cli/target/bacon.jar
```

To install the latest ***released*** version:
```bash
curl -fsSL https://raw.github.com/project-ncl/bacon/master/bacon_install.py | python3 - 
```

To install the latest ***snapshot*** (no need to compile):
```bash
curl -fsSL https://raw.github.com/project-ncl/bacon/master/bacon_install.py | python3 - snapshot
```

This will install the `bacon`, `pig`, `da` and `pnc` commands in the `~/bin`
directory, which on Linux will make it available in your shell.

To update the installed version:
```bash
# released version
bacon update

# snapshot version
bacon update snapshot
```

# Configuration

An example configuration is present here: https://github.com/project-ncl/bacon/blob/master/config.yaml

The default configuration used by `bacon` should be located in folder: `~/.config/pnc-bacon/` with name `config.yaml`. We can specify a different folder for the location of the `config.yaml` via the `-p` flag:

```bash
bacon pnc build cancel -p <alternate folder containing config.yaml> 1000
```

We can specify several profiles in the configuration file. This is useful when dealing with different PNC servers and/or configurations. We can use the `--profile` flag to choose the non-default one:

```bash
bacon pnc build cancel --profile coolProfile 1000
```

## Authentication

To authenticate to PNC Authentication servers, add this to your `config.yaml`:

```yaml
keycloak:
    url: "http://keycloak.com"
    realm: ""
    username: ""

    # if regular user
    clientId: ""
    password: ""

    # if service account
    # clientSecret: ""
```

---

# PiG
PiG allows users to setup PNC with the product, build configurations, and much more via a YAML file. This makes it much easier to configure PNC for new releases as well as making the configuration portable across different PNC servers.

PiG is run in multiple phases:

- configure
- build
- repo
- licenses
- javadocs
- sources
- shared-content
- docs
- scripts
- addons

The all-in-one phase that combines all the phases is:

- run

The `configure` phase pushes all the settings in the YAML file to PNC, and the `build` phase tells PNC to build everything.

```bash
bacon pig <phase> ...
```
## Configuration

The application is configured via the `build-config.yaml` file. 

A PiG `build-config.yaml` looks like this: https://github.com/project-ncl/bacon/blob/master/example-pig-config.yaml

TODO: add a command that allows users to specify variables via cli

## configure

Usage:
```bash
bacon pig configure <directrory containing build-config.yaml>
```

## build

Usage:
```bash
bacon pig configure <directrory containing build-config.yaml>
```

You can specify if you want temporary builds or not with the `-t` flag.

## Deliverables

This section covers the required deliverables for a product release:

- licenses
- maven-repository
- src zip
- javadoc zip

TODO: describe each section more

## Add ons

TODO: Description of add-ons
