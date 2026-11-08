# HeadlessMc Plugin Template

A template for building [HeadlessMc](https://github.com/headlesshq/headlessmc) plugins.
For a working example see our [Quilt plugin](https://github.com/headlesshq/headlessmc-quilt).

## Setup

Configure your plugin information inside `build.gradle`:
```groovy
headlessmcPlugin {
    id = 'example'
    name = 'Example'
    description = 'An example description.'
    authors = ['you']
    license = 'MIT'
    homepage = 'https://github.com/you/your-plugin'
}
```

Then build and run:
```shell
./gradlew build
./gradlew headlessmc --args="plugin ls"
```

When you are done with your plugin consider adding it to our 
[official plugin repository](https://github.com/headlesshq/headlessmc-plugins).

## Configuration

To build plugins for HeadlessMc, we use the
[HeadlessMc Gradle plugin](https://github.com/headlesshq/headlessmc-gradle-plugin#writing-headlessmc-plugins).
It defines the following configuration options in your `build.gradle`

* `headlessmcPlugin { ... }` describes the plugin. It is written into `META-INF/headlessmc-plugin.json`,
  which HeadlessMc reads: id, version, name, description, authors, license, homepage,
  compatible HeadlessMc versions, minimum Java version, dependencies on other plugins and the nested libraries
  with their hashes.
* The `headlessmc` configuration contains the HeadlessMc runtime, the plugin is compiled against it,
  but it is never packaged.
* `include` dependencies are nested into the plugin jar under `META-INF/jars` (Jar-in-Jar), together with their
  transitive dependencies, except for the libraries HeadlessMc already contains.

This template ships a [Renovate](https://docs.renovatebot.com/) config
that keeps Gradle dependencies, the Gradle wrapper and GitHub Actions up to date.
For it to take effect, install the [Renovate GitHub app](https://github.com/apps/renovate) on your repository.

## Releases

Plugins generated from this template use [release-please](https://github.com/googleapis/release-please)

1. Use [semantic commits](https://www.conventionalcommits.org/) such as `feat: add a command` or `fix: handle null`.
2. release-please keeps a release PR open on `main`. Merge it to release: it bumps `version` in
   `gradle.properties`, updates the changelog and creates the GitHub release.
3. The workflow then builds the plugin, attaches the jar to the release and prints the entry for the
   [official plugin repository](https://github.com/headlesshq/headlessmc-plugins) in the job summary.

Setup in your repository: enable **Allow GitHub Actions to create and approve pull requests** under
Settings → Actions → General, release-please needs it to open the release PR.
