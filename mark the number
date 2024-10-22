import cv2
import random
import cvzone
from cvzone.HandTrackingModule import HandDetector

cap = cv2.VideoCapture(0)
detector = HandDetector(detectionCon=0.8, maxHands=1)

current_number = random.randint(0, 5)
font = cv2.FONT_HERSHEY_SIMPLEX
success_message = "Correct!"
next_message = "Next number coming..."
text_color = (0, 255, 0)
wrong_message = "Try again!"
number_size = 5
num_detected = False
detected_number = None

def display_number(img, number):
    text = str(number)
    cv2.putText(img, text, (100, 200), font, number_size, text_color, thickness=3)

while True:
    success, img = cap.read()
    if not success:
        break
    hands, img = detector.findHands(img)

    display_number(img, current_number)
    if hands:
        fingers = detector.fingersUp(hands[0])
        detected_number = fingers.count(1)
        if detected_number == current_number:
            cv2.putText(img, success_message, (50, 400), font, 2, text_color, 3)
            num_detected = True
            cv2.putText(img, next_message, (50, 450), font, 1.5, (0, 0, 255), 2)
            cv2.imshow("Number Detection", img)
            cv2.waitKey(2000)
            current_number = random.randint(0, 5)
            num_detected = False
        else:
            cv2.putText(img, wrong_message, (50, 400), font, 2, (0, 0, 255), 3)
            
    cv2.imshow("Number Detection", img)
    
    if cv2.waitKey(1) & 0xFF == ord('q'):
        break
    
cap.release()
cv2.destroyAllWindows()
