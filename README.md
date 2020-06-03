Generative adversarial networks
===============================

### Acknowledgment

This Repository is based on this wonderful medium article :https://medium.com/ai-society/gans-from-scratch-1-a-deep-introduction-with-code-in-pytorch-and-tensorflow-cb03cdcdba0f



Generative adversarial networks ,shortly called GANs, is network the does the opposite of what most other deep learning networks tries to do. Instead of getting an input image or sequence and classifying it. The network takes some sort of input parameters that can be usually understood by human and create an image accordingly. GANs consists of two main components, The discriminator and generator. the discriminator network tries to classify whether the image is real or created by the generator. on the other hand , the generator ties to learn how to force the generator to classify its output as real,So the training of each network depends on being better than other network ,hence the name. The loss function for the Discriminator network is as follows:

$$J^{(D)}\left(\theta^{(D)}, \theta^{(G)}\right)=-\frac{1}{2} \mathbb{E}_{x \sim p_{\text {data}}} \log D(x)-\frac{1}{2} \mathbb{E}_{z} \log (1-D(G(z)))$$

where $D(x)$ equals $1$ when the discriminator classifies real data correctly and equals $0$ when the discriminator classifies fake data falsely. One can observe that when the discriminator classify correctly the loss goes to zero ,and when it classify the output,the loss goes to $\infty$.As for the generator loss,we will discuss the two of the proposed formulas in the following sections.

Generator loss
--------------

The first proposed loss formula may be $J^{(G)}=-J^{(D)}$. This loss means that the Generator takes penalty when the discriminator perform better. This seems intuitive,however, the first term the
$\frac{1}{2} \mathbb{E}_{x \sim p_{\text {data }}} \log D(x)$ has to-do with the correct classification of real data for the discriminator, which is irrelevant to the generator performance,therefore,this may not be the optimal value for the generator's loss function instead a better formula maybe $J^{(G)}=-\frac{1}{2} \mathbb{E}_{z} \log (D(G(z)))$,which represents the second term of the discriminator loss only. In the following section we will observer the results of the two loss functions.

Generator loss results comparison
---------------------------------

![Discriminator loss for $J^{(G)}=-J^{(D)}$ after 70 epochs of
training.Final loss value is $1.16$.](imgs/DGAN_a.png)

![Discriminator loss for
$J^{(G)}=-\frac{1}{2} \mathbb{E}_{z} \log (D(G(z)))$ after 70 epochs of
training.Final loss value is $1.247$.](imgs/DGAN_b.png)

 Discriminator loss for $J^{(G)}=-\frac{1}{2} \mathbb{E}_{z} \log (D(G(z)))$ after 70 epochs of training. Final loss value is $1.247$.

![Generator loss for $J^{(example5.assets/GGAN_a.png)}=-J^{(D)}$ after 70 epochs of
training.Final loss value is $1.972$.](imgs/GGAN_a.png)

 Generator loss for $J^{(G)}=-J^{(D)}$ after 70 epochs of training. Final loss value is $1.972$.

![Generator loss for
$J^{(example5.assets/GGAN_b.png)}=-\frac{1}{2} \mathbb{E}_{z} \log (D(G(z)))$ after 70 epochs of
training.Final loss value is $0.815$.](imgs/GGAN_b.png)

Generator loss for $J^{(G)}=-\frac{1}{2} \mathbb{E}_{z} \log (D(G(z)))$ after 70 epochs of training. Final loss value is $0.815$.

As seen from the figures above, setting
$J^{(G)}=-\frac{1}{2} \mathbb{E}_{z} \log (D(G(z)))$ does not only reduce the generator loss,but also it makes the generator and discriminator training runs much smoother. This is due to the fact that the generator now trains in the best direction possible,which in turn makes it converge smoother.

![The output of GANs network after 71 epochs with the generator loss
function
$J^{(G)}=-J^{(D)}$.](imgs/hori_epoch_71_a.png)

The output of GANs network after 71 epochs with the generator loss function $J^{(G)}=-J^{(D)}$.

![The output of GANs network after 71 epochs with the generator loss
function
$J^{(G)}=-\frac{1}{2} \mathbb{E}_{z} \log (D(G(z)))$.](imgs/hori_epoch_71_b.png)

The previous two figures shows that when $J^{(G)}=-\frac{1}{2} \mathbb{E}_{z} \log (D(G(z)))$, the results are better as the 
model converges faster.
