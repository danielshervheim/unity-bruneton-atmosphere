# Bruneton's Improved Atmospheric Scattering for Unity

This is an extension of scrawk's [implementation](https://github.com/Scrawk/Brunetons-Improved-Atmospheric-Scattering) of ebruneton's [improved atmospheric scattering](https://github.com/ebruneton/precomputed_atmospheric_scattering) paper.

Scrawk's Unity port, while excellent, was restricted in many ways due to various hardcoded parameters. As he himself noted:

> The demo uses a image effect shader as a example of how to use the scattering. The sphere rendered and its light shafts are hard coded into the shader as its just a example. Some work would be needed to convert this into a practical implementation

This is my attempt at a practical implementation. The result is a tool that generates a single material that you can use as a skybox directly.

## Goals
- To modify the existing codebase as little as possible.
- To enable previewing of the atmosphere in the editor.
- To remove the hardcoded sphere, and image-effect rendering assumptions.
- To enable better control over when / how the scattering textures get precomputed and saved.

## What I changed
- Added `AtmosphereEditorWindow.cs`, an editor window to easily generate the required textures.
- Added `Atmosphere.shader`, a skybox shader to use the generated textures.

## Requirements

This project requires a graphics card that supports the following Unity features:
- Compute Shader
- Texture3D
- RenderTexture

## How to install

### Method 1: copy into your project

1. Download this repo.
2. Copy the `AtmosphericSkybox` folder into your projects `Assets` folder.

### Method 2: add as a package dependency

1. (pre-Unity 2019) Add the following line to the dependencies in `Packages/manifest.json`:

```json
"com.dss.atmosphere": "https://github.com/danielshervheim/Brunetons-Improved-Atmospheric-Scattering.git#upm"
```

2. (Unity 2019+) Or, just paste the url (with `#upm` at the end) in the "add package from git" option in the package manager.

## How to setup

#### Generating the atmosphere

1. Select "Atmosphere/Generate" from the menu bar.
2. Set the precomputation parameters as desired.
3. Press "Precompute".
4. Choose paths to save the generated material and textures.

#### Using it as a skybox

1. Select "Window > Lighting > Settings" from the menu bar.
2. Locate the "Environment" heading in the lighting window.
3. Drag generated material into the *Skybox Material* slot.
4. Drag your scene's main directional light into the "Sun Source" slot.

## A note on color space

- For best results, ensure that your projects color space is set to **linear**, rather than gamma.
- If you are using the tonemap post-processing effect, then be sure to disable the **tonemap** checkbox on the material.


## Results

![midday](https://i.imgur.com/ewiTBgX.png)
![sunset](https://i.imgur.com/FI0mD97.png)
![twilight](https://i.imgur.com/FRgBzV9.png)