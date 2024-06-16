#### Images vs Containers

The Image
	Contains the environment + code
	Are like the templates or blueprints
	Are read only! If you use a `COPY` statement to add some files to the image any modification that you add to the files will not be updates on the image unless you rebuild the image.
The Container
	Running instances of the images
	Multiple containers can run the same image


![[Concepts.excalidraw]]



#### Prebuilt images vs Custom images
Prebuilt images 
	Can be found on docker hub
Custom images 
	Defined in Dockerfile
	Implement a prebuilt image that is then customized


#### Image layers and cached
Every instruction in your dockerfile represents a layer.
![[Layers.excalidraw]]

- Docker saves in cache the different layers.
- If you rebuild an image and don't modify the dockerfile it will rebuild it very fast
- If in the example above you modify the __layer 3__ and rebuild, docker will only used cache from layers 1 and 2.

- Optimization technique based on layers.
In the example above your code gets copied in __layer 2__ 
That means every time you modify your code you rebuild the image and it has to copy it to the image and then do layer 3, layer 4... 
This is not efficient as layer 3 installed nodejs. We should not do this every time. If you do this it would be much more efficient

![[Layers_optimization.excalidraw]]

