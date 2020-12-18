import pyttsx3
import speech_recognition as sr
import datetime
import wikipedia
import webbrowser
import os
import random

engine = pyttsx3.init('sapi5')
voices = engine.getProperty('voices')
engine.setProperty('voice', voices)


def speak(audio):
    engine.say(audio)
    engine.runAndWait()


def welcome():
    hour = int(datetime.datetime.now().hour)
    if 0 <= hour <= 12:
        speak("hii , good morning sir...")
    elif 12 < hour < 18:
        speak("hii , good afternoon sir...")
    else:
        speak("hii , good evening sir...")
    speak("I am rocky . i am your personal assistant . how may i help you...")


def comm():
    r = sr.Recognizer()
    with sr.Microphone() as source:
        print("listening...")
        r.pause_threshold = 0.8
        audio = r.listen(source)

    try:
        print("Recognizing...")
        query = r.recognize_google(audio, language='en-in')
        print(f"{query}\n")
        speak("you search that" + query)
    except Exception as e:
        print(e)
        speak("sorry sir , i cannot able to recognize what you speak...please try again..")
        return "None"
    return query


if __name__ == "__main__":

    welcome()
    while True:
        query = comm().lower()
        if 'wikipedia' in query:
            print('Searching Wikipedia...')
            query = query.replace("wikipedia", "")
            results = wikipedia.summary(query, sentences=3)
            speak("According to your search")
            print(results)
            speak(results)

        elif 'youtube' in query:
            webbrowser.open("youtube.com")
            exit()

        elif 'google' in query:
            webbrowser.open("google.com")
            exit()

        elif 'vs code' in query:
            codepath = "C:\\Program Files\\Microsoft VS Code\\Code.exe"
            os.startfile(codepath)
            exit()

        elif 'pycharm' in query:
            codepath = "C:\\Program Files\\JetBrains\\PyCharm Community Edition 2020.3\\bin\\pycharm64.exe"
            os.startfile(codepath)
            exit()

        elif 'word' in query:
            codepath = "C:\\Program Files\\Microsoft Office\\root\\Office16\\WINWORD.EXE"
            os.startfile(codepath)
            exit()

        elif 'atom' in query:
            codepath = "C:\\Users\\DELL\\AppData\\Local\\atom\\atom.exe"
            os.startfile(codepath)
            exit()

        elif 'onenote' in query:
            codepath = "C:\\Program Files\\Microsoft Office\\root\\Office16\\ONENOTE.EXE"
            os.startfile(codepath)
            exit()

        elif 'edge' in query:
            codepath = "C:\\Program Files (x86)\\Microsoft\\Edge\\Application\\msedge.exe"
            os.startfile(codepath)
            exit()

        elif 'play some music' in query:
            music_dir = "D:\\songsforall"
            songs = os.listdir(music_dir)
            os.startfile(os.path.join(music_dir, songs[0]))
            exit()

