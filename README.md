#For Recognize Our Speech and convert it into text
from datetime import datetime

import speech_recognition as sr

#To Access Web Pages

import webbrowser

#To convert Text into audio

import pyttsx3

from openai import OpenAI

#This is for songs(Created By me)

import musiclibrary

#Giving names to the recognizer and converter

sensor = pyttsx3.init()


#Function for convert text to audio using ttsx

def speak(text):
    sensor.say(text)
    sensor.runAndWait()


#Function for making actions according to the commands we give
def processCommand(c):
    print(c)
    if "google" in c.lower():
        speak("opening google")
        webbrowser.open("https://google.com")
    elif "the time" in c.lower():
        hour=datetime.now().strftime("%H")
        min=datetime.now().strftime("%M")
        speak(f"time is {hour} ,{min}")
    elif "good job" in c.lower():
        speak("thank you")
    elif "who created you" in c.lower():
        speak("mister abhinay sir")
    elif "em chestunnav" in c.lower():
        speak("neekendhuku raa.")
    elif "youtube" in c.lower():
        speak("opening youtube")
        webbrowser.open("https://youtube.com")
    elif "linkedin" in c.lower():
        speak("opening linkedin")
        webbrowser.open("https://linkedin.com")
    elif "facebook" in c.lower():
        speak("opening facebook")
        webbrowser.open("https://facebook.com")
    elif "hotstar" in c.lower():
        speak("opening hotstar")
        webbrowser.open("https://www.hotstar.com/")
    elif c.lower().startswith("play"):
        song = c.lower().split(" ")[1]
        link = musiclibrary.music[song]
        webbrowser.open(link)
    else:
        OpenAI()


'''Main Part'''


def printCommand(c):
    print(c)

if _name_ == "_main_":
    #This is what it speaks at first
    speak("Hi. My name is alexa How can I help You")
    #loop for continues listening
    while True:
        try:
            #Activating Microphone to hear our commands
            with sr.Microphone() as source:
                print("Listening...")
                # For Listening
                audio = sr.Recognizer().listen(source)
            # Using google recognizer for less errors.
            word = sr.Recognizer().recognize_google(audio)
            print("recognising..")
            #Function to print the command
            printCommand(word)
            #Only do when we call it with name(papa)
            if "alexa" in word.lower():
                speak("Yes")
                #again Taking command
                with sr.Microphone() as source:
                    print("papa Activated...")
                    audio = sr.Recognizer().listen(source,timeout=5)
                command = sr.Recognizer().recognize_google(audio)
                processCommand(command)
        except Exception as e:
            print("I can't understand!")
