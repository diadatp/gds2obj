# gds2obj
Convert GDSII to Wavefront OBJ.

sky130.mtl is the material file for layers in the gds file. Edit it to change rendered colours and lighting properties (shading model).

- KLayout's Python API is used to read in a GDSII file.
- Shapes from layers of the input file are merged into KLayout Regions.
- Boolean operations are performed between the Regions to create virtual Regions like (ndiff = diff - nwell & nsdm).
- A Region's Shapes are iterated over as SimplePolygons and passed to a triangulation library.
- The triangulation is necessary as some OBJ viewers (like OBJLoader2) won't accept concave polygons.
- The resulting set of triangles is extruded to the correct thickness and appropriate faces are made on sides.
- Data is written to the output file in OBJ groups by layer and material is set.
