SPLIT RENDER TOOL
Blender Addon

Are you getting "System is out of GPU memory" error? Do you want/need to render a 32K image? Did you render a sequence in which one object is wrong, 
but you don't want to render the hole sequence again? Do you have some older graphics cards (2GB, 4GB, etc) that can't process any of your projects?
Split Render Tool is the addon you need.

SRT brings 2 different functionalities to you:

On one hand, you will be able to animate Blender's crop area frame by frame, bringing the ability to render any part in your scene. This way you don't 
need to render the hole frame, saving you a lot of time.

And on the other hand, it claims to be able to render any file size and any project, on any hardware using your GPU (NOTE: 512 and 1GB GPUs will not 
be able to render large files resolutions yet, like 8K +). It will split the render into small pieces, and merge them later. User interaction is not 
needed at all to merge split files.

SRT goes far away from other similar addons, being able to render single frames and animations. It renders in any file format, and there is an option 
to render in OpenEXR Multilayer format separate passes into different files.

It is well known that split a render into several pieces and merge them later has issues with Denoising internal AI. Blender Denoising works by 
analizing all the image, processing all pixels, and returning the final image. So when we split an image, it just analize those pixels, but AI does 
not know what is beyond them. The resulting image after merge all pieces will have at the borders some pixels that not match with the rest of the 
image. Leaving us with a useless image.

SRT fixes that issue WITHOUT user interaction. This is how it handles the render:
After selecting the number of splits, it will render them, and additionally it will render the borders with some margin. Then it compose the split 
images into one image, and it will add those additional borders on top of it.



Features:

Split Render
	
- Render single frames or animations.
- Split final image into small pieces, and merge them automatically. 
- Fix the split borders issue in final image (only in Combined pass).
- Option in OpenEXR Multilayer format to separate passes into different files.
- System failure detector. If anything goes wrong, SRT detects it and offers you the option to fix it with one click. 

Animated Border
	
- Animate render border like any other object.
- Keyframe options to add and remove them.
- Bake system to animate border.
- Preview crop region while scrolling the timeline, like animating any object property. (NOTE: Preview crop region only works in Blender 3.6 +)
- Option to create a new Blender file with a composition that blurs the edges of the image.
- Option to blur edges based on ellipse mask.
- Option to control the blur size.

Common
	
- Option to use Blender's output file instead of the same folder as Blend file.
- Information about resolution and border sizes.
- Information about render times (Splits of a frame and frames).
- All image file formats.


SRT is compatible with Blender 2.93.3 to 3.6

Because of the way SRT works (at least yet), there is no preview while rendering, and Blender UI gets locked. Unfortunately to cancel the render 
process you need to kill blender app manually. (Something I'm trying hard to solve)

GPUs with 512, 1GB and 2GB might not be able to render big resolutions (8K +). This limitation will be removed in the future. 

By default the output is set to a new folder in Blender' s file folder, called as the Blend file. And the images names start with "srt_" 
followed by frame number (ex: srt_0012.xxx)


How to install this addon:

- Download the zip file.
- Open Blender and go to Edit - Settings
- Go to Add-ons Tab.
- Press Install button, and search for the downloaded zip file.
- Select it and press Install
- Just click the box to enable it and you are ready to go.


How to use this addon:


First steps
	
- Due to the nature of SRT, the project file from within its executed will be slightly modified and saved. SRT automatically detects any failure
  on its processes, and shows a button to fix them (if is the case). Anyway, it is A GOOD PRACTICE to duplicate your original project (to have a
  backup of it) before use SRT.


Split Render
	
- Set your scene settings as usual (file format, resolution, start and end frames, passes, etc)
- Select number of splits in addon preferences (I've managed to render a 16k image with 6 splits in an AMD RADEON 570 4GB, but it depends on the
  complexity of the project too) (NOTE: the more splits, the more time will spent to finish the image)
- And click Render image or Render animation button
- You can separate passes into different files (Only OpenEXR Multilayer format) by enabling Separate layers
- You can enable Use Blender's output, to render files where you want (if output is a folder, the name of files will be "srt_xxxx.xxx")
- You can enable Don't delete cropped files to preserve , split files


Animated border	

- Set your scene settings as usual (file format, resolution, start and end frames, passes, etc).
- Jump to the frame you want to add key, expand Animated border settings tab, set the crop region to your liking, and press Add keyframe button.
- You need at least 2 keyframes (obviously) to Bake the animation (in order to setup all frames between keyframes).
	(NOTE: Additionally you can scroll the timeline to create the bake info, from Blender 3.6 +)
- Then you can press Render animated border button (it will render from start frame to end frame)
- You can enable Create final composition file, and you will end up with a new Blender file called as the original one, plus "_COMPOSITION"
  (ex: AmazingCube.blend > AmazingCube_COMPOSITOR.blend). There will be two image nodes, the second one is connected to some nodes in order to
  blur the edges (The first one will be your original render)
- You can enable Use ellipse mask, so the blur will be based on an ellipse shape instead of square shape
- You can use the slider to control the blur size on edges (in pixels)
	(NOTE: Because it is in pixels, you will need to adjust this value depending on final resolution. 15-30 pixels is ok for 1920x1080 resolution)

