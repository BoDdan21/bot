from gtts import gTTS
import random
import time
import playsound
import speech_recognition as sr

def listen_command():
    # obtain audio from the microphone
    r = sr.Recognizer()
    with sr.Microphone() as source:
        print("скажите вашу команду!")
        audio = r.listen(source)

    # recognize speech using Google Speech Recognition
    try:
        our_speech = r.recognize_google(audio, language="ru")
        print("вы сказали: "+our_speech)
        return r.recognize_google(audio)
    except sr.UnknownValueError:
        return "ошибка"
    except sr.RequestError:
        return "ошибка"

    return input("скажите вашу команду: ")

def do_this_command(massage):
    massage = massage.lower()
    if " Привет" in massage:
        say_massage("привет!")
    if " Как дела" in massage:
        say_massage("Хорошо!")
    elif " пока" in massage:
        say_massage("пока!")
        exit()
    else:
        say_massage("команда не распозвана")

def say_massage(massage):
    voice = gTTS(massage, lang="ru")
    file_voise_name = "_audio_"+str(time.time())+"_"+str(random.randint(0,100000))+".mp3"
    voice.save(file_voise_name)
    playsound.playsound(file_voise_name)
    print("пятница"+massage)


if __name__ == '__main__':
    while True:
        command = listen_command()
        do_this_command(command)
