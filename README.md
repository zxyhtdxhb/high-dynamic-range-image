# high-dynamic-range-image
Creating HDR image from image stack with multiple exposures

## Introduction
The goal of this project is to recover high dynamic range radiance maps from photographs in order to crease an image that captures details from the entire dynaimic range. We first implement algorithm from [Debevec, Malik](http://www.pauldebevec.com/Research/HDR/debevec-siggraph97.pdf) to recover high dynamic range radiance map and then apply tone mapping and intensity adjustment to convert the radiance map into displayable HDR image.

## Algorithm Overview
### High Dynamic Range Radiance Map Construction
1. Film Response Curve Recovery
>Film response curve is a function g=ln(f-1) maps from pixel values Zij (from 0 to 255) to the log of exposure values: g(Zij) = ln(Ei) + ln(tj) (equation 2 in Debevec). Zij is the observed pixel value at pixel i at image j from image stack and it is a function of scene radiance and known exposure duration, Zij = f(Ei * Δtj). Ei is the unknown scene radiance at pixel i, and scene radiance integrated over some time (Ei * Δtj) is the exposure at a given pixel. 
>This response curve can be used to determine radiance values in any images acquired by the imaging processing associated with g, not just the images used to recover the response curve.

2. High Dynamic Range Radiance Map Construction
>Once the response curve g is recovered, we can construct a radiance map based on equation 6 in Debevec. In order to reducing noise in the recovered radiance value, we use all the available exposrues for a particular pixel to computer its radiance.

### Tone Mapping
>Global tone mapping: In this project, we use gamma correction as global tone mapping. The output image is proportional to the input raised to the power of the inverse of gamma. 

### Color Adjustment
>In order to construct HDR image to be as closer to input image as possible, we adjust the output image average intensity for each channel (B, G, R) to be the same as template image. Typically, we use middle image from image stack as template.

## Result 1
### Original image
<table>
<tr>
<th><img src="https://github.com/vivianhylee/high-dynamic-range-image/raw/master/example/sample-00.png" /><br>Exposure 1/160 sec</th>
<th><img src="https://github.com/vivianhylee/high-dynamic-range-image/raw/master/example/sample-01.png" /><br>Exposure 1/125 sec</th>
<th><img src="https://github.com/vivianhylee/high-dynamic-range-image/raw/master/example/sample-02.png" /><br>Exposure 1/80 sec</th>
<th><img src="https://github.com/vivianhylee/high-dynamic-range-image/raw/master/example/sample-03.png" /><br>Exposure 1/60 sec</th>
<th><img src="https://github.com/vivianhylee/high-dynamic-range-image/raw/master/example/sample-04.png" /><br>Exposure 1/40 sec</th>
<th><img src="https://github.com/vivianhylee/high-dynamic-range-image/raw/master/example/sample-05.png" /><br>Exposure 1/15 sec</th>
</tr>
</table>

### HDR image
<img src="https://github.com/vivianhylee/high-dynamic-range-image/raw/master/example/output1.png" width="500"/>

## Result 2
### Original image
<table>
<tr>
<th><img src="https://github.com/vivianhylee/high-dynamic-range-image/raw/master/example/sample2-00.jpg" /><br>Exposure 1/400 sec</th>
<th><img src="https://github.com/vivianhylee/high-dynamic-range-image/raw/master/example/sample2-01.jpg" /><br>Exposure 1/250 sec</th>
<th><img src="https://github.com/vivianhylee/high-dynamic-range-image/raw/master/example/sample2-02.jpg" /><br>Exposure 1/100 sec</th>
<th><img src="https://github.com/vivianhylee/high-dynamic-range-image/raw/master/example/sample2-03.jpg" /><br>Exposure 1/40 sec</th>
<th><img src="https://github.com/vivianhylee/high-dynamic-range-image/raw/master/example/sample2-04.jpg" /><br>Exposure 1/25 sec</th>
<th><img src="https://github.com/vivianhylee/high-dynamic-range-image/raw/master/example/sample2-05.jpg" /><br>Exposure 1/8 sec</th>
<th><img src="https://github.com/vivianhylee/high-dynamic-range-image/raw/master/example/sample2-06.jpg" /><br>Exposure 1/3 sec</th>
</tr>
</table>

### HDR image
<img src="https://github.com/vivianhylee/high-dynamic-range-image/raw/master/example/output2.png" width="500"/>




