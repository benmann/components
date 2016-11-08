# Bower Components

[![Discord chat](https://img.shields.io/badge/discord-join%20chat%20%E2%86%92-brightgreen.svg?style=flat)](https://discord.gg/yJtVBnp)

> Bower needs your help (**yes, really**). If you're willing to help, please [donate](https://salt.bountysource.com/teams/bower) or contribute

This repository contains list of Bower components and their metadata (currently only url of main repository).

All components reside in `/packages/<COMPONENT>` folder, and have following structure:

```
{
  // Name of package (needed to maintain backward compatibility with old registry)
  "name": "jquery",
  // Repository URL that Bower should use to resolve package
  "url": "https://github.com/jquery/jquery-dist.git"
}
```

## Usage

Registry is versioned, starting with `1.0.0` that reflects state of old registry at the time it was deprecated. You can use this version as starting point, and gradually "bump" registry version in `.bowerrc`, at the same time ensuring projects still works. Please see *Migration* section to see how you can point your Bower to this registry.

We **highly discourage** using `master` version of this repository, and it can change unpredictable. Instead, choose appripriate tag from [available releases](https://github.com/bower/components/releases), and set registry url as follows:

```json
{
  "registry": "https://raw.githubusercontent.com/bower/components/x.x.x"
}
```

## Migration

The structure of this repository matches old registry's API, and `1.0.0` tag reflects its frozen state. It means you can (and should) seamlessly migrate by creating or updating your `.bowerrc` file (either in project's directory or home directory):

```json
{
  "registry": "https://raw.githubusercontent.com/bower/components/1.0.0"
}
```

This change should be 100% backward-compatible with most of old clients. **At some point we will turn off old registry, so please make this change as soon as possible**.

If you also want to preserve search / register / unregister functionality (please mind, it might be deprecated):

```json
{
  "registry": {
    "default": "https://raw.githubusercontent.com/bower/components/master",
    "search": "https://bower.herokuapp.com",
    "register": "https://bower.herokuapp.com",
    "publish": "https://bower.herokuapp.com"
  }
}
```

## Modifying registry

We opt-out of changing entries in `/packages` folder directly. Instead, we encourage contributors to create migration scripts in `/migrations` directory that updates entries appropriately. PRs proposing these migrations shoudn't include changes in `/packages` directory. Maintainers of Bower Components are responsible for reviewing migrations, and running them periodically.

Respository uses [semver](http://semver.org/) for versioning, and uses the same nomenclature for migrations:

- *major* migrations can break bower client, running them results in major semver bump
- *minor* migrations are 100% backward-compatible, and add extra stuff, they result in minor semver bump

## Private registry

You can fork this registry and point Bower to it instead, like so:

```json
{
  "registry": "https://raw.githubusercontent.com/sheerun/components/1.0.0"
}
```

Please [e-mail us](email:team@bower.io) if you're interested in registry in non-public repository.

## License

MIT