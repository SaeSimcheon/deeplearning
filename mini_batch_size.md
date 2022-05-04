### mini_batch_size에 관함.

[Although large mini-batches improve computational efficiency by providing parallelism, research shows that large mini-batches lead to networks with a poorer ability to generalise and that take longer to train. ](https://www.topbots.com/how-solve-memory-challenges-deep-learning-neural-networks-graphcore/)

- 큰 mini batch 사이즈는 연산상의 효율을 가져다줄 수 있지만, 늦은 수렴 때문에 네트워크의 일반화 능력을 저하시키고, 더 긴 학습 시간을 갖게 한다고 함.


[참고](https://stats.stackexchange.com/questions/164876/what-is-the-trade-off-between-batch-size-and-number-of-iterations-to-train-a-neu)

[전반적인 가이드](https://www.kaggle.com/code/residentmario/full-batch-mini-batch-and-online-learning/notebook)


# Full batch, mini-batch, and online learning
## Definitions

Neural networks are trained in a series of epochs. 

### Epoch : one forward pass -> one backpropogation pass over all of the provided training samples. 


### Full batch learnin
- Compute the true gradient
- The true gradient provides an exact answer to the question of which stepping direction is optimal, as far as gradient descent is concerned.


### Mini-batch learning
- Update the training weights several times over the course of a single epoch
- Computing an approximation of the true gradient

### Online learning
- Adjust the gradient after every single forward and backwards pass.

### Sample
- Individual instance in data.

### Batch 
- The subset of full data which consists of samples. [If training, a batch results in only one update to the model.](https://keras.io/getting_started/faq/#what-do-sample-batch-and-epoch-mean)

### Batch size
- The amount of a subset of full data which consists of samples.

Tradeoffs

Full batch 
- Less random than mini-batch or online learning, both of which are dependent on the batch.
- Nice smooth steps towards the globally optimal decision point.

- The entire data must be in memory.


Minibatch
- More exposed to randomness in the dataset and in the choice of the batch size so that updating model seems more random than full batch.
- The smaller the batch size, the greater the randomness.
- Assuming a batch size chosen is appropriate, the model converges quickly than full batch case.
- Full batch case must perform the full dataset scan for every single weight update. 
- Mini-batch learners get to perform the same process for weight update multiple times per epoch. Assuming you choose an representative batch size this results in multiplicatively faster training.


Online learners 
- The most random of all.
- Because the steps they take are all over the place, they're significantly harder to debug. For this reason they are not usually used in static applications. However they are useful for applications that perform machine learning a runtime, as they eliminate the need for an expensive batch recomputation on reaching arbitrary input volume thresholds.

Best practices
- Full batch learning is generally used for very small datasets.
- Online learning is the domain of sophisticated production data systems that live in production. 
- Minibatch learning is the general strategy.
- Determining the correct batch size is left to experimentation, since it is highly data-dependent. 


### Small ve large 

```
- small -> less efficient in computing(gradient calculation), but fast convergence. higher Volatility. 
- large -> more efficient in computing(gradient calculation), but slow convergence. lower Volatility.
  - tend to converge to minima with poorer generalization characteristics. Sharp minima, are less able to escapce from sharp minima.
```

### Learning rate and batch size

[Bigger batches should have bigger learning rate.]
- An important factor to be considered when selecting a batch size is the learning rate. 
A larger learning rate will compensate for a reliable slow-learning gradient, and a smaller learning rate will compensate for a more random fast-learning gradient. This visualization, taken from this blog post on the subject, shows a comparison between larger and smaller batch sizes, the learning rate, and the error rate the model ultimately converges to:



[Effect of Batch Size on Model Behavior 참고.](https://machinelearningmastery.com/how-to-control-the-speed-and-stability-of-training-neural-networks-with-gradient-descent-batch-size/)

```
The plots show that small batch results generally in rapid learning but a volatile learning process with higher variance in the classification accuracy. Larger batch sizes slow down the learning process but the final stages result in a convergence to a more stable model exemplified by lower variance in classification accuracy.
```

