# ai-chatbot 
import speech_recognition as sp
import pyttsx3
import webbrowser
import os
import subprocess
import sys
import datetime

def say(text):
    engine = pyttsx3.init()
    engine.say(text)
    engine.runAndWait()

def takecommand(): 
    r = sp.Recognizer()
    with sp.Microphone() as source:
        r.pause_threshold = 1.0
        print("Listening...")
        audio = r.listen(source)
        try:
            query = r.recognize_google(audio, language="en-in")
            print(f'User said: {query}')
            return query.lower()
        except Exception as e:
            print("Sorry, I did not catch that.")
            return "None"

say("hello, I am your councellor jarvis , how can i help u")
while True:
    text = takecommand()
    
    if text == "stop listening me":
        say("Goodbye!")
        break
    
    # Websites to open
    sites = [["youtube", "https://www.youtube.com"], 
             ["wikipedia", "https://www.wikipedia.org"], 
             ["facebook", "https://www.facebook.com"],
             ["instagram", "https://www.instagram.com"],
             ["NMIET website","https://www.nmiet.edu.in/"]]
    
    for site in sites:
        if site[0] in text:
            say(f"Opening {site[0]}...")
            webbrowser.open(site[1])
            break
    
    # Songs to play
    songs = [
        ["unstoppable", "https://www.youtube.com/watch?v=oS07d8Gr4tw"], 
        ["agar tum sath ho", r"C:\Users\haris\Music\Agar Tum Saath Ho (1).mp3"], 
        ["sawan aaya hain", r"C:\Users\haris\Music\01_-_Sawan_Aaya_Hai(wapking.cc).mp3"],
        ["believer", "https://youtube.com/watch?v=W0DM5lcj6mw"],
        ["youtube shorts", "https://www.youtube.com/shorts"],
        ["vatana", "https://www.youtube.com/watch?v=uMs81fRenGw"]
    ]
    
    if text.startswith("play"):
        for song in songs:
            if song[0] in text:
                say(f"Playing {song[0]}...")
                if song[1].startswith("http"):
                    webbrowser.open(song[1])
                else:
                    if sys.platform == "win32":
                        os.startfile(song[1])
                    else:
                        opener = "open" if sys.platform == "darwin" else "xdg-open"
                        subprocess.call([opener, song[1]])
                break
        else:
            say("Song not found.")
    
    # Time command
    if "what is time now" in text:
        strfTime = datetime.datetime.now().strftime("%I:%M %p")
        say(f"Sir, the time is {strfTime}")
    
    # Nutan College Information Dataset
    colleges = [
        {
            "name": "Nutan College",
            "fees_structure": {
                "B.E": "INR 1.20 Lakhs per year",
                "Diploma": "INR 60,000 per year"
            },
            "cutoff": {
                "Computer Engineering": "90 percentile in MHT-CET or JEE",
                "Mechanical Engineering": "80 percentile in MHT-CET or JEE"
            },
            "website": "https://www.nutancollege.edu.in",
            "status": "Affiliated with Savitribai Phule Pune University, AICTE Approved",
            "address": "Talegaon Dabhade, Pune, Maharashtra",
            "formation_year": 1999,
            "reviews": "The college is known for its strong emphasis on technical education and has a good reputation among students and alumni.",
            "additional_info": "Nutan College offers various undergraduate and diploma courses in engineering and is recognized for its infrastructure and faculty."
        }
    ]

    nutan_info = colleges[0]  # Fetch the Nutan College dataset

    # College Fee Structure
    if "nutan college fees" in text:
        say(f"The fees for B.E. is {nutan_info['fees_structure']['B.E']} per year.")
        say(f"The fees for Diploma is {nutan_info['fees_structure']['Diploma']} per year.")

    # College Cutoff
    elif "nutan college cut off" in text:
        say(f"The cutoff for Computer Engineering is {nutan_info['cutoff']['Computer Engineering']}.")
        say(f"The cutoff for Mechanical Engineering is {nutan_info['cutoff']['Mechanical Engineering']}.")

    # College Website
    elif "nutan college website" in text:
        say(f"The official website for Nutan College is {nutan_info['website']}.")
        webbrowser.open(nutan_info['website'])

    # College Status
    elif "nutan college status" in text:
        say(f"Nutan College is {nutan_info['status']}.")

    # College Address
    elif "nutan college address" in text:
        say(f"The address of Nutan College is {nutan_info['address']}.")

    # College Formation Year
    elif "nutan college formation year" in text:
        say(f"Nutan College was formed in {nutan_info['formation_year']}.")

    # College Reviews
    elif "nutan college reviews" in text:
        say(f"Reviews about the college: {nutan_info['reviews']}")

    # Additional Information
    elif "give nutan college information" in text or "nutan college info" in text:
        say(f"Additional information about the college: {nutan_info['additional_info']}")

    else:
        if text != "None":
            
            say(text)
