# PauseSpigot
Fork of PandaSpigot with performance improvements

# PandaSpigot [![Build](https://github.com/hpfxd/PandaSpigot/actions/workflows/build.yml/badge.svg)](https://github.com/hpfxd/PandaSpigot/actions/workflows/build.yml)
Fork of Paper for 1.8.8 focused on improved performance and stability.

## Highlights
- **Backported API enhancements from newer versions**
    - ServerTickStartEvent & ServerTickEndEvent
    - PlayerChunkLoadEvent & PlayerChunkUnloadEvent
    - PlayerHandshakeEvent
    - EntityMoveEvent

- **Greatly improved network performance**
    - **Updating to Netty 4.1** offers the ability to use newer Java versions with epoll on Linux.
    - **Improved flush handling** to massively improve entity tracker performance.
    - **Support for Unix domain sockets** to avoid the overhead of TCP when using a proxy on the same machine.
    - **Using LazyRunnables** to avoid expensive thread wakeup calls when sending non-flushed packets.

- **More configuration options**, such as:
    - Customizable knockback
    - World and player data saving

See a full list of patches [here](./patches/).

## Using
You can download the latest pre-built artifact [here](https://nightly.link/hpfxd/PandaSpigot/workflows/build/master/Server%20JAR.zip).

## API
See our API patches [here](./patches/api/).
<details>
<summary>Maven</summary>

```xml
<repositories>
    <repository>
        <id>hpfxd-repo</id>
        <url>https://repo.hpfxd.com</url>
    </repository>
</repositories>

<dependencies>
    <dependency>
        <groupId>com.hpfxd.pandaspigot</groupId>
        <artifactId>pandaspigot-api</artifactId>
        <version>1.8.8-R0.1-SNAPSHOT</version>
        <scope>provided</scope>
    </dependency>
</dependencies>
```
</details>

<details>
<summary>Gradle (kts)</summary>

```kotlin
repositories {
    mavenCentral()
    maven(url = "https://repo.hpfxd.com")
    maven(url = "https://oss.sonatype.org/content/repositories/snapshots") // for bungeecord-chat
}

dependencies {
    compileOnly("com.hpfxd.pandaspigot:pandaspigot-api:1.8.8-R0.1-SNAPSHOT")
}
```
</details>

## Building
To compile PandaSpigot, you'll need:
- JDK 8 (or above)
- Git
- Maven (Required to build upstream projects)
- Bash

Building, patching, and compiling are all done through the main `panda` script.

PandaSpigot can be built by running `./panda build`, and you will find the final Paperclip jar in `PandaSpigot-Server/build/libs/pandaspigot.jar`

## Contributing
You can mostly follow [Paper's contributing guide](https://github.com/PaperMC/Paper/blob/ver/1.16.5/CONTRIBUTING.md), just remember:
- Multi-line changes start with `// PandaSpigot start` and end with `// PandaSpigot end`
- If the change isn't obvious, add a small explanation like this: `// PandaSpigot start - reason`
- One-line changes should have `// PandaSpigot` at the end of the line.
- Follow Java code style (aka. Oracle style), with some exceptions:
  - If you are modifying upstream files, keep your diff size minimal. Going over 80 characters per line is fine to make this happen.
  - When in doubt or the code around your change is in a clearly different style, use the same style as the surrounding code.

When contributing, please think about the side effects of any changes you write.
Plugin compatibility is important, and we wish to minimize any breakage.

Please do not open pull requests for features that you cannot justify the existence of,
and the added maintenance costs of that come along with them. If you are thinking of
adding a feature that may be controversial, please open an issue first!
