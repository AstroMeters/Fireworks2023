# Project: Measurement of optical spectras from fireworks

> [!NOTE]
> The first measerument was conducted during the New Year's Eve 2023. Project is currently in early stage of data analysis.

## Introduction

Fireworks, while visually stunning, pose significant risks to the environment and human health. They release various chemicals, including heavy metals that can be toxic. This exposure can lead to health issues like respiratory problems and long-term health impacts.

In addition to health risks, fireworks negatively impact air quality. High levels of airborne particles in the air are often recorded after fireworks shows, highlighting their significant effect. Unlike emissions from industrial processes or vehicles, 
the control over these emissions is limited.

![EOSR0916_s](https://github.com/roman-dvorak/Fireworks2023/assets/5196729/0ded7bbc-ed8d-42df-afb6-dae9101b5f0a)

For more details on this issue, refer to these articles:
* [AVEX Czech Academy of Sciences: FIREWORKS: toxic show with unbearable health risks.](https://www.icpf.cas.cz/wp-content/uploads/2023/07/2_2023-AVEX-ohnostroje-def.pdf) (in Czech)
* [ChmiBrno.org: The impact of firing pyrotechnics on air quality – a summary.](https://chmibrno.org/blog/2023/12/27/vliv-odpalovani-zabavni-pyrotechniky-na-kvalitu-ovzdusi-shrnuti/) (in Czech).
* [irozhlas.cz: New Year's fireworks, despite regulations, reached record of air pollution levels. Tábor ‘holds best’ among cities.](https://www.irozhlas.cz/veda-technologie/priroda/ohnostroje-oslavy-novy-rok-petardy-znecisteni-ovzdusi-jachym-brzezina-chmu_2301021800_nov) (in Czech)

>[!NOTE]
> This experiment was conducted based on a long-standing interest in the issue of New Year's fireworks in the Europe. It builds on previous [measurements of dust particles](https://wayback.webarchiv.cz/wayback/20220325020234/http://www.ujf.cas.cz/cs/novinky/Vedci-z-UJF-AV-CR-zmerili-znecisteni-atmosfery-novorocnimi-ohnostroji/) in the vertical atmospheric profile using ThunderFly drones, the development of the [TF-ATMON system](https://www.thunderfly.cz/tf-atmon.html) for atmospheric measurements, and discussions with meteorologists from CHMI and scientists from the Czech Academy of Sciences.

>[!TIP]
> **If you want to view the measured spectra directly, you can view them in this [PDF document](media/merged.pdf) or [separate page](gallery.md) in the form of a Fireworks gallery. The results from the analysis will be placed [here](analysis.md).**


## Experiment
Our experiment conducted on New Year's Eve 2023 in Prague aimed to identify elements in fireworks using spectral analysis.
The following goal of this experiment was to validate whether optical spectra of fireworks can be measured using this method, we also wanted to know what is needed for such measurements and what kind of results we might expect.
Additionally, we wanted identify any issues inherent in this approach and propose potential improvements for future measurements.

The setup was strategically placed in higher floors of tower-building in Prague housing estate for optimal viewing and data capture. We conducted capturing diverse spectra representing different chemical elements used in the publicly-availible fireworks.

## Used aparature
![EOSR0971](https://github.com/roman-dvorak/Fireworks2023/assets/5196729/b99c4376-7233-4b5c-962b-cb13943ac42c)

The setup was assembled using equipment available to us, allowing to conduct measurement without the need for purchasing expensive gear. This setup was chosen as "the best", with the idea that it could be simplified for futhure measurement based on this experiences (check observed problems at end of this document).

- **80/500 ED Telescope**: An optical device with an 80 mm lens diameter and 500 mm focal length, optimized for capturing clear, detailed images.
- **Spectral Grating 100 lines/millimeter**: Separates light into individual spectral lines for chemical element identification ([SA-100](https://www.rspec-astro.com/star-analyser/)).
- **Monochromatic High-Speed Camera**: Records 1000-800 frames per second, important for capturing fast-moving pyrotechnic events ([Chronos 1.4 monochrome](https://www.krontech.ca/product/chronos-1-4-high-speed-camera/)).
- **Tripod**: A sturdy tripod under the telescope allowing for quick aiming of the setup.
- **Finder Scope**: A device for quickly aiming the telescope.
- **Computer with sufficient storage capacity**: The camera produces a large amount of data; a 6-second recording is approximately 7 GB. Data was immediately uploaded via network to the connected computer.


The following images shows the attaching of a diffraction grating to the camera. Grating was screwed to the end of a C-mount to 1.25" barrel adapter. It ensures constant sensor-grating distance within the optical system.

<img src="https://github.com/roman-dvorak/Fireworks2023/assets/5196729/c4ff3cd2-e0c2-44e5-9d8e-66ef24d8ffd8" height="200pt"/> <img src="https://github.com/roman-dvorak/Fireworks2023/assets/5196729/514a96e6-aef7-419b-b3b0-fe0772c6c94e" height="200pt"/> 

## RAW data availability
The RAW data, totaling around 110GB, are available upon request due to their large size. This data includes complete spectral information captured during the experiment.

You can also view (comprimed) video recordins in this [YouTube playlist](https://www.youtube.com/playlist?list=PL3olITvRKy4xV_I5JRlAe6PY4d6_L131k).
[![](https://github.com/roman-dvorak/Fireworks2023/assets/5196729/d03159fc-214c-4bee-bee1-a95ba2072c05)](https://www.youtube.com/playlist?list=PL3olITvRKy4xV_I5JRlAe6PY4d6_L131k).

## Data processing

### Data
The high-speed Chronos camera, offering various data outputs, was used for the measurements. Most data were saved in RAW12 format, efficiently containing values of two nighbourght pixels in three bytes, minimizing unused space and network data flow. Recordings were immediately stored on a connected computer via NFS, using this efficient RAW format to optimize data storage and transfer time.

> Data structure of 12RAW format
> 
> `[8-bits 1st pixel]`,`[last 4 bits of 1st pixel,  first 4 bits of 2nd pixel]`, `[last 8 bits of 2nd pixel]`

Images from RAW12 were converted to 16-bit TIFF images using a Python script, making them compatible with many editors like ImageJ. The command used was `/pyraw2dng.py -M -w 1280 -l 1024 -p $raw_file $dng_files`.

These images were converted to preview videos using FFMPEG (`ffmpeg -framerate 60 -i ${VID}/_%06d.tiff -vf "curves=all='0/0 0.1/0.3 1/1'" -codec:v libx264 -crf 18 -pix_fmt yuv420p ${VID}_export.mp4`) for fast and seamless viewing of videos. Output of ffmpeg is avialible in the mentioned youtube [playlist](https://www.youtube.com/playlist?list=PL3olITvRKy4xV_I5JRlAe6PY4d6_L131k). During the conversion of RAW frames to video, dark parts of the video were highligted using curves in ffmpeg. Therefore, these videos are not suitable for further analysis.

The RAW 16-bit TIFF images were subsequently used for more precise analysis and processing using Python 3 and the Jupyter Notebook environment. 

## Processing steps

#### 1. Selecting good frame
The first step in the process involves manually selecting interesting frames. This is done by reviewing the preview videos and finding the corresponding frame in the form of a 16-bit TIFF image exported from the RAW12 format. During this selection, the visibility of individual spectra, their distinctness, correct brightness, and lack of overlap with other spectra or particles are assessed. The focus of the video is also a important aspect to consider.

#### 2. Importing intu jupyter notebook project
The selected frame is then imported into a Jupyter Notebook by providing the absolute path to the image file and asseting this filename into `filename` variable. 

#### 3. Selecting interesting spectrum
Subsequently, interactive sliders are used to select the spectrum of interest. These sliders adjust the position and direction of the line along which the spectrum is calculated. Settings include the starting point (x1, y1) of the line, its angle against the pixel matrix, length of the line, and the width of the area over which the sum of pixel values is calculated in the normal direction to the selected profile.

The selected line is then dynamically visualized over image, including the display of intensity along the chosen profile.
![obrazek](https://github.com/roman-dvorak/Fireworks2023/assets/5196729/5f2ea1ac-e321-4cab-9f03-d3bda1fd8d71)

#### 4. Selecting source position
Next step is to local position of spectra source in frame.

Next interactive slider is utilized to select the position of the zero pixel (the actual source of the spectrum) in the image. The selected position is immediately displayed above the intensity profile as a vertical line, allowing for precise and fast alignment of the spectrum's origin in the image.
![obrazek](https://github.com/roman-dvorak/Fireworks2023/assets/5196729/02abe01b-652c-40dc-8d27-fe901f62d9d5)

#### 5. Spectrum calculation
In the next step, the pixel position is converted into a wavelength using a predefined calibration.
This process results in two graphs. The first graph displays the entire profile with the wavelength in the first order of the spectrum (note that the second order of the spectrum is also visible in the screenshot). The second graph shows only visible part of the spectrum, which is identical across all profiles.
![obrazek](https://github.com/roman-dvorak/Fireworks2023/assets/5196729/0fa76737-6383-415f-bf42-80aeb7d3f275)


#### 6. PDF analysis report
In the final step, the exported graphs are saved as `.png` images, and a PDF report is created, which can be seen in the following image. 
[![obrazek](https://github.com/roman-dvorak/Fireworks2023/assets/5196729/6caa9542-298b-4a28-89a2-adfae01138a6)](media/merged.pdf)

**What does the PDF report contain?**
The title includes the name (including the full path) of the file that was analyzed. The line below it contains the configuration used for this generation. With this information, an identical output can be generated.

The first image shows a preview of the frame with the highlighted line (profile) along which the spectrum analysis was conducted. The line is as wide as the width of the analyzed strip.

The first graph displays the intensity profile along to the shown profile/line.

The second graph then shows the visible part of the measured spectrum. If there are two curves in the figure, it means that the recording includes both the first order of the spectrum and the minus first order. This can be recognized by the number next to the wavelength label in parentheses.


# Fireworks gallery
> [!TIP]
> Due to larger amount of processed images spectra gallery is placed in own [document](gallery.md).
> Or you can browse [PDF report](media/merged.pdf) of all analyzed measurements.


## Spectra callibration

For the conversion of pixel position to wavelength [nm], the following equation was used:


$$\theta := arctan2( px \cdot  pixelsize_m , L_m)$$

$$wl := \dfrac{ D_m \cdot sin(\theta) }{ order } \cdot 10^9 $$


where:

* $px$: Distance in pixels
* $wl$: Output wavelength
* $D_m$: Number of lines per m on the diffraction grating
* $L_m$: Distance of the diffraction grating from the sensor plane
* $pixelsize_m$: Pixel size (pitch)
* $order$: Desired order of the spectrum
* $\theta$: Difraction angle

**Input values**
| Parametrer | Value | Note |
|-----|-------|-------|
| $D_m$ | $1.0 \times 10^{5}$ | Number of lines per meter (100 lines/mm) |
| $L_M$ | $0.0477$ | Distance between grating and sensor plane in m ($11.7 + 36 mm$) |
| $pixelsize_m$ | $1.0 \times 10^{-5}$ | Pixel pitch in m |


Calibration were done over measured/obtained values of setup. Then it was recalibrated over high-pressure sodium lamps.

Calibration was validated with green (532 nm) laser pointer. 
![obrazek](https://github.com/roman-dvorak/Fireworks2023/assets/5196729/678e22ce-9dbc-41e7-883b-c5792ec0ee97)


>[!CAUTION]
> Calibration should be improved/checked with some better callibration sources.


# Element recognisation in measured spectral profiles

Estimation of elements from spectra is a critical part of this project. Specific elements are identified based on their unique spectral lines. This process involves comparing observed spectra against known spectral lines of various elements. By analyzing the position and intensity of these lines, it's possible to determine the composition of the substance being observed.

**Description of the analysis of individual spectra and their elements is located in a separate document called [Analysis](analysis.md).**

>[!CAUTION]
>I currently do not have  this part of project implemented in any form. During exploring of availible options, I found it difficult to find an accessible spectrum catalog for this purpose. If you have any tips or ideas on how to solve this, I would appreciate any suggestions and comments.
>
>Also, I am still unsure whether the resolution and quality of the measured spectra allow for such an analysis.


# Observed problems
During the measurement process, the following problems of this approach were identified:


1. **Focusing Issue**: The setup had a low depth of field, making it difficult to focus on fireworks at varying distances. The best method was to wait for a firework at a selected distance and focus on the nearest lamp. Over the telescopes's precise focusing capability, directly focusing on fireworks was challenging.
2. **Dynamic Nature of Fireworks**: The rapid changes and movements of fireworks necessitated a tripod that allows quick adjustments. A video tripod with an ALT/AZ head might be more better choice than a photographic tripod with a ball head.
3. **Long Record Saving Time**: The high-speed camera took several minutes to save a few seconds of record. A lower frame rate, like 100-500 FPS, which some cameras can stream via USB, might suffice, as many interesting fireworks were missed due to saving duration. But short exposition time (bellow 1ms) and global shutter is required. 
4. **Difficulty in selection of Correct Exposure**: Despite the camera's 12-bit depth, choosing the right exposure was problematic. Some parts of the fireworks were overexposed, while others had insufficient signal.
5. **High Magnification**: The telescope with a 500 mm focal length had an excessively high magnification, and combined with a small sensor chip, resulted in a very narrow field of view. This made it difficult to locate the fireworks. An optical finder scope was used to reduced this issue.
6. **Optical Finder Scope**: It would be better to replace the optical finder scope with a red-dot finder, which is easier to look through and more user-friendly for fast locating of fireworks.
