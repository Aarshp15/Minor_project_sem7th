# Minor_project_sem7th
import pyttsx3
import speech_recognition as sr
import datetime
import wikipedia
import webbrowser
import os
import requests



engine = pyttsx3.init()
voices = engine.getProperty('voices')
#print(voices[0].id) 
engine.setProperty('voice', voices[0].id)


def speak(audio):
    engine.say(audio)
    engine.runAndWait()

def wishme():
    hour = int(datetime.datetime.now().hour)
    if hour>=0 and hour<12:
        speak("Good Morning!")

    elif hour>=12 and hour<18:
        speak("Good Afternoon!")

    else:
        speak("Good Evening!")

    speak("I am Jarvis sir. Please tell me how may I help you")    
                
def takecommand():
    #It takes microphone input from the user and returns string output

    r = sr.Recognizer()
    with sr.Microphone() as source:
        print("listening...")
        r.pause_threshold = 1
        audio = r.listen(source)

    try:
        print("Recognizing...")
        query = r.recognize_google(audio,language='en-in')
        print(f"User said:{query}\n")

    except Exception as e:
        #print(e)
        print("say that again please...")
        return "None"
    return query        



if __name__ == "__main__":
    wishme()
    while True:
        query = takecommand().lower()

        #logic for executing tasks based on query
        if 'wikipedia' in query:
            speak('Searching wikipedia...')
            query = query.replace("wikipedia","")
            results = wikipedia.summary(query, sentences=4)
            speak("According to wikipedia")
            print(results)
            speak(results)

        elif 'open youtube' in query:
            webbrowser.open("youtube.com")

        elif 'open google' in query:
            webbrowser.open("google.com")    

        elif 'open coursera' in query:
            webbrowser.open("coursera.com")    

        elif 'open greeks for greeks' in query:
            webbrowser.open("greeks for greeks.com")    

        elif 'open spotify' in query:
            webbrowser.open("spotify.com")  

        

        elif 'play music' in query:
            music_dir = "D:\Aarsh_music"
            songs = os.listdir(music_dir)
            print(songs)
            os.startfile(os.path.join(music_dir,songs[0]))


        elif 'the time' in query:
            strTime = datetime.datetime.now().strftime("%H:%M:%S:")
            speak(f"sir, the time is {strTime} ")   


        elif 'open code' in query:
            codePath = "C:\\Users\\mittp\\AppData\\Local\\Programs\\Microsoft VS Code\\Code.exe"
            os.startfile(codePath)


def get_weather(api_key, city):
    base_url = "http://api.openweathermap.org/data/2.5/weather"
    params = {
        "q": city,
        "appid": api_key,
        "units": "metric", #use "imperial" for Fahrenheit
    }

    response = requests.get(base_url, params=params)
    data = response.json()


    #Extract relevant weather information
    temperature = data["main"]["temp"]
    weather_description = data["weather"][0]["description"]

    return temperature, humidity, weather_description


#Example usage
api_key = "edcc3689604ad995917d0dff6c4cad2e"
city = "New York"
temperature, humidity, weather_description = get_weather(api_key, city)
print(f"The current temperature in {city} is {temperature}°C with a humidity of {humidity}%.")
print(f"The weather is {weather_description}.")


#Auto genrate mail by AI Desktop Assistant


import speech_recognition as sr
import yagmail

recognizer=sr.Recognizer
with sr.Microphone() as source:
    print('Clearing background noise...')
    source = sr.AudioFile('your_audio_file.wav')
    recognizer.adjust_for_ambient_noise(source,duration=1)
    print("Waiting for your message...")
    recordedaudio=recognizer.listen(source)
    print('Done recording..!')
try:
    print('Printing the message...')
    text=recognizer.recognize_google(recordedaudio,language='en-US')

    print('Your message:{}'.formet(text))

except Exception as ex:
    print(ex)

#Automate mails:

reciever='arshpanchal099@gmail.com'
message=text
sender=yagmail.SMTP('fins.ashp47@gmail.com')
sender.send(to=reciever,subject='This is an automated mail',contents=message)

          


         

    
    
