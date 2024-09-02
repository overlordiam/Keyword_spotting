# Keyword Spotting

## Overview
This project presents a comprehensive comparison between discrete and continuous audio tokens in the context of keyword spotting. Using Python, PyTorch, and SpeechBrain, the study evaluates the performance of various audio representation methods, including both continuous features extracted from state-of-the-art models and discrete tokens generated by neural audio codecs.

## Key Components:
### Continuous Audio Features:
- WavLM
- HuBERT
- Wav2vec
### Discrete Audio Tokens:
- EnCodec
- Discrete Autoencoder Codec (DAC)

### Loss function: Negative Log Likelihood

### Task: Keyword Spotting

## Tools and Libraries:
- Python
- PyTorch
- SpeechBrain
- Matplotlib
  
## Observations
All models went through extensive hyperparameter tuning. A variety of neural networks were excersized, with highlights being RNNs, LSTMs and Transformers.

### Continuous features
Continuous features are real-valued features extracted from audio signals. Since they are continuous, they have fine-grained values/information of the downstream task and perform incredibly well, even with just a simple classifier.

#### Fbanks
Fbanks does very good job in extracting and downsizing features from the audio signal. It does not overfit or underfit on the data as well. This only strengthens the case for continuous features in speech related tasks. The error rate dips to very low values. The final test error rate is 2%, which is amazing. They soon reach saturation near the end of 20 epochs.

#### Wav2Vec
The model seems to overfit slightly on the data even though we just use a simple linear layer as a classifier. This is because we are fine-tuning all the layers of Wav2Vec on the downstream task on a relatively small dataset. With more data, this problem can be tackled. Ideally, the training would have been stopped at epoch 5 or 6 but for clarity and understanding, we continue to train for 20 epochs. The error rate is not a smooth decline but it is reducing nonetheless. Through fine-tuning, it reaches an error rate of 1.65% on the test set which proves the effectiveness of Wav2Vec.

#### Hubert
Similar to Wav2Vec, the model seems to overfit slightly on the data even though we just use a simple linear layer as a classifier. This is because we are fine-tuning all the layers of HuBERT on the downstream task on a relatively small dataset. With more data, this problem can be tackled. Again, ideally the training would stop at the 5th epoch. The error rate is not a smooth decline but it is reducing nonetheless. Through fine-tuning, it reaches an error rate of 1.23% on the test set on HuBERT.

#### WavLM (best performing model)
WavLM performs exceedingly well within a few epochs. The error rate is not smooth but decreases in time. The final test error rate is 0.76% which is amazing.

### Discrete features
Discrete features in Speech Recognition contain distinct, categorical data about the audio signals. They give us linguistic information like phenomes or words. The main reason why we want to utilize discrete features is due to their compactness. They are more data efficient and robust. We will mainly use Encodec for the experimentation.

### Encodec (best performing model)
sequence based models will be an excellent choice since audio signals are technically sequential. We see that the model does not overfit on the data as well. The error rate also gradually decreases in an almost smooth curve. The final test error rate is 56% which is very good compared to Xvector.

## Conclusion
It is by no surprise that the models with continuous features perform very well since they have fine-grained information of the input audio. Architectures using WavLM reach error rates of 0.56% which is an optimal performance. However, they are more computationally expensive. On the other hand, architectures using discrete features show great promise with error rates as low as 20%. They are more efficient and show great potential as well. 
