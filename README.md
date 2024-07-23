# RafaelDemarchi-001
Áudio texto Demarchi 
import os
from google.cloud import speech

# Configuração das credenciais da API
os.environ["GOOGLE_APPLICATION_CREDENTIALS"] = "path/to/your/credentials.json"

def transcribe_audio(audio_path):
    client = speech.SpeechClient()

    with open(audio_path, "rb") as audio_file:
        content = audio_file.read()

    audio = speech.RecognitionAudio(content=content)
    config = speech.RecognitionConfig(
        encoding=speech.RecognitionConfig.AudioEncoding.LINEAR16,
        sample_rate_hertz=16000,
        language_code="pt-BR",
    )

    response = client.recognize(config=config, audio=audio)

    for result in response.results:
        print("Transcription: {}".format(result.alternatives[0].transcript))

# Caminho para o arquivo de áudio
audio_path = "path/to/extracted_audio_download.wav"
transcribe_audio(audio_path)
