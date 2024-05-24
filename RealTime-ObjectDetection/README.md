

## Introduction
 This repo contains object_detection.py, which can perform the following task -
 - Object detection from a live video frame, in any video file, or in an image
 - Counting the number of objects in a frame
 - Measuring the distance of an object using depth information
 - Inference on Multiple Camera feed at a time
 
For object detection, YOLO-V3 has been used, which can detect 80 different objects. Some of those are-
- person
- car
- bus
- stop sign
- bench
- dog
- bear
- backpack, and so on.

### User Instruction




To execute object_dection.py, you require Python version > 3.5 (depending on whether you are using GPU or not) and have to install the following libraries.

### Installation
``` python
    $ pip install -r requirements.txt
         or
    $ pip install opencv-python
    $ pip install numpy
    $ pip install pandas
    $ pip install matplotlib
    $ pip install Pillow
    $ pip install imutils
```
<hr>


```

```


After unzipping the project, there are two ways to run this. If you want to see your output in your browser, execute the "app.py" script or run "object_detection.py" to execute it locally.


If you want to run object detection and distance measurement on a video file, write the name of the video file to variable <b>id</b> in either "app.py" or "object_detection.py" or if you want to run it on your webcam just put 0 in <b>id</b>.




For multiple camera support, you need to add a few lines of codes as follows in app.py-

``` python
   def simulate(camera):
       while True:
           frame = camera.main()
           if frame != "":
               yield (b'--frame\r\n'
                   b'Content-Type: image/jpeg\r\n\r\n' + frame + b'\r\n\r\n')

   @app.route('/video_simulate')
   def video_simulate():
       id = 0
       return Response(gen(ObjectDetection(id)), mimetype='multipart/x-mixed-replace; boundary=frame')
```

Depending on how many feeds you need, add the two methods in "app.py" with different names and add a section in index.html.

``` html
<div class="column is-narrow">
        <div class="box" style="width: 500px;">
            <p class="title is-5">Camera - 01</p>
            <hr>
            <img id="bg" width=640px height=360px src="{{ url_for('video_simulate') }}">
            <hr>

        </div>
    </div>
    <hr>
```
