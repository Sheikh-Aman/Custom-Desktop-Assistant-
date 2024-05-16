# Custom-Desktop-Assistant-

import speech_recognition as sr
import os
import webbrowser
import datetime


# assistant output function

def say(text):
    os.system(f'say "{text}"')

    
# user input function

def takeCommand():
    r = sr.Recognizer()
    with sr.Microphone() as source:
        audio = r.listen(source)
        try:
            print("Recognizing...")
            query = r.recognize_google(audio, language="en-in")
            print(f"User said: {query}")
            return query
        except Exception as e:
            return "Some Error Occurred. Sorry from Ginger !"

if __name__ == '__main__':
    print('Welcome to Ginger A.I')
    say(" Ginger A.I")
    while True:
        print("Listening...")
        query = takeCommand()

        actions = {

            #conversations with assistance
            "What is the time": lambda: say(f"The time is {datetime.datetime.now().strftime('%H:%M:%S')}"),
            "how are you": lambda: say("I am fine, thank you. How about you, sir"),
            "I am doing well": lambda: say("that's great, sir"),
            "I am good": lambda: say("that's great, sir"),
            "I am fine": lambda: say("that's great, sir"),
            "what is your name": lambda: say("I am Ginger, your assistance sir"),

            #websites
            "open google": lambda: webbrowser.open("https://www.google.com"),
            "open youtube": lambda: webbrowser.open("https://www.youtube.com"),
            "open wikipedia": lambda: webbrowser.open("https://www.wikipedia.com"),
            "open instagram": lambda: webbrowser.open("https://www.instagram.com"),
            "open facebook": lambda: webbrowser.open("https://www.facebook.com"),
            "open linkedin": lambda: webbrowser.open("https://www.linkedin.com"),
            "open twitter": lambda: webbrowser.open("https://www.twitter.com"),
            "open jetbrains": lambda: webbrowser.open("https://www.jetbrains.com"),

            #application
            "open calendar": lambda: os.system("open /System/Applications/Calendar.app"),
            "open music": lambda: os.system("open /System/Applications/Music.app"),
            "open weather": lambda: os.system("open /System/Applications/Weather.app"),
            "open facetime": lambda: os.system("open /System/Applications/FaceTime.app"),
            "open maps": lambda: os.system("open /System/Applications/Maps.app"),
            "open chrome": lambda: os.system("open /Applications/Google Chrome.app"),
            "open clock": lambda: os.system("open /System/Applications/Clock.app"),
            "open app store": lambda: os.system("open /System/Applications/App Store.app"),
            "open whatsapp": lambda: os.system("open /Applications/WhatsApp.app"),
            "open safari": lambda: os.system("open /System/Volumes/Preboot/Cryptexes/App/System/Applications/Safari.app"),
            "open calculator": lambda: os.system("open /System/Applications/Calculator.app"),

            "ginger quit": exit,
        }


        for trigger, action in actions.items():
            if trigger.lower() in query.lower():
                action()
                break
        else:
            print("Chatting...")
            say(query)
