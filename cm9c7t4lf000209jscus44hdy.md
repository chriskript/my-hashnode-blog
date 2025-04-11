---
title: "Rendering a 3D Solar System with Three.js"
seoTitle: "Create 3D Solar System Using Three.js"
seoDescription: "Create a 3D solar system simulator using Three.js. Learn about rendering, lighting, interactivity, and optimizing performance in web development"
datePublished: Fri Apr 11 2025 03:16:01 GMT+0000 (Coordinated Universal Time)
cuid: cm9c7t4lf000209jscus44hdy
slug: rendering-a-3d-solar-system-with-threejs
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1744339182813/5a1e757a-8385-4398-a394-7611f5b38657.jpeg
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1744341304069/892a4cc2-d7f4-4a3d-a936-2ac8f86ee79b.png
tags: web-development, threejs, simulation, solar-system

---

Have you ever looked up at the night sky and wondered how you could bring that magic into your code? Recently, I embarked on a journey to build my very own **3D solar system simulator** using Three.js, and the project turned out to be as challenging as it was rewarding. In this post, I share the process, the code design, and the lessons learned from expanding my skills in 3D graphics and interactive web development.

You can preview the live demo [here](https://chriskript.github.io/threejs-solar-system/).

---

## Why I Did It

The idea started as a playful experiment to merge my interest in space with my passion for coding. I wanted to:

* **Gain deeper familiarity with Three.js**, a powerful JavaScript library for 3D rendering.
    
* **Challenge myself with realistic rendering techniques**, including shadows, textures, and smooth animations.
    
* **Explore interactive elements**, allowing users to click on the planets to see detailed information.
    
* **Enhance my technical portfolio** by tackling a project that combines both creativity and performance optimization.
    

Building this solar system pushed me beyond simple static scenes. I learned how to manage multiple objects, optimize rendering, and implement real-time camera controls—all crucial skills for a modern web developer working with complex graphics.

---

## How I Did It

### Project Structure and Setup

I began by organizing the project with a clear folder structure: a primary folder containing `src` and `textures` directories along with an `index.html` and `index.js`. This organization made it easier to maintain and load the assets needed for a realistic scene.

```markdown
└── The-globe-threejs
    ├── src
    ├── textures
    │   ├── earth_diffuse.jpg
    │   ├── earth_bump.jpg
    │   └── … (other planet textures)
    ├── index.html
    └── index.js
```

The **HTML** included the basic skeleton, referencing Three.js and OrbitControls via an import map. This kept the setup neat and leveraged a modern ES modules approach.

```xml
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Three JS Solar System by Chriskript</title>
    <style>
      body { margin: 0; }
    </style>
    <script type="importmap">
      {
        "imports": {
          "three": "https://cdn.jsdelivr.net/npm/three@0.161.0/build/three.module.js",
          "jsm/": "https://cdn.jsdelivr.net/npm/three@0.161.0/examples/jsm/"
        }
      }
    </script>
  </head>
  <body>
    <script type="module" src="index.js"></script>
  </body>
</html>
```

### Building the Scene and Adding Interactivity

#### 1\. **Setting Up the Renderer, Camera, and Controls**

The first part of the JavaScript initialized the basic components:

* **Renderer:** A WebGLRenderer with anti-aliasing and shadow mapping.
    
* **Camera:** A perspective camera, positioned to capture the entire scene.
    
* **Scene:** A container for everything in the simulation.
    
* **Orbit Controls:** These provided an intuitive way to navigate around the solar system.
    

I also added a unique element—a golden icosahedron—just as a demonstration object in the scene. Although optional, it was a fun way to experiment with shadows and wireframe overlays.

#### 2\. **Creating a Realistic Environment**

To mimic the vastness of space, I implemented a procedurally generated starfield using instanced rendering. By randomly positioning thousands of tiny spheres, I achieved an immersive backdrop that gives the feeling of a true cosmic scene.

#### 3\. **Lighting and the Sun**

Realism in 3D scenes often comes down to lighting. I created the Sun not only as a glowing sphere with an emissive material but also attached a point light to simulate actual sunlight. This approach ensured that shadows and highlights on the planets could be rendered realistically.

#### 4\. **Planets, Orbits, and Moons**

I defined data for each planet (like Mercury, Venus, Earth, etc.) that included properties such as size, distance from the Sun, color, and orbital speed. Each planet was created using a helper function (`createPlanet`) that constructs a sphere with the appropriate textures and bump maps. The Earth, for example, benefits from both a diffuse texture and a subtle bump map for added detail.

Moons are handled similarly with a dedicated function (`createMoon`), and for Saturn, I added an extra layer of detail by designing rings using `RingGeometry`.

#### 5\. **Interactive Raycasting and Information Overlay**

One of the most exciting interactive features is the raycasting mechanism:

* On mouse click, the code calculates the position in 3D space.
    
* If a planet or the Sun is clicked, an info overlay appears with relevant details (e.g., distance, size, orbital speed).
    
* A smooth camera interpolation (`lerp`) moves the view toward the selected planet, enhancing the user experience.
    

```javascript
// Example snippet for raycasting interaction:
window.addEventListener('click', (event) => {
  // Convert mouse coordinates and check intersections...
  if (intersects.length > 0) {
    // Update overlay and camera target
    updateInfoOverlay(clickedPlanetData);
  } else {
    hideInfoOverlay();
  }
});
```

The overlay itself is a simple HTML element styled to sit atop the canvas—displaying key data and making the simulation more engaging.

#### 6\. **Animation and Performance**

The main animation loop ties everything together:

* Each frame rotates the planets around the Sun at different speeds.
    
* The Sun rotates slowly, and the camera is dynamically updated to follow user interactions.
    
* I also used `OrbitControls` to enable smooth panning and zooming around the target objects.
    

The constant updating of the scene not only brings it to life but also provided a valuable opportunity to learn about performance tuning in real-time 3D rendering.

---

## How This Project Helped Me Grow

Working on this solar system simulator offered several key takeaways:

* **Deepened Understanding of Three.js:**  
    I learned how to set up scenes, manage complex hierarchies, and use advanced features like instanced rendering and texture mapping.
    
* **Enhanced JavaScript Skills:**  
    Implementing interactive features like raycasting and smooth camera movements sharpened my skills in writing efficient, performance-oriented JavaScript code.
    
* **Practical Experience with 3D Mathematics:**  
    Concepts like rotation, interpolation (lerp), and proper object nesting were crucial. I gained a much clearer understanding of 3D geometry and spatial awareness.
    
* **User Experience and Interaction:**  
    Designing an intuitive overlay and responsive controls pushed me to consider the user experience, further broadening my perspective on web development beyond just the code.
    
* **Attention to Optimization:**  
    Dealing with thousands of stars and multiple dynamic objects taught me how to think about performance. I explored techniques that are essential when working on complex visualizations or games.
    

---

This project was much more than a coding exercise—it was an exploration into the world of 3D graphics, interactive design, and performance optimization. By building a solar system simulator with Three.js, I not only expanded my technical toolbox but also gained the confidence to tackle more ambitious projects in the future.

Whether you’re a beginner eager to learn or an experienced developer looking for a creative challenge, I hope this walkthrough inspires you to push the boundaries of what you can create with code.

Feel free to check out the complete code and interact with the demo on my [GitHub repository](https://github.com/chriskript/threejs-solar-system). Happy coding, and may your curiosity always reach for the stars!