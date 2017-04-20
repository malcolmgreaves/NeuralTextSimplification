# Exploring Neural Text Simplification

## Abstract
We present the first attempt at using sequence to sequence neural networks to model text simplification (TS). Unlike the previously proposed automated methods, our neural text simplification (NTS) systems are able to simultaneously perform lexical simplification and content reduction. An extensive human evaluation of the output has shown that NTS systems achieve good grammaticality and meaning preservation of output sentences and higher level of simplification than the state-of-the-art automated TS systems. We train our models on the [Wikipedia corpus](http://ssli.ee.washington.edu/tial/projects/simplification) containing _good_ and _good partial_ alignments.
```
	@InProceedings{neural-text-simplification,
	  author    = {Sergiu Nisioi and Sanja Štajner and Simone Paolo Ponzetto and Liviu P. Dinu},
	  title     = {Exploring Neural Text Simplification Models},
	  booktitle = {{ACL} {(2)}},
	  publisher = {The Association for Computer Linguistics},
	  year      = {2017}
	}
```

## Simplify Text | Generate Predictions (no GPUs needed)
1 Checkout the OpenNMT source:
```
   git submodule init
   git submodule update
```
2 Download the pre-trained released models [NTS]() and [NTS-w2v]():
```
   python models/download.py
```
3 Run translate.sh from the scrpts dir:
```
   cd src/scripts
   ./translate.sh
```
4 Check your predictions in the results directory:
```
   cd ../../results_NTS
```

## Content of this Repository
#### ./predictions
Contains predictions from previous systems (Wubben et al., 2012), (Glavas and Stajner, 2015), and (Xu et al., 2016), and the generated predictions of the NTS models reported in the paper:
- NTS_default_b5_h1 - the default model, beam size 5, hypothesis 1
- NTS_BLEU_b12_h1 - the BLEU best ranked model, beam size 12, hipothesis 1
- NTS_SARI_b5_h2 - the SARI best ranked model, beam size 12, hipothesis 1

- NTS-w2v_default_b5_h1 - the default model, beam size 5, hypothesis 1
- NTS-w2v_BLEU_b12_h1 - the BLEU best ranked model, beam size 12, hipothesis 1
- NTS-w2v_SARI_b12_h2 - the SARI best ranked model, beam size 12, hipothesis 2

#### ./data 
Contains the training, testing, and [reference](https://github.com/cocoxu/simplification) sentences used to train and evaluate our models.

#### ./models
Contains a script to download the pre-trained models used to output the results reported in our paper.  
```
	python models/download.py
```
In case the download fails, you may use the direct links for [NTS](https://drive.google.com/file/d/0B_pjS_ZjPfT9QjFsZThCU0xUTnM) and [NTS-w2v](https://drive.google.com/file/d/0B_pjS_ZjPfT9U1pJNy1UdV9nNk0)

#### ./configs
Contains the OpenNMT config file. To train, please update the config file with the appropriate data on your local system and run 
```
	th train -config $PATH_TO_THIS_DIR/configs/NTS.cfg
```
#### ./src 
- train_word2vec.py a script that creates a word2vec model from a local corpus, using gensim
- SARI.py copy of the [SARI](https://github.com/cocoxu/simplification) implementation
- evaluate.py evaluates BLEU and SARI given a source file, a directory of predictions and a reference file in tsv format
```
	python evaluate.py ../data/test.en ../data/references/references.tsv ../predictions/
```	
- ./scripts - contains some of our scripts that we used to preprocess the data, output translations, and create the concatenated embeddings
- ./OpenNMT - the patch with some changes that need to be applied to the latest checkout of OpenNMT. 
Alternatively, one could use [our forked code](https://github.com/senisioi/OpenNMT/) directly.
