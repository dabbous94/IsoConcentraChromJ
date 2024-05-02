# IsoConcentraChromJ - Nuclear Chromatin Distribution Explorer
Chromatin exhibits non-random distribution within the nucleus being arranged into discrete domains that are spatially organized throughout the nuclear space. Both the spatial distribution and structural rearrangement of chromatin domains in the nucleus depend on epigenetic modifications of DNA and/or histones. IsoConcentraChromJ is an automated, user-friendly, ImageJ plugin aimed quantitatively delineating the spatial distribution of chromatin regions in concentric patterns.
The IsoConcentraChromJ can be applied to quantitative chromatin analysis in both two- and three-dimensional spaces, presented in two files 2d IsoConcentraChromJ.ijm and 3d IsoConcentraChromJ.ijm, respectively.

**2d IsoConcentraChromJ**: The ImageJ plugin follows a structured workflow consisting of four key mechanisms, each applied sequentially for user convenience by one click. 

  1. **Clear Outside and Image Plitting**
     * Clears Outside the nuclear selected by the user
     * Splits the entire image into channels
       
  3. **Nucleus Filtering**
     *Identifies the nuclei of interest within the image, by allowing sequential procedure within a series of steps, including thresholding and masking.
       * Implements thresholding dialog for the user to select the suitable threshold method for his research.
       * Converts the thresholded image into a binary image.
       * Select the boundary edges around the masked image to identify the full nuclei area.
     
  5. **Nucleus Splitting**
       * Performs a partition of the nucleus into multiple distinct regions based on biological characteristics
       * Detects the centroid of the full nuclei
       * Quantifies the edge coordinates of the full nuclei
       * Calculates the coordinates of the intermediate region using the equation below
         
              x_new=(X_Full- X_centroid_Full )*(Shrink_Factor  +X_centroid_Full  )
              y_new=(Y_Full- Y_centroid_Full )*(Shrink_Factor  +Y_centroid_Full  )

          * Shrink_Factor: the splitting percentage that can be adjusted by the user. for the intermediate region is 66.66%
      * Calculates the coordinates for the center region
          *  Shrink_Factor: 33.33 %
      * Save the new regions' ROIs into the ROI manager
        
  7. **Statistical analysis**
       * The user must draw a Region of Interest (ROI) that serves as the background subtraction area within the two previously mentioned channels
       * Calculates the Normalization Factor using the following equation
         
             NF_DNA=(total_MID_DNA)⁄nSlices*voxel_Depth                          	
             NF_Acetylated=(total_MID_Acetylated)⁄nSlices*voxel_Depth
           *   The two parameters NF_DNA and NF_Acetylated  represent the normalization factors for the single channels (DNA and Acetylation). These factors allow to standardize the data across different regions of interest, and their calculation uses the Mean Integrated Density (MID) of the background subtraction area  MID.  
       * Normalize the total IntDen for each area using the following equation:
    
              Normalized_(Intensity_area )=IntDen_area-( NF*area)             
       * Computes the integrated density for each of the specified areas and subsequently determines the concentric ratios.
       * Calculated ten ratios, denoted as A/B, A1/B, A1/A, A2/B, A2/A, A3/B, A3/A, B1/B, B2/B, and B3/B.
    
 **3d IsoConcentraChromJ**: Similar to the 2d plugin but works for the 3D images by adding the z_stack to all equations and methodology described before.

 **Imaging Data**: 10 2D and 3D images used in our analysis are all presented in the folders 2D and 3D.
