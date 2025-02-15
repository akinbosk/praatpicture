# praatpicture 1.2.2
* Added `talking` argument to `emupicture()`, allowing users to make
`talking_praatpicture()` plots with embedded audio directly from an EMU 
database.

# praatpicture 1.2.1
* Fixed color issue when plotting point tiers in `tgplot()`.

# praatpicture 1.2.0

* Shiny support has been added with the `shiny_praatpicture()` function.
* The `proportion` argument no longer has to add up to 100.
* Users can now specify the location of a `.TextGrid` file when plotting
annotations.

# praatpicture 1.1.4

* It's now possible to change font sizes, text adjustment, alignment, etc. 
when using the `annotate` argument

# praatpicture 1.1.3

* Fixed bug that made it impossible to control which channel to highlight
when plotting multiple channels and other frames

# praatpicture 1.1.2 

* Added option to add a vector of strings to `wave_color`, for plotting 
different channels using different colors.

# praatpicture 1.1.1

* Fixed bug that made it impossible to control the lower frequency range of
spectrograms.

# praatpicture 1.1.0

* Options added to draw straight lines (vertical, horizontal, or otherwise) on 
plot components with the `draw_lines` argument. This replaces the 
`formant_dottedLines` argument, but doesn't otherwise change the look of the
default formant plot.
* Background coloring can now be added to lines and speckles when any of the
`*_plotOnSpec` options are `TRUE`. This is done by adding a vector of two 
strings to the `*_color` argument, e.g. `pitch_color=c('blue','lightblue')` for
a blue pitch contour on a light blue background. For `formant_color`, which 
already allowed a vector of multiple strings, this creates a range of options: 
If you pass just two strings but are plotting >2 formants, e.g. 
`c('black','white')` all formants will be plotted in black on a white background.
If you pass N formants + 1 string, the final color will be used as background
for all formants. If you pass double the number of formants, the second half
will be used for individual background colors. 
* Option added for both drawing and speckling formants and pitch in a single
plot. Before `*_plotType` had to be either `'draw'` or `'speckle'`, now also
allows `c('draw','speckle')`. 

# praatpicture 1.0.0

* On CRAN!

# praatpicture 0.6.1

* Initial CRAN submission.
