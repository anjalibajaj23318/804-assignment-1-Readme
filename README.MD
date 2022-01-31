# **MM804**

# **Graphics and Animation Assignment 1**

**Project Directory Structure**

```
│ assignment1.py
├───input
│ lily_full.stl
│ ...
├───output
│ MM804_ASSIGNMENT1_8.jpeg
│ ...
```

**Model used in the project**

1.	Name of the model: Lily - Animal Crossing (from Pocket Camp, ripped by Centrixe)
2.	File size: 1,197,984 bytes (1.2 MB)
3.	Number of vertices: 11574

**Output of the Project**

Output is a jpeg file containing different types of representation of objects, namely, wireframe, and surface with flat, Gouraud and Phong shading.

Top-Left : there is a Wireframe representation.

Top-Right : there is Flat shading representation.

Bottom-Left : there is Gouraud shading representation.

Bottom-Right : there is Phong shading representation.

Here is the screenshot of the output obtained:
![assignment_answer](MM804_ASSIGNMENT1_8.jpeg)
![Assignment1_answer](portal1.png)
![Assignment1_answer](portal2.png)
![Assignment1_answer](portal3.png)

**Commented Source code**

# Print VTK version 

```

print(vtk.VTK_VERSION)

```
# Reading the STL file

```
reader = vtk.vtkSTLReader()
reader.SetFileName("lily_full.stl")
```

# Computing the vertices of the object taken

```

print(reader.GetOutput())

```

# Computing normals

```
teanormals = vtk.vtkPolyDataNormals()
teanormals.SetInputConnection(reader.GetOutputPort())
```

# setting actors and mappers

```
mapper = [vtk.vtkPolyDataMapper() for i in range(4)]
actor = [vtk.vtkActor() for i in range(4)]
```

# adding different shadders in the surface as mentioned in the assignment

```
    mapper[i].SetInputConnection(teanormals.GetOutputPort())
    actor[i].SetMapper(mapper[i])
```
       
 # Setting some properties for Wireframe representation

 ```
    if i==0:
        prop=actor[0].GetProperty()
        prop.SetRepresentationToWireframe()# Set Representation to Wireframe
        prop.SetSpecularPower(100)
```
 # Setting some properties for Flat shading
 ```
    elif i == 1:
        prop = actor[i].GetProperty()
        prop.SetInterpolationToFlat() # Set shading to Flat
        prop.SetColor(0,1,1)
        prop.ShadingOn()
        prop.SetDiffuse(0.8)
        prop.SetAmbient(0.3)
        prop.SetSpecular(0.4)
        prop.SetSpecularPower(100)
```
 # Setting some properties for Gourand shading
```
    elif i == 2:
        prop = actor[i].GetProperty()
        prop.SetInterpolationToGouraud() # Set shading to Gouraud
        prop.SetColor(1,0.5,1)
        prop.ShadingOn()
        prop.SetDiffuse(0.8)
        prop.SetAmbient(0.3)
        prop.SetSpecular(0.4)
        prop.SetSpecularPower(100)
```
 # Setting some properties for Phong s shading
```
    else:
        prop = actor[i].GetProperty()
        prop.SetInterpolationToPhong() # Set shading to Phong
        prop.SetColor(1,1,0)
        prop.ShadingOn()
        prop.SetDiffuse(0.8)
        prop.SetAmbient(0.3)
        prop.SetSpecular(0.4)
        prop.SetSpecularPower(200)
```

# Setting a Render Window

```
renWin = vtk.vtkRenderWindow()
renWin.SetSize(1000, 1000)
```

# Configuring the Renderer
```
ren = [vtk.vtkRenderer() for i in range(4)]
for i in range(4):
    ren[i].AddActor(actor[i])
```

 # adding light
 ```
    lightkit = vtk.vtkLightKit()
    lightkit.AddLightsToRenderer(ren[i])
```

 # adding 4 viewport in the rendered scene
```
 ren[0].SetViewport(0,0.5,0.5,1)  # Top-Left # Wireframe
    ren[1].SetViewport(0.5,0.5,1,1) # Top-Right #Flat
    ren[2].SetViewport(0,0,0.5,0.5) # Bottom-Left # Gouraud
    ren[3].SetViewport(0.5,0,1,0.5) # Bottom-Right # Phong
```

# Configuring interactor and render loop
```
iren = vtk.vtkRenderWindowInteractor()
iren.SetRenderWindow(renWin)
renWin.Render()
win2Im = vtk.vtkWindowToImageFilter()
win2Im.SetInput(renWin) 
win2Im.ReadFrontBufferOff()
win2Im.Update()
```
# writing the output scene as an image
```
imWriter = vtk.vtkJPEGWriter() 
imWriter.SetFileName("MM804_ASSIGNMENT1_8.jpeg") 
imWriter.SetInputConnection(win2Im.GetOutputPort()) 
imWriter.Write()
iren.Start()
```
**README FILE**

# VTK and Python Version

- [VTK - 9.1.0]()
- [Python - 3.9.7]()


# Implementation

```
Open assignment1.py in the file in any editor of your choice. 
Push the input file lily_full.stl into the folder where the asignment1.py file is present. 

Run the file through python assignment1.py 


```

# Build With

- [VTK](https://vtk.org/doc/nightly/html/)
- [Python](https://docs.python.org/3/)


# Installation

- [VTK](https://vtk.org/doc/nightly/html/)


# Language used

- Working with Python: Codes have been written in python which is compact, easier to debug, and allows for ease of extensibility.
