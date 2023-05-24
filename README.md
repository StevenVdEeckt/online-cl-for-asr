# Online Continual Learning for Automatic Speech Recognition
Supplementary material to the paper "Rehearsal-Free Online Continual Learning for Automatic Speech Recognition", accepted at Interspeech 2023.

## ESPnet

ESPnet [Wanatabe et al., 2018] is used for all experiments. More specifically, we use ESPnet2.

## model

The model used in the experiments is an encoder-decoder end-to-end ASR model. It consists of a Conformer encoder and a Transformer decoder and has approx. 47M parameters. The configuration files can be found in the model folder. Note that there is one for the initial model, i.e. the model trained on the initial task $T_0$, and one for the model during online continual learning. 

The model folder also contains the token list (i.e. outputs) of the model. It consists of 5000 word pieces generated by SentencePiece model [Kudo and Richardson, 2018] on the initial task.  

## data

The Mozilla Common Voice dataset [Ardila et al., 2020] is used for the experiments. We consider the Common Voice 7.0 release (July 2021) and only the English data. To obtain six tasks, we consider only the speakers whose country is known and take the following six countries to obtain six tasks: 

Task  | Country | #utterances (train)
------------- | ------------- | ------------- 
us | United States | 349.6k
eng | England | 117.2k
aus | Australia | 57.1k
ind | India  | 71.6k
sco | Scotland | 10.7k
ire | Ireland | 7.3k

All information regarding the utterances and speakers per task can be found in the data folder. 

In all the experiments, us, being the largest task, is the initial task, i.e. it is used to obtain the initial model. The remaining five tasks are learned in an online continual learning fashion. They are sorted by task as explained in the paper. Moreover, within each task, batches are also sorted (alphabetically) by speaker.

## hyper-parameters

A small 'test experiment' is used to determine the values of the hyper-parameters. To this end, English from Phillippines, Singapore, Hongkong, Malaysia, Wales and Bermuda is used as one small 'test' task. This task, consisting of 13.2k utterances, is in size approximately 5% of the tasks of the 'real experiment'. Thus, the number of utterances that has to be learned in an online continual learning fashion is much smaller for this 'test experiment' than for the 'real experiment'. To determine the optimal value for a hyper-parameter, we try three different values and choose the value that results in the lowest AWER (average WER) over initial task us and the test task. Since the tesk task is so small, we put extra weight on 'overcoming forgetting' by giving us a higher weight (2 vs. 1) in. the computation of AWER. 

## References 

Ardila et al., “Common voice: A massively-multilingual speech corpus,” in Proceedings of the 12th Conference on Language Resources and Evaluation (LREC 2020), 2020, pp. 4211–4215. 

T. Kudo and J. Richardson, “SentencePiece: A simple and language independent subword tokenizer and detokenizer for neural text processing,” in Proceedings of the 2018 Conference on Empirical Methods in Natural Language Processing: System Demonstrations. Association for Computational Linguistics, 2018, pp. 66–71. 

S. Watanabe et al., “ESPnet: End-to-end speech processing toolkit,” in Proceedings of Interspeech, 2018, pp. 2207–2211. 
