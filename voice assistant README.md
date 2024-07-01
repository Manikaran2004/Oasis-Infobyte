# importing speech recognition package from google api
import speech_recognition as sr 
from gtts import gTTS # google text to speech
import os # to save/open files
import wolframalpha # to calculate strings into formula
from selenium import webdriver # to control browser operations
num = 1
def assistant_speaks(output):
	global num
	# num to rename every audio file 
	# with different name to remove ambiguity
	num += 1
	print("Person : ", output)
	toSpeak = gTTS(text = output, lang ='en', slow = False)
	# saving the audio file given by google text to speech
	#file = str(num)+".mp3 
	toSpeak.save(file)
	# playsound package is used to play the same file.
	playsound.playsound(file, True) 
	os.remove(file)
def process_text(input):
	try:
		if 'search' in input or 'play' in input:
			# a basic web crawler using selenium
			search_web(input)
			return
		elif "who is the prime minister of india" in input or "who is the pm of india" in input:
			speak = "The prime minister of india is Narendra Modi"
			assistant_speaks(speak)
			return
		elif "what is the national bird of india" in input:
			speak = """peacock is the national bird of india"""
			assistant_speaks(speak)
			return
   elif "How many days are there in a week" in input:
     speak = "There are 7 days in a week"
     assistant_speaks(speak)
     return
  elif "who is the president of india" in input:
     speak = "Droupadi Murmu is the president of india"
     assistant_speak(speak)
     return
		elif "calculate" in input.lower():
			# write your wolframalpha app_id here
			app_id = "WOLFRAMALPHA_APP_ID" 
			client = wolframalpha.Client(app_id)
			indx = input.lower().split().index('calculate')
			query = input.split()[indx + 1:]
			res = client.query(' '.join(query))
			answer = next(res.results).text
			assistant_speaks("The answer is " + answer)
			return
		elif 'open' in input:
			# another function to open 
			# different application available
			open_application(input.lower()) 
			return
		else:
			assistant_speaks("I can search the web for you, Do you want to continue?")
			ans = get_audio()
			if 'yes' in str(ans) or 'yeah' in str(ans):
				search_web(input)
			else:
				return
	except :
		assistant_speaks("I don't understand, I can search the web for you, Do you want to continue?")
		ans = get_audio()
		if 'yes' in str(ans) or 'yeah' in str(ans):
			search_web(input)
def search_web(input):
	driver = webdriver.Firefox()
	driver.implicitly_wait(1)
	driver.maximize_window()
	if 'youtube' in input.lower():
		assistant_speaks("Opening in youtube")
		indx = input.lower().split().index('youtube')
		query = input.split()[indx + 1:]
		driver.get("http://www.youtube.com/results?search_query =" + '+'.join(query))
		return
	else:
		if 'google' in input:
			indx = input.lower().split().index('google')
			query = input.split()[indx + 1:]
			driver.get("https://www.google.com/search?q =" + '+'.join(query))
		elif 'weather report' in input:
			indx = input.lower().split().index('google')
			query = input.split()[indx + 1:]
			driver.get("https://www.accuweather.com/search?q =" + '+'.join(query))
		else:
			driver.get("https://www.google.com/search?q =" + '+'.join(input.split()))
		return
# function used to open application
# present inside the system.
def open_application(input):
	if "chrome" in input:
		assistant_speaks("Google Chrome")
		os.startfile('C:\Program Files (x86)\Google\Chrome\Application\chrome.exe')
		return
	elif "weather report" in input or "weather" in input:
		assistant_speaks("Opening weather report")
		os.startfile('C:\Program Files\accuweather.com')
		return
	elif "control smart home" in input:
		assistant_speaks("Opening smart home")
		os.startfile('C:\ProgramData\www.smarthome.com')
		return
	elif "email" in input or "gmail" in input:
		assistant_speaks("Opening gmail")
		os.startfile('C:\ProgramData\mail.google.com')
		return
	else:
		assistant_speaks("Application not available")
		return

