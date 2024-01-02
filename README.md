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

## Experiment
Our experiment conducted on New Year's Eve 2023 in Prague aimed to identify elements in fireworks using spectral analysis.
The following goal of this experiment was to validate whether optical spectra of fireworks can be measured using this method, we also wanted to know what is needed for such measurements and what kind of results we might expect.
Additionally, we wanted identify any issues inherent in this approach and propose potential improvements for future measurements.

The setup was strategically placed in higher floors of tower-building in Prague housing estate for optimal viewing and data capture. We conducted capturing diverse spectra representing different chemical elements used in the publicly-availible fireworks.

## Aparature
![EOSR0971](https://github.com/roman-dvorak/Fireworks2023/assets/5196729/b99c4376-7233-4b5c-962b-cb13943ac42c)

The setup was assembled using equipment available to us, allowing the measurement to be conducted without the need for purchasing expensive gear. This setup was chosen as "the best", with the idea that it could be simplified for futhure measurement based on this experiences.

- **500/80 ED Telescope**: An optical device with an 80 mm lens diameter and 500 mm focal length, optimized for capturing clear, detailed images.
- **Spectral Grating 100 lines per millimeter**: Separates light into individual spectral lines for chemical element identification.
- **Monochromatic High-Speed Camera**: Records 1000-800 frames per second, important for capturing fast-moving pyrotechnic events.
- **Tripod**: A sturdy tripod under the telescope allowing for quick aiming of the setup.
- **Finder Scope**: A device for quickly aiming the telescope.
- **Computer with sufficient storage capacity**: The camera produces a large amount of data; a 6-second recording is approximately 7 GB. Data was immediately uploaded via network to the connected computer.


## RAW data availability
The RAW data, totaling around 150GB, are available upon request due to their large size. This data includes complete spectral information captured during the experiment.

You can also view (comprimed) video recordins in this [YouTube playlist](https://www.youtube.com/playlist?list=PL3olITvRKy4xV_I5JRlAe6PY4d6_L131k).
[![](https://github.com/roman-dvorak/Fireworks2023/assets/5196729/d03159fc-214c-4bee-bee1-a95ba2072c05)](https://www.youtube.com/playlist?list=PL3olITvRKy4xV_I5JRlAe6PY4d6_L131k).

## Data processing


## Spectra callibration

For the conversion of pixel position to wavelength, the following equation was used:


$$\theta := arctan2( px \cdot  pixelsize_m , L_m)$$

$$wl := \dfrac{ D_m \cdot sin(\theta) }{ order }$$


where:

* $px$: Distance in pixels
* $wl$: Output wavelength
* $D_m$: Number of lines per mm on the diffraction grating
* $L_m$: Distance of the diffraction grating from the sensor plane
* $pixelsize_m$: Pixel size (pitch)
* $order$: Desired order of the spectrum
* $\theta": Difraction angle


Calibration were done over measured/obtained values of setup. Then it was recalibrated over high-pressure sodium lamps. Calibration was validated with green (532 nm) laser. 

>[!CAUTION]
> Calibration should be improved/checked with some better callibration sources.



# Observed problems
During the measurement process, the following problems of this approach were identified:


1. **Focusing Issue**: The setup had a low depth of field, making it difficult to focus on fireworks at varying distances. The best method was to wait for a firework at a selected distance and focus on the nearest lamp. Over the telescopes's precise focusing capability, directly focusing on fireworks was challenging.
2. **Dynamic Nature of Fireworks**: The rapid changes and movements of fireworks necessitated a tripod that allows quick adjustments. A video tripod with an ALT/AZ head might be more better choice than a photographic tripod with a ball head.
3. **Long Record Saving Time**: The high-speed camera took several minutes to save a few seconds of record. A lower frame rate, like 100-500 FPS, which some cameras can stream via USB, might suffice, as many interesting fireworks were missed due to saving duration.
4. **Difficulty in selection of Correct Exposure**: Despite the camera's 12-bit depth, choosing the right exposure was problematic. Some parts of the fireworks were overexposed, while others had insufficient signal.
5. **High Magnification**: The telescope with a 500 mm focal length had an excessively high magnification, and combined with a small sensor chip, resulted in a very narrow field of view. This made it difficult to locate the fireworks. An optical finder scope was used to reduced this issue.
6. **Optical Finder Scope**: It would be better to replace the optical finder scope with a red-dot finder, which is easier to look through and more user-friendly for fast locating of fireworks.
