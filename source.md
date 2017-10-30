<section id="themes">
	<h2>Themes</h2>
		<p>
			Set your presentation theme: <br>
			<!-- Hacks to swap themes after the page has loaded. Not flexible and only intended for the reveal.js demo deck. -->
                        <a href="#" onclick="document.getElementById('theme').setAttribute('href','css/theme/black.css'); return false;">Black (default)</a> -
			<a href="#" onclick="document.getElementById('theme').setAttribute('href','css/theme/white.css'); return false;">White</a> -
			<a href="#" onclick="document.getElementById('theme').setAttribute('href','css/theme/league.css'); return false;">League</a> -
			<a href="#" onclick="document.getElementById('theme').setAttribute('href','css/theme/sky.css'); return false;">Sky</a> -
			<a href="#" onclick="document.getElementById('theme').setAttribute('href','css/theme/beige.css'); return false;">Beige</a> -
			<a href="#" onclick="document.getElementById('theme').setAttribute('href','css/theme/simple.css'); return false;">Simple</a> <br>
			<a href="#" onclick="document.getElementById('theme').setAttribute('href','css/theme/serif.css'); return false;">Serif</a> -
			<a href="#" onclick="document.getElementById('theme').setAttribute('href','css/theme/blood.css'); return false;">Blood</a> -
			<a href="#" onclick="document.getElementById('theme').setAttribute('href','css/theme/night.css'); return false;">Night</a> -
			<a href="#" onclick="document.getElementById('theme').setAttribute('href','css/theme/moon.css'); return false;">Moon</a> -
			<a href="#" onclick="document.getElementById('theme').setAttribute('href','css/theme/solarized.css'); return false;">Solarized</a>
		</p>
</section>

H:

# Rendering

Visual Computing

H:

# Outline

1. Introduction: the problem
2. Ray-tracing approach
3. Rasterization approach
4. Final thoughts

H:

## Introduction: Alberti's Veil
### Linear perspective

<figure>
    <img height='400' src='fig/durer2.gif' />
    <figcaption>[Dürer's Alberti Veil](http://visualcomputing.github.io/Cognitive)</figcaption>
</figure>

V:

## Introduction: [Virtual camera model](https://www.scratchapixel.com/lessons/3d-basic-rendering/3d-viewing-pinhole-camera/virtual-pinhole-camera-model)
### Representation

<figure>
    <img height='400' src='fig/pinholecam.png' />
    <figcaption>Non inversion of the rendered image</figcaption>
</figure>

V:

## Introduction: [Virtual camera model](https://www.scratchapixel.com/lessons/3d-basic-rendering/3d-viewing-pinhole-camera/virtual-pinhole-camera-model)
### Frustum

<figure>
    <img height='400' src='fig/frustum.png'/>
    <figcaption>Near and far clipping frustum planes</figcaption>
</figure>

V:

## Introduction: [Virtual camera model](https://www.scratchapixel.com/lessons/3d-basic-rendering/3d-viewing-pinhole-camera/virtual-pinhole-camera-model)
### Image plane

<figure>
    <img height='400' src='fig/clippingplanescanvas.png'/>
    <figcaption>Various valid canvas positions</figcaption>
</figure>

V:

## Introduction: [Virtual camera model](https://www.scratchapixel.com/lessons/3d-basic-rendering/3d-viewing-pinhole-camera/virtual-pinhole-camera-model)
### Image plane

<figure>
    <img height='400' src='fig/canvascoordinates.png'/>
    <figcaption>Positioning the canvas at the near plane</figcaption>
</figure>

V:

## Introduction: [Virtual camera model](https://www.scratchapixel.com/lessons/3d-basic-rendering/3d-viewing-pinhole-camera/virtual-pinhole-camera-model)
### Frustum

<figure>
    <img height='400' src='fig/frustumsideview.png'/>
    <figcaption>Frustum side view</figcaption>
</figure>

V:

## Introduction: Virtual camera model
### Challenges

> 1. Spatial coherence -> Visibility
<p>
> 2. Visual appealing -> Shading

V:

## Introduction: Virtual camera model
### Challenges: Visibility
#### Geometry related

<video width="400" height="400" controls data-autoplay loop src="vid/coordinate_system_no_depth.ogv"></video>

V:

## Introduction: Virtual camera model
### Challenges: Shading
#### Physics related

<figure>
    <img height='400' src='fig/rendering_eq.png'/>
    <figcaption>[Rendering equation](https://en.wikipedia.org/wiki/Rendering_equation)</figcaption>
</figure>

N:

integral equation in which the equilibrium radiance leaving a point is given as the sum of emitted plus reflected radiance under a geometric optics approximation

H:

## Raster approach: strategy
### Object centric

<figure>
    <img height='400' src='fig/rasterization.png'/>
    <figcaption>Perspective projection of points</figcaption>
</figure>

V:

## Raster approach: strategy
### Object centric

<figure>
    <img height='400' src='fig/rasterization1.png'/>
    <figcaption>Perspective projection of a point</figcaption>
</figure>

V:

## Raster approach: strategy
### Object centric

```processing
for (each point in scene) {
transform point from world space to camera space;
perform perspective divide (x/-z, y/-z);
  if (point lies within canvas boundaries) {
    convert coordinates to NDC space;
    convert coordinates from NDC to raster space;
    record point in image;
  }
}
```

V:

## Raster approach: visibility
### [Hidden surface removal (HSR)](https://en.wikipedia.org/wiki/Hidden_surface_determination) algorithms

1. [Painter's algorithm](https://en.wikipedia.org/wiki/Painter%27s_algorithm)
1. [Binary space partioning (BSP)](https://en.wikipedia.org/wiki/Binary_space_partitioning)
1. [Warnock algorithm](https://en.wikipedia.org/wiki/Warnock_algorithm)
1. [Z-Buffering](https://en.wikipedia.org/wiki/Z-buffering)

V:

## Raster approach: visibility
### [Hidden surface removal (HSR)](https://en.wikipedia.org/wiki/Hidden_surface_determination) algorithms
#### [Painter's algorithm](https://en.wikipedia.org/wiki/Painter%27s_algorithm)

<figure>
    <img height='400' src='fig/painter_algorithm.png'/>
    <figcaption>Draw distant objects first</figcaption>
</figure>

V:

## Raster approach: visibility
### [Hidden surface removal (HSR)](https://en.wikipedia.org/wiki/Hidden_surface_determination) algorithms
#### [Binary space partioning (BSP)](https://en.wikipedia.org/wiki/Binary_space_partitioning)

<figure>
    <img height='400' src='fig/bsp_input.gif'/>
    <figcaption>Input scene</figcaption>
</figure>

V:

## Raster approach: visibility
### [Hidden surface removal (HSR)](https://en.wikipedia.org/wiki/Hidden_surface_determination) algorithms
#### [Binary space partioning (BSP)](https://en.wikipedia.org/wiki/Binary_space_partitioning)

<figure>
    <img height='400' src='fig/bsp1.gif'/>
    <figcaption>(Offline) subdivision step</figcaption>
</figure>

V:

## Raster approach: visibility
### [Hidden surface removal (HSR)](https://en.wikipedia.org/wiki/Hidden_surface_determination) algorithms
#### [Binary space partioning (BSP)](https://en.wikipedia.org/wiki/Binary_space_partitioning)

<figure>
    <img height='400' src='fig/bsp2.gif'/>
    <figcaption>(Offline) subdivision step</figcaption>
</figure>

V:

## Raster approach: visibility
### [Hidden surface removal (HSR)](https://en.wikipedia.org/wiki/Hidden_surface_determination) algorithms
#### [Binary space partioning (BSP)](https://en.wikipedia.org/wiki/Binary_space_partitioning)

<figure>
    <img height='400' src='fig/bsp.gif'/>
    <figcaption>BSP Tree</figcaption>
</figure>

V:

## Raster approach: visibility
### [Hidden surface removal (HSR)](https://en.wikipedia.org/wiki/Hidden_surface_determination) algorithms
#### [Binary space partioning (BSP)](https://en.wikipedia.org/wiki/Binary_space_partitioning)

<figure>
    <img height='400' src='fig/bsp_scene.jpg'/>
    <figcaption>(Runtime) BSP visit</figcaption>
</figure>

V:

## Raster approach: visibility
### [Hidden surface removal (HSR)](https://en.wikipedia.org/wiki/Hidden_surface_determination) algorithms
#### [Warnock algorithm](https://en.wikipedia.org/wiki/Warnock_algorithm)

<figure>
    <img height='400' src='fig/warnock1.png'/>
    <figcaption>Polygon visibility cases: a) polygon fills the viewport, b) polygon partially and c) completely visible, d) polygon invisible</figcaption>
</figure>

V:

## Raster approach: visibility
### [Hidden surface removal (HSR)](https://en.wikipedia.org/wiki/Hidden_surface_determination) algorithms
#### [Warnock algorithm](https://en.wikipedia.org/wiki/Warnock_algorithm)

<figure>
    <img height='400' src='fig/warnock.png'/>
    <figcaption>Subdivision step example</figcaption>
</figure>

V:

## Raster approach: visibility
### [Hidden surface removal (HSR)](https://en.wikipedia.org/wiki/Hidden_surface_determination) algorithms
#### [Z-Buffering](https://en.wikipedia.org/wiki/Z-buffering)

<figure>
    <img height='400' src='fig/zbuffer.png'/>
    <figcaption>Zbuffer data</figcaption>
</figure>

V:

## Raster approach: shading

<section>

<section>

# SHADING

</section>

<section>

## WHY IS SHADING BETTER FOR SHADING?

*   Shading is used to create effects like shadows, soft shadows when area lights are used, and more generally global illumunation effects such as reflection, refraction, indirect reflections and indirect diffuse.
*   Ray-tracing is good at both solving the visibility problem and finding the visibility between surfaces.
*   The shading process requires finding the visibility between surfaces.

</section>

<section>

## SO... WHY DO GPUs USE RASTRERIZATION OVER RAY TRACING?

![](images/3.png)</section>

<section>

## CREATE AN IMAGE IN RAY-TRACING

*   Cast a ray for each pixel in the image.
*   The first rays emitted are called primary rays or camera rays.
*   More rays can be spawned from primary rays. These other rays are called secondary rays.
*   When a primary ray is cast into the scene, the next step is to find if it intersects any object in the scene.
*   When primary rays are used to solve the visibility problem, we can use the term ray-casting.

</section>

<section>

## HOW DOES SHADING WORK ON RAY-TRACING?

There are 2 main types of rays, Primary rays and secondary rays, Secondary rays can be Shadow Rays or reflection rays depending on their function.

</section>

<section>

## HOW DOES SHADING WORK ON RAY-TRACING?

![](images/4.png) ![](images/5.png)</section>

</section>

H:

## Ray-tracing approach: strategy
### Image centric

<figure>
    <img height='400' src='fig/ray_trace_diagram.png'/>
    <figcaption>Casting rays into a scene</figcaption>
</figure>

V:

## Ray-tracing approach: strategy
### Image centric

<figure>
    <img height='400' src='fig/ballsrender.png'/>
    <figcaption>Photorealism</figcaption>
</figure>

V:

## Ray-tracing approach: strategy
### Image centric

```processing
for (each pixel in the image) {
  // step 1
  build a camera ray: trace line from current pixel location to camera's aperture;
  // step 2
  cast ray into the scene;
  // step 3
  if (ray intersects an object) {
    set current pixel's color with object's color at the intersection point;
  } else {
    set current pixel's color to black;
  }
}
```

V:

## Ray-tracing approach: visibility

<figure>
    <img height='400' src='fig/ray-tracing-points.png'/>
    <figcaption>Visibility computation</figcaption>
</figure>

V:

## Ray-tracing approach: visibility

```processing
for (each pixel in the image) {
  // step 1
  build a camera ray: trace line from current pixel location to camera's aperture;
  // step 2
  cast ray into the scene;
  // step 3
  for (each object in the scene) {
    set current pixel's color with closest object's color at the intersection point;
  }
}
```

V:

## Ray-tracing approach: shading

<!–
Desarrollar el tema que se encuentra aca (en slides verticales, i.e., empleando el tag 'V:'):
https://www.scratchapixel.com/lessons/3d-basic-rendering/ray-tracing-overview
desde la seccion: 'Casting Rays into the scene'

el tema para seguirla seria este de aca:
https://www.scratchapixel.com/lessons/3d-basic-rendering/ray-tracing-overview/light-transport-ray-tracing-whitted
pero no el Lunes, sino quizas mas adelante
–>

H:

## Final thoughts

> Problem: Implement Alberti's Veil on a computer -> virtual (pinhole) camera model

<!-- .element: class="fragment" data-fragment-index="1"-->

> Challenges: visibility (geometry) & shading (physics)

<!-- .element: class="fragment" data-fragment-index="2"-->

> Strategies: Raster vs Ray-tracing

<!-- .element: class="fragment" data-fragment-index="3"-->

V:

## Final thoughts
### Raster vs Ray-tracing

| _Feature_         | Rasterization | Ray-tracing |
|-------------------|---------------|-------------|
| _Philosophy_      | [Intromission](https://en.wikipedia.org/wiki/Visual_perception#Early_studies)  | [Emission](https://en.wikipedia.org/wiki/Visual_perception#Early_studies) |
| _Visibility_      | Easy          | Trivial     |
| _Shading_ realism | _Promising_   | Great       |
| _Parallelizable_  | Easy          | Hard        |
| _Complexity_      | Linear        | Exponential |

V:

## Final thoughts
### [OpenGL pipeline](https://www.khronos.org/opengl/wiki/Rendering_Pipeline_Overview)

<figure>
    <img height='400' src='fig/rendering_pipeline.png'/>
    <figcaption>Opengl Rendering Pipeline</figcaption>
</figure>

N:

1. Virtual camera: vertex specification & vertex shader
2. Shading: fragment shader
3. Visibility (z-buffer): per sample operations

V:

## Final thoughts
### [OpenGL pipeline](https://www.khronos.org/opengl/wiki/Rendering_Pipeline_Overview): [Virtual camera model](https://learnopengl.com/#!Getting-started/Coordinate-Systems)

<figure>
    <img height='400' src='fig/coordinate_systems.png'/>
    <figcaption>Matrix transform operations</figcaption>
</figure>

H:

## References

1. [Learn Computer Graphics From Scratch!](http://www.scratchapixel.com/)
1. [2D cross-product](https://www.gamedev.net/forums/topic/289972-cross-product-of-2d-vectors/)
1. [OpenGL coordinate systems](https://learnopengl.com/#!Getting-started/Coordinate-Systems)
1. [OpenGL pipeline](https://www.khronos.org/opengl/wiki/Rendering_Pipeline_Overview)
