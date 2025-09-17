# lab02-debugging

# Submission
Collaborators: Didn't directly collaborate with anyone, but overheard lots of what Nico's and Lillian's thinking out loud as well as Rui's conversation with Rebecca about reflection.
Solution: https://www.shadertoy.com/view/wflBDf
Bugs:
- Line 97 where uv2 is created, the type was declared as vec but should be vec2. This was easy to find because Shadertoy was throwing a syntax error.
- Line 100 where raycast() is called should be passed the uv2 variable instead of uv because we want the range of pixel coordinates to be in [-1, 1] instead of [0, 1]. I noticed after fixing the first bug that the screen was stretched horizontally, so I figured that the bug would be somewhere in the raycast definitions of H and V.
- Line 11 where H is being updated had length being multiplied by (iResolution.x / iResolution.x) aka 1, so I changed the denominator to be iResolution.y in order to fix the stretching effect in the horizontal direction.
- Line 18 where the raymarching loop is defined, the number of iterations is too small so I increased it to 256 from 64 in order to march far enough to hit all areas of the floor as is shown in the video. The floor being warped and not expanding far enough was one of the first things that I noticed and I figured it would be in the raymarch function.
- Line 75 where dir is updated to be reflect(eye, nor) is incorrect because to get a reflection we need the direction of the camera ray (not the location of the camera) and the normal of the object so if we instead call reflect(dir, nor) to update dir we get the correct reflection. This was also an obvious issue of the program from the start, but harder to find within the functions because of how many functions and lines there are related to the material, reflection, specular reflection, etc.

# Setup 

Create a [Shadertoy account](https://www.shadertoy.com/). Either fork this shadertoy, or create a new shadertoy and copy the code from the [Debugging Puzzle](https://www.shadertoy.com/view/flGfRc).

Let's practice debugging! We have a broken shader. It should produce output that looks like this:
[Unbelievably beautiful shader](https://user-images.githubusercontent.com/1758825/200729570-8e10a37a-345d-4aff-8eff-6baf54a32a40.webm)

It don't do that. Correct THREE of the FIVE bugs that are messing up the output. You are STRONGLY ENCOURAGED to work with a partner and pair program to force you to talk about your debugging thought process out loud.

Extra credit if you can find all FIVE bugs.

# Submission
- Create a pull request to this repository
- In the README, include the names of both your team members
- In the README, create a link to your shader toy solution with the bugs corrected
- In the README, describe each bug you found and include a sentence about HOW you found it.
- Make sure all three of your shadertoys are set to UNLISTED or PUBLIC (so we can see them!)
