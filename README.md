# text_extract_with_textract
Text extraction with Python Textract

Installing textract

>>!apt-get install python-dev libxml2-dev libxslt1-dev antiword unrtf poppler-utils pstotext tesseract-ocr flac ffmpeg lame libmad0 libsox-fmt-mp3 sox libjpeg-dev swig libpulse-dev
>>
>>!pip install textract

All other libraries we are using are on the latest release

We just need three libraries to execute the task

>>from google.colab.patches import cv2_imshow
>>
>>import cv2
>>
>>import textract

We first read the image with cv2.imread() and find the largest controur to crop the visiting card along its edges.
Steps:
1) Rescaling the image: We enlarge the image. Any type of smoothning before edge detection tends to give decent result for edge detection
2) Making it grayscale
3) Edge detection with canny
4) Closing function (A morphological function where dilation is followed by erosion)
5) Finding contour
6) cropping through the extreme contour

Processing the cropped image:
1) Grayscaling the cropped image
2) OTSU binary thresholding
3) Saving the obtained binary image with cv2.imwrite()

Extraction of text with Python Textract
Since, the text after processing from Textract comes in binary format, We process the text,

>>text=text[1:]
>>
>>text = ''.join(text.split("'"))
>>
>>text = ' '.join(text.split("\\n"))
>>
>>text = ''.join(text.split("\\x"))

This removed unnecessary string and unicodes from the text.

Sample output:
Input image:
![medakit-ltd-LmI4nW2PNcY-unsplash](https://user-images.githubusercontent.com/38774802/115117505-880aa880-9fbc-11eb-924a-819d6e3d7669.jpg)

Cropped image after contour detection:
![cropped](https://user-images.githubusercontent.com/38774802/115117515-948f0100-9fbc-11eb-9f87-a55075f99026.png)

Binary conversion:
![letsee](https://user-images.githubusercontent.com/38774802/115117523-a07ac300-9fbc-11eb-86d8-e9c32deb1715.PNG)

Extracted text:
   a: Medakit           COVID-19 RAPID TEST  BECAUSE YOUR LIFE MATTERS  RESULTS IN 15 MINUTES 0c


Image credit: 
Photo by <a href="https://unsplash.com/@medakit?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Medakit Ltd</a> on <a href="https://unsplash.com/s/photos/visiting-card?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Unsplash</a>
  
