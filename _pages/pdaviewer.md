---
layout: page
title: What is DaltonView?
permalink: /daltonview/
---

## [Download Executable (Windows Only)](https://u.pcloud.link/publink/show?code=kZIhtF0Z6NvagFBteLSceA7yfS636pgR056V) ##

This PDA Viewer is made to simplify the analysis of Thermo UPLC Raw files. While there are other programs that focus on mass spec., there aren't many that work with PDA data. This program has been made to analyze PDA data specifically. It is a Python-based Qt application that utilizes Thermo Scientific's RawFileReader .Net assemblies. Python is not required to run this program.

A general outline to using the program:
* Find your .raw file with the Select File button
* Load in your .raw file with the Load File button
* Set the range of the chromatogram (top plot) using min RT and max RT (RT == retention time)
* * The yaxis is scaled automatically based on this selection
* Select the Scan # either by entry or by using the arrows
* * The RT of the current Scan # is indicated by a stick in the chromatogram
* * Double up/down arrow == Increase/decrease Scan # by 10
* * Single up/down arrow == Increase/decrease Scan # by 1
* * The intial scan number is set randomly. If it is outside of the range, reset it by putting in '1'.
* Set the range of the spectrum (bottom plot) using min WL and max WL (WL == wavelength)
* * The yaxis is scaled automatically based on this selection
* Save the figure if you want to keep the image of the spectrum for later reference
* Export all data with the Save Data button

Some notes about the Save Data feature:
* Three files are created as **tab-delimited** text files
* They are saved in the same folder as the loaded .raw file
* They **do not** have column headers
* * The _Chromatogram.txt file has two columns: [RT] and [Intensity in microAU]
* * The _Wavelengths.txt file has one column: [Wavelengths in nanometers]
* * the _Spectra.txt file is a 2D array
* * * Each column corresponds the each time in [RT]
* * * Each row corresponds to each wavelength in [Wavelengths]
* * * The data are microAU values at that Wavelength,RT combination

<img src="\images\pdaviewer.png" style="margin: 20px auto 20px; display: block; width: 70%;"/>


This program is early in development and more features are expected to be added over time. Feel free to suggest some features by emailing info{at}daltonian.co.