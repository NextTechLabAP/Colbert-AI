<h1 align="center">Colbert AI</h1>
<p align="center">
  <img src="https://img.shields.io/github/stars/NextTechLabAP/Colbert-AI?style=flat-square">
  <a href="https://github.com/NextTechLabAP/Colbert-AI/issues"><img alt="GitHub issues" src="https://img.shields.io/github/issues/NextTechLabAP/Colbert-AI?style=flat-square"></a>
  <a href="https://github.com/NextTechLabAP/Colbert-AI/network"><img alt="GitHub forks" src="https://img.shields.io/github/forks/NextTechLabAP/Colbert-AI?style=flat-square"></a>
  <a href="https://github.com/NextTechLabAP/Colbert-AI/blob/master/LICENSE"><img alt="GitHub license" src="https://img.shields.io/github/license/NextTechLabAP/Colbert-AI?style=flat-square"></a>
  <img src="https://img.shields.io/badge/version-2.0-yellow?style=flat-square">
</p>

![ColbertAI](https://i.imgur.com/Qd5CRvv.png)
 
--- 

### What is Colbert AI?
Colbert AI is a Deep Learning Language Model that generates text in the style of *Stephen Colbert's* famous monologues. 

### How did we build it?
We used State of the Art Deep Learning Language model: Open AI's GPT-2 and Fine Tuned it using text from YouTube video captions. 

## Technical Details

### Libraries used
- [Transformers](https://github.com/huggingface/transformers)
- [GPT-2](https://github.com/openai/gpt-2)
- [Pytorch](https://github.com/pytorch/pytorch)
- youtube_dl

#### Downloading Video Captions From YouTube
- The playlist is specified by `PLAYLIST_URL` in [`download.py`](./download.py)
- `youtube_dl` module to download captions of each video from the playlist and saving all of them in *data/captions* folder

#### Generating Text Corpus from Captions
- We only looked for text where the speaker was Stephen Colbert
- Individual captions were merged into single file, separated by an End of Text Marker

### Usage Guide:
#### Using Colbert-AI to generate text based on Stephen Colbert's monologues.
- Clone this repository, using:
  ```
  git clone https://github.com/NextTechLabAP/Colbert-AI.git
  ````
- Install all requirements on `requirements.txt` using:
  ```
  pip install -r requirements.txt
  ```
- Run `python3 download.py` to download the captions
- Run `python3 caption_processing.py` to process the captions
- Open the `Colbert-AI-v2.ipynb` Jupyter Notebook
- Change path to captions.txt
- Rull all cells
#### Using Colbert-AI to generate text based on a custom text corpus
-  Clone this repository, using:
   ```
   git clone https://github.com/NextTechLabAP/Colbert-AI.git
   ```
- Open the `Colbert-AI-v2.ipynb` Jupyter Notebook
- Change path from `captions.txt` to the Custom Text Corpus file
- Rull all cells

### The Model
![GPT-2](https://camo.githubusercontent.com/fcbb88b1da94de3e5d4d773ad8ab395ae45f300a/68747470733a2f2f692e696d6775722e636f6d2f797249785056582e706e67)
#### GPT-2 has 4 different models:
- GPT-2 Small (124M Model)
- GPT-2 Medium (345M Model)
- GPT-2 Large (774M Model)
- GPT-2 Extra Large (1558M Model)

We used GPT-2 Medium for our use case since we focused on building a lighter model so we could fine-tune it further. 

#### Functions Used

##### `choose_from_top(Probability, N)`:
- Function to first select top N tokens from the probability list and then based on the selected N-word distribution
##### `generate_text(Input_Text, Length) `:
- At each prediction step, GPT2 model needs to know all of the previous sequence elements to predict the next one. Below is a function that will tokenize the starting input text, and then in a loop, one new token is predicted at each step and is added to the sequence, which will be fed into the model in the next step. In the end, the token list is decoded back into a text.

#### Generating Text
##### Text Can be Generated using `generate_text`. One of the Text Samples generated using prompt "Artificial Intelligence is ":
- *Artificial general intelligence is the most likely future of the human race; it's a science which is not just possible but inevitable."*

#### Fine-Tuning
- Dataset has been preprocessed and prepared in `Text_Corpus` class.
- **Variable Hyperparameters**
  - `BATCH_SIZE = (1)`
  - `EPOCHS = (30)`
  - `LEARNING_RATE = (1e-5)`
  - `WARMUP_STEPS = (10000)`
  - `MAX_SEQ_LEN = (550)`
##### Training the Model
We trained the model and saved the model weights after each epoch. Then we generated Text Samples from the saved weights.

##### Results
- *Now, there are some people out there who think trump's a bad person. For instance, this weekend, I watched the presidential candidate's first candidate round-up, and he was named "The man who can't get anything he wants to get right." ( cheers and applause ) that's a good quality. That's a good quality, because the only person who can't get anything right is Donald Trump. ( laughter ) and I'm not sure he's read the new book, "The man who can't get anything wrong."*

- *This is a big day for the president of the united states. Trump is about to be released from impala. (laughter) (applause) and this is huge news because this is a big week for him because the court has decided that he can no longer use the n-word, because, in a letter to his staff, the president said, "If I didn't use the n-word, then why are all the other white house staff members calling me a cuck?!" (laughter) (applause) (cheers and applause) (piano riff) and trump's not the only person who has been in jail for the "N-word." last week, Austin turns out to be a founder of "N-god," which was also the name of a movie. (cheers and applause) and now trump is going to have a new "N-god." (laughter) and, of course, the "N-god"*


## Contributors
- [@iam-abbas](https://github.com/iam-abbas)
- [@cshubhamrao](https://github.com/cshubhamrao)

**Mentions:** 
- [Martins Frolovs](https://towardsdatascience.com/teaching-gpt-2-a-sense-of-humor-fine-tuning-large-transformer-models-on-a-single-gpu-in-pytorch-59e8cec40912)
