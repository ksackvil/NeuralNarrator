# Flags

Here we'll describe in detail the full set of command line flags available for preprocessing, training, and sampling scripts. Each argument is shown in the following format:

`argument`: (Default) some description

## train.py

`--data_dir`: ('data/tinyshakespeare') Data directory containing input.txt (textfile which we will train our model on).

`--input_encoding`: (None) Character encoding of input.txt, from [here](https://docs.python.org/3/library/codecs.html#standard-encodings).

`--log_dir`: ('logs') Directory containing tensorboard logs.

`--save_dir`: ('save') Directory to store checkpointed models.

`--rnn_size`: (256) The number of hidden units in the RNN. Larger values (256 or 512) are commonly used to learn more powerful models and for bigger datasets, but this will significantly slow down computation.

`--num_layers`: (2) The number of layers present in the RNN.

`--model`: ('lstm') The type of recurrent network to use; either 'lstm' or 'rnn'. 'lstm' is slower but better.

`--batch_size`: (50) Number of sequences to use in a minibatch.

`--seq_length`: (25) Number of timesteps for which the recurrent network is unrolled for backpropagation through time.


`--num_epochs`: (50) How many training epochs to use for optimization. To many epochs can cause overfitting.

`--save_every`: (1000) How often to save intermediate checkpoints. Set to 0 to disable intermediate checkpointing. Note that we always save a checkpoint on the final iteration of training.

`--grad_clip`: (5.0) Maximum value for gradients. Set to 0 to disable gradient clipping.

`--learning_rate`: (0.002) Learning rate for optimization.

`--decay_rate`: (0.97) Decay rate for rmsprop.

`--gpu_mem`: (0.666) % of GPU memory to be allocated to this process.

`--init_from`: (None) To continue training from saved model at this path. Path must contain files saved by previous training process:
    - 'config.pkl'        : configuration;
    - 'words_vocab.pkl'   : vocabulary 
    - 'checkpoint'        : paths to model file(s) (created by tf). Note: this file contains absolute paths, be careful when moving files around;
    - 'model.ckpt-*'      : file(s) with model definition (created by tf)
    
## sample.py

`--save_dir`: ('save') Directory to load stored checkpoint models from.

`-n`: (200) Number of words to sample in characters.

`--prime`: (' ') You can optionally start off the generation process with a string; if this is provided the start text will be processed by the trained network before we start sampling.

`--pick`: (1) Set this to 1 for weighted pick, or 2 for beam search pick.

`--width`: (4) Width of beam search.

`--sample`: (1) Set this to 0 to use max at each timestep, 1 to sample at each timestep, 2 to sample on spaces.

`--count` `-c`: (1) Number of samples to print.

`--quiet` `-q`: (False) Suppress printing the prime text. 
