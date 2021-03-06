# Post-processing for marker-controlled Watershed segmentation
This accomplishes a very specific task of classifying pixels following a Watershed segmentation. The Watershed segmentation step was tested on ImageJ

For extracting the left atrial myocardial wall, we have tested a Marker-controlled Watershed segmentation [ImageJ](https://imagej.nih.gov/ij/) implementation on CMR images of the left atrium [Varela et al.](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4328285). The Watershed process is run on the [Gradient magnitude](https://en.wikipedia.org/wiki/Image_gradient) of the CMR image. 

However, it requires post-processing for finalising the atrial wall segmentation. The following repository contains two separate tools that accomplish these post-processing tasks. 

## Usage 
The usage for the first tool ```combinmask``` is:
```
combinmask <watershed_mask_img> <outfile> <mask_label_1> <mask_label_2> <output_mask_label>
```
This program outputs a mask image by combining pixels with label1 and label2, ***BUT*** only those label2 pixels that are adjacent to label1

The output from the first tool is used as input to the second tool below; 

The usage for the second tool ```watershed2wall``` is:
```
watershed2wall <input_MRI_img> <mask_from_combinmask> <out_img> <intensity_t1> <intensity_t2> <max_dist>
```
where ```intensity_t1``` and ```intensity_t2``` are intensities (min,max) sampled from atrial wall. ```max_dist``` is the limit on the  distance from atrial chamber that this program should search. 


## Example 

In the example below, the ```combinmask``` combines the Watershed segmentation of LA and wall into a single mask. 

The Watershed segmentation is obtained from the marker-controlled Watershsed implementation in [ImageJ](https://imagej.nih.gov/ij/). The segmentation is run on the gradient-magnitude edge output of the original MRI image of the atrial wall. 

The ```watershed2wall``` tool extracts pixels that are within a distance ```max_dist``` from the mask and within thresholds ```t1``` and ```t2```. 

![alt tag](https://s3.postimg.org/qhe2rr1nn/Capture.png)

## Further reading
[Karim et al. 'Segmentation Challenge on the Quantification of Left Atrial Wall Thickness'](http://www.doc.ic.ac.uk/~rkarim/files/stacom_2016.pdf) and link to [Springer repository](https://link.springer.com/chapter/10.1007%2F978-3-319-52718-5_21)

[Varela, M., Kolbitsch, C., Theron, A., Morgan, R., Henningsson, M., Schaeffter, T., Aslanidi, O.: 3D high-resolution atrial wall thickness maps using black-blood psir. J. Cardiovasc. Magn. Reson. (Suppl.) 17 (2015). Society of Magnetic Resonance Imaging (SCMR)](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4328285/)

## Author 
```
Dr. Rashed Karim 
Department of Biomedical Engineering 
King's College London 
```
