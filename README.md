
<!-- README.md is generated from README.Rmd. Please edit that file -->

# praatpicture

<!-- badges: start -->
<!-- badges: end -->

If you’ve ever had to fiddle around with getting a Praat Picture to look
and export just right in order to insert it in an R markdown file or
slide deck, then this package is for you! It’s a simple set of functions
designed to emulate some common plots made in Praat Picture with base R
plotting. It allows for flexibly combining waveforms, spectrograms,
TextGrids, pitch tracks, formant tracks, and intensity tracks in a
single plot. Waveforms and spectrograms are generated directly in R (the
latter using the function `phonTools::spectrogram()`, which takes some
time to plot and looks a little different from an equivalent Praat
spectrogram, but still looks quite nice!). TextGrids, pitch tracks,
formant tracks, and intensity tracks can be plotted as long as there are
files with the `.TextGrid`, `.PitchTier`, `.Formant`, and
`.IntensityTier` exported from Praat in the same directory and with the
same base name as the sound file. These are loaded in using functions
from the `rPraat` package. Default settings are as similar as possible
to those in Praat, and the same with the different options for changing
these settings.

If you run into bugs or have suggested changes, please let me know!

## Installation

You can install the development version of `praatpicture` like so:

``` r
#install.packages('devtools')
devtools::install_github('rpuggaardrode/praatpicture')
```

## Examples

``` r
library('praatpicture')
```

The Praat Picture I see (and use) most commonly simply consists of a
relatively small waveform, a larger spectrogram, and an aligned
TextGrid. Accordingly this is very simple to make with `praatpicture()`.
Simply pass the name of a sound file with the `.wav` or `.mp3` extension
to the function, and voila!

``` r
praatpicture('inst/extdata/1.wav')
```

<img src="man/figures/README-unnamed-chunk-4-1.png" width="100%" />

Often you won’t want to plot an entire sound file, but only a small
portion of it. This is no problem – simply use the `start` and `end`
arguments to tell R exactly what you want to plot. If we just want to
plot the portion between 0.5–1.1 seconds of the above file, we do it
like this:

``` r
praatpicture('inst/extdata/1.wav', start=0.5, end=1.1)
```

<img src="man/figures/README-unnamed-chunk-5-1.png" width="100%" />

By default, the first tier in the TextGrid is plotted. If we want to
plot different tiers, we can tell R using the `tiers` argument. The
`freqrange` argument controls the frequency limits of the spectrogram.
We can use the `proportion` argument to control how much space is taken
up by different frames. The `tfrom0` argument controls whether the
x-axis starts from 0 or from the `start` time.

Say we want to redo the plot with the 3rd and 4th tiers of the TextGrid,
with frequencies up to 8000 Hz, showing the original time on the x axis,
and with a bit less space for the waveform and more space for the
TextGrid. It would look like this:

``` r
praatpicture('inst/extdata/1.wav', start=0.5, end=1.1, tiers=c(3,4), 
             freqrange=c(0,8000), tfrom0=FALSE, proportion=c(20, 50, 30))
```

<img src="man/figures/README-unnamed-chunk-6-1.png" width="100%" />

Other options for generating spectrograms, like in Praat, are
`windowlength` (in seconds), `dynamicrange`, `timestep`, and
`windowshape`.

If we want to reorder the components of the plot, or look at other
components, we do so using the `frames` argument. If for example we
wanted to plot a pitch track instead of a spectrogram, we do it like so:

``` r
praatpicture('inst/extdata/1.wav', start=0.5, end=1.1, tiers=c(3,4), 
             frames=c('sound', 'pitch', 'TextGrid'))
```

<img src="man/figures/README-unnamed-chunk-7-1.png" width="100%" />

I personally prefer the Praat’s ‘speckle’ method of drawing pitch, which
we can set using the `pitchtype` argument. We can also adjust the y-axis
using `pitchrange`, and the scale using `pitchscale`. Say we want pitch
between 100–200 Hz speckled in a log-scale, we do it like this:

``` r
praatpicture('inst/extdata/1.wav', start=0.5, end=1.1, tiers=c(3,4), 
             frames=c('sound', 'pitch', 'TextGrid'), pitchtype='speckle', 
             pitchscale='logarithmic', pitchrange=c(100,200))
```

<img src="man/figures/README-unnamed-chunk-8-1.png" width="100%" />

Additionally there’s the argument `semitones_re` which sets the
reference level if the scale is in semitones.

We could also plot formants instead of pitch:

``` r
praatpicture('inst/extdata/1.wav', start=0.5, end=1.1, tiers=c(3,4), 
             frames=c('sound', 'formant', 'TextGrid'))
```

<img src="man/figures/README-unnamed-chunk-9-1.png" width="100%" /> Or
even just formants – there’s no requirement to plot waveform and
TextGrid, we could just plot a single frame. If we wanted to draw
formants with lines instead in a slightly narrower range (say, between
500–4000 Hz), we would use the `formantrange` and `formanttype`
arguments.

``` r
praatpicture('inst/extdata/1.wav', start=0.5, end=1.1, frames='formant', 
             formantrange=c(500,4000), formanttype='draw')
```

<img src="man/figures/README-unnamed-chunk-10-1.png" width="100%" />

We could also have more frames – for example, waveform, pitch track,
intensity tier, and TextGrid at the same time, like this:

``` r
praatpicture('inst/extdata/1.wav', start=0.5, end=1.1, tiers=c(3,4),
             frames=c('intensity', 'sound', 'pitch', 'TextGrid'),
             pitchtype='speckle', pitchrange=c(100,160))
```

<img src="man/figures/README-unnamed-chunk-11-1.png" width="100%" />

Additionally, because `praatpicture`s are base R plots, it understands
all global base plotting arguments. If, say, you want your Praat Picture
to be red on a light grey background, using a larger monospaced font
that’s both bold and italic, there’s literally nothing stopping you.

``` r
praatpicture('inst/extdata/1.wav', start=0.5, end=1.1, tiers=c(3,4),
             frames=c('intensity', 'sound', 'pitch', 'TextGrid'), tier_names=F,
             pitchtype='speckle', pitchrange=c(100,160), bg='lightgrey', 
             bty='c', fg='red', font=4, ps=16, family='mono')
```

<img src="man/figures/README-unnamed-chunk-12-1.png" width="100%" />
