# capture-video-using-laptop-pc-webcam or  play download video with audio... 

import cv2
import numpy as np
from ffpyplayer.player import MediaPlayer   #use for audio in video
#cap = cv2.VideoCapture(0)
cap = cv2.VideoCapture('video.mkv')

Player =MediaPlayer('video.mkv')#sourcepath
fourcc = cv2.VideoWriter_fourcc(*'xvid')
out = cv2.VideoWriter('navneetu',fourcc,20.0,(640,480))

def make_1080p():
    cap.set(3,1280)
    cap.set(4,1080)
def change_res(width,height):
 cap.set(3,width)
 cap.set(4,height)

def rescale_frame(frame,percent=75):
    scale_percent = 75
    width = int(frame.shape[1] * scale_percent/100)
    height = int(frame.shape[0] * scale_percent /100)
    dim = (width,height)
    return cv2.resize(frame,dim,interpolation =cv2.INTER_AREA)
                 
make_1080p()


while True:
    ret,frame =cap.read() #read image
    frame = rescale_frame(frame,percent=30) # Rescale frame
    frame2 = rescale_frame(frame,percent=180)
    Audio_frame, val = Player.get_frame()#read audio
    b = cv2.resize(frame,(1280,720),fx=0,fy=0, interpolation = cv2.INTER_CUBIC)
    out.write(b)
    
    #cv2.imshow("Frame",frame) # display frame/image
    #cv2.imshow("video",frame)
    #cv2.imshow('frame',frame)
    cv2.imshow('frame',frame2)


    key = cv2.waitKey(1) #wait till key press
    if key == ord("q"):   #exit loop on 'q' key press
        break

cap.release()  #release Video capture object
cv2.destroyAllWindows() #destroy all from windows
    
