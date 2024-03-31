# Healthy-plankton
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
