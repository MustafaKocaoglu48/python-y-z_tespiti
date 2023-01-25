# python-yüz_tespiti
---
### Dışarıdan verilen bir videodaki insan yüzünü tespit eden program.
````
import cv2

face_cascade = cv2.CascadeClassifier("haarcascade_frontalface_default.xml")

capture = cv2.VideoCapture("1.mp4")

while True:
    ret, img = capture.read()
    if img is None:
        break
    gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)
    faces = face_cascade.detectMultiScale(gray, 1.3, 4)

    for (x, y, w, h) in faces:
        cv2.rectangle(img, (x, y), (x + w, y + h), (255, 0, 0), 4)
        roi_gray = gray[y:y + h, x:x + w]  # ilgilenilen bölge
        roi_color = img[y:y + h, x:x + w]
    cv2.imshow("detected", img)
    k = cv2.waitKey(1) & 0xFF
    if k == 27:
        break
# Döngüyü kırmak için 'q' tuşuna basın
    if cv2.waitKey(1) & 0xFF == ord('q'):
        break
capture.release()
cv2.destroyAllWindows()
````
