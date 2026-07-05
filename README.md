1. Introduction 
Neural Machine Translation (NMT) is a deep learning approach to the translation of text from one language to another. This is a customized Sequence-to-Sequence (Seq2Seq) model for Sanskrit-to-English translation using only available parallel corpus. The word order and complex grammar of Sanskrit is flexible and translation is challenging, because it is a morphologically rich and low-resource language. The aim is to obtain precise English translations and to test the system via BLEU, BERTScore, inference time and model parameters.
2. Architecture
Invariant Input: The input is given as Sanskrit token embeddings
Bahdanau Attention: Bahdanau Attention computes attention scores between the encoder states and the current decoder state and thus drives the decoder to attend to relevant source words.

Decoder: The decoder in LSTM is an LSTM that outputs one token in English per step based on the previous token, the state of the decoder, and the context vector of the attention. 
Beam Search: To improve the translation quality over greedy decoding, during inference beam search (with beam width = 5) is used to keep multiple candidate translations.

3. Training Procedure
Normalization, validation and alignment with Source_id: Unicode normalization, Whitespaces normalization, Sentence validation. 
Tokenizer: SentencePiece BPE tokenizer with the provided Sanskrit Training Corpus. English vocabulary learned from the training data with <PAD>, <SOS>, <EOS> and <UNK> tokens. 
Hyperparameters: 
Embedding=256, Hidden=512, Layers=2, Dropout=0.3, Batch Size=64, Epochs=30, Learning Rate=0.001, Optimizer=Adam, Beam Width=5. 
Optimization & Regularization: Cross-Entropy Loss, Teacher Forcing, Gradient Clipping, Xavier Initialization, Early Stopping and Dropout.

4. Results

Inference Time (seconds): 3.6618924140930176
Total Parameters : 16513696
Trainable Parameters : 16513696
BLEU Score: 0.002919898098670178
BERT Precision : 0.7507842183113098
BERT Recall    : 0.8183308839797974
BERT F1 Score  : 0.7827749252319336
 
Adding training/validation loss curve from the notebook as below:
 
5. Translation Examples
 
6. Experiments 
Analyze the effect of various decoding strategies (Greedy vs Beam Search), teacher forcing ratio, dropout ratio and hidden dimensions. Make observations about the quality of translation and convergence. 
7. Discussion 
The components of the design are: Bidirectional LSTM: It captures the context from both directions, Bahdanau Attention: It improves the word alignment, SentencePiece: Subword Tokenization, Beam Search: Improving the quality of the inference. 
Problem Issues: Insufficient parallel data, abundance in Sanskrit morphology, flexibility in sentence pattern and sparseness in vocabulary. 
Limitations: Long sentences or sentences on specific domains may be more difficult to perform on correctly, as there is less training data for these these cases. 
Future Work: Investigate Transformers architectures, multilingual pretraining, larger parallel corpora and advanced decoding strategies.
 8. References 
 [1] Sequence to Sequence Learning with Neural Networks by Sutskever, Vinyals, and Le, NLP paper at NeurIPS 2014. 
[2] Neural Machine Translation by Jointly Learning to Align and Translate, ICLR, 2015,Bahdanau, Cho, Bengio. 
[3] Kudo and Richardson (SentencePiece, EMNLP, 2018). 
[4] BLEU: A Method for Automatic Evaluation of Machine Translation, ACL 2002, Papineni et al.

9.Pre-trained Model Disclosure

No translation models have been pre-trained for training or inference. The model Seq2Seq (Bidirectional LSTM Encoder, Bahdanau Attention, LSTM Decoder) was trained from scratch, using just the given dataset. A training corpus was given to SentencePiece for training it to tokenize the sentences. The BERTScore was evaluated using a pre-trained BERT model, but was not used to generate translations.
<img width="432" height="655" alt="image" src="https://github.com/user-attachments/assets/7ca289b2-a83f-4128-8092-1a4369987d06" />
