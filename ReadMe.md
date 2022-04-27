# Subsea imaging in fishing and shipping

In this task I created 3 notebooks. One about fish classification, fish segmentation and one about marine fouling.

Link to the datasets and trained models:
* https://drive.google.com/drive/folders/1RKkmM1h0tRuDznmGwJA2kU1_1orjn5pT?usp=sharing

Links that helped me:
* https://walkwithfastai.com/Segmentation
* https://towardsdatascience.com/image-segmentation-with-fastai-9f8883cc5b53
* https://github.com/fastai/fastbook

## Marine fouling

When I first this project I had the dataset in a folder in my google drive. Either use this method or zip like in thw two others.

This is from one of the mini-project I did. In this notebook I first mounted my google drive to retrieve the dataset. After that I used ImageDataLoaders.from_folder() to create the dls. After doing some training with Resnet34 I already got a high accuracy at 91% and stop training. In the end of the project I used cofusion_matrix to get an overview over Actual/Predicted.

After that I exported the model and tested it with widgets in the app notebook of the project.

## Fish classification

To run this project you have retrieve classification.zip from example google drive

In this part I wanted to create a fish classifier. With the dataset I had many folders with subfolders like "empty" (no fish) and "valid" (fish), and there ws also a CSV file. 

I first played a bit with the CSV file and got an overview over the attributes on the objects. Before I created a datablock I created the methods get_x() which returned the ID of the object, get_y() which returned the class of the object, and splitter which splitted the dataset in a training and a validation set. At this point I failed my attempt. The main problem was the dataset. What happened was that when I created the model and tried to train it, I got errors about files not existing which did not make sense to me since it did in fact exist in both the CSV file and in the path.

Moving on I abondend the CSV file and used regular expression to filter the categories. The regular expression would filter the numbers at the start and the end which can be seen at the Confusion matrix.

The problem continued in training the model. There was no errors, but after running plot_loss() we can see that it became underfit, which is a model that fails to sufficiently learn the problem and performs poorly on a training dataset and does not perform well on a holdout sample.

Even tho the results were great, this was a failed attempt.

## Fish segmentation

To run this project you have retrieve Segmantation.zip from example google drive

Did not finish it.

In this part I wanted to to segmentation since it is hard to see fish underwater sometimes, so I wanted to use segmentation fix that. At the start I mounted teh google drive to get the dataset, and then created a img_path and labels to filter the images.

To this project I needed to sort out the labels and I needed a text file. To do that I made functional method with regular expression to get an array of both. For the text file I copied the array and pasted it in a notepad. After creating a code I noticed a little error. Even if I copied the list into array(code_list, dtype='<U17') the output did not retrieve the whole name. This may be th reason I did not finish it.

I created a get_msk and FileSplitter. get_msk retrieved the mask and FileSplitter took in the text file and split the items depending on the value of mask.

When creating the Datablock I made the batch size smaller because the original size made to much for the GPU ram. Running the code it worked well and I got good results when I ran dls.show_batch().

It was at the training part I could not continue at. Doing the training I used net.learner. Since the way a CNN works is it breaks down an image into smaller and smaller parts until is has just one thing to predict. A U-Net then takes this and makes it bigger and bigger again and it does this for every stage of the CNN.

After doing that part I tried to find a learning rate, but then I got a bad learning rate. Ignoring this a trying to train with learn.fit_flat_cos() I got a message "Userwarning: Your generator is empty".
At my first attempt I used a different were I actually got a result. However I was not satisified with because I did not like the dataset. Trying this dataset I got great images when using show_batch() that I wanted to do with this dataset. Sadly, I my work stopped at this part.
