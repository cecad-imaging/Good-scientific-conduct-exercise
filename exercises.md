# Exercises

## Getting started with OMERO [1]
1.	Let´s get started with the image data management server OMERO. Please start the webclient (i.e. open https://omero-1.cecad.uni-koeln.de in your favorite webbrowser).
2.	Make yourself familiar with the user interface:
3.	First, click on your group name (CIF-Good Scientific Conduct, in the upper left of the window) and let OMERO display the data of all group members (`CIF-Good Scientific Conduct> CIF-Good Scientific Conduct >All Members`).
4.	Go to the project GSC exercise and select the dataset sample data.
5.	Be aware that there are just these two levels of hierarchy in OMERO (i.e. Projects and Datasets). However, check out the Tags tab and realize that tags are a very powerful approach to keep your data organized.
6.	Select one of the images. Assign tags, a comment and a rating using the function in the General tab (right side of the window). Here, in the Attachments section, you can also manage attachments (i.e. add, delete or download non-image files belonging to your image data.
7.	Also, have a look at the buttons in the top right corner of the General tab. Here you can get a link referring to your image, or download your images in their original version or converted to a general image file format. Please just try to download on of the images.
8.	Select one of the *sted-confocal* images and on the right switch to the acquisition tab. The Original Metadata gives you easy access to your acquisition settings.
9.	Proceed to the Preview tab. Here you can adjust the color and brightness of your image (i.e. the corresponding lookup table). If you select `Save to All` these settings are applied to all images in the current dataset (which would not be good in our case).
10.	If you double click one of the image thumbnails, it opens the image in a new tab and you could do measurements and annotations using the ROI tools. Close the image tab.
Optional:
11.	If you have the Omero.insight software installed, please open the config window by clicking the little wrench icon and enter the server address omero-1.cecad.uni-koeln.de. Confirm settings and enter your credentials in login screen to connect to Omero.
12.	Unfold the Display Groups dropdown menu in the toolbar and tick the All Members checkbox in your group.
13.	Start the importer (toolbar icon with blue arrow and colorful circles). Select an image file from your local hard drive for upload. Create your own project and dataset, start the import and close the importer when done.
14.	NOTE: You need the insight client to upload new images. This is impossible with the webclient.
15.	Update the projects view (icon on top of the Project tab) and find your uploaded file.

## FIJI and OMERO  [2]
FIJI (FIJI is just ImageJ) is a very versatile and extendible open source tool for image processing and analysis. By installing the omero-insight-ij-plugin you can access your data stored on OMERO.
1.	To install the plugin unpack the archive file you downloaded from the OMERO download site (be aware that the plugin version has to match the server version) and move the folder in the plugins folder of FIJI. After restarting FIJI a new entry (OMERO) should appear in the plugins menu.
2.	Choose `Plugins>OMERO>Connect to OMERO` from the menu. Open the *sted-confocal.lif [Fab Antikoerper]* image by double clicking. (Adjust the `Display Groups` settings to `All Members` for the CIF-Good Scientific Conduct group to find the data by Peter Zentis.
3.	In FIJI select a square ROI in the image. Crop the image to this ROI (`Ctrl-Shift-X`) and select `Plugins>OMERO>Save image(s) to OMERO`. In the following dialog select *GSC exercise* as project and give a name of your choice for the dataset. Then click `Add to the Queue` and `Import`. (If it does not work try to restart FIJI and try again.)
4.	Update the view in the OMERO insight window. Find the cropped image you just saved and open it by double clicking it.
5.	In FIJI draw a ROI into that image. Click `Plugins>OMERO>Save ROIs to OMERO`. Click `Save` in following dialog.
6.	Update the view in the insight client and check whether you can find your ROI.

## Brightness and contrast adjustment, background correction
1.	From the OMERO menu in FIJI select Connect to OMERO (`Plugins>OMERO>Connect to OMERO`). Find (e.g. via `Tags>Peter Zentis>exercise 1` and open the file *gel.tif*.
2.	Draw a rectangular ROI around the fifth lane from the top and run `Analyze>Plot Profile`
3.	From the resulting plot determine the maxima of the two major peaks and calculate the intensity ratio.
4.	Now do Brightness and Contrast adjustment (`Ctrl-Shift-C`) i.e. click first `Auto` and then `Apply`. Again plot the Profile and calculate the intensity ratio.
5.	Close the image and open it anew from OMERO. Assume you knew about a constant background in your image of 62 intensity units. Correct for this by `Process>Math>Subtract>`, set to `62` and confirm. Now again create a profile plot of the fifth lane and calculate the intensity ratio.

## Size measurements  [3]
The image you obtain with a microscope is blurred by the optics of the microscope itself. The point spread function describes the impulse response of the microscope, i.e. the 3D diffraction pattern resulting from a single point. In microscopes, the image formation process is linear, which means that the imaging of many objects produces a result that is the sum of individually imaged objects. Therefore, image formation in a microscope can be seen as a convolution of the true object with the PSF.
Estimating the PSF of a microscope then allows image deconvolution – a process where the true image is estimated by trying to reverse the effects of the convolution. The problem is that deconvolution is an ill-posed problem – no unique solution might exist and noise can strongly influence a solution. Computing intense deconvolution algorithms are used to approximate the true image; a PSF for deconvolution can be obtained by measuring sub-resolution beads with known radii or by theoretical estimation using parameters of the optical system.

In this exercise, we use an artificial ground-truth image (which in reality is not known!) and convolve this image with a single slice of a measured PSF.
1.	From the OMERO menu in FIJI select Connect to OMERO (`Plugins>OMERO>Connect to OMERO`). Find (e.g. via `Tags>Peter Zentis>exercise 2` and open the file *bead-groundtruth.tif*.
2.	Measure the size of the beads in the groundtruth image: Threshold the image (`Ctrl+Shift+T`, choose `Huang` as autothreshold algorithm and `Apply`) and measure by `Analyze> Analyze Particles`. Save your image, ROIs and measurement to OMERO.
3.	Download the attachment of `PSF-LeicaSP8-63x-Ar488.tif` (this is a txt-file containing the image converted to an ASCII encoded table).
4.	Re-open the *groundtruth image* from OMERO. Select `Process>Filter>Convolve`. In the dialog select `Open` and choose the downloaded *PSF txt-file*. Run the convolution.
5.	Acknowledge what the microscope “does to the truth”. Do again a Huang Autothreshold and measure via Analyze Particles. Compare the results!

## Resampling  [4]
1.	From the OMERO menu in FIJI select Connect to OMERO (`Plugins>OMERO>Connect to OMERO`). Find (e.g. via `Tags>Peter Zentis>exercise 3` and open the file *resampling-test.tif*. This is a 20x20 pixel black-and-white image. Use the magnification tool to zoom to the maximum magnification. You should now see a one pixel wide and a two pixel wide vertical white line and a 1px diagonal line.
2.	Before we perform image manipulations, we duplicate the original image for convenience (`Image>Duplicate` or `Ctrl+Shift+D`).
3.	Go to `Image>Adjust>Size`. Perform a resize to 30 x 30 pixels (150% size), with no interpolation, and compare the result with the original figure. Use the Line-Tool to measure the width of both vertical lines. You should observe that one line was not scaled while the other was scaled to 150%.

## Creating a figure [5]
1.	Return to the OMERO.web client. Find the image *sted-confocal.lif [Fab Antikoerper]* in the Projects tab of Omero.web and `right-click` on the file name in the list of the Project tab.
2.	In the context menu, select `Open with>Omero.figure`. A new figure window with the selected image opens up. First of all, press the `Save` button.
3.	To make sure our image is the active element in the figure, click on the image. Go to the Info tab, click on the `chain icon` to lock the aspect ratio of the image, then change the width to 150. Click the `Set dpi` button and enter a value of 600 dpi. (So OMERO will take care of the resampling of your image, if required)
4.	Switch to the Preview tab. Change LUT of the second channel to red and adjust the brightness of the individual channels.
5.	Switch to the Labels tab. Press the `Edit` button. Draw a small square shaped ROI (press shift while drawing) in an interesting region of the image. Set the line thickness to 10, choose a color.
6.	Press the `Show` button in the Scalebar section of the Labels tab. Adjust size and color switch on the label.
7.	Write ’Merged’ in the textbox in the Add Labels section. Change the font size to 18 and make sure position is set to Top. Click `Add`. Now replace ’Merged’ in the textbox by ’Overview’, switch Position to Left Vertical and click `Add` again.
8.	Copy and paste the image five times. Arrange them into two row of three images. After roughly moving the images in place, select them all and use the `Align to Grid` button in the menu bar for quick alignment.
9.	Select the second image in the first row. Switch to the Preview tab and switch off the second channel. Now switch to the Labels tab. Delete the Overview label. Change the ’Merged’ label to ’Confocal’.
10.	Select the third image in the first row. Switch to the Preview tab and switch off the first channel. Now switch to the Labels tab. Delete the Overview label. Change the ’Merged’ label to ’STED’.
11.	Select the first image in the second row. In the Labels tab delete the Merged label and change the ’Overview’ label to ’Magnified ROI’.
12.	Switch to the Preview tab. Press the `Crop` button. Select the ROI from figure and click `OK`. Confirm the deletion of the ROI in the cropped image. In the Labels tab adjust the scalebar size if necessary.
13.	In the further images switch off one channel as in the first row, delete all labels, crop and adjust scalebars in the same way.
14.	`Save` the figure and play with the export function.
