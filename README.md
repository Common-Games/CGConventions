Common Games Conventions Style Guide
===========================

### For file structure, naming conventions, and other things

These standardized conventions are for keeping your project organized allowing you to quickly find the assets your need. 
Games are large projects that can span months, and having conventions such as these will avoid headaches in the long run.
It'll also help greatly with 

# Table of Contents

- [Directory/File Structure](#directoryfile-structure)
    - [GameObject](#gameobjects)
    - [Assets](#assets)
    - [Scripts](#scripts)
    - [Models](#models)
- [Asset Workflow](#asset-workflow)
    - [Models](#models-workflow)
    - [Textures](#textures-workflow)
    - [Configuration files](#settings-workflow)
    - [Localization](#localization-workflow)
    - [Audio](#audio-workflow)
- [Be Consistent](#be-consistent)

# Directory/File Structure

> *No* `spaces` on file or directory names.

## GameObjects

1. For Descriptors, use `tree_small` *not* `small_tree`. While the latter sound better, it is much more effective to group all tree objects together instead of all small objects.

2. `camelCase` where necessary. Use `weapon_miniGun` instead of `weapon_gun_mini`. Avoid this if possible, for example, `vehicles_fighterJet` should be `vehicles_jet_fighter` if you plan to have multiple types of jets.

3. Prefer using descriptive suffixes over numbers where possible: `truck_damaged` not `truck_01`. 

4. If using numbers as a suffix, always use 2 digits `_01`. 

5. **Do not** use numbers as a versioning system! Use `git`, you plebe.

### Persistent/Important GameObjects

`_snake_case`

Use a leading underscore to make object instances that are not specific to the current scene stand out.

### Debug Objects

`[SNAKE_CASE]`

Enclose objects that are only being used for debugging/testing and are not part of the release with brackets.

## Assets

Naming in: `PascalCase`

1. Prefer a deep folder structure over having long asset names.

2. Directory names should be as concise as possible, prefer one or two words. If a directory name is too long, it probably makes sense to split it into sub directories.

3. Unless it's asset specific, try to have only one file type per folder. Use `Textures/Trees`, `Models/Trees` and *not* `Trees/Textures`, `Trees/Models`. That way its easy to set up root directories for the different software involved, for example, Substance Painter would always be set to save to the Textures directory.

4. If your project contains multiple environments or art sets, use the asset type for the parent directory: `Trees/Jungle`, `Trees/City` *not* `Jungle/Trees`, `City/Trees`. Since it makes it easier to compare similar assets from different sets to ensure continuity across the sets.

```
Assets
├── [Source]
|   ├── Art
|   |   ├── Models
|   |   |   ├── Architectural
|   |   |   |   ├── Buildings
|   |   |   |   └── Props
|   |   |   ├── Environmental
|   |   |   |   ├── Rocks
|   |   |   |   ├── Vegetation
|   |   |   |   └── Water
|   |   |   ├── Actors
|   |   |   |   ├── Characters
|   |   |   |   |   ├── Humanoid
|   |   |   |   |   └── Creatures
|   |   |   |   |       ├── Animals
|   |   |   |   |       └── Monsters
|   |   |   |   ├── Vehicles
|   |   |   |   └── Robots
|   |   |   └── Items
|   |   |       ├── Weapons
|   |   |       ├── Armour
|   |   |       └── Consumables
|   |   |   
|   |   ├── General 3D
|   |   |   ├── Meshes      # FBX and BLEND files
|   |   |   ├── Animations
|   |   |   ├── Materials   
|   |   |   └── Textures    # PNG files
|   |   |   
|   |   ├── Audio 
|   |   |   ├── Music
|   |   |   ├── Ambient  (Rain)
|   |   |   ├── Foley    (Footsteps, scraping/rattling, rattling, etc)
|   |   |   |   ├── Feet
|   |   |   |   ├── Moves
|   |   |   |   └── Specifics 
|   |   |   |
|   |   |   ├── Effects  (UI Button clicks, slowmo transition)   
|   |   |   └── Dialogue (Narration, characters speaking)
|   |   |   
|   |   └── Sprites      # PNG files (W/ Sprite setting)
|   |
|   ├── Prefabs
|   |
|   ├── Scenes
|   | 
|   ├── Scripts
|   |   ├── Core    (Project Specific Scripts)
|   |   |   ├── Environment (Scripts for objects in the world)
|   |   |   ├── PlayerSystems (Player character scripts: Movement, Camera) 
|   |   |   ├── Managers  (System Managers)
|   |   |   ├── UI
|   |   |   ├── Utilities (Project specific Utilities)
|   |   |   └── Temporary (Test or Placeholder scripts)
|   |   |
|   |   ├── Shaders
|   |   |
|   |   └── Framework   (Shared Scripts)
|   |       ├── Common-Games 
|   |       |   ├── Shaders 
|   |       |   ├── Tools
|   |       |   └── Utilities 
|   |       |       └── Extensions
|   |       |
|   |       └── UltEvents
|   |
|   ├── Settings
|   |
|   └── Docs # Project Documentation (Should be on the GitHub wiki as well)
|
├── Plugins   # External assets/tools you want to compile separately from the rest.
└── Resources # Configuration files, localization text and other user files.
```

## Scripts

> For C# and shader files use `PascalCase`.

1. Use namespaces that match your directory structure.

2. A Framework directory is great for having code that can be reused across projects.

**The Scripts folder varies depending on the project, however, these folders should be consistent across projects:**

```
Scripts
    ├── Core    (Project Specific Scripts)
    |   ├── Environment (Scripts for objects in the world)
    |   ├── PlayerSystems (Player character scripts: Movement, Camera) 
    |   ├── Managers  (System Managers)
    |   ├── UI
    |   ├── Utilities (Project specific Utilities)
    |   └── Temporary (Test or Placeholder scripts)
    |
    ├── Shaders
    |
    └── Framework   (Shared Scripts)
        ├── Common-Games 
        |   ├── Shaders 
        |   ├── Tools
        |   └── Utilities 
        |       └── Extensions
        |
        └── UltEvents
```

## Models

Separate files from the modelling program and ready to use, exported models.

```
Models
+---Blend
\---FBX
```

# Asset Workflow

### Models workflow

File extension: `FBX`

Even though Unity supports Blender files by default, it is better to keep what is being worked on and what is a complete, exported model separate. This is also a must when using other software, such as Substance for texturing.

Use `Y up`, `-Z forward` and `uniform scale` when exporting.

### Textures workflow

File extension: `PNG`, `TIFF` or `HDR`

Choose either a `Specularity/Glossiness` or `Roughness/Metallic` workflow. 

Specularity maps have the advantage of being having the possibility to be RGB maps instead of grayscale (useful for tinted metals), apart from that there is little difference between the result from either workflow.

<details>
  <summary>1. Texture Suffixes</summary>
  
  Suffix | Texture
  :------|:-----------------
  `_A`  | Albedo
  `_SP`  | Specular
  `_R`   | Roughness
  `_MT`  | Metallic
  `_GL`  | Glossiness
  `_N`   | Normal
  `_H`   | Height
  `_DP`  | Displacement
  `_EM`  | Emission
  `_AO`  | Ambient Occlusion
  `_MA`   | Mask
  </details>
  
<details>
    <summary>2. RGB Masks</summary>
    It is good practice to use a single texture to combine black and white masks in a single texture split by each RGB channel. Using this, most textures should have:
    
```
texture_A.png  # Albedo
texture_N.png   # Normal Map
texture_MA.png   # Mask
```
    
    
Channel | Spec/Gloss        | Rough/Metal
:-------|:------------------|:-----------
R       | Specularity       | Roughness
G       | Glossiness        | Metallic
B       | Ambient Occlusion | Ambient Occlusion

##### The blue channel can vary depending on the type of material:

 - For materials with subsurface scattering shader (characters) use the `B` channel for *subsurface opacity/strength*
 - For materials with anisotropic shader (brushed metal) use the `B` channel for the *anisotropic direction map*

</details>
 
## Audio workflow
 
 File extension: `WAV` while mixing, `OGG` in game.
 
 Preload small sound clips to memory, load on the fly for longer music and less frequent ambient noise files.

## Prefabs workflow

## Settings workflow

File extension: `INI`

Fast and easy to parse, clean and easy to tweak.

`XML`, `JSON`, and `YAML` are also good alternatives, pick one and be consistent.

Use binary file formats for files that should not be changed by the player. For multiplayer games store configuration data on a secure server.

## Localization workflow

File extension: `CSV`

Widely used by localization software, makes it trivial to edit strings using spreadsheets.

# Be Consistent

> The point of having style guidelines is to have a common vocabulary of coding so people can concentrate on what you're saying rather than on how you're saying it. We present global style rules here so people know the vocabulary, but local style is also important. If code you add to a file looks drastically different from the existing code around it, it throws readers out of their rhythm when they go to read it. Avoid this.

- [Microsoft C# Style Guide](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/inside-a-program/coding-conventions)

- [Google C++ Style Guide](https://google.github.io/styleguide/cppguide.html)

---
