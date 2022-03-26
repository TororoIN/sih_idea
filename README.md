# sih_idea
The problem statement NR1166 requires us to develop an application based on NLP technologies for effective mass conceptual learning in vernacular languages. 
Our solution is to use ASR, Translation, Emotional Speech Synthesis and Voice Conversion to generate speech in target language using the source speaker's voice and emotions. For this, we use

- Wav2Vec2.0 for ASR (WER 15.927, CER 8.872)
- BERT (IndicBERT) for Translation
- VAE-Tacotron for Emotional Speech Synthesis
- AutoVC for Zero Shot Voice Conversion

## Reason for choice of architecture
- Wav2Vec2.0
The Wav2Vec2.0 model by FAIR is a ground-breaking model, reason being that it pretrains on unlabelled speech data and then can be fine-tuned for even 10 minutes of audio to generate results on par with algorithms trained on labelled speech data. The importance of this architecture is that, we dont need massive speech corpora to achieve SOTA results. 

- VAE-Tacotron
The VAE-Tacotron architecture is a simple Tacotron model with a VAE to encode Emotion from samples along with Text. The VAE extracts latent emotion representations from the sample and along with the Text encoder, provides it to the Tacotron Decoder. This, helps in generating speech with emotions similar to that of the sample provided to the VAE. Normally, training a Tacotron model takes weeks, if not months, due to the LAS (Location Sensitive Attention) layer. We replace this with a Guided Attention layer. In Guided attention, the mechanism is penalised for every instance it deviates from the 'alignment diagonal', which is a quick way to achieve alignment. Another trick we have used is using transliterated text, so that a model trained on English Corpus can be used as a pretrained model. This helps in two ways. (1) It reduces training time, hence reducing emissions
(2) In case of low resource languages, the model can be fine-tuned with little data.

- AutoVC
The AutoVC architecture is a dual encoder decoder architecture for Voice Conversion. The model comprises of a style encoder and a content encoder. According to the paper, the when a speaker embedding is provided to an encoder with a controlled bottleneck width, the network learns to disentangle the speaker information from the sample for regeneration. The idea behind the content encoder bottleneck width is that, with a narrow bottleneck, the loss of information is high and with a wide bottleneck, the speaker information is still present in the sample. An appropriate width bottleneck effectively disentngles the speaker information from the sample.
