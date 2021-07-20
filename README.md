# Car-counter-using-opencv-python

First The Requirements are as follows:
  1. python version 3.7.8
  2. opencv python version 4.5.3.56

Now First importing opencv
  import cv2

Then i opend the video named video1.mp3

  cap = cv2.VideoCapture("video1.mp4")
  while True:
    ret, frame = cap.read()
    height, width, _ = frame.shape
    cv2.imshow("Frame", frame)
    # cv2.imshow("Mask", mask)

    key = cv2.waitKey(1)
    if key == 27:
        break

  cap.release()
  cv2.destroyAllWindows()
Then i put my name there
  cv2.putText(frame , "Aman Tripathi",(375,30),cv2.FONT_HERSHEY_COMPLEX_SMALL,1,(255,0,0),2)
Then creating an object detector
  object_detector = cv2.createBackgroundSubtractorMOG2(history=100, varThreshold=40)
 Then i created a maskfor detecting cars
  mask = object_detector.apply(frame)
  _, mask = cv2.threshold(mask, 254, 255, cv2.THRESH_BINARY)
  contours, _ = cv2.findContours(mask, cv2.RETR_TREE, cv2.CHAIN_APPROX_SIMPLE)
 
Then created a bounding box around the car
   detections = []
    for cnt in contours:
        # Calculate area and remove small elements
        area = cv2.contourArea(cnt)
        if area > 100:
            #cv2.drawContours(roi, [cnt], -1, (0, 255, 0), 2)
            x, y, w, h = cv2.boundingRect(cnt)
            
            detections.append([x, y, w, h])
            
Then i imported my tracker module that will track the cars and perticular id's for each car
  boxes_ids = tracker.update(detections)
    for box_id in boxes_ids:
        x, y, w, h, id = box_id
        cv2.putText(frame, str(id), (x, y - 15), cv2.FONT_HERSHEY_PLAIN, 2, (255, 0, 0), 2)
        cv2.rectangle(frame, (x, y), (x + w, y + h), (0, 255, 0), 3)

Then i counted all the id's
  cv2.putText(frame, str(id), (780, 30), cv2.FONT_HERSHEY_COMPLEX_SMALL, 1, (210, 20, 25), 2)
    
That's all
  
  
  
            
