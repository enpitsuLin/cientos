# Sky

<DocsDemo>
  <SkyDemo />
</DocsDemo>

`<Sky />` is a wrapper for the [Three.js `Sky` add-on](https://threejs.org/examples/?q=sky#webgl_shaders_sky).

## Usage

<<< @/.vitepress/theme/components/SkyDemo.vue{3,9}

## Props

| Prop                | Description                                                                                                                         | Default    |
| :------------------ | :---------------------------------------------------------------------------------------------------------------------------------- | ---------- |
| `elevation`         | Sun's elevation from the horizon, in degrees                                                                                        | `0.6`      |
| `azimuth`           | Sun's [azimuth angle](https://en.wikipedia.org/wiki/Solar_azimuth_angle), in degrees – its horizontal coordinate on the horizon     | `180`      |
| `mie-coefficient`   | [Mie scattering](https://en.wikipedia.org/wiki/Mie_scattering) amount                                                               | `0.005`    |
| <nobr>`mie-directional-g`</nobr> | [Mie scattering](https://en.wikipedia.org/wiki/Mie_scattering) direction                                               | `0.7`      |
| `rayleigh`          | [Rayleigh scattering](https://en.wikipedia.org/wiki/Rayleigh_scattering)                                                            | `3`        |
| `turbidity`         | Haziness                                                                                                                            | `3.4`      |
| `distance`          | Sky box scale                                                                                                                       | `450000`   |
