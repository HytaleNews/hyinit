# Hyinit
A restriction-free Mixin bootstrapper for HytaleServer.
Backwards compatible with [Hyxin](https://www.curseforge.com/hytale/mods/hyxin).

## User Guide
Hyinit is NOT a standard early plugin, so do not place it in the earlyplugins folder.
Instead, move the original `HytaleServer.jar` into the `server/` subdirectory as `HytaleServerOriginal.jar`, and place `HytaleServer-X.X.X.jar` (the Hyinit JAR) in the `server/` subdirectory as `HytaleServer.jar`.

Your directory layout should look like this:
```
<server root>/
├── earlyplugins/
└── server/          ← also accepted as Server/ (capital S)
    ├── HytaleServer.jar          ← Hyinit JAR (renamed)
    └── HytaleServerOriginal.jar  ← original Hytale server JAR
```

For example, if you are currently using a command like this to start the server normally:
```shell
java -Xms10G -Xmx10G -jar HytaleServer.jar --assets=../Assets.zip
````
Move your original `HytaleServer.jar` to `server/HytaleServerOriginal.jar` (or `Server/HytaleServerOriginal.jar`), then place the Hyinit JAR as `server/HytaleServer.jar` (or `Server/HytaleServer.jar`). The server will now start through Hyinit automatically:
```shell
java -Xms10G -Xmx10G -jar server/HytaleServer.jar --assets=../Assets.zip
````
Now, you can install mod JARs that depend on Hyinit Mixin environment in the earlyplugins folder.

## Developer Guide
### Dependencies
Hyinit currently does not have its own API, so you should depend directly on
[FabricMC's Mixin fork](https://github.com/FabricMC/Mixin) and [MixinExtras](github.com/LlamaLad7/MixinExtras):
```kotlin
dependencies {
    // Mixin
    compileOnly("net.fabricmc:sponge-mixin:${MIXIN_VERSION}")
    // MixinExtras
    compileOnly("io.github.llamalad7.mixinextras:mixinextras-fabric:${MIXINEXTRAS_VERSION}")
}
```

### Adding Mixins
Put JARs with your Mixins in the `earlyplugins` folder.
In `manifest.json`, add the following entry:
```json
{
    "Mixins": [
        "your_mixin_config.mixins.json"
    ]
}
```

### Hyxin Compatibility
`manifest.json` with the following entry will also be read for compatibility with Hyxin:
```json
{
    "Hyxin": {
        "Configs": [
            "your_mixin_config.mixins.json"
        ]
    }
}
```

## Note
The MixinService and the Mixin class loader implementations are partially based on
[fabric-loader's](https://github.com/FabricMC/fabric-loader) Knot implementation.
