# Extracting-frames-from-Webcam

import cv2
import os
import time 
capture = cv2.VideoCapture(0)
frame_interval = 3  # in seconds
previous_time = time.time()
frame_number = 0
output_directory = 'output_frames'
os.makedirs(output_directory, exist_ok=True)

while True:
    ret, frame = capture.read()

    if not ret:
        break

    current_time = time.time()
    elapsed_time = current_time - previous_time

    if elapsed_time >= frame_interval:
        frame_filename = os.path.join(output_directory, f'frame_{frame_number:04d}.jpg')
        cv2.imwrite(frame_filename, frame)
       
        previous_time = current_time

        cv2.imshow('Frame', frame)
    if cv2.waitKey(1) & 0xFF == ord('q'):
        break

    frame_number += 1
capture.release()
cv2.destroyAllWindows()
print(f'Frames extracted and saved to {output_directory}')
       

