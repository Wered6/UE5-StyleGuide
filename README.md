# Wered UE5 Style Guide forked from [Allar's](https://github.com/Allar/ue5-style-guide)

@TODO: Add C++ section, directory structure in C++, plugins, modules, add tldr with links

## Table of contents

<details>
<summary><a href="#terms">0. Important Terminology</a></summary>

- [0.1 Levels/Maps](#terms-levels-maps)
- [0.2 Identifiers](#terms-identifiers)
- [0.3 Cases](#terms-cases)
- [0.4 Variables / Properties](#terms-vars-props)

</details>

<details>
<summary><a href="#principles">1. Principles</a></summary>

- [1.1 If your UE5 project already has a style guide, you should follow it](#principles-follow-style-guide)
- [1.2 All structure, assets, and code in any Unreal Engine 5 project should look like a single person created it, no matter how many people contributed](#principles-single-person)
- [1.3 Friends do not let friends have bad style](#principles-friends)
- [1.4 A team without a style guide is no team of mine](#principles-team-without-style-guide)

</details>

<details>
<summary><a href="#naming">2. Naming Convention</a></summary>

- [2.1 Forbidden Characters](#naming-forbidden-characters)
- [2.2 Blueprints Naming](#naming-bp)
    - [2.2.1 Base Asset Name - 'Prefix_BaseAssetName_Variant_Suffix'](#naming-base-asset-name)
        - [2.2.1.1 Name Modifiers](#naming-modifiers)
            - [2.2.1.1.1 Most Common](#naming-modifiers-common)
            - [2.2.1.1.2 Animations](#naming-modifiers-animations)
            - [2.2.1.1.3 Artificial Intelligence](#naming-modifiers-ai)
            - [2.2.1.1.4 Blueprints](#naming-modifiers-bps)
            - [2.2.1.1.5 Materials](#naming-modifiers-materials)
            - [2.2.1.1.6 Textures](#naming-modifiers-textures)
                - [2.2.1.1.6.1 Texture Packing](#naming-modifiers-textures-packing)
            - [2.2.1.1.7 Miscellaneous](#naming-modifiers-misc)
            - [2.2.1.1.8 Paper 2D](#naming-modifiers-paper2d)
            - [2.2.1.1.9 Physics](#naming-modifiers-physics)
            - [2.2.1.1.10 Sounds](#naming-modifiers-sounds)
            - [2.2.1.1.11 User Interface](#naming-modifiers-ui)
            - [2.2.1.1.12 Effects](#naming-modifiers-effects)
- [2.3 CPP Naming](#naming-cpp)

</details>

<details>
<summary><a href="#structure">3. Content Directory Structure</a></summary>

- [3.1 Folder Names](#structure-folder-names)
    - [3.1.1 Always Use PascalCase](#structure-folder-names-case)
    - [3.1.2 Never Use Spaces](#structure-folder-names-no-spaces)
    - [3.1.3 Never Use Unicode Characters And Other Symbols](#structure-folder-names-no-unicode)
- [3.2 Use A Top Level Folder For Project Specific Assets](#structure-top-level)
    - [3.2.1 No Global Assets](#structure-top-level-no-global-assets)
    - [3.2.2 Reduce Migration Conflicts](#structure-top-level-migration-conflicts)
    - [3.2.3 Samples, Templates, and Marketplace Content Are Risk-Free](#structure-top-level-risk-free)
    - [3.2.4 DLC, Sub-Projects, and Patches Are Easily Maintained](#structure-top-level-dlc)
- [3.3 Use `Developer` Folder For Local Testing](#structure-developer-folder)
- [3.4 All Map<sup>*</sup> Files Belong In A Folder Called `Maps`](#structure-maps-folder)
- [3.5 Use A `Core` Folder For Critical Blueprints And Other Assets](#structure-core-folder)
- [3.6 Redundant Folders](#structure-redundant-folders)
    - [3.6.1 Creating a folder named `Assets` is redundant](#structure-redundant-folders-assets)
    - [3.6.2 Creating a folder named `Meshes`, `Textures`, or `Materials` is redundant](#structure-redundant-folders-meshes-textures-materials)
- [3.7 Huge Asset Sets Get Their Own Folder Layout](#structure-huge-sets)
- [3.8 `MaterialLibrary`](#structure-material-library)
- [3.9 No Empty Folders](#structure-no-empty-folders)

</details>

<details>
<summary><a href="#bp">4. Blueprints</a></summary>

- [4.1 Compiling](#bp-compiling)
- [4.2 Variables](#bp-vars)
    - [4.2.1 Naming](#bp-vars-naming)
        - [4.2.1.1 Nouns](#bp-vars-naming-nouns)
        - [4.2.1.2 PascalCase](#bp-vars-naming-case)
        - [4.2.1.3 Boolean `b` Prefix](#bp-vars-naming-bool-prefix)
        - [4.2.1.4 Boolean Names](#bp-vars-naming-bool-names)
            - [4.2.1.4.1 No questions](#bp-vars-naming-bool-names-no-questions)
            - [4.2.1.4.2 No Continuous tense](#bp-vars-naming-bool-names-no-continuous-tense)
            - [4.2.1.4.3 Complex States](#bp-vars-naming-bool-names-complex-states)
        - [4.2.1.5 Considered Context](#bp-vars-naming-context)
        - [4.2.1.6 Do *Not* Include Atomic Type Names](#bp-vars-naming-atomic)
        - [4.2.1.7 Do Include Non-Atomic Type Names](#bp-vars-naming-complex)
        - [4.2.1.8 Arrays](#bp-vars-naming-arrays)
    - [4.2.2 Editable Variables](#bp-vars-editable)
        - [4.2.2.1 Descriptions](#bp-vars-editable-descriptions)
        - [4.2.2.2 Slider And Value Ranges](#bp-vars-editable-ranges)
    - [4.2.3 Categories](#bp-vars-categories)
    - [4.2.4 Variable Access Level](#bp-vars-access)
        - [4.2.4.1 Private Variables](#bp-vars-access-private)
    - [4.2.5 Advanced Display](#bp-vars-advanced)
    - [4.2.6 Transient Variables](#bp-vars-transient)
    - [4.2.7 Config Variables](#bp-vars-config)
- [4.3 Functions, Events, and Event Dispatchers](#bp-funcs)
    - [4.3.1 Naming](#bp-funcs-naming)
        - [4.3.1.1 Verb Rule](#bp-funcs-naming-verb-rule)
        - [4.3.1.2 Property RepNotify Functions Always `OnRep_Variable`](#bp-funcs-naming-onrep)
        - [4.3.1.3 Info Functions Returning Bool Should Ask Questions](#bp-funcs-naming-bool)
        - [4.3.1.4 Event Handlers and Dispatchers Should Start With `On`](#bp-funcs-naming-event-handlers)
        - [4.3.1.5 Remote Procedure Calls Should Be Prefixed With Target](#bp-funcs-naming-rpcs)
    - [4.3.2 All Functions Must Have Return Nodes](#bp-funcs-return)
    - [4.3.3 No Function Should Have More Than 50 Nodes](#bp-funcs-node-limit)
    - [4.3.4 All Public Functions Should Have A Description](#bp-funcs-description)
    - [4.3.5 All Functions Must Be Categorized By Project Name Initials](#bp-funcs-category)
- [4.4 Blueprint Graphs](#bp-graphs)
    - [4.4.1 No Spaghetti](#bp-graphs-spaghetti)
    - [4.4.2 Align Wires Not Nodes](#bp-graphs-align-wires)
    - [4.4.3 White Exec Lines Are Top Priority](#bp-graphs-exec-first)
    - [4.4.4 Getters Are Invoked In Every Use](#bp-graphs-getters-invoking)
    - [4.4.5 Graphs Should Be Reasonably Commented](#bp-graphs-comments)
    - [4.4.6 Graphs Should Handle Casting Errors Where Appropriate](#bp-graphs-cast-error-handling)
    - [4.4.7 Graphs Should Not Have Any Dangling / Loose / Dead Nodes](#bp-graphs-dangling-nodes)

</details>

<details>
<summary><a href="#sm">5. Static Meshes</a></summary>

- [5.1 Static Mesh UVs](#sm-uvs)
    - [5.1.1 All Meshes Must Have UVs](#sm-uvs-no-missing)
    - [5.1.2 All Meshes Must Not Have Overlapping UVs for Lightmaps](#sm-uvs-no-overlapping)
- [5.2 LODs Should Be Set Up Correctly](#sm-lods)
- [5.3 Modular Socketless Assets Should Snap To The Grid Cleanly](#sm-modular-snapping)
- [5.4 All Meshes Must Have Collision](#sm-collision)
- [5.5 All Meshes Should Be Scaled Correctly](#sm-scaled)

</details>

<details>
<summary><a href="#levels">6. Levels</a></summary>

- [6.1 No Errors Or Warnings](#levels-no-errors-or-warnings)
- [6.2 Lighting Should Be Built](#levels-lighting-should-be-built)
- [6.3 No Player Visible Z Fighting](#levels-no-visible-z-fighting)
- [6.4 Fab Specific Rules](#levels-fab-rules)
    - [6.4.1 Overview Level](#levels-fab-rules-overview)
    - [6.4.2 Demo Level](#levels-fab-rules-demo)

</details>

<details>
<summary><a href="#textures">7. Textures</a></summary>

- [7.1 Dimensions Are Powers of 2](#textures-dimensions)
- [7.2 Texture Density Should Be Uniform](#textures-density)
- [7.3 Textures Should Be No Bigger than 8192](#textures-max-size)
- [7.4 Textures Should Be Grouped Correctly](#textures-group)

</details>

<a name="terms"></a>
<a name="0"></a>

## 0. Important Terminology

<a name="terms-levels-maps"></a>
<a name="0.1"></a>

##### 0.1 Levels/Maps

The word 'map' generally refers to what the average person calls a 'level' and may be used interchangeably. See this term's
history [here](https://en.wikipedia.org/wiki/Level_(video_gaming)).

<a name="terms-identifiers"></a>
<a name="0.2"></a>

##### 0.2 Identifiers

An `Identifier` is anything that resembles or serves as a "name". For example, the name of an asset, or the name of a material later, or a
blueprint property, a variable, or a folder name, or for a data table row name, etc...

<a name="terms-cases"></a>
<a name="0.3"></a>

##### 0.3 Cases

There are a few different ways you can `CaseWordsWhenNaming`. Here are some common casing types:

> ###### PascalCase
>
> Capitalize every word and remove all spaces, e.g. `DesertEagle`, `StyleGuide`, `ASeriesOfWords`.
>
> ###### camelCase
>
> The first letter is always lowercase, but every following word starts with uppercase, e.g. `desertEagle`, `styleGuide`, `aSeriesOfWords`.
>
> ###### Snake_case
>
> Words can arbitrarily start upper or lowercase, but words are separated by an underscore, e.g. `desert_Eagle`, `Style_Guide`,
`a_Series_of_Words`.

<a name="terms-vars-props"></a>
<a name="0.4"></a>

##### 0.4 Variables / Properties

The words 'variable' and 'property' in most contexts are interchangeable. If they are both used together in the same context, however:

###### Property

Usually refers to a variable defined in a class. For example, if `BP_Barrel` had a variable `bExploded`, `bExploded` may be referred to as a
property of `BP_Barrel`.

When in the context of a class, it is often used to imply accessing previously defined data.

###### Variable

Usually refers to a variable defined as a function argument or a local variable inside a function.

When in the context of a class, it is often used to convey discussion about its definition and what it will hold.

**[⬆ Back to Top](#table-of-contents)**

<a name="principles"></a>
<a name="1"></a>

## 1. Principles

These principles have been adapted from [the idiomatic.js style guide](https://github.com/rwaldron/idiomatic.js/).

<a name="principles-follow-style-guide"></a>
<a name="1.1"></a>

### 1.1 If your UE5 project already has a style guide, you should follow it

If you are working on a project or with a team that has a pre-existing style guide, it should be respected.

Style guides should be living documents. You should propose style guide changes to an existing style guide as well as this guide if you feel
the change benefits all usages.

> #### "Arguments over style are pointless. There should be a style guide, and you should follow it."
> [*Rebecca Murphey*](https://rmurphey.com)

<a name="principles-single-person"></a>
<a name="1.2"></a>

### 1.2 All structure, assets and code in any Unreal Engine 5 project should look like a single person created it, no matter how many people contributed

Moving from one project to another should not cause a re-learning of style and structure. Conforming to a style guide removes unneeded
guesswork and ambiguities.

It also allows for more productive creation and maintenance as one does not need to think about style. Simply follow the instructions. This
style guide is written with best practices in mind, meaning that by following this style guide you will also minimize hard to track issues.

<a name="principles-friends"></a>
<a name="1.3"></a>

### 1.3 Friends do not let friends have bad style

If you see someone working either against a style guide or no style guide, try to correct them.

When working within a team or discussing within a community such
as [Unreal Source]([http://join.unrealslackers.org/](https://discord.gg/unrealsource)), it is far easier to help and to ask for help when
people are consistent. Nobody likes to help untangle someone's Blueprint spaghetti or deal with assets that have names they can't
understand.

If you are helping someone whose work conforms to a different but consistent and sane style guide, you should be able to adapt to it.

<a name="principles-team-without-style-guide"></a>
<a name="1.4"></a>

### 1.4 A team without a style guide is no team of mine

When joining an Unreal Engine 5 team, one of your first questions should be "Do you have a style guide?". If the answer is no, you should be
skeptical about their ability to work as a team.

<a name="naming"></a>
<a name="2"></a>

**[⬆ Back to Top](#table-of-contents)**

## 2. Naming Conventions

Naming conventions should be treated as law. A project that conforms to a naming convention is able to have its assets managed, searched,
parsed and maintained with incredible ease.

Most things are prefixed with prefixes being generally an acronym of the asset type followed by an underscore.

<a name="naming-forbidden-characters"></a>
<a name="2.1"></a>

### 2.1 Forbidden Characters

In any `Identifier` of any kind, **never** use the following unless absolutely forced to:

* White space of any kind
* Backward slashes `\`
* Symbols i.e. `#!@$%`
* Any Unicode character

Any `Identifier` should strive to only have the following characters when possible (the RegEx `[A-Za-z0-9_]+`)

* ABCDEFGHIJKLMNOPQRSTUVWXYZ
* abcdefghijklmnopqrstuvwxyz
* 1234567890
* _ (sparingly)

The reasoning for this is this will ensure the greatest compatibility of all data across all platforms across all tools, and help prevent
downtime due to potentially bad character handling for identifiers in code you don't control.

<a name="naming-bp"></a>
<a name="2.2"></a>

### 2.2 Blueprints Naming

<a name="naming-bp-base-asset-name"></a>
<a name="2.2.1"></a>

### 2.2.1 Base Asset Name - `Prefix_BaseAssetName_Variant_Suffix`

All assets should have a *Base Asset Name*. A Base Asset Name represents a logical grouping of related assets. Any asset that is part of
this logical group should follow the standard of  `Prefix_BaseAssetName_Variant_Suffix`.

Keeping the pattern `Prefix_BaseAssetName_Variant_Suffix` and in mind and using common sense is generally enough to warrant good asset
names. Here are some detailed rules regarding each element.

`Prefix` and `Suffix` are to be determined by the asset type through the following [Name Modifier](#naming-modifiers) tables.

`BaseAssetName` should be determined by a short and easily recognizable name related to the context of this group of assets. For example, if
you had a character named Bob, all of Bob's assets would have the `BaseAssetName` of `Bob`.

For unique and specific variations of assets, `Variant` is either a short and easily recognizable name that represents logical grouping of
assets that are a subset of an asset's base name. For example, if Bob had multiple skins these skins should still use `Bob` as the
`BaseAssetName` but include a recognizable `Variant`. An 'Evil' skin would be referred to as `Bob_Evil` and a 'Retro' skin would be referred
to as `Bob_Retro`.

For unique but generic variations of assets, `Variant` is a two-digit number starting at `01`. For example, if you have an environment
artist generating nondescript rocks, they would be named `Rock_01`, `Rock_02`, `Rock_03`, etc. Except for rare exceptions, you should never
require a three-digit variant number. If you have more than 100 assets, you should consider organizing them with different base names or
using multiple variant names.

Depending on how your asset variants are made, you can chain together variant names. For example, if you are creating flooring assets for an
Arch Viz project, you should use the base name `Flooring` with chained variants such as `Flooring_Marble_01`, `Flooring_Maple_01`,
`Flooring_Tile_Squares_01`.

***Examples***

**Bob**

| Asset Type               | Asset Name   |
|--------------------------|--------------|
| Skeletal Mesh            | SK_Bob       |
| Material                 | M_Bob        |
| Texture (Diffuse/Albedo) | T_Bob_D      |
| Texture (Normal)         | T_Bob_N      |
| Texture (Evil Diffuse)   | T_Bob_Evil_D |

**Rocks**

| Asset Type               | Asset Name   |
|--------------------------|--------------|
| Static Mesh (01)         | S_Rock_01    |
| Static Mesh (02)         | S_Rock_02    |
| Static Mesh (03)         | S_Rock_03    |
| Material                 | M_Rock       |
| Material Instance (Snow) | MI_Rock_Snow |

<a name="naming-modifiers"></a>
<a name="2.2.2"></a>

### 2.2.2 Name Modifiers

When naming an asset, use these tables to determine the prefix and suffix to use with an asset's [Base Asset Name](#base-asset-name).

<a name="naming-modifiers-common"></a>
<a name="2.2.2.1"></a>

### 2.2.2.1 Most Common

| Asset Type          | Prefix | Suffix    | Notes                                      |
|---------------------|--------|-----------|--------------------------------------------|
| Level / Map         |        |           |                                            |
| Level (Persistent)  |        | _P        |                                            |
| Level (Audio)       |        | _Audio    |                                            |
| Level (Lighting)    |        | _Lighting |                                            |
| Level (Geometry)    |        | _Geo      |                                            |
| Level (Gameplay)    |        | _Gameplay |                                            |
| Blueprint           | BP_    |           |                                            |
| Blueprint Component | BP_    | Component | I.e. BP_InventoryComponent                 |
| Material            | M_     |           |                                            |
| Static Mesh         | S_     |           | Many use SM_. We use S_.                   |
| Skeletal Mesh       | SK_    |           |                                            |
| Texture             | T_     | _?        | See [Textures](#naming-modifiers-textures) |
| Particle System     | PS_    |           |                                            |
| Widget Blueprint    | WBP_   |           |                                            |
| Animation Blueprint | ABP_   |           |                                            |

<a name="naming-modifiers-animations"></a>
<a name="2.2.2.2"></a>

### 2.2.2.2 Animations

| Asset Type                | Prefix | Suffix | Notes |
|---------------------------|--------|--------|-------|
| Aim Offset                | AO_    |        |       |
| Aim Offset 1D             | AO_    |        |       |
| Animation Blueprint       | ABP_   |        |       |
| Animation Composite       | AC_    |        |       |
| Animation Montage         | AM_    |        |       |
| Camera Animation Sequence | CAS_   |        |       |
| Blend Space               | BS_    |        |       |
| Blend Space 1D            | BS_    |        |       |
| Level Sequence            | LS_    |        |       |
| Morph Target              | MT_    |        |       |
| Paper Flipbook            | PFB_   |        |       |
| Rig                       | Rig_   |        |       |
| Control Rig               | CR_    |        |       |
| Skeletal Mesh             | SK_    |        |       |
| Skeleton                  | SKEL_  |        |       |

<a name="naming-modifiers-ai"></a>
<a name="2.2.2.3"></a>

### 2.2.2.3 Artificial Intelligence

| Asset Type        | Prefix       | Suffix  | Notes |
|-------------------|--------------|---------|-------|
| AI Controller     | AIC_         |         |       |
| Behavior Tree     | BT_          |         |       |
| Blackboard        | BB_          |         |       |
| Decorator         | BTDecorator_ |         |       |
| Service           | BTService_   |         |       |
| Task              | BTTask_      |         |       |
| Environment Query | EQS_         |         |       |
| EnvQueryContext   | EQS_         | Context |       |

<a name="naming-modifiers-bps"></a>
<a name="2.2.2.4"></a>

### 2.2.2.4 Blueprints

| Asset Type                 | Prefix | Suffix    | Notes                                   |
|----------------------------|--------|-----------|-----------------------------------------|
| Blueprint                  | BP_    |           |                                         |
| Blueprint Component        | BP_    | Component | I.e. BP_InventoryComponent              |
| Blueprint Function Library | BPFL_  |           |                                         |
| Blueprint Interface        | BPI_   |           |                                         |
| Blueprint Macro Library    | BPML_  |           | Do not use macro libraries if possible. |
| Enumeration                | E      |           | No underscore.                          |
| Structure                  | F or S |           | No underscore.                          |
| Widget Blueprint           | WBP_   |           |                                         |

<a name="naming-modifiers-materials"></a>
<a name="2.2.2.5"></a>

### 2.2.2.5 Materials

| Asset Type                    | Prefix  | Suffix | Notes |
|-------------------------------|---------|--------|-------|
| Material                      | M_      |        |       |
| Material (Post Process)       | PP_     |        |       |
| Material Function             | MF_     |        |       |
| Material Instance             | MI_     |        |       |
| Material Parameter Collection | MPC_    |        |       |
| Subsurface Profile            | SP_     |        |       |
| Physical Materials            | PM_     |        |       |
| Decal                         | M_, MI_ | _Decal |       |

<a name="naming-modifiers-textures"></a>
<a name="2.2.2.6"></a>

### 2.2.2.6 Textures

| Asset Type                          | Prefix | Suffix | Notes                                                   |
|-------------------------------------|--------|--------|---------------------------------------------------------|
| Texture                             | T_     |        |                                                         |
| Texture (Diffuse/Albedo/Base Color) | T_     | _D     |                                                         |
| Texture (Normal)                    | T_     | _N     |                                                         |
| Texture (Roughness)                 | T_     | _R     |                                                         |
| Texture (Alpha/Opacity)             | T_     | _A     |                                                         |
| Texture (Ambient Occlusion)         | T_     | _O     |                                                         |
| Texture (Bump)                      | T_     | _B     |                                                         |
| Texture (Emissive)                  | T_     | _E     |                                                         |
| Texture (Mask)                      | T_     | _M     |                                                         |
| Texture (Specular)                  | T_     | _S     |                                                         |
| Texture (Metallic)                  | T_     | _M     |                                                         |
| Texture (Packed)                    | T_     | _*     | See notes below about [packing](#anc-textures-packing). |
| Texture Cube                        | TC_    |        |                                                         |
| Media Texture                       | MT_    |        |                                                         |
| Render Target                       | RT_    |        |                                                         |
| Cube Render Target                  | RTC_   |        |                                                         |
| Texture Light Profile               | TLP_   |        |                                                         |

<a name="naming-modifiers-textures-packing"></a>
<a name="2.2.2.6.1"></a>

#### 2.2.2.6.1 Texture Packing

It is common practice to pack multiple layers of texture data into one texture. An example of this is packing Emissive, Roughness, Ambient
Occlusion together as the Red, Green and Blue channels of a texture respectively. To determine the suffix, simply stack the given suffix
letters from above together, e.g. `_ERO`.

> It is generally acceptable to include an Alpha/Opacity layer in your Diffuse/Albedo's alpha channel and as this is common practice, adding
`A` to the `_D` suffix is optional.

Packing 4 channels of data into a texture (RGBA) is not recommended except for an Alpha/Opacity mask in the Diffuse/Albedo's alpha channel
as a texture with an alpha channel incurs more overhead than one without.

<a name="naming-modifiers-misc"></a>
<a name="2.2.2.7"></a>

### 2.2.2.7 Miscellaneous

| Asset Type                 | Prefix   | Suffix  | Notes                                                                                     |
|----------------------------|----------|---------|-------------------------------------------------------------------------------------------|
| Animated Vector Field      | VFA_     |         |                                                                                           |
| Camera Anim                | CA_      |         |                                                                                           |
| Color Curve                | Curve_   | _Color  |                                                                                           |
| Curve Table                | Curve_   | _Table  |                                                                                           |
| Data Asset                 | DA_      |         |                                                                                           |
| Data Table                 | DT_      |         |                                                                                           |
| Float Curve                | Curve_   | _Float  |                                                                                           |
| Foliage Type               | FT_      |         |                                                                                           |
| Force Feedback Effect      | FFE_     |         |                                                                                           |
| Landscape Grass Type       | LG_      |         |                                                                                           |
| Landscape Layer            | LL_      |         |                                                                                           |
| Matinee Data               | Matinee_ |         |                                                                                           |
| Media Player               | MP_      |         |                                                                                           |
| File Media Source          | FMS_     |         |                                                                                           |
| Object Library             | OL_      |         |                                                                                           |
| Redirector                 |          |         | Fix them immediately or when you 100% sure no one is using object they are redirecting to |
| Sprite Sheet               | SS_      |         |                                                                                           |
| Static Vector Field        | VF_      |         |                                                                                           |
| Substance Graph Instance   | SGI_     |         |                                                                                           |
| Substance Instance Factory | SIF_     |         |                                                                                           |
| Touch Interface Setup      | TI_      |         |                                                                                           |
| Vector Curve               | Curve_   | _Vector |                                                                                           |

<a name="naming-modifiers-paper2d"></a>
<a name="2.2.2.8"></a>

### 2.2.2.8 Paper 2D

| Asset Type         | Prefix | Suffix | Notes |
|--------------------|--------|--------|-------|
| Paper Flipbook     | PFB_   |        |       |
| Sprite             | SPR_   |        |       |
| Sprite Atlas Group | SPRG_  |        |       |
| Tile Map           | TM_    |        |       |
| Tile Set           | TS_    |        |       |

<a name="naming-modifiers-physics"></a>
<a name="2.2.2.9"></a>

### 2.2.2.9 Physics

| Asset Type        | Prefix | Suffix | Notes |
|-------------------|--------|--------|-------|
| Physical Material | PM_    |        |       |
| Physics Asset     | PHYS_  |        |       |
| Destructible Mesh | DM_    |        |       |

<a name="naming-modifiers-sounds"></a>
<a name="2.2.2.10"></a>

### 2.2.2.10 Sounds

| Asset Type        | Prefix  | Suffix | Notes                                                           |
|-------------------|---------|--------|-----------------------------------------------------------------|
| Dialogue Voice    | DV_     |        |                                                                 |
| Dialogue Wave     | DW_     |        |                                                                 |
| Media Sound Wave  | MSW_    |        |                                                                 |
| Reverb Effect     | Reverb_ |        |                                                                 |
| Sound Attenuation | ATT_    |        |                                                                 |
| Sound Class       |         |        | No prefix/suffix. Should be put in a folder called SoundClasses |
| Sound Concurrency |         | _SC    | Should be named after a SoundClass                              |
| Sound Cue         | A_      | _Cue   | `A` from `A`udio                                                |
| Sound Mix         | Mix_    |        |                                                                 |
| Sound Wave        | A_      |        | `A` form `A`udio                                                |

<a name="naming-modifiers-ui"></a>
<a name="2.2.2.11"></a>

### 2.2.2.11 User Interface

| Asset Type         | Prefix | Suffix | Notes |
|--------------------|--------|--------|-------|
| Font               | Font_  |        |       |
| Slate Brush        | Brush_ |        |       |
| Slate Widget Style | Style_ |        |       |
| Widget Blueprint   | WBP_   |        |       |

<a name="naming-modifiers-effects"></a>
<a name="2.2.2.12"></a>

### 2.2.2.12 Effects

| Asset Type              | Prefix | Suffix | Notes |
|-------------------------|--------|--------|-------|
| Particle System         | PS_    |        |       |
| Material (Post Process) | PP_    |        |       |

**[⬆ Back to Top](#table-of-contents)**

<a name="structure"></a>
<a name="3"></a>

## 3. Content Directory Structure

Equally important as asset names, the directory structure style of a project should be considered law. Asset naming conventions and content
directory structure go hand in hand, and a violation of either causes unneeded chaos.

This style guide promotes using the Content Browser's filtering and search capabilities to locate assets by type, rather than relying on
folder-based organization. By leveraging these built-in tools, team members can efficiently find specific asset types without needing to
navigate through nested folder structures.

> If you are using the prefix [naming convention](#2.3) above, using folders to contain assets of similar types such as `Meshes`,
`Textures`, and `Materials` is a redundant practice as asset types are already both sorted by prefix and able to be filtered in the
> content browser.

### Example Project Content Structure

<pre>
|-- Content
    |-- <a href="#3.2">GenericShooter</a>
        |-- Art
        |   |-- Industrial
        |   |   |-- Ambient
        |   |   |-- Machinery
        |   |   |-- Pipes
        |   |-- Nature
        |   |   |-- Ambient
        |   |   |-- Foliage
        |   |   |-- Rocks
        |   |   |-- Trees
        |   |-- Office
        |-- Characters
        |   |-- Bob
        |   |-- Common
        |   |   |-- <a href="#3.7">Animations</a>
        |   |   |-- Audio
        |   |-- Jack
        |   |-- Steve
        |   |-- <a href="#3.1.3">Zoe</a>
        |-- <a href="#3.5">Core</a>
        |   |-- Characters
        |   |-- Engine
        |   |-- <a href="#3.1.2">GameModes</a>
        |   |-- Interactables
        |   |-- Pickups
        |   |-- Weapons
        |-- Effects
        |   |-- Electrical
        |   |-- Fire
        |   |-- Weather
        |-- <a href="#3.4">Maps</a>
        |   |-- Campaign1
        |   |-- Campaign2
        |-- <a href="#3.8">MaterialLibrary</a>
        |   |-- Debug
        |   |-- Metal
        |   |-- Paint
        |   |-- Utility
        |   |-- Weathering
        |-- Placeables
        |   |-- Pickups
        |-- Weapons
            |-- Common
            |-- Pistols
            |   |-- DesertEagle
            |   |-- RocketPistol
            |-- Rifles
</pre>

The reasons for this structure are listed in the following subsections.

<a name="structure-folder-names"></a>
<a name="3.1"></a>

### 3.1 Folder Names

These are common rules for naming any folder in the content structure.

<a name="structure-folder-names-case"></a>
<a name="3.1.1"></a>

#### 3.1.1 Always Use PascalCase[<sup>*</sup>](#terms-cases)

PascalCase refers to starting a name with a capital letter, and then instead of using spaces, every following word also starts with a
capital
letter. For example, `DesertEagle`, `RocketPistol`, and `ASeriesOfWords`.

See [Cases](#terms-cases).

<a name="structure-folder-names-no-spaces"></a>
<a name="3.1.2"></a>

#### 3.1.2 Never Use Spaces

Re-enforcing [3.1.1](#3.1.1), never use spaces. Spaces can cause various engineering tools and batch processes to fail. Ideally, your
project's root also contains no spaces and is located somewhere such as `D:\Project` instead of
`C:\Users\My Name\My Documents\Unreal Projects`.

<a name="structure-folder-names-no-unicode"></a>
<a name="3.1.3"></a>

#### 3.1.3 Never Use Unicode Characters And Other Symbols

If one of your game characters is named 'Zoë', its folder name should be `Zoe`. Unicode characters can be worse than [Spaces](#3.1.2) for
engineering tool, and some parts of UE5 don't support Unicode characters in paths either.

Related to this, if your project has [unexplained issues](https://answers.unrealengine.com/questions/101207/undefined.html) and your
computer's username has a Unicode character (i.e., your name is `Zoë`), any project located in your `My Documents` folder will suffer from
this issue. Often simply moving your project to something like `D:\Project` will fix these mysterious issues.

Using other characters outside `a-z`, `A-Z`, and `0-9` such as `@`, `-`, `_`, `,`, `*`, and `#` can also lead to unexpected and hard to
track issues on other platforms, source control and weaker engineering tools.

<a name="structure-top-level"></a>
<a name="3.2"></a>

### 3.2 Use A Top Level Folder For Project Specific Assets

All of a project's assets should exist in a folder named after the project. For example, if your project is named 'Generic Shooter', *all*
of it's content should exist in `Content/GenericShooter`.

> The `Developers` folder is not for assets that your project relies on and therefore is not project-specific.
> See [Developer Folders](#structure-developer-folder) for details about this.

There are multiple reasons for this approach.

<a name="structure-top-level-no-global-assets"></a>
<a name="3.2.1"></a>

#### 3.2.1 No Global Assets

Often in code style guides it is written that you should not pollute the global namespace, and this follows the same principle. When assets
are allowed to exist outside a project folder, it often becomes much harder to enforce a strict structure layout as assets not in a
folder encourages the bad behavior of not having to organize assets.

Every asset should have a purpose, otherwise it does not belong in a project. If an asset is an experimental test and shouldn't be used by
the project, it should be put in a [Developer](#structure-developer-folder) folder.

<a name="structure-top-level-migration-conflicts"></a>
<a name="3.2.2"></a>

#### 3.2.2 Reduce Migration Conflicts

When working on multiple projects, it is common for a team to copy assets from one project to another if they have made something useful for
both. When this occurs, the easiest way to perform the copy is to use the Content Browser's Migrate functionality as it will copy over not
just the selected asset but all of its dependencies.

These dependencies are what can easily get you into trouble. If two project's assets do not have a top level folder, and they happen to have
similarly named or already previously migrated assets, a new migration can accidentally wipe any changes to the existing assets.

This is also the primary reason why Epic's Marketplace staff enforces the same policy for submitted assets.

After a migration, safe merging of assets can be done using the 'Replace References' tool in the content browser with the added clarity of
assets not belonging to a project's top level folder are clearly pending a merge. Once assets are merged and fully migrated, there shouldn't
be another top-level folder in your Content tree. This method is *100%* guaranteed to make any migrations that occur completely safe.

##### Master Material Example

For example, say you created a master material in one project that you would like to use in another project, so you migrated that asset over.
If this asset is not in a top level folder, it may have a name like `Content/MaterialLibrary/M_Master`. If the target project doesn't have a
master material already, this should work without issue.

As work on one or both projects progresses, their respective master materials may change to be tailored for their specific projects due to
the course of normal development.

The issue comes when, for example, an artist for one project created a nice generic modular set of static meshes and someone wants to
include that set of static meshes in the second project. If the artist who created the assets used material instances based on
`Content/MaterialLibrary/M_Master` as they're instructed to, when a migration is performed there is a great chance of conflict for the
previously migrated `Content/MaterialLibrary/M_Master` asset.

This issue can be hard to predict and hard to account for. The person migrating the static meshes may not be the same person who is familiar
with the development of both projects' master material. They may not be even aware that the static meshes in question rely on material
instances which then rely on the master material. The Migrate tool requires the entire chain of dependencies to work however, and so it will
be forced to grab `Content/MaterialLibrary/M_Master` when it copies these assets to the other project, and it will overwrite the existing asset.

It is at this point where if the master materials for both projects are incompatible in *any way*, you risk breaking possibly the entire
material library for a project and any other dependencies that may have already been migrated, simply because assets were not stored
in a top level folder. The simple migration of static meshes now becomes a very ugly task.

<a name="structure-top-level-risk-free"></a>
<a name="3.2.3"></a>

#### 3.2.3 Samples, Templates and Marketplace Content Are Risk-Free

An extension to [Reduce Migration Conflicts](#structure-top-level-migration-conflicts), if a team member decides to add sample content, template
files, or assets they bought from the marketplace, it is guaranteed, as long as your project's top-level folder is uniquely named,that these new
assets will not interfere with your project.

You cannot trust marketplace content to fully conform to the [top level folder rule](#structure-top-level). There exists many assets that have
the majority of their content in a top level folder but also have possibly modified Epic sample content as well as level files polluting the
global `Content` folder.

When adhering to [top level folder rule](#structure-top-level), the worst fab conflict you can have is if two fab assets both have the same Epic
sample content. If all your assets are in a project-specific folder, including sample content you may have moved into your folder, your project
will never break.

<a name="structure-top-level-dlc"></a>
<a name="3.2.4"></a>

#### 3.2.4 DLC, Sub-Projects and Patches Are Easily Maintained

For projects that include DLC or multiple subprojects that may be migrated out or not included in certain builds, create separate top-level
content folders for these assets. This organization makes it easier to cook DLC separately from the main project content and allows
subprojects to be migrated in and out with minimal effort. When you need to modify an asset's material or add specific override behavior in
a patch, you can safely make these changes in a patch folder without risking damage to the core project.

<a name="structure-developer-folder"></a>
<a name="3.3"></a>

### 3.3 Use Developers Folder For Local Testing

During a project's development, it is very common for team members to have a sort of 'sandbox' where they can experiment freely without
risking the core project. Because this work may be ongoing, these team members may wish to put their assets on a project's source control
server. Not all teams require using the Developer folder, but ones that do use them often run into a common problem with assets submitted to
source control.

It is very easy for a team member to accidentally use assets that are not ready for use, which will cause issues once those assets are
removed. For example, an artist may be iterating on a modular set of static meshes and still working on getting their sizing and grid
snapping correct. If a world builder sees these assets in the main project folder, they might use them all over a level not knowing they
could be subject to incredible change and/or removal. This causes massive amounts of re-working for everyone on the team to resolve.

If these modular assets were placed in a Developer folder, the world builder should never have had a reason to use them, and the whole issue
would never happen. The Content Browser has specific View Options that will hide Developer folders (they are hidden by default), making it
impossible to accidentally use Developer assets under normal use.

Once the assets are ready for use, an artist simply has to move the assets into the project-specific folder and fix up redirectors. This is
essentially 'promoting' the assets from experimental to production.

<a name="structure-maps-folder"></a>
<a name="3.4"></a>

### 3.4 All Map[<sup>*</sup>](#terms-levels-maps) Files Belong In A Folder Called Maps

Map files are incredibly special, and it is common for every project to have its own map naming system, especially if they work with
sublevels or streaming levels. No matter what system of map organization is in place for the specific project, all levels should belong in
`/Content/Project/Maps`.

Being able to tell someone to open a specific map without having to explain where it is is a great time saver and general 'quality of life'
improvement. It is common for levels to be within subfolders of `Maps`, such as `Maps/Campaign1/` or `Maps/Arenas`, but the most important
thing here is that they all exist within `/Content/Project/Maps`.

This also simplifies the job of cooking for engineers. Wrangling levels for a build process can be extremely frustrating if they have to dig
through arbitrary folders for them. If a team's maps are all in one place, it is much harder to accidentally not cook a map in a build. It
also simplifies lighting build scripts as well as QA processes.

<a name="structure-core-folder"></a>
<a name="3.5"></a>

### 3.5 Use A `Core` Folder For Critical Blueprints And Other Assets

Use `/Content/Project/Core` folder for assets that are absolutely fundamental to a project's workings. For example, base `GameMode`,
`Character`, `PlayerController`, `GameState`, `PlayerState`, and related Blueprints should live here.

This creates a very clear "don't touch these" message for other team members. Non-engineers should have very little reason to enter the
`Core` folder. Following a good code structure style, designers should be making their gameplay tweaks in child classes that expose
functionality. World builders should be using prefab Blueprints in designated folders instead of potentially abusing base classes.

For example, if your project requires pickups that can be placed in a level, there should exist a base Pickup class in `Core/Pickups` that
defines base behavior for a pickup. Specific pickups such as a Health or Ammo should exist in a folder such as
`/Content/Project/Placeables/Pickups/`. Game designers can define and tweak pickups in this folder however they please, but they should not
touch `Core/Pickups` as they may unintentionally break pickups project-wide.

<a name="structure-redundant-folders"></a>
<a name="3.6"></a>

### 3.6 Redundant Folders

<a name="structure-redundant-folders-assets"></a>
<a name="3.6.1"></a>

#### 3.6.1 Creating a folder named `Assets` is redundant

All assets are assets.

<a name="structure-redundant-folders-meshes-textures-materials"></a>
<a name="3.6.2"></a>

#### 3.6.2 Creating a folder named `Meshes`, `Textures`, or `Materials` is redundant

All asset names are named with their asset type in mind. These folders offer only redundant information, and the use of these folders can
easily be replaced with the robust and easy-to-use filtering system the Content Browser provides.

Want to view only static mesh in `Environment/Rocks/`? Simply turn on the Static Mesh filter. If all assets are named correctly, they will
also be sorted in alphabetical order regardless of prefixes. Want to view both static meshes and skeletal meshes? Simply turn on both
filters. This eliminates the need to potentially have to `Control-Click` select two folders in the Content Browser's tree view.

> This also extends the full path name of an asset for very little benefit. The `S_` prefix for a static mesh is only two characters, whereas
`Meshes/` is seven characters.

Not doing this also prevents the inevitability of someone putting a static mesh or a texture in a `Materials` folder.

<a name="structure-huge-sets"></a>
<a name="3.7"></a>

### 3.7 Huge Asset Sets Get Their Own Folder Layout

This can be seen as a pseudo-exception to [Redundant Folders](#structure-redundant-folders).

There are certain asset types that have a huge volume of related files where each asset has a unique purpose. The two most common are
Animation and Audio assets. If you find yourself having 15+ of these assets that belong together, they should be together.

For example, animations that are shared across multiple characters should lay in `Characters/Common/Animations` and may have subfolders
such as `Locomotion` or `Cinematic`.

> This does not apply to assets like textures and materials. It is common for a `Rocks` folder to have a large number of textures if there
> are a large number of rocks, however, these textures are generally only related to a few specific rocks and should be named appropriately.
> Even if these textures are part of a [Material Library](#structure-material-library).

<a name="structure-material-library"></a>
<a name="3.8"></a>

### 3.8 MaterialLibrary

If your project makes use of master materials, layered materials or any form of reusable materials or textures that do not belong to any
subset of assets, these assets should be located in `Content/Project/MaterialLibrary`.

This way all 'global' materials have a place to live and are easily located.

> This also makes it incredibly easy to enforce a 'use material instances only' policy within a project. If all artists and assets should be
> using material instances, then the only regular material assets that should exist are within this folder. You can easily verify this by
> searching for base materials in any folder that isn't the `MaterialLibrary`.

The `MaterialLibrary` doesn't have to consist purely of materials. Shared utility textures, material functions and other things of this
nature should be stored here as well within folders that designate their intended purpose. For example, generic noise textures should be
located in `MaterialLibrary/Utility`.

Any testing or debug materials should be within `MaterialLibrary/Debug`. This allows debug materials to be easily stripped from a project
before shipping and makes it incredibly clear if production assets are using them if reference errors are shown.

<a name="structure-no-empty-folders"></a>
<a name="3.9"></a>

### 3.9 No Empty Folders

There simply shouldn't be any empty folders. They clutter the content browser.

If you find that the content browser has an empty folder you can't delete, you should perform the following:

1. Be sure you're using source control.
2. Immediately run Fix Up Redirectors on your project.
3. Navigate to the folder on-disk and delete the assets inside.
4. Close the editor.
5. Make sure your source control state is in sync (i.e., if using Perforce, run a Reconcile Offline Work on your content directory)
6. Open the editor. Confirm everything still works as expected. If it doesn't, revert, figure out what went wrong and try again.
7. Ensure the folder is now gone.
8. Submit changes to source control.

**[⬆ Back to Top](#table-of-contents)**

<a name="bp"></a>
<a name="4"></a>

## 4. Blueprints

This section will focus on Blueprint classes and their internals. When possible, style rules conform
to [Epic's Coding Standard](https://docs.unrealengine.com/latest/INT/Programming/Development/CodingStandard).

Remember: Blueprinting badly bears blunders, beware! (Phrase by [KorkuVeren](http://github.com/KorkuVeren))

<a name="bp-compiling"></a>
<a name="4.1"></a>

### 4.1 Compiling

All blueprints should compile with zero warnings and zero errors. You should fix blueprint warnings and errors immediately as they can
quickly cascade into terrifying unexpected behavior.

Do **not** submit broken blueprints to source control.

Broken blueprints can cause problems that manifest in other ways, such as broken references, unexpected behavior, cooking failures and
frequent unneeded recompilation. A broken blueprint has the power to break your entire game.

<a name="bp-vars"></a>
<a name="4.2"></a>

### 4.2 Variables

The words `variable` and `property` may be used interchangeably.

<a name="bp-vars-naming"></a>
<a name="4.2.1"></a>

#### 4.2.1 Naming

<a name="bp-vars-naming-nouns"></a>
<a name="4.2.1.1"></a>

##### 4.2.1.1 Nouns

All non-boolean variable names must be clear, unambiguous and descriptive nouns.

<a name="bp-vars-naming-case"></a>
<a name="4.2.1.2"></a>

##### 4.2.1.2 PascalCase

All non-boolean variables should be in the form of [PascalCase](#terms-cases).

***Examples***

* `Score`
* `Kills`
* `TargetPlayer`
* `Range`
* `CrosshairColor`
* `AbilityID`

<a name="bp-vars-naming-bool-prefix"></a>
<a name="4.2.1.3"></a>

##### 4.2.1.3 Boolean `b` Prefix

All booleans should be named in PascalCase but prefixed with a lowercase `b`.
UE5 Blueprint editors know not to include the `b` in user-friendly displays of the variable.

***Examples***

| **Bad** | **Good** |
|---------|----------|
| `Dead`  | `bDead`  |
| `Evil`  | `bEvil`  |

<a name="bp-vars-naming-bool-names"></a>
<a name="4.2.1.4"></a>

##### 4.2.1.4 Boolean Names

<a name="bp-vars-naming-bool-names-no-questions"></a>
<a name="4.2.1.4.1"></a>

###### 4.2.1.4.1 Booleans should not be phrased as questions

All booleans should be named as descriptive adjectives when possible if representing general information. Do not include words that phrase
the variable as a question, such as `Is`. This is reserved for functions.

***Examples***

| **Bad**      | **Good**   |
|--------------|------------|
| `bIsDead`    | `bDead`    |
| `bIsHostile` | `bHostile` |

<a name="bp-vars-naming-bool-names-no-continuous-tense"></a>
<a name="4.2.1.4.2"></a>

#### 4.2.1.4.2 Booleans should not be phrased in continuous tense

Try to not use verbs such as `bRunning`. Verbs tend to lead to complex states.

<a name="bp-vars-naming-bool-names-complex-states"></a>
<a name="4.2.1.4.3"></a>

###### 4.2.1.4.3 Complex States

Do not use booleans to represent complex and/or dependent states. This makes state adding and removing complex and no longer easily
readable. Use an enumeration instead.

Example: When defining a weapon, do **not** use `bReloading` and `bEquipping` if a weapon can't be both reloading and equipping. Define an
enumeration named `EWeaponState` and use a variable with this type named `WeaponState` instead. This makes it far easier to add new states
to weapons.

Example: Do **not** use `bRunning` if you also need `bWalking` or `bSprinting`. This should be defined as an enumeration with clearly defined
state names.

<a name="bp-vars-naming-context"></a>
<a name="4.2.1.5"></a>

##### 4.2.1.5 Considered Context

All variable names must not be redundant with their context as all variable references in Blueprint will always have context.

***Examples***

Consider a Blueprint called `BP_PlayerCharacter`. All of these variables are named redundantly. It is implied that the variable is representative
of the `BP_PlayerCharacter` it belongs to
because it is `BP_PlayerCharacter` that is defining these variables.

| **Bad**               | **Good**       |
|-----------------------|----------------|
| `PlayerScore`         | `Score`        |
| `PlayerKills`         | `Kills`        |
| `MyTargetPlayer`      | `TargetPlayer` |
| `MyCharacterName`     | `Name`         |
| `CharacterSkills`     | `Skills`       |
| `ChosenCharacterSkin` | `Skin`         |

<a name="bp-vars-naming-atomic"></a>
<a name="4.2.1.6"></a>

##### 4.2.1.6 Do *Not* Include Atomic Type Names

Atomic or primitive variables are variables that represent data in their simplest form, such as booleans, integers, floats and
enumerations.

Strings and vectors are considered atomic in terms of style when working with Blueprints; however, they are technically not atomic.

> While vectors consist of three floats, vectors are often able to be manipulated as a whole, same with rotators.

> Do *not* consider Text variables as atomic, they are secretly hiding localization functionality. The atomic type of string of characters is
`String`, not `Text`.

Atomic variables should not have their type name in their name.

Example: Use `Score`, `Kills`, and `Description` **not** `ScoreFloat`, `FloatKills`, `DescriptionString`.

The only exception to this rule is when a variable represents 'a number of' something to be counted *and* when using a name without a variable
type is not easy to read.

Example: A fence generator needs to generate X number of posts. Store X in `NumPosts` or `PostsCount` instead of `Posts` as `Posts` may
potentially read as an Array of a variable type named `Post`.

<a name="bp-vars-naming-complex"></a>
<a name="4.2.1.7"></a>

##### 4.2.1.7 Do Include Non-Atomic Type Names

Non-atomic or complex variables are variables that represent data as a collection of atomic variables. Structs, Classes, Interfaces and
primitives with hidden behavior such as `Text` and `Name` all qualify under this rule.

> While an Array of an atomic variable type is a list of variables, Arrays do not change the 'atomicness' of a variable type.

These variables should include their type name while still considering their context.

If a class owns an instance of a complex variable, i.e., if a `BP_PlayerCharacter` owns a `BP_Hat`, it should be stored as the variable type
as without any name modifications.

Example: Use `Hat`, `Flag`, and `Ability` **not** `MyHat`, `MyFlag`, and `PlayerAbility`.

If a class does not own the value a complex variable represents, you should use a noun along with the variable type.

Example: If a `BP_Turret` has the ability to target a `BP_PlayerCharacter`, it should store its target as `TargetPlayer` as when in the
context of `BP_Turret` it should be clear that it is a reference to another complex variable type that it does not own.

<a name="bp-vars-naming-arrays"></a>
<a name="4.2.1.8"></a>

##### 4.2.1.8 Arrays

Arrays follow the same naming rules as above but should be named as a plural noun.

Example: Use `Targets`, `Hats`, and `EnemyPlayers`, **not** `TargetList`, `HatArray`, `EnemyPlayerArray`.

<a name="bp-vars-editable"></a>
<a name="4.2.2"></a>

#### 4.2.2 Editable Variables

All variables that are safe to change the value of to configure behavior of a blueprint should be marked as `Editable`.

Conversely, all variables that are not safe to change or should not be exposed to designers should *not* be marked as editable, unless for
engineering reasons the variable must be marked as `Expose On Spawn`.

Do not arbitrarily mark variables as `Editable`.

<a name="bp-vars-editable-descriptions"></a>
<a name="4.2.2.1"></a>

##### 4.2.2.1 Descriptions

Every variable should have `Description` filled (especially if it's `Editable`) that explains what for this variable is and how changing
this value affects the behavior of the blueprint.

<a name="bp-vars-editable-ranges"></a>
<a name="4.2.2.2"></a>

##### 4.2.2.2 Slider And Value Ranges

All `Editable` variables should make use of slider and value ranges if there is ever a value that a variable should *not* be set to.

Example: A blueprint that generates fence posts might have an editable variable named `PostsCount` and a value of -1 would not make any
sense. Use the range fields to mark 0 as a minimum.

If an editable variable is used in a Construction Script, it should have a reasonable Slider Range defined so that someone cannot accidentally
assign it a large value that could crash the editor.

A Value Range only needs to be defined if the bounds of a value are known. While a Slider Range prevents accidental large number inputs, an
undefined Value Range allows a user to specify a value outside the Slider Range that may be considered 'dangerous' but still valid.

<a name="bp-vars-categories"></a>
<a name="4.2.3"></a>

#### 4.2.3 Categories

All variables should be stored in the top category named as initials of the project i.e. `GenericShooter` - `GS`.

All `Editable` variables should be in subcategory called `Config`.

If a class has a large number of variables, all `Editable` variables should be categorized into subcategories using the category `Config`
as the base category. Non-editable variables should be categorized into descriptive categories describing their usage.

> You can define subcategories by using the pipe character `|`, i.e. `GS | Config | Animations`.

Example: A weapon class set of variables might be organized as:

    |-- GS
    |   |-- Config
    |   |   |-- Animations
    |   |   |-- Effects
    |   |   |-- Audio
    |   |   |-- Recoil
    |   |   |-- Timings
    |   |-- Animations
    |   |-- State
    |   |-- Visuals

<a name="bp-vars-access"></a>
<a name="4.2.4"></a>

#### 4.2.4 Variable Access Level

In C++, variables have a concept of access level. `Public` means any code outside the class can access the variable. `Protected` means only
the class and any child classes can access this variable internally. `Private` means only this class and no child classes can access this
variable.

Blueprints do not have a defined concept of `protected` access currently.

Treat `Editable` variables as `public` variables. Treat non-editable variables as `protected` variables.

<a name="bp-vars-access-private"></a>
<a name="4.2.4.1"></a>

##### 4.2.4.1 Private Variables

Unless it is known that a variable should only be accessed within the class it is defined and never a child class, do not mark variables as
`private`. Until variables are able to be marked `protected`, reserve `private` for when you absolutely know you want to restrict child
class usage.

<a name="bp-vars-advanced"></a>
<a name="4.2.5"></a>

#### 4.2.5 Advanced Display

If a variable should be editable but often untouched, mark it as `Advanced Display`. This makes the variable hidden unless the advanced
display arrow is clicked.

To find the `Advanced Display` option, it is listed as an advanced displayed variable in the variable details list.

<a name="bp-vars-transient"></a>
<a name="4.2.6"></a>

#### 4.2.6 Transient Variables

`Transient` variables are variables that do not need to have their value saved and loaded and have an initial value of zero or null. This is
useful for references to other objects and actors whose value isn't known until run-time. This prevents the editor from ever saving a reference
to it and speeds up saving and loading of the blueprint class.

Because of this, all transient variables should always be initialized as zero or null. To do otherwise would result in hard to debug errors.

<a name="bp-vars-config"></a>
<a name="4.2.7"></a>

#### 4.2.8 Config Variables

Do not use the `Config Variable` flag. This makes it harder for designers to control blueprint behavior. Config variables should only be
used in C++ for rarely changed variables. Think of them as `Advanced Advanced Display` variables.

<a name="bp-funcs"></a>
<a name="4.3"></a>

### 4.3 Functions, Events and Event Dispatchers

This section describes how you should author functions, events and event dispatchers. Everything that applies to functions also applies to
events, unless otherwise noted.

<a name="bp-funcs-naming"></a>
<a name="4.3.1"></a>

#### 4.3.1 Naming

The naming of functions, events and event dispatchers is critically important. Based on the name alone, certain assumptions can be made
about functions. For example:

* Is it a pure function?
* Is it fetching state information?
* Is it a handler?
* Is it an RPC?
* What is its purpose?

These questions and more can all be answered when functions are named appropriately.

<a name="bp-funcs-naming-verb-rule"></a>
<a name="4.3.1.1"></a>

#### 4.3.1.1 Verb rule

All functions should be verbs.  
All functions and events perform some form of action, whether it's getting info, calculating data or causing something to explode.
Therefore, all functions should all start with verbs. They should be worded in the present tense whenever possible. They should also have
some context as to what they are doing.

`OnRep` functions, event handlers and event dispatchers are an exception to this rule.

***Examples***

| **Bad**                                              | **Good**                                                                                                                     |
|------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------|
| `Dead` - Is Dead? Will deaden?                       | `Fire` - Good example if in a Character / Weapon class, as it has context. Bad if in a Barrel / Grass / any ambiguous class. |
| `Rock`                                               | `Jump` - Good example if in a Character class, otherwise, needs context.                                                     |
| `ProcessData` - Ambiguous, these words mean nothing. | `Explode`                                                                                                                    |
| `PlayerState` - Nouns are ambiguous.                 | `ReceiveMessage`                                                                                                             |
| `Color` - Verb with no context, or ambiguous noun.   | `SortPlayerArray`                                                                                                            |
|                                                      | `GetArmOffset`                                                                                                               |
|                                                      | `GetCoordinates`                                                                                                             |
|                                                      | `UpdateTransforms`                                                                                                           |
|                                                      | `EnableBigHeadMode`                                                                                                          |
|                                                      | `IsEnemy` - ["Is" is a verb.](http://writingexplained.org/is-is-a-verb)                                                      |

<a name="bp-funcs-naming-onrep"></a>
<a name="4.3.1.2"></a>

#### 4.3.1.2 Property RepNotify Functions Always `OnRep_Variable`

All functions for replicated with notification variables should have the form `OnRep_Variable`. This is forced by the Blueprint editor.

<a name="bp-funcs-naming-bool"></a>
<a name="4.3.1.3"></a>

#### 4.3.1.3 Info Functions Returning Bool Should Ask Questions

When writing a function that does not change the state of or modify any object and is purely for getting information, state, or computing a
yes/no value, it should ask a question. This should also follow [the verb rule](#bp-funcs-verb-rule).

This is extremely important as if a question is not asked, it may be assumed that the function performs an action and is returning whether
that action succeeded.

***Examples***

| **Bad**                                                                        | **Good**                                                                                                                                                                                     |
|--------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `Fire` - Is on fire? Will fire? Do fire?                                       | `IsDead`                                                                                                                                                                                     |
| `OnFire` - Can be confused with event dispatcher for firing.                   | `IsOnFire`                                                                                                                                                                                   |
| `Dead` - Is dead? Will deaden?                                                 | `IsAlive`                                                                                                                                                                                    |
| `Visibility` - Is visible? Set visibility? A description of flying conditions? | `IsSpeaking`                                                                                                                                                                                 |
|                                                                                | `IsHavingAnExistentialCrisis`                                                                                                                                                                |
|                                                                                | `IsVisible`                                                                                                                                                                                  |
|                                                                                | `HasWeapon` - ["Has" is a verb.](http://grammar.yourdictionary.com/parts-of-speech/verbs/Helping-Verbs.html)                                                                                 |
|                                                                                | `WasCharging` - ["Was" is past-tense of "be".](http://grammar.yourdictionary.com/parts-of-speech/verbs/Helping-Verbs.html) Use "was" when referring to 'previous frame' or 'previous state'. |
|                                                                                | `CanReload` - ["Can" is a verb.](http://grammar.yourdictionary.com/parts-of-speech/verbs/Helping-Verbs.html)                                                                                 |

<a name="bp-funcs-naming-event-handlers"></a>
<a name="4.3.1.4"></a>

#### 4.3.1.4 Event Handlers and Dispatchers Should Start With `On`

Any function that handles an event or dispatches an event should start with `On` and continue to
follow [the verb rule](#bp-funcs-verb-rule). The verb may move to the end, however, if past-tense reads better.

[Collocations](http://dictionary.cambridge.org/us/grammar/british-grammar/about-words-clauses-and-sentences/collocation) of the word `On`
are exempt from following the verb rule.

`Handle` is not allowed. It is 'Unreal' to use `On` instead of `Handle`, while other frameworks may prefer to use `Handle` instead of `On`.

***Examples***

| **Bad**         | **Good**                                |
|-----------------|-----------------------------------------|
| `OnData`        | `OnDeath` - Common collocation in games |
| `OnTarget`      | `OnPickup`                              |
| `HandleMessage` | `OnReceiveMessage`                      |
| `HandleDeath`   | `OnMessageRecieved`                     |
|                 | `OnTargetChanged`                       |
|                 | `OnClick`                               |
|                 | `OnLeave`                               |

<a name="bp-funcs-naming-rpcs"></a>
<a name="4.3.1.5"></a>

#### 4.3.1.5 Remote Procedure Calls Should Be Prefixed With Target

Any time an RPC is created, it should be prefixed with either `Server_`, `Client_`, or `Multicast_`. **No exceptions**.

After the prefix, follow all other rules regarding function naming.

***Examples***

| **Bad**                                                    | **Good**                      |
|------------------------------------------------------------|-------------------------------|
| `FireWeapon` - Does not indicate it's an RPC of some kind. | `Server_FireWeapon`           |
| `ServerClientBroadcast` - Confusing.                       | `Client_NotifyDeath`          |
| `AllNotifyDeath` - Use `Multicast`, never `All`.           | `Multicast_SpawnTracerEffect` |
| `ClientWeapon` - No verb, ambiguous.                       | `OnMessageRecieved`           |
|                                                            | `OnTargetChanged`             |
|                                                            | `OnClick`                     |
|                                                            | `OnLeave`                     |

<a name="bp-funcs-return"></a>
<a name="4.3.2"></a>

#### 4.3.2 All Functions Must Have Return Nodes

All functions must have return nodes, no exceptions.

Return nodes explicitly note that a function has finished its execution. In a world where blueprints can be filled with `Sequence`,
`ForLoopWithBreak`, and backwards reroute nodes, explicit execution flow is important for readability, maintenance and easier debugging.

The Blueprint compiler is able to follow the flow of execution and will warn you if there is a branch of your code with an unhandled return
or bad flow if you use return nodes.

In situations where a programmer adds a pin to a Sequence node or logic after a for loop completes, but an early return might occur within
the loop iteration, this can lead to accidental errors in code flow. The Blueprint compiler's warnings will immediately alert developers to
these flow control issues.

<a name="bp-funcs-node-limit"></a>
<a name="4.3.3"></a>

#### 4.3.3 No Function Should Have More Than 50 Nodes

Simply, no function should have more than 50 nodes. Any function this big should be broken down into smaller functions for readability and
ease of maintenance.

The following nodes are not counted as they are deemed to not increase function complexity:

* Comment
* Route
* Cast
* Getting a Variable
* Breaking a Struct
* Function Entry
* Self

<a name="bp-funcs-description"></a>
<a name="4.3.4"></a>

#### 4.3.4 All Functions Should Have A Description

Simply, any function should have its description filled out.

<a name="bp-funcs-category"></a>
<a name="4.3.5"></a>

#### 4.3.5 All Functions Must Be Categorized By Project Name Initials

All functions must be categorized by project name initials, so it would be easier to distinguish between our and engine functions.
For example `Generic Shooter`, `GS` or `GS|Config`.

<a name="bp-graphs"></a>
<a name="4.4"></a>

### 4.4 Blueprint Graphs

This section covers things that apply to all Blueprint graphs.

<a name="bp-graphs-spaghetti"></a>
<a name="4.4.1"></a>

#### 4.4.1 No Spaghetti

Wires should have clear beginnings and ends. You should never have to mentally untangle wires to make sense of a graph. Many of the
following sections are dedicated to reducing spaghetti.

<a name="bp-graphs-align-wires"></a>
<a name="4.4.2"></a>

#### 4.4.2 Align Wires Not Nodes

Always align wires, not nodes. You can't always control the size and pin location on a node, but you can always control the location of a
node and thus control the wires. Straight wires provide a clear linear flow. *Wiggly wires wear wits wickedly*. You can straighten wires by
using the Straighten Connections command with BP nodes selected. `Hotkey: Q`

**Good example:** The tops of the nodes are staggered to keep a perfectly straight white exec line.
![Aligned By Wires](https://github.com/Wered6/UE5-StyleGuide/blob/main/images/bp-graphs-align-wires-good.png?raw=true "Aligned By Wires")

**Bad Example:** The tops of the nodes are aligned, creating a wiggly white exec line.
![Bad](https://github.com/Wered6/UE5-StyleGuide/blob/main/images/bp-graphs-align-wires-bad.png?raw=true "Wiggly")

**Acceptable Example:** Certain nodes might not cooperate no matter how you use the alignment tools. In this situation, try to minimize the
wiggle by bringing the node in closer.
![Acceptable](https://github.com/Wered6/UE5-StyleGuide/blob/main/images/bp-graphs-align-wires-acceptable.png?raw=true "Acceptable")

<a name="bp-graphs-exec-first"></a>
<a name="4.4.3"></a>

#### 4.4.3 White Exec Lines Are Top Priority

If you ever have to decide between straightening a linear white exec line or straightening data lines of some kind, always straighten the white
exec line.

<a name="bp-graphs-getters-invoking"></a>
<a name="4.4.4"></a>

#### 4.4.4 Getters Are Invoked In Every Use

When you call getters or pure functions, keep in mind they run every time they're used—even if connected to multiple wires. This means a
pure function will recalculate everything inside it each time it's called.

So instead of connecting one getter node to multiple places and creating wire spaghetti, it's better to just use a new getter node each time
you need that value.

**Good example:** Every wire has its own getter, and it's more readable.
![Good](https://github.com/Wered6/UE5-StyleGuide/blob/main/images/bp-graphs-getters-invoking-good.png?raw=true "Good")

**Bad example:** Wires are connected to one getter, it might be less readable in longer connections.
![Bad](https://github.com/Wered6/UE5-StyleGuide/blob/main/images/bp-graphs-getters-invoking-bad.png?raw=true "Bad")

<a name="bp-graphs-comments"></a>
<a name="4.4.5"></a>

#### 4.4.5 Graphs Should Be Reasonably Commented

Blocks of nodes should be wrapped in comments that describe their higher-level behavior. While every function should be well named so that
each node is easily readable and understandable, groups of nodes contributing to a purpose should have their purpose described in
a comment block. If a function has few blocks of nodes, and it's clear that the nodes are serving a direct purpose in the
function's goal, then they do not need to be commented as the function name and description should suffice.

<a name="bp-graphs-cast-error-handling"></a>
<a name="4.4.6"></a>

#### 4.4.6 Graphs Should Handle Casting Errors Where Appropriate

If a function or event assumes that a cast always succeeds, it should appropriately report a failure in logic if the cast fails. This lets
others know why something 'supposed to work' doesn't. A function should also attempt a graceful recover after a failed cast if it's known that
the reference being cast could ever fail to be cast.

This does not mean every cast node should have its failure handled. In many cases, especially events regarding things like collisions, it is
expected that execution flow terminates on a failed cast quietly.

<a name="bp-graphs-dangling-nodes"></a>
<a name="4.4.7"></a>

#### 4.4.7 Graphs Should Not Have Any Dangling / Loose / Dead Nodes

All nodes in all blueprint graphs must have a purpose. You should not leave dangling blueprint nodes around that have no purpose or are not
executed.

**[⬆ Back to Top](#table-of-contents)**

<a name="sm"></a>
<a name="5"></a>

## 5. Static Meshes

This section will focus on Static Mesh assets and their internals.

<a name="sm-uvs"></a>
<a name="5.1"></a>

### 5.1 Static Mesh UVs

<a name="sm-uvs-no-missing"></a>
<a name="5.1.1"></a>

#### 5.1.1 All Meshes Must Have UVs

Pretty simple. All meshes, regardless of how they are to be used, should not be missing UVs.

<a name="sm-uvs-no-overlapping"></a>
<a name="5.1.2"></a>

#### 5.1.2 All Meshes Must Not Have Overlapping UVs for Lightmaps

Pretty simple. All meshes, regardless of how they are to be used, should have valid non-overlapping UVs.

<a name="sm-lods"></a>
<a name="5.2"></a>

### 5.2 LODs Should Be Set Up Correctly

This is a subjective check on a per-project basis, but as a general rule, any mesh that can be seen at varying distances should have proper
LODs.

<a name="sm-modular-snapping"></a>
<a name="5.3"></a>

### 5.3 Modular Socketless Assets Should Snap To The Grid Cleanly

This is a subjective check on a per-asset basis; however, any modular socketless assets should snap together cleanly based on the project's
grid settings.

It is up to the project whether to snap based on a power of 2 grid or on a base 10 grid. However, if you are authoring modular socketless
assets for the marketplace, Epic's requirement is that they snap cleanly when the grid is set to 10 units or bigger.

<a name="sm-collision"></a>
<a name="5.4"></a>

### 5.4 All Meshes Must Have Collision

Regardless of whether an asset is going to be used for collision in a level, all meshes should have proper collision defined. This helps the
engine with things such as bounds calculations, occlusion and lighting. Collision should also be well-formed to the asset.

<a name="sm-scaled"></a>
<a name="5.5"></a>

### 5.5 All Meshes Should Be Scaled Correctly

This is a subjective check on a per-project basis; however, all assets should be scaled correctly to their project. Level designers or
blueprint authors should not have to tweak the scale of meshes to get them to confirm in the editor. Scaling meshes in the engine should be
treated as a scale override, not a scale correction.

**[⬆ Back to Top](#table-of-contents)**

<a name="levels"></a>
<a name="6"></a>

## 6. Levels / Maps

[See Terminology Note](#terms-levels-maps) regarding "levels" vs. "maps".

This section will focus on Level assets and their internals.

<a name="levels-no-errors-or-warnings"></a>
<a name="6.1"></a>

### 6.1 No Errors Or Warnings

All levels should load with zero errors or warnings. If a level loads with any errors or warnings, they should be fixed immediately to
prevent cascading issues.

You can run a map check on an open level in the editor by using the console command "map check".

<a name="levels-lighting-should-be-built"></a>
<a name="6.2"></a>

### 6.2 Lighting Should Be Built

It is normal during development for levels to occasionally not have lighting built. When doing a test/internal/shipping build or any build
that is to be distributed, however, lighting should always be built.

<a name="levels-no-visible-z-fighting"></a>
<a name="6.3"></a>

### 6.3 No Player Visible Z Fighting

Levels should not have any [z-fighting](https://en.wikipedia.org/wiki/Z-fighting) in all areas visible to the player.

<a name="levels-fab-rules"></a>
<a name="6.4"></a>

### 6.4 Fab Specific Rules

If a project is to be sold on the Fab, it must follow these rules.

<a name="levels-fab-rules-overview"></a>
<a name="6.4.1"></a>

#### 6.4.1 Overview Level

If your project contains assets that should be visualized or demoed, you must have a map within your project that contains the name
"Overview".

This overview map, if it is visualizing assets, should be set up according
to [Epic's guidelines](https://dev.epicgames.com/documentation/en-us/fab/asset-file-format-and-structure-requirements-in-fab#maps).

For example, `InteractionComponent_Overview`.

<a name="levels-fab-rules-demo"></a>
<a name="6.4.2"></a>

#### 6.4.2 Demo Level

If your project contains assets that should be demoed or come with some sort of tutorial, you must have a map within your project that
contains the name "Demo". This level should also contain documentation within it in some form that illustrates how to use your project. See
Epic's Content Examples project for good examples on how to do this.

If your project is a gameplay mechanic or other form of a system as opposed to an art pack, this can be the same as your "Overview" map.

For example, `InteractionComponent_Overview_Demo`, `ExplosionKit_Demo`.

**[⬆ Back to Top](#table-of-contents)**

<a name="textures"></a>
<a name="7"></a>

## 7. Textures

This section will focus on Texture assets and their internals.

<a name="textures-dimensions"></a>
<a name="7.1"></a>

### 7.1 Dimensions Are Powers of 2

All textures (except UI textures) must be dimensioned in powers of 2. Textures can be non-square.

For example, `128x512`, `1024x1024`, `2048x1024`, `1024x2048`, `1x512`.

<a name="textures-density"></a>
<a name="7.2"></a>

### 7.2 Texture Density Should Be Uniform

All textures should be of a size appropriate for their standard use case. Appropriate texture density varies from project to project, but
all textures within that project should have a consistent density.

For example, if a project's texture density is 8 pixels per 1 unit, a texture that is meant to be applied to a 100x100 unit cube should be
1024x1024, as that is the closest power of 2 that matches the project's texture density.

<a name="textures-max-size"></a>
<a name="7.3"></a>

### 7.3 Textures Should Be No Bigger than 8192

No texture should have a dimension that exceeds 8192 in size, unless you have a very explicit reason to do so. Often, using a texture this
big is simply just a waste of resources.

<a name="textures-group"></a>
<a name="7.4"></a>

### 7.4 Textures Should Be Grouped Correctly

Every texture has a Texture Group property used for LODing, and this should be set correctly based on its use. For example, all UI textures
should belong in the UI texture group.

**[⬆ Back to Top](#table-of-contents)**

## Major Contributors

* [Michael Allar](http://allarsblog.com): [GitHub](https://github.com/Allar), [Twitter](https://twitter.com/michaelallar)
* [CosmoMyzrailGorynych](https://github.com/CosmoMyzrailGorynych)
* [billymcguffin](https://github.com/billymcguffin)
* [akenatu](https://github.com/akenatsu)

## License

Copyright © 2016 Gamemakin LLC

See [LICENSE](/LICENSE)

**[⬆ Back to Top](#table-of-contents)**
