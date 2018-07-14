## Procedural Terrain Generation with Marching Cubes

## Running the code
Build rastify and run rstest from the bin folder. Rastify/anyDSL should be built in release mode, as debug mode takes a very long time to compile.

## Modifying the code

1. samples/testing/main.cpp 

    * The marching cubes grid size is set on line 105 where the pipeA is defined. The grid should be the same size along each dimension.

    * mcubeslength should then be set to the size of the grid along each dimension.

    * initlength is the length that the marching cube grid occupies along each dimension. i.e. a mcubeslength of 10, and an initlength of 100, means there are 10x10x10 marching cubes and each cube has length 10 along each dimension since (100/10 = 10).
    
2. samples/testing/stages.impala

    * Here the density field is set in the geometryShader. Coloring is controlled in the fragmentShader.

2. src/mcubes.impala
    
    * New density functions can be defined here. Unfortunately there is no set convention as to whether positive portions of the field are inside or outside of the isosurface. This is because I had trouble with triangles not rendering for some configurations. 

    * Due to this, it may be required to flip the normals in lighting(). Just uncomment line 364.

    * Additionally, I did not know how to pass a density field through the graphics pipeline, as the parameters are defined in c++, and the density field is defined in impala. Therefore whenever the density field is changed in the geometry shader, it also has to be changed in the follow locations in mcubes.impala:

        1. line: 304 in getNormal(). 
        2. line: 325 in ambient_occlusion().
