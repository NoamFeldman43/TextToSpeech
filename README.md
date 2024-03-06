
### Text-to-Speech Conversion using IBM Watson
This documentation provides instructions on how to use the IBM Watson Text-to-Speech service to convert text into speech using Python. The provided code demonstrates how to convert both a simple string and text from a file into speech audio files.

## Setup Instructions
# 1. Install Dependencies

Ensure you have the required dependencies installed. You can install them using pip:

    !pip install ibm_watson


ֳֳ# 2. Obtain API Key and Service URL
Before running the code, you need to obtain your IBM Watson Text-to-Speech API key and service URL. You can get them by signing up for the IBM Cloud and creating a Text-to-Speech service instance. Replace 'YOUR API KEY' and 'YOUR SERVICE URL' in the code with your actual API key and service URL.

# 3. Authenticate

    from ibm_watson import TextToSpeechV1
    from ibm_cloud_sdk_core.authenticators import IAMAuthenticator
    apikey = 'YOUR API KEY'
    url = 'YOUR SERVICE URL'
    # Setup Services
    authenticator = IAMAuthenticator(apikey)
    tts = TextToSpeechV1(authenticator=authenticator)
    tts.set_service_url(url)

## Code Explanation
# 1. Convert Strings
This part of the code demonstrates how to convert a simple string into speech and save it as an MP3 file.

    with open('./speech.mp3', 'wb') as audio_file:
    res = tts.synthesize('Hello World!', accept='audio/mp3', voice='en- 
    US_AllisonV3Voice').get_result()
    audio_file.write(res.content)
    
 # 2. Reading from a File
This part reads text from a file (churchill.txt), removes newline characters, concatenates the lines, and then converts the text into speech, saving it as an MP3 file.  

    with open('churchill.txt', 'r') as f:
    text = f.readlines()
    text = [line.replace('\n','') for line in text]
    text = ''.join(str(line) for line in text)

    with open('./winston.mp3', 'wb') as audio_file:
    res = tts.synthesize(text, accept='audio/mp3', voice='en-GB_JamesV3Voice').get_result()
    audio_file.write(res.content)

# 3. Convert with a Different Language Model
The code lists available voices (language models) that can be used for text-to-speech conversion.    

     import json
     voices = tts.list_voices().get_result()
     print(json.dumps(voices, indent=2))
    

happy coding ⭐
