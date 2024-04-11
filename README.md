# TWS3Dmito
# Machine learning-based 3D segmentation of mitochondria in polarized epithelial cells
**Nan W Hultgren, Tianli Zhou, David S Williams**

Department of Ophthalmology and Stein Eye Institute, University of California, Los Angeles, CA 90095, USA; Department of Neurobiology, David Geffen School of Medicine at UCLA, University of California, Los Angeles, CA 90095, USA; Molecular Biology Institute, University of California, Los Angeles, CA 90095, USA; Brain Research Institute, University of California, Los Angeles, CA 90095, USA. Electronic address: dswilliams@ucla.edu.

Mitochondrion. 2024 Apr 8:101882. doi: [10.1016/j.mito.2024.101882](10.1016/j.mito.2024.101882)

Classifier 10_1 Segmentation Protocol
Updated 4/09/24, NH

Pre-Segmentation Clean-up Using Imaris (Optional)
1.	Generate a surface of mitochondrion channel (check “Smooth” option; “Surface detail” = 0.100 µm; check “Background Subtraction” option, “Diameter of large sphere which fits into the object” = 0.300 µm); 
2.	Select and delete noise and mitochondria of adjacent cells (have only mitochondria in cell of interest remaining in the surface);
3.	Create a mask using the remained surface (check “Constant inside/outside”, “Set voxel intensity outside” = 0);
4.	Save mask as a tiff image (select “Open Microscopy Environment: TIFF” instead of “TIFF”; “TIFF” option will save each Z-slice as individual image).

**Segmentation Using TWS 3D Classifier 10_1**
1.	Download classifier_10_1.model and data_10_1.arff files and save in desired folder on your computer.
2.	Open one image in TWS 3D GUI;
3.	Load “classifier 10_1” and “data 10_1”;
4.	Click “Get probability” (nod “Get result”);
5.	Save probability map.

Optimize Classifier (Optional)
If Classifier 10_1 yields unsatisfactory result due to evident deviation of image quality from training set (noise level, acquisition methods etc.):
1.	Select a couple representative images from dataset;
2.	Open one image in TWS 3D GUI;
3.	Load “classifier 10_1” and “data 10_1”;
4.	Mark mitochondria and background regions (left click and drag cursor across the region) across z-sections and add them to corresponding “classes” (click “Add to Mitochondria” or “Add to Background”);
5.	Click “Train classifier”;
6.	Inspect result: mitochondria marked in red and background marked in green;
7.	Correct obvious mistakes by repeating step 4-6 until satisfactory;
8.	Save classifier and data;
9.	Repeat process on other images.

Thresholding
1.	Open probability map in ImageJ;
2.	Separate channels and close the background channel (green background with black mitochondria), leaving the mitochondria channel open (black background with red mitochondria)
3.	At this point, image may look badly segmented. Do not be alarmed yet, could be due to a bug in how ImageJ displays the image. Auto adjust brightness and contrast to make sure. 
4.	“Adjust Threshold” (select method “Default” and “Over/Under”, check “Dark Background”, input 0.8 as the lower limit for thresholding, leave upper limit at maximum); This number can be changed to best fit user preference but should be consistent across all analysis in one data set.
5.	Click “Apply” and check “Dark Background (of binary masks)” to confirm;
6.	Save thresholded image.

The thresholded binary images can now be used for qualitative evaluation or quantitative analysis.

Examples of Post-segmentation Quantitative Analysis
Analysis Option 1: 3D Object Counter
1.	Open thresholded image and the 3D OC window;
2.	Configure 3D OC (in “3D OC Options” under “Analyze” menu”);
3.	Check “Volume” and click “OK” to generate a result window and save the generated list to a .csv file (only consider mitochondrion with volume between 0.1 µm3 and 15 µm3 for further analysis).

Analysis Option 2: MitoLoc
1.	Open thresholded image and MitoLoc window;
2.	Outline the cell of interest and add to ROI manager (when window opened, polygon selection tool is automatically picked for outlining; if already cleaned-up with Imaris, then the whole image can be circled out); 
3.	Start MitoLoc and save the generated list to a .csv file (only consider mitochondrion with volume between 0.1 µm3 and 15 µm3 for further analysis).
