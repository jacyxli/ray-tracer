# Ray Tracer
This program takes as input a description of the scene objects, lighting, and viewing parameters, and produce a .ppm file containing the ray-traced image of the scene.

## Features
The ray tracer supports the following elements:
- Spheres and convex polyhedra
- Solid colored objects
- Ambient, diffuse and specular shading, shadows and reflection 
- Anti-aliasing, super-sampling 9 rays per pixel 
- Refraction 
- Checkerboard textured objects 
- Triangle meshes 
- Transformations: scale and translate 
- Full image based texture for spheres 

## Compile
Standard Compilation - use make (make clean removes unnecessary files).

    make
    ./raytracer [input_fileName]

## Usage
**Basics**
Example:
    
    ./raytracer testfiles/test2.in

**Textures**
full image based texture can be implemented to spheres by editing the PIGMENT section of the .in file. The line containing texture information is as follows:

    texture     [image_filename]
Example: 

    texture     flowers.ppm

Please see texture1.in for reference.
In this case, test1.in is edited to change the blue color of two spheres to a texture image (flowers.ppm). 

    ./raytracer testfiles/test1.in

## FILES
Source code:
- C++ files: face.cpp image.cpp light.cpp main.cpp matrix.cpp mesh.cpp ray.cpp scene.cpp shape.cpp surFinish.cpp texture.cpp util.cpp vector.cpp vertext.cpp
- Header files: face.h image.h light.h main.h matrix.h mesh.h ray.h scene.h shape.h surFinish.h texture.h util.h vector.h vertex.h 
Image files[nput, output]:
- flowers.ppm (texture image)
- test1.in test1.ppm
- test2.in test2.ppm
- test3.in test3.ppm
- test4.in test4.ppm
- test5.in test5.ppm
- test6.in test6.ppm
- test7.in test7.ppm
- texture1.in texture1.ppm
Executable file:
- raytracer
Others:
- README
- Makefile
	
**Structs:**
- Camera (declared in image.h)
This is a struct for camera frame, which stores both the eye position and the 	camera axis vectors read from the .in file.

- Pigment (declared in shape.h)
This is a struct for pigment. It can handle three cases: solid color, checkerboard, and full image texture. 

**Classes:**
- Vector
This is a class for vector consisting of three floating points. It contains necessary vector calculation functions. It represents RGB color, vector, and point in our program.

- Matrix
This class stores an 2D array to represent a matrix and contains essential matrix calculation. 

- Vertex
This is a class for individual vertex of a mesh. It contains vertex position, vertex normal, pointers to adjacent faces, and the number of adjacent faces. 

- Face
This is a class for individual face of a mesh. It contains face normal, pointers to associated vertices, and the number of such vertices.

- Mesh
This is a class that loads a mesh file and stores information in appropriate Vertex and Face structures. 

- Image
This is a class for the screen setup and eventually the output .ppm image file. It stores an array of all pixel colors, the width and height of the image, and the camera frame struct. It also maps the pixel defined in raster frame to that defined in camera frame, and outputs .ppm file. 

- Light
This is a class for light sources. It contains the essential information of each individual light source, including type, position, intensity and attenuation. 

- Ray
This is a class for each individual ray, consisting of type, origin and direction vectors, and ray min/max distances. It also calculates a destination point given a distance.

- SurFinish
This is a class for all the read-in information of surface finish, including coefficients of ambient, diffuse, specular, shininess, reflective, transmission, and index of refraction. 

- Texture
This is a class for full image based texture. It contains the filename of an image to be read, the width and height of that texture image, and an 2D array storing color information. It handles reading .ppm files and storing the information.

- Shape
Shape class stores its type, pigment, surface finishes, and matrices. It has three subclasses - sphere, polyhedron, and triangle mesh. Each of these three shapes have their own intersection function and normal calculation. 

- Scene
This is a class that reads input file and stores the scene information appropriately into our pre-defined data structures for later usage.

- Util
This is a math library we construct for convenience. 

Main.cpp:
This is where our main loop for ray tracing is at. It reads the file containing descriptions of a scene, creates a screen, casts rays through each pixel of the screen to the world, traces each ray recursively, and calculates the color via Phong shading model. 


## Notes
**Basic setup:**

background color: 0.5, 0.5, 0.5

recursion depth: 4
