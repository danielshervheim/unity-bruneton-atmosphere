# Bruneton's Improved Atmospheric Scattering for Unity

A physically-based atmospheric skybox shader for Unity. Based on work by [Eric Bruneton](https://github.com/ebruneton/precomputed_atmospheric_scattering) and [Scrawk](https://github.com/Scrawk/Brunetons-Improved-Atmospheric-Scattering).

## How to Install

The core-utils package uses the [scoped registry](https://docs.unity3d.com/Manual/upm-scoped.html) feature to import
dependent packages. Please add the following sections to the package manifest
file (`Packages/manifest.json`).

To the `scopedRegistries` section:

```
{
  "name": "DSS",
  "url": "https://registry.npmjs.com",
  "scopes": [ "com.dss" ]
}
```

To the `dependencies` section:

```
"com.dss.atmosphere": "1.0.2"
```

After changes, the manifest file should look like below:

```
{
  "scopedRegistries": [
    {
      "name": "DSS",
      "url": "https://registry.npmjs.com",
      "scopes": [ "com.dss" ]
    }
  ],
  "dependencies": {
    "com.dss.atmosphere": "1.0.2",
    ...
```

## How to Use

Please see the [readme](Packages/com.dss.atmosphere/README.md) in the package directory for usage information.

## Results

![midday](img/ewiTBgX.png)
![sunset](img/FI0mD97.png)
![twilight](img/FRgBzV9.png)

## Credit

This is an extension of scrawk's [implementation](https://github.com/Scrawk/Brunetons-Improved-Atmospheric-Scattering) of ebruneton's [improved atmospheric scattering](https://github.com/ebruneton/precomputed_atmospheric_scattering) paper.

Scrawk's Unity port, while excellent, was restricted in many ways due to various hardcoded parameters. As he himself noted:

> The demo uses a image effect shader as a example of how to use the scattering. The sphere rendered and its light shafts are hard coded into the shader as its just a example. Some work would be needed to convert this into a practical implementation

This is my attempt at a practical implementation. The result is a tool that generates a single material that you can use as a skybox directly.

**Goals**

- To modify the existing codebase as little as possible.
- To enable previewing of the atmosphere in the editor.
- To remove the hardcoded sphere, and image-effect rendering assumptions.
- To enable better control over when / how the scattering textures get precomputed and saved.

**What I changed**

- Added `AtmosphereEditorWindow.cs`, an editor window to easily generate the required textures.
- Added `Atmosphere.shader`, a skybox shader to use the generated textures.