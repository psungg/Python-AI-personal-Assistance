# Python-AI-personal-Assistance

**SpeechRecognition** provides as many popular APIs, including Google Web Speech API

The SpeechRecognition Library allows us to use microphone (real-time) and audio file

**To install the SpeechRecognition Library**

    pip install SpeechRecognition
    
**To import**

    import speech_recognition as sr
    
**To use microphone as source for speech recognition**

    pip install PyAudio

**To perform speech recognition: sr.Recoginizer()**

    recognizerObject = sr.Recognizer()

**To create a Microphone object as a input source for speech recognition: sr.Microphone()**

    with sr.Microphone() as source:

**To capture the Microphone input: recognizerObject.listen(MicrophoneObject)**

    voice = recognizerObject.listen(source)
    
timeout: the maximum number of seconds that this will wait for a phrase to start before giving up and throwing an speech_recognition.WaitTimeoutError

    voice = recognizerObject.listen(source, timeout = 5)

**API to use**

**Google Web Speech API**

    recognizerObject.recognize_google(MicrophoneObject)
    
**IBM Speech to Text API**

    recognizerObject.recognize_ibm(MicrophoneObject)
    
**Microsoft Bing Speech API**

    recognizerObject.recognize_bing(MicrophoneObject)
    
**Google Cloud Speech API** (google cloud speech package is required)

    recognizerObject.recognize_google_cloud(MicrophoneObject)
    
**CMU Sphinx API** (PocketSphinx is required)

    recognizerObject.recognize_sphinx(MicrophoneObject)
    
    statement = recoginzer.Object.recognize_google(voice)

**Webbrowser Module**

**To use the webbrowser module**

    import webbrowser
    
**To open URL in a new window of the default web browser**

    webbrowser.open_new("URL")
    
**To open URL in a new tab of the default web browser**

    webbrowser.open_new_tab("URL")

**datetime Module**

**To use the datetime module**

    import datetime
    
**To get a combination of a current date and time**

    Attributes: year, month, day, hour, minute, second, microsecond
    
    datetime.datetime.now() #for current date and time  
    datetime.datetime.now().year #for current year  
    datetime.datetime.now().month #for current month  
    datetime.datetime.now().day #for current date  
    datetime.datetime.now().hour #for current hour  
    
    eg. hour = datetime.datetime.now().hour
    
**strtime() method** is used for converting the datetime to string that represents date and time according to the format  

    datetime.datetime.now().strtime("format")  
    
    eg. strTime = datetime.datetime.now().strtime("%H: %M: %S")  
    
    **Example of strtime Format**  
    %A     Full Weekday Name    Sunday,Monday,...  
    %B     Full Month Name      January,Febuary,...  
    %Y     Year                 2022,2023,...  
    %H     Hour (24 hrs)        00,01,...,23  
    %M     Minute               00,01,...,59  
    %S     Second               00,01,...,59  

**time module**

**To use time module**

    import time
    
**sleep() method** is used to suspend the processing thread (add some delay) for a given number of seconds

    time.sleep(second)
    
    eg. time.sleep(3) #pause the processing thread for 3 seconds

## AI Personal Assistant (Speech Recognition)

1. Create Recognizer object for speech recognition
2. Create text to speech object for the AI Personal Assistant to reply the user
3. Make the AI Personal Assistant greet the user
4. Make the AI Personal Assistant ready to take command  
    a. Create Microphone object to get the input voice  
    b. Wait and listen for the input for 5 seconds  
    c. Recognize the input speech  
    d. Compare the recognized speech to the known commands  
    e. Perform according to the command  
    f. If cannot catch the command, ask the user to repeat it again  
5. Prepare the known commands and response the user via speech, eg:  
    a. Open youtube in web browser  
    b. Open google in web browser  
    c. Tell for the current time  
    d. Answer the question "How are you?"  
    e. Stop the AI Personal Assistant  
6. Wait for at least 3 seconds before continue to the new command and keep looping until the user asks the AI Personal Assistant to stop

```
pip install SpeechRecognition
```

```
pip install PyAudio
```

```python
import speech_recognition as sr
import pyttsx3
import webbrowser
import datetime
import time

def greeting():
    hour = datetime.datetime.now().hour
    if hour >= 0 and hour < 12:
        speak("Hello, Good morning")
        print("Hello, Good morning")
    elif hour >= 12 and hour < 15:
        speak("Hello, Good afternoon")
        print("Hello, Good afternoon")
    else:
        speak("Hello, Good evening")
        print("Hello, Good morning")
        
def speak(text):
    engine.say(text)
    engine.runAndWait()
    
def takeCommand():
    with sr.Microphone() as source:
        recognizerObject.adjust_for_ambient_noise(source)
        print("Listening...")
        voice = recognizerObject.listen(source, timeout = 5)
        try:
            statement = recognizerObject.recognize_google(voice)
            print("Got it")
            print("User said:"+statement)
        except Exception as e:
            print("Pardon me, please say it again")
            speak("Pardon me, please say it again")
            return "None"
        return statement

recognizerObject = sr.Recognizer()
engine = pyttsx3.init()

print("Loading AI Personal Assistant - Javis")
speak("Loading your AI Personal Assistant - Javis")

greeting()

while True:
    print("I'm ready to service. How can I help you?")
    speak("I'm ready to service. How can I help you?")
    
    statement = takeCommand().lower()
    
    if statement == "None":
        continue
    if "Goodbye" in statement or "stop" in statement or "bye" in statement:
        speak("Your AI Personal Assistance Javis is shutting down, goodbye")
        print("Your AI Personal Assistance Javis is shutting down, goodbye")
        break
        
    if "youtube" in statement:
        webbrowser.open_new_tab("https://www.youtube.com")
        speak("Opening Youtube")
        print("Opening Youtube")
        
    if "google" in statement:
        webbrowser.open_new_tab("https://www.google.com")
        speak("Opening Google")
        print("Opening Google")
        
    if "time" in statement:
        strTime = datetime.datetime.now().strftime("%H:%M:%S")
        speak("The time is"+strTime)
        print("The time is "+strTime)
        
    elif "how are you" in statement:
        speak("I'm doing great. I wish I can serve you best as your AI Personal Assistant")
    time.sleep(3)
```
## Result

![Fig01](https://github.com/psungg/Python-AI-personal-Assistance/blob/main/Images/Fig01.png)
