# GTNH 1.7.10 Mod Template

A reusable GitHub repository template for creating Minecraft 1.7.10 Forge mods that target GT New Horizons.

The build setup is based on the maintained [GTNewHorizons ExampleMod1.7.10](https://github.com/GTNewHorizons/ExampleMod1.7.10) starter package and uses GTNHGradle/RetroFuturaGradle. The checked-in example mod is intentionally minimal and uses placeholder names so the template builds before it is customized.

## Use this template

1. On GitHub, open this repository's **Settings** and enable **Template repository** once.
2. Select **Use this template** > **Create a new repository** whenever you start a mod.
3. Clone the newly created repository; do not develop a real mod directly in this template repository.
4. Replace the placeholders listed below.
5. Run the setup and build commands.

## Customize a new mod

Replace these values throughout the new repository. Rename files and directories where indicated; a text-only replacement is not enough for the Java package or main class.

| Placeholder | Replace with | Also rename |
| --- | --- | --- |
| `MyMod` | Mod name/main class, such as `ExampleMachines` | `MyMod.java` |
| `mymodid` | Lowercase mod ID, such as `examplemachines` | Java package directory |
| `com.myname.mymodid` | Your root Java package | `src/main/java/com/myname/mymodid/` |
| `YourName` | Author or team name | Nothing |
| `https://github.com/yourname/yourmod` | The new repository URL | Nothing |
| `<year>` and `<copyright holders>` | License copyright details | Rename `LICENSE-template` to `LICENSE` and update the bundled resource license |

At minimum, review:

- `gradle.properties` for the mod name, ID, package, generated `Tags` class, Java mode, Mixins, and publishing options.
- `src/main/java/` for package declarations, the main class, proxies, and configuration.
- `src/main/resources/mcmod.info` for description, author, URL, and dependency metadata.
- `dependencies.gradle` and `repositories.gradle` for mod dependencies.
- `LICENSE-template` and `src/main/resources/LICENSE` for the license you want to use and bundle in the mod jar.

Keep the mod ID lowercase and stable after release. Java packages should be lowercase. Do not add secrets or publishing tokens to the repository; GitHub Actions consumes them from repository secrets.

## Set up the development workspace

The template currently follows upstream's selected Java toolchain. A compatible JDK can also be provisioned by Gradle when toolchain downloads are available.

On Windows:

```powershell
.\gradlew.bat setupDecompWorkspace
.\gradlew.bat build
```

On Linux or macOS:

```bash
./gradlew setupDecompWorkspace
./gradlew build
```

Import the project into IntelliJ IDEA as a Gradle project after setup. Useful tasks include `runClient`, `runServer`, `spotlessApply`, and `build`.

## Dependencies and GTNH integration

Add dependencies in `dependencies.gradle`; avoid modifying `build.gradle.kts` unless the build genuinely needs custom behavior. The comments in `dependencies.gradle` document the supported configurations, including deobfuscated development dependencies.

Mixins, access transformers, shadowed dependencies, Maven publishing, CurseForge, and Modrinth are opt-in settings in `gradle.properties`. Leave features disabled until the mod needs them.

## Continuous integration and releases

The included GitHub Actions workflows use GTNH's shared workflows:

- Pushes and pull requests to `main` or `master` run the build and server smoke tests.
- Pushing a version tag, such as `1.0.0`, builds a GitHub release.

Configure repository secrets only for services you enable, such as Maven, Modrinth, or CurseForge publishing.

## Keeping the build setup current

GTNH's build tooling evolves even though Minecraft remains on 1.7.10. Before making manual build-script changes, compare this template with the latest [official starter package](https://github.com/GTNewHorizons/ExampleMod1.7.10/releases/tag/master-packages) and review the [GTNHGradle documentation](https://github.com/GTNewHorizons/GTNHGradle).

The build exposes update/help tasks as they become available. Run the following to see the tasks supported by the checked-in version:

```powershell
.\gradlew.bat tasks
.\gradlew.bat propertiesHelp
```

## Upstream documentation

- [GTNH ExampleMod1.7.10](https://github.com/GTNewHorizons/ExampleMod1.7.10)
- [ExampleMod FAQ](https://github.com/GTNewHorizons/ExampleMod1.7.10/blob/master/docs/FAQ.md)
- [GTNHGradle](https://github.com/GTNewHorizons/GTNHGradle)
- [GTNH development wiki](https://wiki.gtnewhorizons.com/wiki/Development)
