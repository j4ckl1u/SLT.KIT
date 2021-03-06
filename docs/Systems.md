# Systems

## Cascaded Systems

### ctc-tedlium2.smallTED
 * This system combines the ctc-tedlium2 system and the small TED system.
 * Languages:
   * English-German
 * Training: There is no script to train this system directly, but you can train both system individually with the scripts in that folder
 * Download: You can download the system with the following script (remember to set the appropriate source and target language to select the correct MT system, if you haven't done that yet):

 ```bash
 export sl=en
 export tl=de
 /opt/SLT.KIT/systems/ctc-tedlium2.smallTED/Download.sh
 ```
  * For the individual components used in this system refer to the components of the two individual systems
  * Testing:
  ```bash
  /opt/SLT.KIT/systems/ctc-tedlium2.smallTED/Test.sh ${testset}
  ```
  
   * Output of the ASR component:  /data/ctc/eval/${testset}.s
   * Segmented and punctuated transcript: /data/monoTransPrepro/eval/ctc.${testset}.s
   * Translation: /data/mt/eval/ctc.${testset}.t
   * Results: /results/ctc-tedlium2.smallTED/ctc.${testset}/Summary.md

### ctc-tedlium2.midSize
  * Same as ctc-tedlium2.smallTED except using the midSize system for MT and segmentation/punctuation

## ASR Systems

### ctc-tedlium2
 * ASR system using the CTC loss trained on Byte Pair Units
 * Language: English
 * Training: The standard network uses BPE units created with 300 merge operations. You can retrain this model with BPE units created with 10000 merge operations:
```bash
# Train 300
/opt/SLT.KIT/systems/ctc-tedlium2/Train.sh
# Train 10000
/opt/SLT.KIT/systems/ctc-tedlium2/Train.sh 10000
```
* Download: You can download the models (both 300 and 10000) using the following script:

```bash
/opt/SLT.KIT/systems/ctc-tedlium2/Download.sh
```

 * Testing (10000 model):
 ```bash
 /opt/SLT.KIT/systems/ctc-tedlium2/Test.sh ${testset}
 ```
 
 * Data
   * Model: /model/ctc/bpe${bpe_steps}.mdl, /model/ctc/bpe${bpe_steps}.log, /model/ctc/units${bpe_steps}.json
   * Test Output: /data/ctc/eval/${testset}.s, /data/ctc/eval/${testset}.logits

### las-tedlium2

* ASR system using listen-attend-spell architecture
* Language: English
* Training: You can train the system with the scripts
```bash
/opt/SLT.KIT/systems/las-tedlium2/Train.sh
```
* Download: You can download the system with the scripts

```bash
/opt/SLT.KIT/systems/las-tedlium2/Download.sh
```
Testing:
 ```bash
 /opt/SLT.KIT/systems/las-tedlium2/Test.sh ${testset}
 ```

## MT/Sentence segmentation

### smallTED
* MT and sentence segmentation trained on the  [TED corpus](https://wit3.fbk.eu/)
* Languages:
  * German-English
  * English-German
  * English-French
* Components:
  * prepro: Preprocessing of the data; Tokenization, true casing
  * monoTransPrepro: Preprocessing for the training of the monolingual translation system. Removing of case and puncuation information, target representation by labels. For details [1]
  * monTrans: NMT-based monolingual translations system to predict punctuation using [OpenNMT-py](http://opennmt.net/)
  * mt: [OpenNMT-py](http://opennmt.net/) based NMT system
* Training: You can train the system with the scripts
```bash
/opt/SLT.KIT/systems/smallTED/Train.sh
```
* Download: You can download the system with the scripts

```bash
/opt/SLT.KIT/systems/smallTED/Download.sh
```
 * Testing:
 ```bash
 /opt/SLT.KIT/systems/smallTED/Test.sh ${testset}
 ```
   * Segmented and punctuated transcript of the provided ASR output in test data: /data/monoTransPrepro/eval/${testset}.s
   * Translation: /data/mt/eval/${testset}.t
   * Translation of the manual transcript: /data/mt/eval/manualTranscript.${testset}.t
   * Results /results/smallTED/${setset}/Summary.md


### midSize

* MT and sentence segmentation trained on the  [TED corpus](https://wit3.fbk.eu/) and the [EPPS corpus](http://statmt.org/europarl/)

[1] Cho, E., Niehues, J., Waibel, A. (2017). NMT-based Segmentation and Punctuation Insertion for Real-time Spoken Language Translation. In Proceedings of the 18th Annual Conference of the International Speech Communication Association (Interspeech 2017). Stockholm, Sweden.
