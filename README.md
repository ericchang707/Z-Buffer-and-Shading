# Z-Buffer-and-Shading
In this project we will use a simplified way of setting a current transformation matrix.  We will NOT be using your code from Project 1A and 1B for this, because I do not want your grade on Project 3 to depend on how well you did on the earlier project.  For this reason, we are not going to use the matrix stack or the usual translate, scale and rotate commands.  Instead, you are going to make use of a routine that we will provide that directly sets the 16 numbers that make up the current transformation matrix.

Here are the functions of the routines that you will write:

Init_Scene() - Calling this routine should initialize your z-buffer.  The initial values of the z-buffer should be very large negative values (far away).  You should also set some default values for the material colors (diffuse, ambient, specular).  A portion of this routine that is already provided will set the current transformation to the identity.

Vertex (x, y, z) - As was the case in Part A, this command specifies the (x, y, z) coordinates of one vertex of a triangle.  However, now the location of the vertex will be affected by the current transformation matrix.  We will provide starter code for this routine, but you will need to merge it with your version of this routine from Part A.

Normal (nx, ny, nz) - This command specifies the (nx, ny, nz) normal vector for the next vertex of a triangle that is defined by a call to Vertex().  Like vertex positions, this surface normal will be affected by the current transformation matrix. Such surface normals will be used when the shading is in either the GOURAUD or PHONG mode.  When the shading mode is FLAT, you will not use this normal and instead use a surface normal that you calculate from the triangle's geometry.

Set_Color (r, g, b) - Specifies the diffuse color for triangle vertices.  Any vertices that are specified using the Vertex() command will be given the color that was last specified by a Set_Color() command.  The red, green and blue values in this command should be floating point values in the range of 0 to 1.

Ambient_Specular (ar, ag, ab, sr, sg, sb, pow) - Set the ambient (ar, ag, ab) and specular (sr, sg, sb) colors, as well as the specular exponent.  Store these values along with each vertex.  If this command is not called for a scene, the specular and diffuse colors should be set to black.

Normal (nx, ny, nz) - Sets the current normal vector for subsequent vertices that are specified by the Vertex() command.  You should store the surface normal with other vertex information such as material colors.

Begin_Shape() - Specify that the vertices of a triangle will soon be specified with the Vertex() command.

End_Shape() - Indicates that all the vertices of a triangle have been give, and that the triangle should be rasterized.  As was the case for Part A,, this is where the bulk of your code is likely to be.  However, the routine will behave differently depending on whether the "shading" variable is set to WIREFRAME, FLAT, or GOURAUD.  If it is set to WIREFRAME, the routine will draw the outline of each triangle in black.  This code will be provided for you.  If it is set to CONSTANT, FLAT, GOURAUD or PHONG, you should call your rasterization code to draw the current triangle.

Set_Light (x, y, z, r, g, b) - Sets the position (x, y, z) and the color (r, g, b) of the light source.  We will be using directional light source, which means we will treat all lights as if they are very far away in the given direction (x, y, z).  It is your responsibility to normalize the (x,y,z) values of a directional light before you use it in your shading equations.  The light position is not affected by the current transformation matrix, that is, its direction is specified in world space.  For this project, there will only be one light source in a scene.

Set_Field_Of_View (fov) - Sets the field of view for perspective projection.  If the value given is zero, then orthographic projection will be used instead.  This routine is provided for you in full.

Set_Matrix (16 floats) - This routine sets the 16 floats that make up the current transformation matrix.  This routine is provided for you in full.

Note that we will be using the x, y, and z values of the vertices.  All three coordinates will be used to transform a vertex by the current transformation matrix.  Also, the z values will be used for determining whether a given pixel is visible or not, based on the z-buffer algorithm.

The provided code in the Vertex() routine will perform orthographic or perspective projection, depending on the field of view.  A zero value for field of view indicates that orthographic projection will be used, which for this assignment essentially means no projection will be performed.  Note that we will not be using the map-to-screen values such as left, right, top, bottom, near, far. When the field of view is non-zero, the provided code in Vertex() performs the perspective projection.  You should not need to modify this part of the code.  What you will need to do is take the calculated xx, yy, zz values and store them for later use in rasterization when End_Shape() is called.  Store these projected vertex coordinates in any data structure that you see fit to use.


