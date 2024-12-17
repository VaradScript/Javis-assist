import speech_recognition as sr
import pyttsx3

# Initialize speech recognition and text-to-speech engines
recognizer = sr.Recognizer()
engine = pyttsx3.init()

def speak(text):
    """
    Speaks the given text using the text-to-speech engine.
    """
    engine.say(text)
    engine.runAndWait()

def listen():
    """
    Listens for user input using speech recognition.
    """
    try:
        with sr.Microphone() as source:
            print("Listening...")
            audio = recognizer.listen(source)
        try:
            text = recognizer.recognize_google(audio)
            print(f"You said: {text}")
            return text
        except sr.UnknownValueError:
            print("Could not understand audio")
        except sr.RequestError as e:
            print(f"Could not request results from Google Speech Recognition service; {e}")
    except Exception as e:
        print(f"An error occurred: {e}")

if __name__ == "__main__":
    while True:
        user_input = listen()
        if user_input:
            # Process user input and perform actions
            if "hello" in user_input:
                speak("Hello, how can I assist you today?")
            elif "goodbye" in user_input:
                speak("Goodbye!")
                break
            else:
                speak("I'm still learning. Try asking me something else.")
