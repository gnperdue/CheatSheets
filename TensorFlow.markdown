
## General notes

* img tensor shapes should be : `N x H x W x NChannels`

## Standard flow

    # usually have something like
    X = tf.placeholder(tf.float32, shape=(None, n_features), name='X')

    # usually build network in `with tf.variable_scope`
    # set up variables with `tf.get_variable`

    # establish the session and initialize variables
    sess = tf.Session()
    init = tf.global_variables_initializer()
    # can also do a subset, e.g.
    # init_ab = tf.variables_initializer([a, b], name='init_subset')
    sess.run(init)
    # can also run solo vars, e.g. `sess.run(W.initializer)`

    # set up an optimizer (need a cost function)
    train_op = tf.train.GradientDescentOptimizer(learning_rate).minimize(cost)
    loss = ... some function

    # run the training
    for epoch in range(training_epochs):
        _, l = sess.run([train_op, loss] feed_dict={X: xs, Y: labels})
        # can get cost in a separate call instead
        # l = sess.run(loss, feed_dict={X: xs, Y: labels})
        if epoch % epoch_print_frequency == 0:
            print(epoch, l)

    # examine learned model params
    w_val = sess.run(w)
    print('learned parameters', w_val)

    sess.close()

## Saving and loading models - checkpoints

* Restore:

        # sess = tf.Session() ...
        saver = tf.train.Saver()
        if os.path.exists('./my_model.ckpt'):
            saver.restore(sess, './my_model.ckpt')
            print('model restored')

* Save (every so often during training):

        # sess = tf.Session() ...
        saver = tf.train.Saver()
        save_path = saver.save(sess, './my_model.ckpt')
        print('model saved in file: %s' % save_path)

## Saving and loading models - protobufs

* Save:

        # saver = tf.train.Saver() ...
        path='./'
        ckpt_name = path + 'model.ckpt'
        fname = path + 'model.tfmodel'
        dst_nodes = ['Y']   # destination nodes
        g_1 = tf.Graph()
        with tf.Sesssion(graph=g_1) as sess:
            x = tf.placeholder(tf.float32, shape=(1, 224, 224, 3))
            net = create_network()
            sess.run(tf.initialize_all_variables())
            saver.restore(sess, ckpt_name)
            graph_def = tf.python.graph_util.convert_variables_to_constants(
                sess, sess.graph_def, dst_nodes
            )
        
        g_2 = tf.Graph()
        with tf.Session(graph=g_2) as sess:
            tf.train.write_graph(
                tf.python.graph_util.extract_sub_graph(graph_def, dst_nodes),
                path, fname, as_text=False
            )

* Import:

        with open('model.tfmodel', mode='rb') as f:
            graph_def = tf.GraphDef()
            graph_def.ParseFromString(f.read())
        
        tf.import_graph_def(net['graph_def'], name='model')

## Graph manipulation

* Reset the operations in a graph:

        from tensorflow.python.framework import ops
        ops.reset_default_graph()

* List the operations in a graph:

        [op.name for op in tf.get_default_graph().get_operations()]

* Look at the graph definiton:

        print sess.graph.as_graph_def()

**Note:** constants are stored in the graph definition. This makes loading
graphs expensive if constants are big. Therefore, only use constants for
primitive types and use variables or readers for data that requires more
memory.

**Note:** don't defer creating/initializing objects until needed in graph
definiion. This can cause us to actually create an object more times than
is needed (e.g., if done in a loop, the operation is created N times!).
Always separate fully the definition of ops from their computation.

## Creating variables

* We generally want to work within a scope:

        def create_layer(X, n_inp, n_out, act=None, scope=None):
            with tf.variable_scope(scope or 'layer'):
                W = tf.get_variable(name='W',
                                    shape=[n_inp, n_out],
                                    initializer=tf.random_normal_initializer(
                                        mean=0.0, stddev=0.1
                                    )
                h = tf.matmul(X, W)
                if activation is not None:
                    h = activation(h)
                return h

Note that we also used a TF initializer here - this will create new random
values every time we call `sess.run(initialize_all_variables())`.

## Reshaping tricks

* We need images to have shape `Batch x H x W x N-Channels` for convolution.
To go from `[None, n_features]` (where `None` is letting us have an arbitrary
batch size) we use `-1` in the `reshape()`:

        X = tf.placeholder(tf.float32, [None, n_features])
        X_tensor = tf.reshape(X, [-1, H, W, NChan])

## Shape

    tensor.shape
    tensor.shape.as_list()
    tensor.get_shale().as_list()

## Evaluating tensors

    print sess.run(W)
    print W.eval()

## TensorBoard

    with tf.Session() as sess:
        writer = tf.summary.FileWriter('./graphs', sess.graph)
        ...   # computations
    
    writer.close()

Then, externally:

    $ python prog.py
    $ tensorboard --logdir="./graphs" --port 6006

Then, go to http://localhost:6006

## InteractiveSession

`InteractiveSession` makes itself the default:

    sess = tf.InteractiveSession()
    ...
    expr.eval()  # no need to specify `sess`
    sess.close()

## Feeding

* `placeholder` must be fed.
* Check others with `tf.Graph.is_feedable(tensor)`

Feeding values is useful for testing, etc.

    a = tf.add(2, 5)
    b = tf.multiply(a, 3)
    with tf.Session() as sess:
        replace_dict = {a: 15}
        sess.run(b, feed_dict=replace_dict)  # returns 45

