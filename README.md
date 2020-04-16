# Wiki Bot
Create a bot to answer the question from wikipedia.

## Install packages
Pre-install visual c++ build tools from [Visual C++ Build Tools](https://visualstudio.microsoft.com/visual-cpp-build-tools/).

```bash
pip install requests
pip install BeautifulSoup4
pip install lxml
pip install html5lib
```

## Utilise Wikipedia to answer question
Reference from [Open Jarvis](https://www.youtube.com/watch?v=T5UIySP9Owc&feature=youtu.be).

### Import packages
Install `pip install SpeechRecognition gtts pygame pipwin` first.

```python
import speech_recognition
import tempfile
import requests
from gtts import gTTS
from pygame import mixer 
from bs4 import BeautifulSoup
```

### Main Code
In terminal, type in `pip install pipwin`. Then type in `pipwin install pyaudio`.

```python
def listen():
    r = speech_recognition.Recognizer()

    with speech_recognition.Microphone() as source:
        r.adjust_for_ambient_noise(source)
        audio = r.listen(source)

    return r.recognize_google(audio, language='zh-TW')

def get_wiki_summary(question):
    r = requests.get('https://zh.wikipedia.org/wiki/{}'.format(question))
    soup = BeautifulSoup(r.content, 'html.parser')
    article = soup.select_one('.mw-parser-output p').text
    return article

def speak(sentence):
    mixer.init()
    with tempfile.NamedTemporaryFile(delete=True) as fp:
        tts = gTTS(text=sentence, lang='zh-TW')
        tts.save("{}.mp3".format(fp.name))
        mixer.music.load('{}.mp3'.format(fp.name))
        mixer.music.play()
    
speak(get_wiki_summary(listen()))
```

