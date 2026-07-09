---
title-slide: false
bibliography: references.bib
csl: vancouver.csl
citeproc: true
theme: serif
background-color: "#ffffff"
transition: slide
navigationMode: linear
hash: true
---

:::: {.columns}
::: {.column width="50%"}

## Sample slides
#### PlaceHolderName
#### Universiti Malaysia Perlis
#### [placeholder@email.com](mailto:placeholder@email.com)

<audio id="bg-music" src="media/audio/sb.m4a" loop></audio>

<div id="audio-credit"
     style="position: absolute; bottom: 40px; right: 20px; font-size: 0.6em; opacity: 0.6;">
  Music: “Adrift” by Scott Buckley (CC BY 4.0)
</div>

<script>
  document.addEventListener('DOMContentLoaded', () => {
    const audio = document.getElementById('bg-music');
    const credit = document.getElementById('audio-credit');

    // hide credit by default
    credit.style.display = 'none';

    const test = new Audio('media/audio/bgm.mp3');

    test.addEventListener('canplaythrough', () => {
      // bgm.mp3 exists → use it, keep credit hidden
      audio.src = 'media/audio/bgm.mp3';
    }, { once: true });

    test.addEventListener('error', () => {
      // bgm.mp3 missing → sb.m4a will play → show credit
      credit.style.display = 'block';
    }, { once: true });

    document.addEventListener('click', () => {
      if (Reveal.getIndices().h === 0) {
        audio.volume = 0.5;
        audio.play();
      }
    }, { once: true });

    Reveal.on('slidechanged', (event) => {
      if (event.indexh > 0) { audio.pause(); }
      else { audio.play(); }
    });
  });
</script>

:::

::: {.column width="50%"}
![](media/pics/logo1.png)
:::

::::

---

:::: {.columns}
::: {.column width="50%"}
### Slide one
**Key Concepts:**
- Energy conservation per @carnot1824.
- $\Delta U = Q - W$
:::

::: {.column width="50%"}
![](media/pics/sample.png)
:::
::::

---

<span class="slide-title" data-title="My Hidden Slide Name"></span>

![](media/pics/wide.jpeg)

---

:::: {.columns}
::: {.column width="50%"}
### The Master Equation
The fundamental relation of thermodynamics:

$$\Delta U = Q - W$$

The work done $W$ is positive when the system expands against an external pressure.
:::

::: {.column width="50%"}
<video data-src="media/videos/sample.mp4" data-autoplay loop muted width="100%"></video>
:::

::::

---

:::: {.columns}
::: {.column width="50%"}
### Visualizing the Gas Law
**Interactive Model:**

- P, V, and T relationships.
- Use the slider to adjust pressure.
- Observe the phase boundary.
:::

::: {.column width="50%"}
<iframe 
  data-src="media/plots/sample.html" 
  width="100%" 
  height="500px" 
  style="border:none;" 
  scrolling="no">
</iframe>
:::
::::

---

:::: {.columns}
::: {.column width="50%"}
### Summary: T-Test Analysis (Machine 1 vs Machine 2)

Our independent two-sample t-tests revealed significant differences in measurement between Machine 1 and Machine 2 under both tested conditions.

**Condition 1: Pressure = 100kPa, Temperature = 303K**
- **T-statistic:** -11.74 (very strong evidence against null)
- **P-value:** < 0.0001
- **Conclusion:** Yes, there is a true difference (p < 0.05).

**Condition 2: Pressure = 300kPa, Temperature = 373K**
- **T-statistic:** -3.23
- **P-value:** 0.0013
- **Conclusion:** Yes, there is a true difference (p < 0.05).

Both conditions indicate that the mean measurements produced by Machine 1 and Machine 2 are statistically different, suggesting a need for further investigation into their operational parameters or calibration.
:::

::: {.column width="50%"}
<!-- You can add an image here, e.g., ![](media/pics/ttest_summary.png) -->
<p style="text-align: center; font-size: 1.2em; color: #555;">Visualizations from Slides 13 and 16 provide detailed views.</p>

<iframe 
  data-src="media/plots/t_test_p100_t303.html" 
  width="100%" 
  height="250px" 
  style="border:none;" 
  scrolling="no">
</iframe>

<iframe 
  data-src="media/plots/t_test_p300_t373.html" 
  width="100%" 
  height="250px" 
  style="border:none;" 
  scrolling="no">
</iframe>
:::
::::

---

:::: {.columns}
::: {.column width="50%"}
### Summary: T-Test Analysis (Machine 1 vs Machine 2)

Our independent two-sample t-tests revealed significant differences in measurement between Machine 1 and Machine 2 under both tested conditions.

**Condition 1: Pressure = 100kPa, Temperature = 303K**
- **T-statistic:** -11.74 (very strong evidence against null)
- **P-value:** < 0.0001
- **Conclusion:** Yes, there is a true difference (p < 0.05).

**Condition 2: Pressure = 300kPa, Temperature = 373K**
- **T-statistic:** -3.23
- **P-value:** 0.0013
- **Conclusion:** Yes, there is a true difference (p < 0.05).

Both conditions indicate that the mean measurements produced by Machine 1 and Machine 2 are statistically different, suggesting a need for further investigation into their operational parameters or calibration.
:::

::: {.column width="50%"}
<!-- You can add an image here, e.g., ![](media/pics/ttest_summary.png) -->
<p style="text-align: center; font-size: 1.2em; color: #555;">Visualizations from Slides 13 and 16 provide detailed views.</p>

<iframe 
  data-src="media/plots/t_test_p100_t303.html" 
  width="100%" 
  height="250px" 
  style="border:none;" 
  scrolling="no">
</iframe>

<iframe 
  data-src="media/plots/t_test_p300_t373.html" 
  width="100%" 
  height="250px" 
  style="border:none;" 
  scrolling="no">
</iframe>
:::
::::

---
# Bibliography
<div id="refs"></div>
