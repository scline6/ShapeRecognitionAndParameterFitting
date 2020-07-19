# ShapeRecognitionAndParameterFitting
This Tensorflow notebook classifies images as rectangle or ellipse, and fits center, theta &amp; major/minor diameter.



OVERVIEW

    I took on the challenge of self-studying deep learning, and this is my first experience. 
    Tensorflow on Colab has been smooth as can be, so that was a pleasant surprise!

    After starting out with the MNIST hand-written digits classification tutorial, I had an idea. 
    What if you could convert 2D or 3D geometric models in triangle mesh, image, or volumetric 
    format into Constructive Solid Geometry (CSG)? Typical CSG models are made from polygons, 
    ellipses, extrusions, polyhedra, cylinders, ellipsoids, boolean operations, hulls, and 
    Minkowski sums. If you generated a training dataset consisting of CSG models with their 
    correct labels (per point or pixel for segmentation), maybe you could train a deep learning 
    model to recognize the constituents of the CSG model. Then you might be able to send in 
    models that were not originally CSG-generated and the deep learning model would reconstruct 
    them as CSG. It is also possible that the nested structure of boolean operations and hulls 
    could prevent feedforward nets from being able to reverse engineer CSG models. Recurrent 
    nets might be required.  All a learning experience - maybe one day I will find out!

    To limit the scope to a reasonable start, I wanted to see if deep learning can classify 2D 
    images that each contains a single shape, either a rectangle and ellipse and estimate the 
    original parameters that were used to generate the rectangles and ellipses. Later, I would 
    like to move on to multiple shapes per image and image segmentation.

    I wrote a simple C++/Qt program that generates rectangles (SHAPE=0) and ellipses (SHAPE=1). 
    The training set has 50000 images, the test set has 15000 images and the validation set has 
    5000 images. The images are 50x50 pixels. When scaled to the 0-1 range, each pixel has width 
    of 0.02.

    Classification went well with over 99.9% accuracy.  The only issues were very small 
    rectangles with pixelated corners that are hard even for a human to distinguish from an 
    ellipse.

    The continuous parameters are CENTER_X, CENTER_Y, THETA, MAJOR_DIAM, MINOR_DIAM. Currently, 
    CENTER_X and CENTER_Y fit very closely to the test data. MAJOR_DIAM and MINOR_DIAM have a 
    decent fit, but could probably be improved. The THETA parameter did not fit well because it 
    belongs to the circular group where 0 degrees is the same as 360 degrees. Replacing THETA 
    with cos(THETA) and sin(THETA) should work better, but I will leave that as a future exercise.



STEPS

    Please open up the ShapeRecognitionAndParameterFitting notebook and follow the steps.  It will 
    walk you through loading image data and labels, defining the deep learning model, training the 
    model, performing inference on test data, and examining the results.
