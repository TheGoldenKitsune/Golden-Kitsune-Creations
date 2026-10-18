# Golden-Kitsune-Creations
Just a showcase of assets that was and will forever be created to help aid people in making there worlds or avatars.

First up...

Grand Pause


Shaders

https://youtu.be/-0E_vNcwXSY?si=Cwbd1V3G5XTXVe_Y

This display is also on gumroad btw

 
https://goldenkitsune.gumroad.com/l/apjpz


# ✨ Shader Showcase — Golden Kitsune Creations

Welcome to the shader collection by **Golden Kitsune Creations**, featuring custom visual effects designed for immersive 3D environments, fantasy worlds, science-fiction scenes, and VRChat world creation.

This showcase currently features two distinct shader systems: a configurable liquid volume shader that simulates colored liquid, animated surface movement, and rising bubbles, and an alien portal shader that generates swirling energy, procedural patterns, liquid-like distortion, and a pulsing outer aura.

Both shaders use real-time rendering calculations to create their effects, allowing creators to customize their appearance through material properties rather than relying entirely on static textures or pre-rendered animations.

The sections below explain what each shader does, how its visual systems operate, and how creators can use its features in their own projects.

---

# 🧪 01. Configurable Liquid Volume

**Shader:** `Twilights Embrace/Configurable Liquid Volume`

**Category:** Animated liquid material / transparent volume effect

**Designed for:** Unity-based 3D environments and VRChat world materials

## Overview

The Configurable Liquid Volume shader creates the appearance of liquid contained within a 3D object. It combines adjustable fill height, an animated liquid surface, directional sloshing, interior color variation, reflective highlights, and procedurally generated rising bubbles.

Instead of displaying a flat, static liquid-colored surface, the shader calculates a changing surface and uses that surface to determine which parts of the volume are visible. The result is a liquid effect with depth, movement, and customizable visual characteristics.

The shader is particularly suited to props and containers that need to appear filled with a substance, whether that substance is ordinary liquid, a magical potion, an alchemical mixture, or a fictional fluid.

## Features and capabilities

### 1. Adjustable liquid fill level

The `_FillLevel` property controls the height of the simulated liquid between the configured bottom and top of the volume.

This allows creators to change how full a container appears without manually rebuilding the liquid surface for every fill amount.

The shader also uses `_VolumeMinY` and `_VolumeMaxY` to define the vertical range used by the fill calculation. These values need to correspond to the intended volume setup.

**Possible applications:**
- Empty, partially filled, and nearly full potion bottles.
- Laboratory containers with different fluid levels.
- Sci-fi tanks containing fictional substances.
- Decorative vessels with customizable contents.

### 2. Animated surface waves

The liquid surface combines multiple sine and cosine wave patterns. These patterns move over time and interact to create a changing surface instead of a perfectly flat top.

Three overlapping wave contributions are used, with separate spatial frequencies and time-dependent movement.

The main controls are:

- `_SurfaceWaveHeight` — controls the amplitude of the surface waves.
- `_SurfaceWaveScale` — controls their spatial frequency and pattern density.
- `_SurfaceWaveSpeed` — controls the rate of animation.
- `_SurfaceThickness` — controls the thickness of the highlighted band around the liquid surface.

This system gives the top of the liquid a continuously changing appearance while keeping the effect procedurally generated.

### 3. Directional liquid sloshing

The shader supports directional tilting through two local-axis controls:

- `_SloshX` — controls the slosh direction along the local X axis.
- `_SloshZ` — controls the slosh direction along the local Z axis.
- `_SloshStrength` — controls how strongly those values affect the surface.

These settings tilt the simulated liquid surface across the container. They can be adjusted to create a level surface, a slight lean, or a more pronounced directional slope.

The slosh is driven by material parameters; the shader does not independently calculate physical container movement or automatically derive sloshing from VRChat player motion.

### 4. Custom liquid colors and interior depth

The shader provides separate color properties for the main liquid, deeper interior, and surface highlight.

- `_LiquidColor` — defines the primary liquid color.
- `_DeepColor` — defines the darker interior color.
- `_SurfaceColor` — defines the color used for the surface highlight.
- `_InteriorAbsorption` — controls how strongly the deeper interior color influences the liquid appearance.

The shader calculates a normalized depth value from the liquid surface and configured volume height. As the depth increases, the displayed color blends from the main liquid color toward the deeper interior color.

This creates a sense of depth without requiring a separate collection of pre-painted depth textures.

HDR-capable color properties allow brighter color values to be used when supported by the rendering environment.

### 5. Procedural rising bubbles

The shader includes an optional bubble system that generates bubble-like details inside the liquid.

It divides the volume into a procedural three-dimensional grid. A hash-based calculation determines which cells contain bubbles, their approximate positions, and their sizes. Time-dependent vertical movement makes the pattern appear to rise through the liquid.

Bubble appearance is divided into a brighter rim and a softer central region.

Available controls include:

- `_EnableBubbles` — enables or disables the bubble effect.
- `_BubbleDensity` — controls how many procedural grid cells are selected to contain bubbles.
- `_BubbleScale` — controls the scale of the bubble pattern.
- `_BubbleMinSize` — sets the minimum bubble size.
- `_BubbleMaxSize` — sets the maximum bubble size.
- `_BubbleRiseSpeed` — controls the upward movement rate.
- `_BubbleRayLength` — controls the interior sampling depth used to evaluate bubbles.
- `_BubbleEdgeStrength` — controls the brightness contribution of bubble rims.
- `_BubbleCoreStrength` — controls the brightness contribution of bubble centers.
- `_BubbleColor` — defines the bubble edge color.

The bubble effect is generated through shader calculations rather than by spawning separate 3D bubble objects.

### 6. Gloss, specular highlights, and viewing-angle effects

The shader adds lighting-dependent highlights to make the liquid appear more dimensional.

- `_SpecularStrength` controls the intensity of the specular contribution.
- `_Glossiness` controls the sharpness of that highlight.
- `_FresnelPower` controls how strongly the viewing-angle effect changes near the edges of a surface.

These properties affect how the liquid responds visually to lighting and camera direction.

The shader also exposes `_Opacity`, allowing the overall transparency of the simulated liquid to be adjusted.

## How the Configurable Liquid Volume works

The effect is built around several coordinated rendering stages.

**Stage 1 — Establish the volume.**

The liquid uses a suitable 3D mesh and configured local-space vertical bounds. These bounds define the range used for the liquid fill calculation.

**Stage 2 — Calculate the surface.**

The shader calculates a base height from the fill level, adds directional sloshing, and overlays animated wave patterns. This produces the changing height of the liquid surface across the container.

**Stage 3 — Shape the visible liquid.**

The surface calculation is used to clip fragments above the simulated liquid level. Vertices belonging to the mesh's upper cap are also adjusted to follow the calculated surface.

This is what allows the shader to create a variable liquid level and an animated top surface. The mesh must have appropriate geometry and an upper cap arranged for this operation.

**Stage 4 — Calculate depth and color.**

For each visible fragment, the shader calculates its relative depth beneath the surface. That value blends the main liquid color toward the deeper interior color.

Lighting, viewing angle, glossiness, and the surface highlight are then incorporated into the final color.

**Stage 5 — Evaluate the bubble volume.**

When bubbles are enabled, the shader samples procedural bubble patterns at multiple positions along the viewing direction. These samples contribute bubble centers and bright rims to the liquid appearance.

**Stage 6 — Produce the transparent result.**

The shader combines the liquid color, highlights, bubbles, and opacity, then applies Unity's fog calculation when applicable. Its transparent rendering configuration blends the result with the scene behind it.

## Practical uses

The Configurable Liquid Volume shader can be used for:

- Fantasy potion bottles and alchemy equipment.
- Magical liquids with custom color palettes.
- Science-fiction fluid tanks and laboratory props.
- Aquarium-style or decorative liquid displays.
- Interactive-looking props with configurable fill levels.
- Environmental details for VRChat worlds.

The shader itself supplies the liquid rendering effect. Inventory systems, interactive filling and emptying, object physics, and player-driven controls would require additional setup or systems outside the shader.

## Technical notes

- Uses a transparent Unity shader with alpha blending.
- Uses a Shader Model 3.0 target.
- Calculates surface waves and bubbles procedurally.
- Uses Unity lighting information for its specular and diffuse contributions.
- Disables depth writing for its transparent pass.
- Uses the configured volume bounds and mesh geometry to determine the simulated liquid shape.
- Includes a transparent diffuse fallback for environments that use the fallback shader.

Performance will depend on the mesh, rendering environment, number of visible instances, and the cost of evaluating the shader per rendered fragment.

---

# 👽 02. VRChat Alien Portal Cone

**Shader:** `VRChat/World/Alien Portal Cone`

**Category:** Animated alien energy / procedural portal effect

**Designed for:** Unity-based VRChat world materials

## Overview

The VRChat Alien Portal Cone shader creates a luminous, animated portal-like effect built around swirling patterns, procedural noise, liquid-like distortion, layered color fields, and a separate expanding aura.

The effect is designed to make a cone-shaped object appear filled with unstable alien energy. Its patterns change over time, creating rotating spirals, flowing bands, bubbling regions, and pulsing highlights.

Unlike a conventional portal that depends entirely on a static image, this shader generates much of its visual structure mathematically. An optional texture can be blended into the generated pattern for additional surface variation.

The shader also includes a second rendering pass dedicated to the outer aura, adding a separate layer of luminous energy around the main portal.

## Features and capabilities

### 1. Multi-layer alien spiral patterns

The portal's main visual structure is generated using several overlapping mathematical patterns.

The shader combines:

- A primary spiral pattern.
- A secondary spiral pattern with a different frequency.
- Radial ring patterns.
- Procedural noise.
- Animated pulse bands.
- A bubbling field.

These layers are combined into a portal field that controls how the different colors appear across the cone.

The main controls include:

- `_SpiralCount` — controls the number of spiral arms used in the pattern calculations.
- `_SwirlSpeed` — controls the direction and speed of the primary angular animation.
- `_SwirlStrength` — controls the amount of vertical warping applied to the angular pattern.
- `_AlienBand` — controls the vertical banding contribution.
- `_ConeRadius` — establishes the radius used by the shader's radial calculations.
- `_ConeHeight` — establishes the height used by its normalized vertical calculations.

The cone's actual geometry still matters: these properties guide the shader's calculations but do not replace the need for a suitably shaped mesh.

### 2. Procedural noise and distortion

The shader generates smooth three-dimensional noise using a hash-based grid calculation and interpolation between neighboring grid values.

That noise influences the angular distortion, pattern formation, bubbling details, and liquid-like movement.

Available controls include:

- `_NoiseScale` — changes the spatial scale of the procedural noise.
- `_NoiseStrength` — changes how strongly noise distorts the main angular pattern.

Increasing the scale creates finer spatial variation, while changing the strength alters the degree of irregularity in the pattern.

This allows creators to move between smoother, more organized energy patterns and more chaotic alien-looking structures.

### 3. Liquid-like surface displacement

The shader does more than animate color. It also offsets mesh vertices along their normals to create a changing surface silhouette.

The displacement combines two wave contributions and a noise-driven component. The effect varies with the vertex's position, angle, and time, and its strength changes along the cone's height.

Its main controls are:

- `_WaveHeight` — controls the amplitude of the surface displacement.
- `_WaveSpeed` — controls the animation rate and direction of the wave calculation.
- `_WaveFrequency` — controls the frequency of the vertical wave pattern.
- `_BubbleScale` — controls the spatial scale of the noise used by the liquid and bubble calculations.

This creates a rippling, irregular surface instead of a completely motionless cone.

### 4. Bubbling alien energy

A separate bubbling field is calculated from animated procedural noise and a wave pattern.

The shader uses this field to create irregular regions that resemble bubbles, foam, or concentrated energy moving through the portal.

Controls include:

- `_BubbleScale` — sets the scale of the procedural bubble pattern.
- `_BubbleStrength` — controls the contribution of the bubble field.
- `_BubbleCutoff` — determines the noise threshold at which bubble-like regions become prominent.

The bubbling field influences both the portal's color and its brightness, allowing these details to become part of the energy pattern rather than appearing as separate objects.

### 5. Gravity-style pulse bands

The shader includes an animated pulse calculation that varies with time, height, and angular position.

This pulse is converted into a band contribution that can brighten selected regions of the portal. It also affects the intensity of the final emission.

The relevant controls are:

- `_PulseSpeed` — controls the pulse animation rate.
- `_PulseStrength` — controls the influence of the pulse on the portal field and emission.
- `_PulseWidth` — controls the width of the pulse band.

The pulse is a visual effect; it does not implement a physical gravity field or exert forces on players or objects.

### 6. Customizable alien color palette

The portal uses several separate color properties to build its appearance.

- `_BaseColor` — defines the dark portal-void color.
- `_PortalColor` — defines the main portal energy color.
- `_HotColor` — defines the brighter alien energy color.
- `_FrothColor` — defines the color used for bubbling and froth-like details.
- `_AuraColor` — defines the color of the outer aura.

The shader blends between these colors according to its spiral patterns, noise, pulse, rim effect, and bubbling field.

This allows the same effect to be styled around different visual themes, such as cyan alien energy, purple dimensional rifts, magenta supernatural portals, or other color combinations.

### 7. Optional texture blending

The portal can use a texture in addition to its procedural patterns.

Its controls are:

- `_Texture` — supplies the optional alien-pattern texture.
- `_TextureBlend` — controls the amount of texture influence.
- `_TextureScale` — controls the texture's UV scale.

The texture is sampled with animated UV offsets. Its brightness is combined with the procedural portal field according to the blend setting.

The texture supplements the generated effect rather than replacing the shader's underlying spiral, noise, and pulse calculations.

### 8. Emission and luminous intensity

The portal's final color is multiplied by an emission calculation that depends on the portal field, pulse, rim, and bubbling details.

`_EmissionStrength` controls the overall emission multiplier.

The shader also includes `_RimPower`, which controls the shape of its viewing-angle rim contribution.

These calculations make the portal appear bright and energetic even without relying on ordinary scene lighting for its main appearance.

The shader explicitly disables ordinary lighting for its rendering passes, emphasizing its own generated colors and emission-like output.

### 9. Separate animated outer aura

The shader includes a second pass that renders an additional shell around the portal.

This pass offsets vertices outward along their normals and animates the offset using the pulse and wave calculations. It then uses a viewing-angle rim calculation to determine the visible aura intensity.

Its main controls are:

- `_AuraColor` — defines the aura's base color.
- `_AuraStrength` — controls the aura's intensity.
- `_AuraSize` — controls the outward expansion of the aura shell.

The aura color also blends toward the hot alien color as the pulse changes.

This separate pass adds another layer to the effect, helping the portal feel more luminous and visually separated from its surroundings.

## How the VRChat Alien Portal Cone works

**Stage 1 — Establish the cone geometry.**

The shader uses the mesh's local position, normal, and UV coordinates to evaluate the portal patterns. The cone radius and height parameters provide reference dimensions for its normalized calculations.

**Stage 2 — Animate the mesh surface.**

The vertex stage calculates procedural displacement using waves, angular position, and animated noise. It offsets vertices along their normals to create a rippling surface.

**Stage 3 — Generate the portal field.**

The fragment stage evaluates the position-dependent spiral patterns, radial rings, vertical bands, and procedural noise. These calculations are combined into a value that describes the main portal pattern.

**Stage 4 — Add bubbling and pulse details.**

The shader evaluates the bubble-like noise field and the animated pulse bands. These values modify the portal field and determine where additional brightness and contrasting colors appear.

**Stage 5 — Blend colors and optional texture.**

The procedural pattern is blended with the optional texture according to its configured blend amount. The resulting field determines the transition between the dark base color, portal energy color, hot color, and froth color.

**Stage 6 — Calculate the luminous result.**

The shader combines emission strength with the portal pattern, rim contribution, bubbling field, and pulse. This produces the final color and transparency for the main portal pass.

**Stage 7 — Render the outer aura.**

A second pass generates the expanded aura shell. It calculates its own animated displacement, pulse, rim intensity, and color before adding the outer luminous layer.

Together, these stages produce a procedural alien portal effect with animated geometry, layered patterns, luminous color transitions, and a separate aura.

## Practical uses

The VRChat Alien Portal Cone shader can be used for:

- Alien teleportation gates and dimensional rifts.
- Sci-fi and extraterrestrial world entrances.
- Magical portals and supernatural gateways.
- Futuristic energy columns and power sources.
- Alien artifacts and environmental decorations.
- Atmospheric focal points in VRChat worlds.
- Stylized effects for fantasy and science-fiction scenes.

The shader supplies the visual effect, not the actual teleportation system. Player movement, destination handling, collision behavior, interaction controls, and portal activation logic would need to be implemented separately if those functions are desired.

## Technical notes

- Uses a transparent Unity shader with a VRChat-oriented fallback tag.
- Uses a Shader Model 3.0 target.
- Includes a main animated portal pass and a separate aura pass.
- Supports GPU instancing variants.
- Generates spiral patterns, procedural noise, and pulse effects through shader calculations.
- Uses vertex displacement for the main surface and aura shell.
- Uses additive blending for its luminous passes.
- Disables depth writing in both passes.
- Includes an unlit transparent fallback.

The actual appearance depends on the cone mesh, its UVs, material configuration, texture assignment, scene setup, and the target rendering environment.

---

# 🔍 At a Glance: Comparing the Two Shaders

| Feature | Configurable Liquid Volume | VRChat Alien Portal Cone |
|---|---|---|
| Primary purpose | Simulated liquid inside a volume | Animated alien portal effect |
| Surface animation | Multi-wave liquid surface | Procedurally displaced cone |
| Directional sloshing | Yes, through X and Z controls | Not a dedicated slosh system |
| Procedural bubbles | Rising bubble centers and rims | Noise-driven bubbling and froth |
| Color depth | Main and deeper interior colors | Layered portal and energy colors |
| Optional texture | No exposed texture property | Yes, with blend and scale controls |
| Luminous aura | No separate aura pass | Yes, a dedicated outer aura pass |
| Main customization | Fill, waves, slosh, colors, gloss, bubbles | Spirals, noise, waves, pulse, colors, texture, aura |
| Teleportation logic | Not included | Not included |

# 🌋 03. VRChat Lava Volume — Procedural Lava Lamp Shader

**Shader:** `VRChat/World/Lava Volume`

**Category:** Procedural volumetric effect / animated magma / emissive material

**Target environment:** Unity and VRChat world creation

## 🔥 Overview

The **VRChat Lava Volume** shader creates the appearance of a transparent container filled with glowing, flowing magma. Instead of using a collection of individual 3D lava objects, it calculates the appearance of the molten material inside a defined volume using procedural mathematics, animated noise, and ray-marching-style sampling.

The result is an animated lava-lamp effect featuring rising magma blobs, elongated dripping tails, glowing hot cores, darker interior regions, and molten pools at the top and bottom of the volume.

The shader combines these elements with customizable colors, optional texture details, simulated gloss, emission, and a separate pulsing outer aura.

It is designed for creators who want to add a lava lamp, miniature magma reactor, alien specimen container, magical energy vessel, or other glowing fluid display to a virtual environment.

## ✨ Features and capabilities

### 1. Procedurally generated rising magma blobs

The central feature is a collection of animated magma formations that move upward through the volume.

The shader defines eight magma blobs with different seeds and time offsets. Each blob is constructed from several overlapping ellipsoidal shapes:

- **Main body:** Creates the rounded mass of molten material.
- **Dripping tail:** Extends below the main body to create a stretched, dripping appearance.
- **Connecting neck:** Bridges the body and tail, helping the formation appear more like a continuous piece of viscous magma.

The shader animates each formation vertically, while two independent sine and cosine calculations introduce horizontal swaying.

The radius also varies over time, creating subtle changes in the shape of the molten formations.

**Customization controls:**

- `_BlobSize` — adjusts the size of the magma formations.
- `_FlowSpeed` — controls the upward movement rate and influences the motion of the procedural turbulence.
- `_DripLength` — adjusts the length of the formations' trailing sections.
- `_VerticalStretch` — stretches the procedural turbulence vertically.

**Possible uses:**
- Lava lamps with slowly rising molten blobs.
- Glowing magma inside glass-like containers.
- Sci-fi reactor cores and experimental energy tanks.
- Alien specimens suspended in luminous fluid.
- Decorative fantasy props containing molten magic.

### 2. Procedural turbulence

The shader generates three-dimensional noise using a hash-based calculation and interpolation between neighboring grid values.

This noise is animated over time and modified by vertical stretching and horizontal offsets. It is combined with the magma formations to produce a more irregular, flowing appearance.

The turbulence helps break up the otherwise smooth ellipsoidal shapes and introduces variation into the interior of the volume.

**Customization controls:**

- `_BlobScale` — changes the spatial scale of the procedural turbulence.
- `_VerticalStretch` — changes the vertical proportions of the turbulence.
- `_FlowSpeed` — influences how quickly the turbulence pattern evolves.

The turbulence is calculated mathematically rather than requiring a pre-rendered animation.

### 3. Molten pools at the top and bottom

The shader includes a dedicated pooling calculation that creates broader regions of magma near the upper and lower boundaries of the normalized volume.

The pool calculation combines a radial mask, vertical boundary bands, and animated noise. This allows the pooled regions to have a more irregular appearance than simple flat bands.

**Customization controls:**

- `_PoolStrength` — controls the contribution of the top and bottom pools.
- `_PoolThickness` — controls the thickness of the boundary regions used to create the pools.

These controls help create the appearance of molten material collecting at the ends of the container while blobs continue to move through the middle.

### 4. Customizable molten colors

The shader uses separate colors for the dark interior, primary lava, hot core, and glossy highlights.

- `_CoolColor` — defines the dark interior tint.
- `_LavaColor` — defines the main molten material color.
- `_HotColor` — defines the brighter hot-core color.
- `_GooHighlightColor` — defines the color of the simulated glossy highlights.

The shader blends between the dark interior and lava color according to the calculated magma mask. Denser regions can transition toward the hot-core color.

This produces a layered molten appearance with darker gaps, glowing orange-red formations, and brighter concentrated regions.

The default palette uses a very dark reddish-brown interior, orange-red lava, a brighter orange hot core, and warm red-orange highlights.

Creators can change these colors to develop different visual themes, such as traditional volcanic magma, alien plasma, supernatural energy, or stylized fantasy liquids.

### 5. Optional lava pattern texture

The shader supports an optional texture that can add additional pattern variation to the procedural magma field.

The texture is sampled using coordinates derived from the sample's angular position around the volume and its vertical position. The resulting coordinates are scaled and animated using separate horizontal and vertical scrolling values.

**Customization controls:**

- `_LavaTexture` — supplies the lava pattern texture.
- `_TextureBlend` — controls how strongly the texture influences the procedural density.
- `_TextureScale` — controls the scale of the sampled texture pattern.
- `_TextureScrollX` — controls horizontal texture movement.
- `_TextureScrollY` — controls vertical texture movement.

The texture modifies the density calculation rather than replacing the entire procedural magma system.

This makes it possible to introduce additional visual variation while retaining the underlying moving blobs and pools.

### 6. Crust and surface-detail texturing

A second optional texture adds another layer of detail to the molten pattern.

The shader samples this texture at a modified version of the lava texture coordinates and uses its brightness to adjust the calculated density.

**Customization control:**

- `_CrustTexture` — supplies the crust-detail texture.
- `_DetailStrength` — controls how strongly this texture modifies the density field.

This system can help introduce a more broken-up or crust-like appearance to the edges of the molten formations.

The shader does not automatically simulate physical solidification or generate separate crust geometry. The texture contributes to the appearance by modifying the procedural density.

### 7. Custom color ramp

The shader supports a color-ramp texture that provides an additional way to customize the transition between dark material and brighter molten regions.

The ramp is sampled using a value derived from the magma mask and hot-core mask.

**Customization controls:**

- `_ColorRamp` — supplies the color-ramp texture.
- `_RampStrength` — controls how strongly the ramp affects the final color.

This allows creators to design more complex color transitions than the default set of solid color properties provides.

For example, a custom ramp could introduce additional intermediate shades between a dark interior and a bright molten core.

### 8. Density, edges, and material opacity

The shader calculates a density field and converts it into a magma mask using a threshold and a smooth transition.

This determines which areas appear to contain molten material and which remain part of the darker interior.

**Customization controls:**

- `_MagmaThreshold` — determines the density threshold at which the molten regions become visible.
- `_EdgeSoftness` — controls how gradually the magma mask transitions around its edges.
- `_MagmaOpacity` — controls the contribution of the molten regions to the accumulated opacity.
- `_AmbientOpacity` — adds a subtle background contribution throughout the sampled volume.
- `_StepOpacity` — controls the opacity contribution of each volume sample.
- `_GooSolidness` — controls how strongly the shader emphasizes the magma and its denser core regions.

Together, these parameters help determine whether the material looks like scattered glowing blobs suspended in darkness or a denser, more continuous molten substance.

### 9. Glossy molten highlights

The shader includes a stylized lighting calculation that adds specular highlights to the magma.

A procedural normal approximation is used to calculate the highlight response against a fixed simulated light direction. The shader also adds a view-dependent sheen to the denser magma regions.

**Customization controls:**

- `_GooGloss` — controls the sharpness of the simulated specular highlight.
- `_GooSpecular` — controls the intensity of the specular contribution.
- `_GooHighlightColor` — defines the highlight color.
- `_GooSolidness` — influences how strongly the denser magma regions contribute to the glossy appearance.

These calculations help the magma look more like a glossy, viscous substance rather than a collection of flat colored shapes.

The lighting is stylized and calculated within the shader; the effect does not use a full physical fluid simulation.

### 10. Emission and molten glow

The shader calculates additional brightness based on the magma mask, hot-core mask, and specular contribution.

**Customization control:**

- `_EmissionStrength` — controls the intensity multiplier applied to the molten glow.

This helps distinguish the hot regions from the darker interior and gives the magma its characteristic luminous appearance.

The shader's output is brightened mathematically. Actual bloom or a visible halo extending beyond the object's silhouette depends on the rendering environment and any additional post-processing effects.

### 11. Animated outer aura

A second rendering pass adds a separate aura around the volume.

This pass expands the object's vertices outward along their transformed normals, then calculates a viewing-angle rim effect. A time-dependent pulse and shimmer modify its brightness.

**Customization controls:**

- `_AuraColor` — defines the aura's color.
- `_AuraStrength` — controls its brightness multiplier.
- `_AuraOpacity` — controls the aura's alpha contribution.
- `_AuraSpeed` — controls the pulse and shimmer animation rate.
- `_AuraSize` — controls how far the aura geometry expands outward.
- `_AuraPower` — controls the shape and falloff of the rim effect.

This separate pass gives the lava lamp a more energetic appearance, making it useful for objects that need to stand out in a dark environment.

The aura is a shader-rendered shell, not a simulated heat field or a physical light source.

## ⚙️ How the Lava Volume shader works

The shader combines procedural volume sampling with density-based color calculations to create the illusion of glowing molten material inside a three-dimensional container.

### Stage 1 — Define the volume

The `_VolumeRadius` and `_VolumeHeight` parameters establish the dimensions used to normalize the sample positions.

The shader evaluates whether each sample falls within the configured cylindrical region. Samples outside this region do not contribute to the magma volume.

The object mesh, transform, and volume parameters must be configured appropriately for the intended result.

### Stage 2 — Generate the magma formations

The shader evaluates eight moving magma formations at different seeds and time offsets.

Each formation combines an ellipsoidal body, a stretched tail, and a connecting section. Their positions and sizes change over time, creating the characteristic rising and swaying motion.

### Stage 3 — Add turbulence and pools

Procedural noise modifies the magma density, while the pooling calculation creates broader molten regions near the top and bottom boundaries.

The highest contribution from the blobs, turbulence, and pools forms the underlying magma field.

### Stage 4 — Sample the volume along the viewing ray

The shader traces a series of sample positions along the viewing direction and evaluates the volume at each position.

The number of samples depends on the rendering platform:

- Six samples are used for the shader's mobile, GLES3, Vulkan, and Metal compilation paths.
- Ten samples are used for other compilation paths covered by the shader's conditional definitions.

The shader adjusts the per-sample opacity on the lower-sample path to compensate for the reduced number of samples.

This approach is commonly described as ray-marching-style volume rendering. It does not construct individual 3D objects for every blob; instead, it calculates the combined appearance of the volume at multiple points along the viewing direction.

### Stage 5 — Apply texture and density shaping

At each sample, the shader evaluates the optional lava texture and crust-detail texture.

Their contributions modify the density before it is converted into the magma mask, core mask, and goo mask.

The threshold and edge-softness settings determine how the resulting density becomes visible molten material.

### Stage 6 — Calculate color and highlights

The shader blends the dark interior, primary lava, and hot-core colors according to the calculated masks.

If enabled, the color-ramp texture further modifies the color. Specular and view-dependent highlight calculations add the appearance of a glossy molten surface.

Emission then increases the brightness of the denser and hotter regions.

### Stage 7 — Accumulate color and opacity

Each sample contributes color and alpha to the final result, with later contributions reduced according to the opacity already accumulated.

This creates a layered impression of material depth, allowing brighter magma formations to appear suspended inside a darker volume.

The shader uses transparent alpha blending and does not write to the depth buffer in its main rendering pass.

### Stage 8 — Render the outer aura

The second pass renders an expanded shell around the original mesh.

Its view-dependent rim, pulse, and shimmer calculations generate a separate layer of colored energy around the lava volume.

The main magma effect and outer aura therefore use different rendering calculations to create a combined appearance.

## 🎮 Practical applications

The Lava Volume shader can be used for:

- **Lava lamps:** Create animated molten blobs inside decorative vessels.
- **Magma reactors:** Represent fictional power sources in futuristic environments.
- **Alien specimen containers:** Display glowing, suspended substances inside laboratory props.
- **Fantasy artifacts:** Create vessels containing magical or supernatural liquids.
- **Volcanic props:** Add small-scale lava effects to environmental objects.
- **VRChat world decorations:** Introduce animated focal points into themed rooms and immersive environments.
- **Sci-fi machinery:** Add a glowing energy core to a machine, generator, or containment device.

The shader provides the visual rendering effect. It does not implement fluid physics, collision, heat transfer, object interaction, or real-world lighting emission.

## 🛠️ Technical details

- Shader name: `VRChat/World/Lava Volume`.
- Uses a transparent rendering queue and transparent fallback configuration.
- Targets Shader Model 3.0.
- Uses procedural three-dimensional noise and hash calculations.
- Generates eight animated magma formations.
- Includes a ray-marching-style sampling loop with platform-dependent sample counts.
- Supports optional lava-pattern, crust-detail, and color-ramp textures.
- Uses alpha blending for the main volume pass.
- Includes a separate additive-blended aura pass.
- Disables depth writing in both passes.
- Disables ordinary lighting for the shader's own rendering calculations.
- Supports GPU instancing variants.
- Includes a fallback to `Unlit/Transparent`.

### Performance considerations

The main rendering pass evaluates multiple volume samples per fragment. As a result, its cost depends on the number of pixels covered by the object, the sampling workload, and the target hardware.

Large objects occupying a substantial portion of the screen can be more expensive to render than smaller props.

The shader's reduced sampling path is intended to lower the workload on specified mobile and graphics API compilation paths. Actual performance should still be tested on the target platform, particularly when several transparent effects overlap.

## 🌋 The result

The VRChat Lava Volume shader combines animated magma blobs, dripping shapes, procedural turbulence, molten pools, layered color, glossy highlights, and a pulsing outer aura into a single customizable visual effect.

Its purpose is to give creators a way to build convincing, stylized molten displays without having to animate a collection of individual magma meshes.

From a decorative lava lamp to a glowing alien reactor, the shader provides a flexible starting point for bringing fictional molten materials to life.

---

**Golden Kitsune Creations — procedural visuals for worlds beyond the ordinary.**

# 🦊 About Golden Kitsune Creations

Golden Kitsune Creations presents custom shader experiments and visual tools designed to give creators more control over the appearance and atmosphere of their digital environments.

These two shaders demonstrate different approaches to procedural rendering: one focuses on creating a convincing, customizable liquid volume, while the other builds a layered alien energy effect from animated mathematical patterns.

Both are intended to be customized through their exposed material properties, giving world creators a starting point for distinctive visual effects without requiring them to write their own shader implementation.

