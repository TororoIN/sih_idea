# sih_idea
The problem statement NR1166 requires us to develop an application based on NLP technologies for effective mass conceptual learning in vernacular languages. 
Our solution is to use ASR, Translation, Emotional Speech Synthesis and Voice Conversion to generate speech in target language using the source speaker's voice and emotions. For this, we use

- Wav2Vec2.0 for ASR (WER 15.927, CER 8.872)
- BERT (IndicBERT) for Translation
- VAE-Tacotron for Emotional Speech Synthesis
- AutoVC for Voice Conversion

## Reason for choice of architecture
- Wav2Vec2.0
The Wav2Vec2.0 model by FAIR is a ground-breaking model, reason being that it pretrains on unlabelled speech data and then can be fine-tuned for even 10 minutes of audio to generate results on par with algorithms trained on labelled speech data. The importance of this architecture is that, we dont need massive speech corpora to achieve SOTA results. 

- VAE-Tacotron
The VAE-Tacotron architecture is a simple Tacotron model with a VAE to encode Emotion from samples along with Text. 
