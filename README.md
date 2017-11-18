<p float="left">
  <img src="img/dbm_mnist/rbm1.png" width="140" />
  <img src="img/dbm_mnist/samples.png" width="143" />
  <img src="img/dbm_cifar2/rbm_small_0.png" width="140" />
  <img src="img/dbm_cifar2/grbm.png" width="140" />
  <img src="img/dbm_cifar2/mrbm.png" width="140" />
  <img src="img/dbm_cifar/samples.png" width="140" />
</p>

# Boltzmann Machines
This repository implements generic and flexible RBM and DBM models with lots of features and reproduces some experiments from *"Deep boltzmann machines"* [**[1]**](#1), *"Learning with hierarchical-deep models"* [**[2]**](#2), *"Learning multiple layers of features from tiny images"* [**[3]**](#3), and some others.

## Table of contents
***TODO***

## What's Implemented
### Restricted Boltzmann Machines (RBM)
* k-step Contrastive Divergence;
* whether to sample or use probabilities for visible and hidden units;
* *variable* learning rate, momentum and number of Gibbs steps per weight update;
* *regularization*: L2 weight decay, dropout, sparsity targets;
* *different types of stochastic layers and RBMs*: implement new type of stochastic units or create new RBM from existing types of units;
* *predefined stochastic layers*: Bernoulli, Multinomial, Gaussian;
* *predefined RBMs*: Bernoulli-Bernoulli, Bernoulli-Multinomial, Gaussian-Bernoulli;
* initialize weights randomly, or from `np.ndarray`s or from another RBM;
* can be modified for greedy layer-wise pretraining of DBM (see [**[1]**](#1) or notes for details);
* *visualizations in Tensorboard* (hover images for details) and more:
<p align="center">
  <img src="img/tensorboard_rbm/msre.png" height="170" title="Mean squared reconstruction error" />
  <img src="img/tensorboard_rbm/pll.png" height="170" title="Pseudo log-likelihood" />
  <img src="img/tensorboard_rbm/feg.png" height="170" title="Free energy gap [4]" />
</p>  

<p align="center">
  <img src="img/tensorboard_rbm/l2_loss.png" height="170" title="L2 loss (weight decay cost times 0.5||W||^2)" />
  <img src="img/tensorboard_rbm/dist_W.png" width="280" title="Distribution of weights and biases" />
  <img src="img/tensorboard_rbm/dist_hb.png" width="280" title="Distribution of weights and biases" />
</p>

<p align="center">
  <img src="img/tensorboard_rbm/dist_dW.png" width="280" title="Distribution of weights and biases updates" />
  <img src="img/tensorboard_rbm/dist_dvb.png" width="280" title="Distribution of weights and biases updates" />
  <img src="img/tensorboard_rbm/hist_W.png" width="280" title="Histogram of weights and biases" />
</p>

<p align="center">
  <img src="img/tensorboard_rbm/hist_hb.png" width="280" title="Histogram of weights and biases" />
  <img src="img/tensorboard_rbm/hist_dW.png" width="280" title="Histogram of weights and biases updates" />
  <img src="img/tensorboard_rbm/hist_dvb.png" width="280" title="Histogram of weights and biases updates" />
</p>

<p align="center">
  <img src="img/tensorboard_rbm/hidden_activations.gif" height="246" title="Hidden activations probabilities (means)" />
  <img src="img/tensorboard_rbm/mnist_5.gif" height="246" title="Weight filters" />
  <img src="img/tensorboard_rbm/mnist_8.gif" height="246" title="Weight filters" />
</p>

<p align="center">
  <img src="img/tensorboard_rbm/cifar_small_6_1.gif" width="161" title="Weight filters" />
  <img src="img/tensorboard_rbm/cifar_small_8_6.gif" width="161" title="Weight filters" />
  <img src="img/tensorboard_rbm/cifar_6.gif"  width="161" title="Weight filters" />
  <img src="img/tensorboard_rbm/cifar_18.gif" width="161" title="Weight filters" />
  <img src="img/tensorboard_rbm/cifar_9.gif"  width="161" title="Weight filters" />
</p>

### Deep Boltzmann Machines (DBM)
* EM-like learning algorithm based on PCD and mean-field variational inference [**[1]**](#1);
* arbitrary number of layers of any types;
* initialize from greedy layer-wise pretrained RBMs (no random initialization for now);
* whether to sample or use probabilities for visible and hidden units;
* *variable* learning rate, momentum and number of Gibbs steps per weight update;
* *regularization*: L2 weight decay, maxnorm, sparsity targets;
* estimate partition function using Annealed Importance Sampling ([**[1]**](#1));
* estimate variational lower-bound (ELBO) using logẐ (currently only for 2-layer binary BM);
* generate samples after training;
* initialize negative particles (visible and hidden in all layers) from data;
* `DBM` class can be used also for training RBM and its features: more powerful learning algorithm, to estimate logẐ and ELBO, to generate samples after training;
* **visualizations in Tensorboard** (hover images for details) and more:
<p align="center">
  <img src="img/tensorboard_dbm/msre.png"         height="170" title="Mean squared reconstruction error" />
  <img src="img/tensorboard_dbm/n_mf_updates.png" height="170" title="Actual number of mean-field updates" />
  <img src="img/tensorboard_dbm/W_norm.png"       height="170" title="Maximum absolute value of weight matrix (for each layer)" />
</p>  

<p align="center">
  <img src="img/tensorboard_dbm/dist_W.png"   width="280" title="Distribution of weights and biases (in each layer)" />
  <img src="img/tensorboard_dbm/dist_W2.png"  width="280" title="Distribution of weights and biases (in each layer)" />
  <img src="img/tensorboard_dbm/dist_hb2.png" width="280" title="Distribution of weights and biases (in each layer)" />
</p>

<p align="center">
  <img src="img/tensorboard_dbm/dist_dW.png"  width="280" title="Distribution of weights and biases updates (in each layer)" />
  <img src="img/tensorboard_dbm/dist_dvb.png" width="280" title="Distribution of weights and biases updates (in each layer)" />
  <img src="img/tensorboard_dbm/dist_mu2.png" width="280" title="Distribution of variational parameters (in each layer)" />
</p>

<p align="center">
  <img src="img/tensorboard_dbm/hist_W.png"  width="280" title="Histogram of weights and biases (in each layer)" />
  <img src="img/tensorboard_dbm/hist_dW.png" width="280" title="Histogram of weights and biases updates (in each layer)" />
  <img src="img/tensorboard_dbm/hist_mu.png" width="280" title="Histogram of variational parameters (in each layer)" />
</p>

<p align="center">
  <img src="img/tensorboard_dbm/mnist_filter_L1_5.gif" width="161" title="Weight filters (in each layer)" />
  <img src="img/tensorboard_dbm/mnist_filter_L2_6.gif" width="161" title="Weight filters (in each layer)" />
  <img src="img/tensorboard_dbm/cifar_filter_L1_6.gif" width="161" title="Weight filters (in each layer)" />
  <img src="img/tensorboard_dbm/cifar_filter_L2_2.gif" width="161" title="Weight filters (in each layer)" />
  <img src="img/tensorboard_dbm/cifar_filter_L2_6.gif" width="161" title="Weight filters (in each layer)" />
</p>

<p align="center">
  <img src="img/tensorboard_dbm/mnist_particle_L1_2.gif" width="161" title="Negative particles (in each layer)" />
  <img src="img/tensorboard_dbm/mnist_particle_L1_4.gif" width="161" title="Negative particles (in each layer)" />
  <img src="img/tensorboard_dbm/cifar_particle_L1_1.gif" width="161" title="Negative particles (in each layer)" />
  <img src="img/tensorboard_dbm/cifar_particle_L1_2.gif" width="161" title="Negative particles (in each layer)" />
  <img src="img/tensorboard_dbm/cifar_particle_L1_4.gif" width="161" title="Negative particles (in each layer)" />
</p>

<p align="center">
  <img src="img/tensorboard_dbm/mnist_particles_L23.gif" height="200" title="Negative particles (in each layer)" />
</p>

### Features
* easy to use with `sklearn`-like interface;
* easy to load and save models;
* easy to reproduce (`random_seed` make reproducible both TensorFlow and numpy operations inside the model);
* all models support any precision (tested `float32` and `float64`);
* configure metrics to display during learning (which ones, frequency, format etc.);
* easy to resume training (note that changing parameters other than placeholders or python-level parameters (such as `batch_size`, `learning_rate`, `momentum`, `sample_v_states` etc.) between `fit` calls have no effect as this would require altering the computation graph, which is not yet supported; **however**, one can build model with new desired TF graph, and initialize weights and biases from old model by using `init_from` method);
* *visualization*: apart from TensorBoard, there also plenty of python routines to display images, learned filters, confusion matrices etc and more.

## Examples
### #1 RBM MNIST: [script](examples/rbm_mnist.py), *[notebook](notebooks/rbm_mnist.ipynb)*
Train Bernoulli RBM with 1024 hidden units on MNIST dataset and use it for classification.

| <div align="center">algorithm</div> | test error, % |
| :--- | :---: |
| RBM features + k-NN | **2.88** |
| RBM features + Logistic Regression | **1.83** |
| RBM features + SVM | **1.80** |
| RBM + discriminative fine-tuning | **1.27** |

<p float="left">
  <img src="img/rbm_mnist/filters.png" width="265" />
  <img src="img/rbm_mnist/filters_finetuned.png" width="265" /> 
  <img src="img/rbm_mnist/confusion_matrix.png" width="310" />
</p>

Also, [one-shot learning idea]:

| number of labeled data pairs (train + val) | RBM + fine-tuning | random initialization | gain |
| :---: | :---: | :---: | :---: |
| 60k (55k + 5k) | 98.73% | 98.20% | **+0.53%** |
| 10k (9k + 1k) | 97.27% | 94.73% | **+2.54%** |
| 1k (900 + 100) | 93.65% | 88.71% | **+4.94%** |
| 100 (90 + 10) | 81.70% | 76.02% | **+5.68%** |

How to reproduce the this table see [here](docs/rbm_discriminative.md). 
In these experiments only RBM was tuned to have high pseudo log-likelihood on a held-out validation set.
Even better results can be obtained if one will tune MLP and other classifiers.

---

### #2 DBM MNIST: [script](examples/dbm_mnist.py), *[notebook](notebooks/dbm_mnist.ipynb)*
Train 784-512-1024 Bernoulli DBM on MNIST dataset and use it for classification, generate samples after training, 
estimate partition function using Annealed Importance Sampling and average log-probability lower-bound (=evidence lower-bound, ELBO) 
on the test set. 

| algorithm | # intermediate distributions | proposal (p<sub>0</sub>) | logẐ | log(Ẑ &plusmn; &#963;<sub>Z</sub>) | avg. test ELBO |
| :---: | :---: | :---: | :---: | :---: | :---: |
| [**[1]**](#1) | 20'000 | base-rate? | 356.18 | 356.06, 356.29 | **-84.62** |
| this example | 200'000 | uniform | 1040.39 | 1040.18, 1040.58 | **-86.37** |
| this example | 20'000 | uniform | 1040.58 | 1039.93, 1041.03 | **-86.59** |

Couple of nats could have been lost because of single-precision.

<p float="left">
  <img src="img/dbm_mnist/rbm1.png" width="280" />
  <img src="img/dbm_mnist/W1_joint.png" width="280" /> 
  <img src="img/dbm_mnist/W1_finetuned.png" width="280" />
</p>
<p float="left">
  <img src="img/dbm_mnist/rbm2.png" width="280" />
  <img src="img/dbm_mnist/W2_joint.png" width="280" /> 
  <img src="img/dbm_mnist/W2_finetuned.png" width="280" />
</p>
<p float="left">
  <img src="img/dbm_mnist/mnist.png" width="274" />
  <img src="img/dbm_mnist/samples.png" width="279" /> 
  <img src="img/dbm_mnist/samples.gif" width="295" />
</p>

| number of labeled data pairs (train + val) | DBM + fine-tuning | random initialization | gain |
| :---: | :---: | :---: | :---: |
| 60k (55k + 5k) | 98.68% | 98.28% | **+0.40%** |
| 10k (9k + 1k) | 97.11% | 94.50% | **+2.61%** |
| 1k (900 + 100) | 93.54% | 89.14% | **+4.40%** |
| 100 (90 + 10) | 83.79% | 76.24% | **+7.55%** |

How to reproduce the this table see [here](docs/dbm_discriminative.md).

Again **tune better**.

Performance on full training set is slightly worse because of harder optimization problem + vanishing gradients.
Also because the optimization problem is harder, the gain when not much datapoints are used is typically larger.

Large number of parameters is one of the most crucial reasons why one-shot learning is not successfuly by utilizing deep learning only. Instead, it is much better to combine deep learning and hierarchical Bayesian modeling by putting HDP prior over units from top-most hidden layer as in #paper.

---

### #3 DBM CIFAR-10 Naïve: [script](examples/dbm_cifar_naive.py), *[notebook](notebooks/dbm_cifar_naive.py)*

<p float="left">
  <img src="img/dbm_cifar_naive/grbm.png" width="210" />
  <img src="img/dbm_cifar_naive/W1_joint.png" width="210" />
  <img src="img/dbm_cifar_naive/mrbm.png" width="210" />
  <img src="img/dbm_cifar_naive/W2_joint.png" width="210" />
</p>
<p float="left">
  <img src="img/dbm_cifar_naive/cifar10_smoothed.png" width="275" />
  <img src="img/dbm_cifar_naive/samples.png" width="275" />
  <img src="img/dbm_cifar_naive/samples.gif" width="296" />
</p>

***TODO***: note that this is *modified* G-RBM for DBM pre-training (see notes or [**[1]**](#1) for details):

| <div align="center">algorithm</div> | test accuracy, % |
| :--- | :---: |
| *Best known MLP w/o data augmentation*: 8 layer ZLin net [**[5]**](#5) | **69.62** |
| *Best known method using RBM (w/o data augmentation?)*: 10k hiddens + fine-tuning [**[3]**](#3) | **64.84** |
| Gaussian RBM + discriminative fine-tuning | **59.78** |
| Pure backprop 3072-5000-10 on smoothed data | **58.20** |
| Pure backprop 782-10k-10 on PCA whitened data [**[3]**](#3) | **51.53** |

<p float="left">
  <img src="img/dbm_cifar_naive/grbm.png" width="265" />
  <img src="img/dbm_cifar_naive/grbm_finetuned.png" width="265" /> 
  <img src="img/dbm_cifar_naive/grbm_confusion_matrix.png" width="307" />
</p>

---

### #4 DBM CIFAR-10: [script](examples/dbm_cifar.py), *[notebook](notebooks/dbm_cifar.py)*

***TODO*** in [**[2]**](#2) they trained on 4M images, here only 490k (x10 augmented CIFAR-10 only)

<p float="left">
  <img src="img/dbm_cifar/rbm_small_0.png" width="210" />
  <img src="img/dbm_cifar/rbm_small_2.png" width="210" /> 
  <img src="img/dbm_cifar/rbm_small_10.png" width="210" />
  <img src="img/dbm_cifar/rbm_small_20.png" width="210" />
</p>
<p float="left">
  <img src="img/dbm_cifar/grbm.png" width="275" />
  <img src="img/dbm_cifar/mrbm.png" width="275" /> 
  <img src="img/dbm_cifar/samples.png" width="275" hspace="11" /> 
</p>
<p float="left">
  <img src="img/dbm_cifar/W1_joint.png" width="275" />
  <img src="img/dbm_cifar/W2_joint.png" width="275" /> 
  <img src="img/dbm_cifar/samples.gif" width="296" /> 
</p>

<p float="left">
  <img src="img/dbm_cifar2/rbm_small_0.png" width="210" />
  <img src="img/dbm_cifar2/rbm_small_2.png" width="210" /> 
  <img src="img/dbm_cifar2/rbm_small_10.png" width="210" />
  <img src="img/dbm_cifar2/rbm_small_20.png" width="210" />
</p>
<p float="left">
  <img src="img/dbm_cifar2/grbm.png" width="275" />
  <img src="img/dbm_cifar2/mrbm.png" width="275" /> 
  <img src="img/dbm_cifar2/samples.png" width="275" hspace="11" /> 
</p>
<p float="left">
  <img src="img/dbm_cifar2/W1_joint.png" width="275" />
  <img src="img/dbm_cifar2/W2_joint.png" width="275" /> 
  <img src="img/dbm_cifar2/samples.gif" width="296" /> 
</p>

***TODO***: takes quite a lot of time to compute, but once trained, these nets can be used for other (similar) datasets/tasks.

| <div align="center">algorithm</div> | test accuracy, % |
| :--- | :---: |
| Gaussian RBM + discriminative fine-tuning + augmentation | **68.11** |
| *Best known method using RBM (w/o data augmentation?)*: 10k hiddens + fine-tuning [**[3]**](#3) | **64.84** |
| Gaussian RBM + discriminative fine-tuning | **64.38** |
| Gaussian RBM + discriminative fine-tuning (example #3) | **59.78** |

How to reproduce the this table see [here](docs/grbm_discriminative.md).

<p float="left">
  <img src="img/dbm_cifar2/grbm.png" width="265" />
  <img src="img/dbm_cifar2/grbm_no_aug_finetuned.png" width="265" /> 
  <img src="img/dbm_cifar2/grbm_confusion_matrix.png" width="307" />
</p>

---

### How to use examples
Use **script**s for training models from scratch, for instance
```
$ python rbm_mnist.py -h

(...)

usage: rbm_mnist.py [-h] [--gpu ID] [--n-train N] [--n-val N] [--n-hidden N]
                    [--w-init STD] [--vb-init] [--hb-init HB]
                    [--n-gibbs-steps N [N ...]] [--lr LR [LR ...]]
                    [--epochs N] [--batch-size B] [--l2 L2]
                    [--sample-v-states] [--dropout P] [--sparsity-target T]
                    [--sparsity-cost C] [--sparsity-damping D]
                    [--random-seed N] [--dtype T] [--model-dirpath DIRPATH]
                    [--mlp-no-init] [--mlp-l2 L2] [--mlp-lrm LRM [LRM ...]]
                    [--mlp-epochs N] [--mlp-val-metric S] [--mlp-batch-size N]
                    [--mlp-save-prefix PREFIX]

optional arguments:
  -h, --help            show this help message and exit
  --gpu ID              ID of the GPU to train on (or '' to train on CPU)
                        (default: 0)
  --n-train N           number of training examples (default: 55000)
  --n-val N             number of validation examples (default: 5000)
  --n-hidden N          number of hidden units (default: 1024)
  --w-init STD          initialize weights from zero-centered Gaussian with
                        this standard deviation (default: 0.01)
  --vb-init             initialize visible biases as logit of mean values of
                        features, otherwise (if enabled) zero init (default:
                        True)
  --hb-init HB          initial hidden bias (default: 0.0)
  --n-gibbs-steps N [N ...]
                        number of Gibbs updates per weights update or sequence
                        of such (per epoch) (default: 1)
  --lr LR [LR ...]      learning rate or sequence of such (per epoch)
                        (default: 0.05)
  --epochs N            number of epochs to train (default: 120)
  --batch-size B        input batch size for training (default: 10)
  --l2 L2               L2 weight decay coefficient (default: 1e-05)
  --sample-v-states     sample visible states, otherwise use probabilities w/o
                        sampling (default: False)
  --dropout P           probability of visible units being on (default: None)
  --sparsity-target T   desired probability of hidden activation (default:
                        0.1)
  --sparsity-cost C     controls the amount of sparsity penalty (default:
                        1e-05)
  --sparsity-damping D  decay rate for hidden activations probs (default: 0.9)
  --random-seed N       random seed for model training (default: 1337)
  --dtype T             datatype precision to use (default: float32)
  --model-dirpath DIRPATH
                        directory path to save the model (default:
                        ../models/rbm_mnist/)
  --mlp-no-init         if enabled, use random initialization (default: False)
  --mlp-l2 L2           L2 weight decay coefficient (default: 1e-05)
  --mlp-lrm LRM [LRM ...]
                        learning rate multipliers of 1e-3 (default: (0.1,
                        1.0))
  --mlp-epochs N        number of epochs to train (default: 100)
  --mlp-val-metric S    metric on validation set to perform early stopping,
                        {'val_acc', 'val_loss'} (default: val_acc)
  --mlp-batch-size N    input batch size for training (default: 128)
  --mlp-save-prefix PREFIX
                        prefix to save MLP predictions and targets (default:
                        ../data/rbm_)
```
or download pretrained ones with default parameters using `models/fetch_models.sh`, 
</br>
and check **notebook**s for corresponding inference / visualization etc.
Note that training is skipped if there is already a model in `model-dirpath` (you can choose different location for training another model).

---

### Memory requirements
* GPU memory: at most 2-3 GB for each model in each example, and it is always possible to decrease batch size and number of negative particles;
* RAM: at most 11GB (to run last example, features from Gaussian RBM are in `half` precision) and (much) lesser for other examples.

## TeX notes
***TODO*** definitely check them out!

## How to install
By default, the following commands install (among others) **tensorflow-gpu~=1.3.0**. If you want to install tensorflow without GPU support, replace corresponding line in [requirements.txt](requirements.txt). If you have already tensorflow installed, comment that line.
```bash
git clone https://github.com/monsta-hd/hd-models
cd hd-models/
pip install -r requirements.txt
```
See [here](docs/virtualenv.md) how to run from a ***virtual environment***.
</br>
See [here](docs/docker.md) how to run from a ***docker container***.

To run some notebooks you also need to install [**JSAnimation**](https://github.com/jakevdp/JSAnimation):
```bash
git clone https://github.com/jakevdp/JSAnimation
cd JSAnimation
python setup.py install
```
After installation, tests can be run with:
```bash
make test
```
All the necessary data can be downloaded with:
```bash
make data
```
### Common installation issues
**ImportError: libcudnn.so.6: cannot open shared object file: No such file or directory**.<br/>
TensorFlow 1.3.0 assumes cuDNN v6.0 by default. If you have different one installed, you can create symlink to `libcudnn.so.6` in `/usr/local/cuda/lib64` or `/usr/local/cuda-8.0/lib64`. More details [here](https://stackoverflow.com/questions/42013316/after-building-tensorflow-from-source-seeing-libcudart-so-and-libcudnn-errors).

## TODO
* add stratification
* experiment: generate half MNIST digit conditioned on the other half using RBM 
* feature: Centering trick
* feature: classification RBMs/DBMs
* feature: ELBO and AIS for arbitrary DBM (again, visible and topmost hidden units can be analytically summed out) and for RBM (perhaps by using DBM class)
* optimize input pipeline e.g. use queues instead of `feed_dict` etc.

## Contributing
***TODO***

## References
**[1]**<a name="1"></a> R. Salakhutdinov and G. Hinton. *Deep boltzmann machines.* In: Artificial Intelligence and
Statistics, pages 448–455, 2009. [[PDF](http://proceedings.mlr.press/v5/salakhutdinov09a/salakhutdinov09a.pdf)]

**[2]**<a name="2"></a> R. Salakhutdinov, J. B. Tenenbaum, and A. Torralba. *Learning with hierarchical-deep models.* IEEE transactions on pattern analysis and machine intelligence, 35(8):1958–1971, 2013. [[PDF](https://www.cs.toronto.edu/~rsalakhu/papers/HD_PAMI.pdf)]

**[3]**<a name="3"></a> A. Krizhevsky and G. Hinton. *Learning multiple layers of features from tiny images.* 2009. [[PDF](https://www.cs.toronto.edu/~kriz/learning-features-2009-TR.pdf)]

**[4]**<a name="4"></a> G. Hinton. *A practical guide to training restricted boltzmann machines.* Momentum, 9(1):926,
2010. [[PDF](https://www.cs.toronto.edu/~hinton/absps/guideTR.pdf)]

**[5]**<a name="5"></a> Lin Z, Memisevic R, Konda K. *How far can we go without convolution: Improving fully-connected networks*, ICML 2016. [[arXiv](https://arxiv.org/abs/1511.02580)]
