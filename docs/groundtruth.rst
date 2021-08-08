Data Preparation
================

Concepts
--------

Rotobot Butler allows us to train from a number of images which 
have a matching image which informs what will be isolated as a 
video layer when the neural network is trained.

We call the image that labels which pixels belong to the mask a label.

The label images make up the ground truth.

Labels
------

So if we are to make video layers of images with people in them.

We labels the pixels that are people with the colour white and label
the background pixels with the colour black

The labels are in a separate image file on disk, which will line up when overlayed with the original image

The closer the match is to the edge of the item the better the model can connect the ground truth to the pattern in the original image.

This label colour by default is white (255,255,255) but you can choose any colour.

This seperates the "person" class from the "background" class.


File Organisation
-----------------


The easiest way to do this is to make two folders: ::

  images
  labels

Within the images folder we can have three images: ::

   - images /
       image.00001.jpg
       image.00002.jpg
       ...
       ...
       image.00997.jpg
       image.01773.jpg
    - labels /
       image.00001.png
       image.00002.png
       ...
       ...
       image.00997.png
       image.01773.png


Data Patterns
-------------

You need to ensure the following patterns:

    - All images are 0 - 255 ( 8 bit per pixel) sRGB colour JPEG or PNG files
    - All images are the same between the label and the image
    - There are many images at least 40 images
    - Each pair of images must be the same size, but different pairs may be different sizes
    - Each of the labels must use the same colour to indicate the label
    - the background colour must be (0,0,0) black
    - All of the pixels in a category must be labelled, ie. not some of hats ALL of the hats

Data Concepts
-------------

Machine leaning is a big field but the dot points below will help you out


    - You can choose anything as a class for a video layer: dog, cat, tree, car train, shirt
    - If you want the trained model to work on all people, you need more than one person as a subject
    - The more examples of a subject you have, the more general your model will be.
    - If you only show it a red shirt and blue pants, it might only recognise people in those clothes
    - When you train on a small dataset, this is called a specific model and may be over fitted to that data.
