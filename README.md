# Overview of results so far
## Basics and local stuff
built TF from source for 2x speed increase on local machine

## modifying `adaptive-style-transfer`
added functionality for reencoding with the following features:
* `--reencodes n` reencodes the data n times
* `--reencode_steps n` save every n-th step of the reencoding process
* `--embeddings` save the embeddings as numpy binary file for every n-th step specified in `--reencode_steps`
* `--log` log interesting variables for reencoding such as the norm of the feature vector as well as the distance between consecutive feature vectors and mainly log the feature vectors themselves for visualization in TensorBoard which allows for PCA and t-SNE

## visualizing results
the results have been visualized using the following methods:
* for few test images scikit-learn and matplotlib give nice 2D images that indicate that embeddings are rather drifting apart:
> TODO: insert pictures for ~10 sample images with ~100 reencodings
![image](images/3030.jpg "Logo Title Text 1")
* for more advanced plots (3D) and easy analysis of scalar values TensorBoard offers nice visualization at the cost of at times very high latency and long loading times for projecting embeddings
> TODO: insert images and maybe videos of TB for many images with many reencodings with color coding images the belong togehter
> TODO: scalar values that show the distance in feature space between consecutive images for the same data set
* for validation purposes use UMAP (TODO:link). This requires again use of a different visualization tool. In this case `bokeh` (TODO:link) was used, which itself uses `vis.js` for plotting 3D graphs
> TODO: UMAP images for same data as before

## Conclusion
Contrary to previous expectations the process of reencoding image data does not tend to converge. Interestingsly after only ~20 (maybe a bit more) reencodings it is almost impossible to infer the original image or the next 20 reencoding steps.
Looking at the scalar data and the plots it even looks like the embeddings diverge to a certain degree although the reencodings of different original images look similar to the human eye.
Even for low resolution pictures (30x30 px) neither the image data nor the embeddings converge. Looking at the t-SNE plot the data looks like a raveled ball of wool.
> TODO: insert video of wool ball
<video controls="controls">
  <source type="video/mp4" src="woolball.mov">
  <p>Your browser does not support the video element.</p>
</video>

## Possible ideas for what still can be done
* parallelize the process of inference

    This is not really practical, as the increase in speed would be lower compared to starting multiple processes on different GPUs for different images.

    Maybe this is applicable to training instead of inference?

* log the discriminators certainty of each reencoding!!!!!

    Still a good idea to certain degree, might show strengths/weaknesses of network.

* replace transformer block with i.e. flower vs. plane discriminator and then see if flowers/planes are better stylized

    This should be talked about in advance, how much benefit this might give. The main problem is the very long training time for the original model (300,000 iterations per style).


