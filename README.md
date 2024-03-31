# Healthy-plankton
#The problem: Baikal has been monitored for more than 75 years, all these years, the analysis of samples is carried out manually. This process is time-consuming and must be performed by highly qualified specialists.
Solution: Development of an object recognition system to simplify environmental monitoring of Lake Baikal.
import cv2

cam = cv2.VideoCapture(0)
hog = cv2.HOGDescriptor()
hog.setSVMDetector(cv2.HOGDescriptor_getDefaultPeopleDetector())
while True:
    ret, frame = cam.read()
    frame = cv2.resize(frame, (400, 300))
    cv2.imshow('Frame', frame)
    rects, weights = hog.detectMultiScale(frame, scale=1, winStride=(2, 2))
    for (x, y, w, h) in rects:
        cv2.rectangle(frame, (x, y), (x + w, y + h), (0, 0, 250), 2)
        cv2.imshow('Frame', frame)
        if cv2.waitKey(1) == ord('q'):
            break
            cv2.destroyWindow()
            cam.release()
