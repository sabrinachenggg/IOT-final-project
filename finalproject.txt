import speech_recognition as sr
from omxplayer.player import OMXPlayer
from pathlib import Path
from time import sleep
import time
import contextlib
with contextlib.redirect_stdout(None):
    import pygame

r=sr.Recognizer()                         #定義speech_recognition裡Recognizer()的名字
with sr.Microphone() as source:                   #使用麥克風監聽取得sourse(監聽完成的音檔)

    def listen():                   #持續監聽的方法
        with sr.Microphone() as source:
            print("please wait")
            r.adjust_for_ambient_noise(source, duration=5)   #調整麥克風噪音 並監聽五秒
            print("Say something!")
            audio=r.listen(source)                          #把監聽到的音訊放入audio當中
            try:
		print("Google Speech Recognition thinks you said:")
                word=r.recognize_google(audio, language="zh-TW")      #用Google Speech Recognition把音檔轉成文字
                print(word)
                return word                    #回傳文字
            except sr.UnknownValueError:                            #除錯_如果沒有收到音訊
                print("Google Speech Recognition could not understand audio")
            except sr.RequestError as e:                             #除錯_如果無法辨識音訊
		print("No response from Google Speech Recognition service: {0}".format(e))

    print("Please wait. Calibrating microphone...")
    r.adjust_for_ambient_noise(source, duration=5)
    print("Say something!")
    audio=r.listen(source)

    try:
        print("Google Speech Recognition thinks you said:")
        word=r.recognize_google(audio, language="zh-TW")
        print(word)
        while word!="Google":
            if word=="音樂":                                        #播放音樂
                pygame.mixer.init()
                pygame.mixer.music.load("/home/sabrina/webapp/PeerPressure.m$
                pygame.mixer.music.play(1,0)
            elif word=="考試":                                         #暫停
				pygame.mixer.music.pause()
            elif word=="聽話":                                       #繼續播放
                pygame.mixer.music.unpause()
            word=listen()                                                #呼叫監聽方法
        pygame.mixer.music.stop()                                        #若聽到goole則跳出迴圈並停止播放音樂

    except sr.UnknownValueError:
        print("Google Speech Recognition could not understand audio")
    except sr.RequestError as e:
        print("No response from Google Speech Recognition service: {0}".form$


