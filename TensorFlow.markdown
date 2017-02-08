
## General notes

* img tensor shapes should be : `N x H x W x NChannels`

## Standard flow

    # usually have something like
    X = tf.placeholder(tf.float32, shape=(None, n_features), name='X')

    # usually build network in `with tf.variable_scope`
    # set up variables with `tf.get_variable`

    # establish the session and initialize variables
    sess = tf.Session()
    init = tf.initialize_all_variables()
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

