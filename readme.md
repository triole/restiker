# Restiker

<!--- mdtoc: toc begin -->

1. [Synopsis](#synopsis)
2. [Config](#config)
3. [Help](#help)<!--- mdtoc: toc end -->

## Synopsis

Restiker is a very simple wrapper around [restic](https://github.com/restic/restic) that can be used to launch backups. Being not versatile on purpose it can't do anything else.

Note that it requires [dasel](https://github.com/TomWright/dasel) to parse the configuration files.

## Config

Restiker's config files support env variables. In addition you can use `${SELFDIR}` as placeholder for the path in which the restiker script resides.

This is what a config looks like...

```go mdox-exec="cat examples/conf.toml"
repo = "rest:https://user:pass@your.restic/repo"

# if cert is not given, restiker will omit the argument
# cert = "/home/myuser/restiker.crt"
cert = "/home/myuser/restiker/conf.toml"

folders_to_backup = [
    "/etc",
    "/home/myuser",
    "/home/my documents",
    "/home/even more documents"
]

# can be empty
additional_args=[
    "-vv"
]
```

Running a backup with the config file example above, a command like the following will be launched...

```go mdox-exec="./restiker examples/conf.toml -d -i"
restic --cacert /home/myuser/restiker/conf.toml -vv -r rest:https://user:pass@your.restic/repo backup "/etc" "/home/myuser" "/home/my documents" "/home/even more documents" 
```

## Help

```go mdox-exec="./restiker -h"

restiker help

  args
    -i/--ignore   ignore if files do not exist
    -d/--debug    do nothing, just print what would have happened
    -h/--help     display this help

  usage
    restiker examples/conf.toml
    restiker examples/conf.toml -d

```
