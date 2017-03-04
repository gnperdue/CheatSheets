
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
    sess.run(init)

    # set up an optimizer (need a cost function)
    train_op = tf.train.GradientDescentOptimizer(learning_rate).minimize(cost)

    # run the training
    for epoch in range(training_epochs):
        sess.run(train_op, feed_dict={X: xs, Y: labels})
        current_cost = sess.run(cost, feed_dict={X: xs, Y: labels})
        if epoch % epoch_print_frequency == 0:
            print(epoch, current_cost)

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

