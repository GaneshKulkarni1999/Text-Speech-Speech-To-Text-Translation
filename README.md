*********************************************# Google Cloud Text-to-Speech Python Example**********************

This is a simple Python script that uses the [Google Cloud Text-to-Speech API](https://cloud.google.com/text-to-speech) to convert text into speech. The resulting speech is saved as an MP3 file on your local machine.

## Prerequisites

Before running this script, ensure that you have the following:

- A **Google Cloud account** and **Google Cloud SDK** installed.
- A **Google Cloud API key** for the Text-to-Speech API. Follow the [Google Cloud Text-to-Speech Setup Guide](https://cloud.google.com/text-to-speech/docs/quickstart-client-libraries) to get your API key.
- The required Python libraries installed (`requests`).

## Installation

1. Clone this repository to your local machine:

    ```bash
    git clone https://github.com/your-username/google-cloud-text-to-speech.git
    cd google-cloud-text-to-speech
    ```

2. Install the required Python packages:

    ```bash
    pip install -r requirements.txt
    ```

    If `requirements.txt` doesn't exist, you can install the `requests` package directly:

    ```bash
    pip install requests
    ```

3. Set your **Google Cloud API key** as an environment variable:

    ```bash
    export GOOGLE_API_KEY="your-api-key-here"
    ```

    **Or**, you can directly replace the `api_key` in the script with your actual API key (not recommended for production).

## Usage

1. Open the Python script (`text_to_speech.py`) in your editor.
2. In the script, change the value of `text` to whatever you want to convert to speech.
3. Run the script:

    ```bash
    python text_to_speech.py
    ```

4. The script will convert the input text into speech and save the resulting audio as `output.mp3` in the same directory.

### Example Request

The script sends a POST request to the Google Cloud Text-to-Speech API with the following data:

```json
{
  "input": {
    "text": "Hello, where are you from?"
  },
  "voice": {
    "languageCode": "en-US",
    "ssmlGender": "NEUTRAL"
  },
  "audioConfig": {
    "audioEncoding": "MP3"
  }
}



*************************************************# Google Cloud Translation API Python Example*****************************

This Python script demonstrates how to use the [Google Cloud Translation API](https://cloud.google.com/translate) to translate text from one language to another. The script will take input text, translate it to a target language, and print the translated text.

## Prerequisites

Before running this script, ensure that you have the following:

- A **Google Cloud account** and **Google Cloud SDK** installed.
- **Google Cloud Translation API** enabled for your Google Cloud project.
- A **Google Cloud API key** for the Translation API. You can get your API key by following the steps in the [Google Cloud Translation Setup Guide](https://cloud.google.com/translate/docs/setup).

## Installation

1. Clone this repository to your local machine:

    ```bash
    git clone https://github.com/your-username/google-cloud-translate.git
    cd google-cloud-translate
    ```

2. Install the required Python packages:

    ```bash
    pip install -r requirements.txt
    ```

    If `requirements.txt` doesn't exist, you can install the `google-cloud-translate` package directly:

    ```bash
    pip install google-cloud-translate
    ```

3. Set up your **Google Cloud API key**:
    - Create a service account and download the credentials JSON file.
    - Set the `GOOGLE_APPLICATION_CREDENTIALS` environment variable to the path of the downloaded credentials file:

    ```bash
    export GOOGLE_APPLICATION_CREDENTIALS="path-to-your-service-account-file.json"
    ```

    Alternatively, you can specify the API key directly in the code (not recommended for production environments).

## Usage

1. Open the Python script (`translate_text.py`) in your editor.
2. Change the `text` variable in the script to the text you want to translate.
3. Specify the target language in the `target_language` variable.
4. Run the script:

    ```bash
    python translate_text.py
    ```

5. The script will print the translated text to the console.

### Example Request

The script uses the Google Cloud Translation API to send a translation request with the following parameters:

```python
from google.cloud import translate_v2 as translate

def translate_text(text, target_language="en"):
    translate_client = translate.Client()
    result = translate_client.translate(text, target_language=target_language)
    return result['translatedText']


**************************************************# Google Cloud Speech-to-Text and Translation API Example************************************

This Python script demonstrates how to use the [Google Cloud Speech-to-Text API](https://cloud.google.com/speech-to-text) to transcribe audio to text, and then use the [Google Cloud Translation API](https://cloud.google.com/translate) to translate the transcribed text into another language.

## Prerequisites

Before running this script, ensure that you have the following:

- A **Google Cloud account** and **Google Cloud SDK** installed.
- **Google Cloud Speech-to-Text API** and **Google Cloud Translation API** enabled for your Google Cloud project.
- A **Google Cloud service account** with the necessary permissions to access the APIs.
- A **Google Cloud API key** or service account credentials for authentication.
- The required Python libraries installed (`google-cloud-speech`, `google-cloud-translate`).

## Installation

1. Clone this repository to your local machine:

    ```bash
    git clone https://github.com/your-username/google-cloud-speech-to-text-translate.git
    cd google-cloud-speech-to-text-translate
    ```

2. Install the required Python packages:

    ```bash
    pip install -r requirements.txt
    ```

    Alternatively, you can install the necessary libraries directly using:

    ```bash
    pip install google-cloud-speech google-cloud-translate
    ```

3. Set up your **Google Cloud service account credentials**:
    - Download the credentials JSON file for your service account from the Google Cloud Console.
    - Set the `GOOGLE_APPLICATION_CREDENTIALS` environment variable to the path of the downloaded credentials file:

    ```bash
    export GOOGLE_APPLICATION_CREDENTIALS="path-to-your-service-account-file.json"
    ```

4. Alternatively, you can pass the API key directly in the code (not recommended for production).

## Usage

1. Place the audio file you want to transcribe in the `audio` folder or specify its location in the script.
2. Open the Python script (`speech_to_text_and_translate.py`) in your editor.
3. Run the script:

    ```bash
    python speech_to_text_and_translate.py
    ```

4. The script will:
    - Transcribe the speech from the audio file.
    - Translate the transcribed text into the specified target language.
    - Print both the original transcription and the translated text.

### Example Code

```python
from google.cloud import speech
from google.cloud import translate_v2 as translate
import os

# Set up Google Cloud service account credentials
os.environ["GOOGLE_APPLICATION_CREDENTIALS"] = r"your-service-account-file.json"

# Function to transcribe audio to text using Google Speech-to-Text API
def transcribe_audio(audio_path):
    client = speech.SpeechClient()

    with open(audio_path, "rb") as audio_file:
        audio_content = audio_file.read()

    audio = speech.RecognitionAudio(content=audio_content)

    config = speech.RecognitionConfig(
        encoding=speech.RecognitionConfig.AudioEncoding.LINEAR16,
        sample_rate_hertz=16000,
        language_code="en-US",
    )

    response = client.recognize(config=config, audio=audio)

    # Extract and return the transcribed text
    transcription = ""
    for result in response.results:
        transcription += result.alternatives[0].transcript + " "
    
    return transcription

# Function to translate text using Google Cloud Translation API
def translate_text(text, target_language="en"):
    translate_client = translate.Client()
    result = translate_client.translate(text, target_language=target_language)
    return result['translatedText']

# Main function
def main():
    audio_path = "audio/sample_audio.wav"  # Path to your audio file
    transcription = transcribe_audio(audio_path)

    print(f"Original Transcription: {transcription}")

    # Translate the transcription into a different language (e.g., Hindi)
    translated_text = translate_text(transcription, target_language="hi")

    print(f"Translated Text: {translated_text}")

if __name__ == "__main__":
    main()

