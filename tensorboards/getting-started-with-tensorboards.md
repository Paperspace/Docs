# TensorBoards via TensorFlow Scripting

Taking advantage of TensorBoards from within a TensorFlow script requires just a few lines of code.

To create a TensorBoard, you need to output your TensorFlow operations into a file, called an event file \(or event log file\).

## First steps with TensorBoards

All you need to do to add a scalar to a TensorBoard is as follows:

```text
# Save accuracy scalar to Tensorboard output.
tf.summary.scalar('train_accuracy', accuracy[1])
tf.summary.scalar('loss', loss)
```

That's it!

### Writing Summaries to Visualize Learning <a id="2.-Writing-Summaries-to-Visualize-Learning"></a>

**Summary** is a special TensorBoard operation that takes in a regular tensor and outputs the summarized data to disk \(i.e. to the event file\). Basically, there are three main types of summaries:

**1. tf.summary.scalar:** used to write a single scalar-valued tensor \(like classification loss or accuracy value\)

**2. tf.summary.histogram:** used to plot a histogram of all the values of a non-scalar tensor \(like weight or bias matrices of a neural network\)

**3. tf.summary.image:** used to plot images \(like input images of a network, or generated output images of an autoencoder or a GAN\)

## tf.summary.scalar

This method writes the values of a scalar tensor that changes over time or iterations. In the case of neural networks \(such as a simple network for a classification task\), it's usually used to monitor changes in the loss function or classification accuracy.

Let's run a simple example to see how it works.

#### Example 1: <a id="Example-2:"></a>

Randomly pick 100 values from a standard Normal distribution, _N\(0, 1\)_, and plot them one after the other.

One way to do so is to simply create a variable and initialize it from a normal distribution \(with mean=0 and std=1\), then run a for loop in the session and initialize it 100 times. The code will be as follows, and the steps required to write the summary is also explained in the code as follows:

```text
import tensorflow as tf
tf.reset_default_graph()   # To clear the defined variables and operations of the previous cell

# create the scalar variable
x_scalar = tf.get_variable('x_scalar', shape=[], initializer=tf.truncated_normal_initializer(mean=0, stddev=1))

# ____step 1:____ create the scalar summary
first_summary = tf.summary.scalar(name='My_first_scalar_summary', tensor=x_scalar)

init = tf.global_variables_initializer()

# launch the graph in a session
with tf.Session() as sess:
    # ____step 2:____ creating the writer inside the session
    writer = tf.summary.FileWriter('./graphs', sess.graph)
    for step in range(100):
        # loop over several initializations of the variable
        sess.run(init)
        # ____step 3:____ evaluate the scalar summary
        summary = sess.run(first_summary)
        # ____step 4:____ add the summary to the writer (i.e. to the event file)
        writer.add_summary(summary, step)
    print('Done with writing the scalar summary')
```

Let's pull up our TensorBoard and check out the result. 

![Fig. 6. TensorBoard page visualizing the written scalar summary](https://www.easy-tensorflow.com/files/3_6.png)

As you see in the figure, the plot panel is shown with the name "My\_first\_scalar\_summary", which we determined in our code. The x-axis and y-axis show the 100 steps and corresponding values \(random values from a standard normal distribution\) of the variable respectively.

#### 2.2. tf.summary.histogram: <a id="2.2.-tf.summary.histogram:"></a>

This method plots the histogram of the values of a non-scalar tensor. This gives us a view of how does the histogram \(and the distribution\) of the tensor values change over time or iterations. In the case of neural networks, it's commonly used to monitor the changes of weights and biases distributions. It's very useful in detecting irregular behavior of the network parameters, such as when many of the weights shrink down or grow large.

Now let's go back to our previous example and add a histogram summary to it.

#### Example 2: <a id="Example-3:"></a>

Continue the previous example by adding a matrix of size 30x40, whose entries come from a standard normal distribution. Initialize this matrix 100 times and plot the distribution of its entries over time, as follows:

```text
import tensorflow as tf
tf.reset_default_graph()   # To clear the defined variables and operations of the previous cell

# create the variables
x_scalar = tf.get_variable('x_scalar', shape=[], initializer=tf.truncated_normal_initializer(mean=0, stddev=1))
x_matrix = tf.get_variable('x_matrix', shape=[30, 40], initializer=tf.truncated_normal_initializer(mean=0, stddev=1))

# ____step 1:____ create the summaries
# A scalar summary for the scalar tensor
scalar_summary = tf.summary.scalar('My_scalar_summary', x_scalar)
# A histogram summary for the non-scalar (i.e. 2D or matrix) tensor
histogram_summary = tf.summary.histogram('My_histogram_summary', x_matrix)

init = tf.global_variables_initializer()

# launch the graph in a session
with tf.Session() as sess:
    # ____step 2:____ creating the writer inside the session
    writer = tf.summary.FileWriter('./graphs', sess.graph)
    for step in range(100):
        # loop over several initializations of the variable
        sess.run(init)
        # ____step 3:____ evaluate the merged summaries
        summary1, summary2 = sess.run([scalar_summary, histogram_summary])
        # s____step 4:____ add the summary to the writer (i.e. to the event file) to write on the disc
        writer.add_summary(summary1, step)
        # repeat steps 4 for the histogram summary
        writer.add_summary(summary2, step)
    print('Done writing the summaries')
```

If you open the TensorBoard in your browser, you'll find two new tabs added to the top menu: "Distributions" and "Histograms". The results will be as follows:

![a\) scalar summary, b\) distribution, &amp; c\) histogram of 2d-tensor values over 100 steps](https://www.easy-tensorflow.com/files/3_7.png)

As you see in the figure, the "Distributions" tab contains a plot that shows the distribution of the values of the tensor \(y-axis\) through steps \(x-axis\). You might ask, what are the light and dark colors?

The answer is that each line on the chart represents a percentile in the distribution over the data. For example, the bottom line \(the very light one\) shows how the minimum value has changed over time, and the line in the middle shows how the median has changed. Reading from top to bottom, the lines have the following meaning: \[maximum, 93%, 84%, 69%, 50%, 31%, 16%, 7%, minimum\]

These percentiles can also be viewed as standard deviation boundaries on a normal distribution: \[maximum, μ+1.5σ, μ+σ, μ+0.5σ, μ, μ-0.5σ, μ-σ, μ-1.5σ, minimum\] so that the colored regions, read from inside to outside, have widths \[σ, 2σ, 3σ\] respectively.

Similarly, in the histogram panel, each chart shows temporal "slices" of data, where each slice is a histogram of the tensor at a given step. It's organized with the oldest timestep in the back, and the most recent timestep in front.

You can easily see the values on the histograms at any step. Just move your cursor on the plot and see the x-y values on the histograms \(Fig. 8 \(a\)\). You can also change the Histogram Mode from "offset" to "overlay" \(see Fig. 8 \(b\)\) to see the histograms overlaid with one another.

![Fig. 8. \(a\) monitor values on the histograms, \(b\) overlayed histograms](https://www.easy-tensorflow.com/files/3_8.png)

As shown in the code, you need to run each summary \(e.g. **sess.run\(\[scalar\_summary, histogram\_summary\]\)**\) and then use your writer to write each of them to disk. In practice, you might use dozens or hundreds of such summaries to track different parameters in your model. This makes running and writing the summaries extremely inefficient. The way around it is to merge all summaries in your graph and run them at once inside your session. This can be done using the **tf.summary.merge\_all\(\)** method. If we use it for Example 3, the code changes as follows:

```text
import tensorflow as tf
tf.reset_default_graph()   # To clear the defined variables and operations of the previous cell

# create the variables
x_scalar = tf.get_variable('x_scalar', shape=[], initializer=tf.truncated_normal_initializer(mean=0, stddev=1))
x_matrix = tf.get_variable('x_matrix', shape=[30, 40], initializer=tf.truncated_normal_initializer(mean=0, stddev=1))

# ____step 1:____ create the summaries
# A scalar summary for the scalar tensor
scalar_summary = tf.summary.scalar('My_scalar_summary', x_scalar)
# A histogram summary for the non-scalar (i.e. 2D or matrix) tensor
histogram_summary = tf.summary.histogram('My_histogram_summary', x_matrix)

# ____step 2:____ merge all summaries
merged = tf.summary.merge_all()

init = tf.global_variables_initializer()

# launch the graph in a session
with tf.Session() as sess:
    # ____step 3:____ creating the writer inside the session
    writer = tf.summary.FileWriter('./graphs', sess.graph)
    for step in range(100):
        # loop over several initializations of the variable
        sess.run(init)
        # ____step 4:____ evaluate the merged summaries
        summary = sess.run(merged)
        # ____step 5:____ add summary to the writer (i.e. to the event file) to write on the disc
        writer.add_summary(summary, step)
    print('Done writing the summaries')
```

```text
Done writing the summaries
```

#### 2.2. tf.summary.image: <a id="2.2.-tf.summary.image:"></a>

As the name says, this type of summary method writes and visualizes tensors as images. In the case of neural networks, this is usually used for tracking the images that are either fed to the network \(say in each batch\) or the images generated in the output \(such as the reconstructed images in an autoencoder; or the fake images made by the generator model of a Generative Adversarial Network\). However, in general, this can be used for plotting any tensor. For example, you can visualize a weight matrix of size 30x40 as an image of 30x40 pixels.

An image summary can be created like so:

```text
tf.summary.image(name, tensor, max_outputs=3)
```

where **name** is the name for the generated node \(i.e. operation\), **tensor** is the desired tensor to be written as an image summary \(we will talk about its shape shortly\), and **max\_outputs** is the maximum number of elements from **tensor** to generate images for. But... what does it mean?! The answers likes in the shape of the **tensor**.

The **tensor** that you feed to **tf.summary.image** must be a 4-D tensor of shape **\[batch\_size, height, width, channels\]** where **batch\_size** is the number of images in the batch, **height** and **width** determine the size of the image and channel is: **1**: for Grayscale images. **3**: for RGB \(i.e. color\) images. **4**: for RGBA images \(where A stands for alpha; see [RGBA](https://en.wikipedia.org/wiki/RGBA_color_space)\).

Let's look at a very simple example to get the idea.

#### Example 3: <a id="Example-4:"></a>

Let's define two variables:

1. Of size 30x10 as 3 **grayscale** images of size 10x10
2. Of size 50x30 as 5 **color** images of size 10x10

and plot them as images in your TensorBoard, as follows:

```text
import tensorflow as tf
tf.reset_default_graph()   # To clear the defined variables and operations of the previous cell

# create the variables
w_gs = tf.get_variable('W_Grayscale', shape=[30, 10], initializer=tf.truncated_normal_initializer(mean=0, stddev=1))
w_c = tf.get_variable('W_Color', shape=[50, 30], initializer=tf.truncated_normal_initializer(mean=0, stddev=1))

# ___step 0:___ reshape it to 4D-tensors
w_gs_reshaped = tf.reshape(w_gs, (3, 10, 10, 1))
w_c_reshaped = tf.reshape(w_c, (5, 10, 10, 3))

# ____step 1:____ create the summaries
gs_summary = tf.summary.image('Grayscale', w_gs_reshaped)
c_summary = tf.summary.image('Color', w_c_reshaped, max_outputs=5)

# ____step 2:____ merge all summaries
merged = tf.summary.merge_all()

# create the op for initializing all variables
init = tf.global_variables_initializer()

# launch the graph in a session
with tf.Session() as sess:
    # ____step 3:____ creating the writer inside the session
    writer = tf.summary.FileWriter('./graphs', sess.graph)
    # initialize all variables
    sess.run(init)
    # ____step 4:____ evaluate the merged op to get the summaries
    summary = sess.run(merged)
    # ____step 5:____ add summary to the writer (i.e. to the event file) to write on the disc
    writer.add_summary(summary)
    print('Done writing the summaries')
```

```text
Done writing the summaries
```

Now, if you open your TensorBoard like before and switch to the **IMAGES** tab, you'll see images that have been output, like these:

![Fig. 9. generated images in TensorBoard](../.gitbook/assets/3_9.png)

_\*\*\*\*_

