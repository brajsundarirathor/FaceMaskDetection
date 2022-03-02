# FaceMaskDetection


import cv2
import matplotlib.pyplot as plt
import numpy as np
img = cv2.imread(r'C:\Users\brajs\Desktop\braj-min.jpg')
plt.imshow(img)
while True:
    cv2.imshow('result',img)
    if cv2.waitKey(2) == 27:
        break
cv2.destroyAllWindows()
haar_data = cv2.CascadeClassifier('faceData.xml')
haar_data.detectMultiScale(img)
while True:
    faces = haar_data.detectMultiScale(img)
    for x,y,w,h in faces:
        cv2.rectangle(img,(x,y),(w+x, h+y), (0,255,0),2)
    cv2.imshow('result',img)
    if cv2.waitKey(2) == 27:
        break
cv2.destroyAllWindows()

capture = cv2.VideoCapture(0)
while True:
    flag, img = capture.read()
    if flag:
        faces = haar_data.detectMultiScale(img)
        for x,y,w,h in faces:
            cv2.rectangle(img,(x,y),(w+x, h+y), (0,255,0),2)
        cv2.imshow('result',img)
        if cv2.waitKey(2) == 27:
            break
capture.release()
cv2.destroyAllWindows()

capture = cv2.VideoCapture(0)
data = []
while True:
    flag, img = capture.read()
    if flag:
        faces = haar_data.detectMultiScale(img)
        for x,y,w,h in faces:
            cv2.rectangle(img,(x,y),(w+x, h+y), (0,255,0),2)
            face = img[y:y+h, x:x+w,:]
            face = cv2.resize(face, (50,50))
            print(len(data))
            if len(data) <400:
                data.append(face)
        cv2.imshow('result',img)
        if cv2.waitKey(2) == 27 or len(data) >= 200 :   #  ASCII value of Escape key is 27
            break
capture.release()
cv2.destroyAllWindows()
