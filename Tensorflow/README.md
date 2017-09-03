## How to restore a model by filename in Tensorflow r12?

### comment

You can restore the model like this:

```python
saver = tf.train.import_meta_graph('./src/models/20170512-110547/model-20170512-110547.meta')
            saver.restore(sess,'./src/models/20170512-110547/model-20170512-110547.ckpt-250000'))
```

Where the path '/src/models/20170512-110547/' contains three files:

```python
model-20170512-110547.meta
model-20170512-110547.ckpt-250000.index
model-20170512-110547.ckpt-250000.data-00000-of-00001
```
And if in one directory there are more than one checkpoints,eg: there are checkpoint files in the path ./20170807-231648/:

```python
checkpoint     
model-20170807-231648-0.data-00000-of-00001   
model-20170807-231648-0.index    
model-20170807-231648-0.meta   
model-20170807-231648-100000.data-00000-of-00001   
model-20170807-231648-100000.index   
model-20170807-231648-100000.meta
```

you can see that there are two checkpoints, so you can use this:

```python
saver =    tf.train.import_meta_graph('/home/tools/Tools/raoqiang/facenet/models/facenet/20170807-231648/model-20170807-231648-0.meta')

saver.restore(sess,tf.train.latest_checkpoint('/home/tools/Tools/raoqiang/facenet/models/facenet/20170807-231648/'))
```

### comment

I also used Tensorlfow r0.12 and I didn't think there is any issue for saving and restoring model. The following is a simple code that you can have a try:
```python
import tensorflow as tf

# Create some variables.
v1 = tf.Variable(tf.random_normal([784, 200], stddev=0.35), name="v1")
v2 = tf.Variable(tf.random_normal([784, 200], stddev=0.35), name="v2")

# Add an op to initialize the variables.
init_op = tf.global_variables_initializer()

# Add ops to save and restore all the variables.
saver = tf.train.Saver()

# Later, launch the model, initialize the variables, do some work, save the
# variables to disk.
with tf.Session() as sess:
  sess.run(init_op)
  # Do some work with the model.

  # Save the variables to disk.
  save_path = saver.save(sess, "/tmp/model.ckpt")
  print("Model saved in file: %s" % save_path)

# Later, launch the model, use the saver to restore variables from disk, and
# do some work with the model.
with tf.Session() as sess:
  # Restore variables from disk.
  saver.restore(sess, "/tmp/model.ckpt")
  print("Model restored.")
  # Do some work with the model
```

although in r0.12, the checkpoint is stored in multiple files, you can restore it by using the common prefix, which is 'model.ckpt' in your case.

### added comment
I'm new to TF and met the same issue. After reading Yuan Ma's comments, I copied the '.index' to the same 'train\ckpt' folder together with '.data-00000-of-00001' file. Then it worked! So, the .index file is sufficient when restoring the models. I used TF on Win7, r12.
