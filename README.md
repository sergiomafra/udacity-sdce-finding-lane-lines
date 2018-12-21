# Finding Lane Lines on the Road

#### Goals

- Make a pipeline that finds lane lines on the road
- Reflect on what I built in this report

---

#### Paths and References

Output images directory:
`test_images_output/`

`solidWhiteCurve.jpg`
`solidWhiteRight.jpg`
`solidYellowCurve.jpg`
`solidYellowCurve2.jpg`
`solidYellowLeft.jpg`
`whiteCarLaneSwitch.jpg`

Output videos directory:
`test_videos_output/`

`solidWhiteRight.mp4`
`solidYellowLeft.mp4`
`challenge.mp4`

---
#### Reflections

**Pipeline description**

The pipeline itself consists of manipulating images and applying filters to them so the computer can see lane lines on a road. In other words, I need to teach the computer how to see taking into consideration some basic things like colors, shapes, orientation, and position in the image.
To do so, I've applied the Canny Edge technique in order to find abrupt color changes on a grayscaled imaged and generate an image with thinner edges.
First I transformed the color scale of the image to grayscale and applied a Gaussian smoothing to it to suppress noise and spurious gradients.
Then I delimited the low and high threshold, meaning that pixels below the low threshold would be discarded (turned black) and pixels above the high threshold will be analyzed to find strong edges. The in-between pixels will be considered only if they are connected to a strong edge. The values of low and high thresholds are 50 and 150 respectively and respecting the maximum indicated ratio of 1:3. 
Subsequently, I applied the Canny edge filter with the OpenCV module generating a new image with the edges on focus.
Because the lane lines will appear in the image only in the lower half of the image, there is no need to analyze the whole image. Therefore a region of consideration was created to shorten drastically the number of irrelevant pixels shaped as a four-sided polygon mask.
Now, the Hough Transform filter and a color filter were applied to the image to finally find the lane lines on the image and paint them as red extrapolated line segments.

**Possible Shortcomings**

- The average slope varies from an image to another, so the line keeps bouncing as the video goes forward. I should find a way to smooth this variance.
- It does not work at all on curves. I still need to figure out how to improve my draw_lines() function to consider curves.
- It probably would not work in a situation which a car would be changing from a line to another.

**Improvement suggestions**

- Study a way to make the pipeline work on curves and changing lines situations.
- Optimize the code speed and efficiency focusing on real-time analyzes.
- Study a better way to correlate Hough Transform variables to improve lane lines identification.