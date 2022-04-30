# Food Label Reader
This repository is the accumulation of all the work done in Computer vision course in Chulalongkorn University 2021.

## What we do
We decide to detecting Food nutrition label in food package by using traditional computer vision method, and read it with OCR model to keep it good use in the future.

## Our Method
### label detection
First, we convert the image into grayscale, use OTSU threshold to change into binary image and use cv2.Canny() as edge detection to detect the corner edge.
Next, we use cv2.findContours() and cv2.approxPolyDP() to find the largest contour areas (assume that is our Food label) and get the coordinate of 4 corners.
### Wrap perspective
After we got all four corner of Food label, we put it into list in order top-left, bottom-left, bottom-right, and top-right. Use cv2.getPerspectiveTransform() to get convert matrix and use cv2.WarpPerspective() to crop and wrap only Food label.
### Noise Removing
After we got the Food label, we use non local mean to remove some noise that may come with image.
### Read it by OCR model
We use OCR Model from [Readme : Thai Scene Text Reader (eikonnex.ai)](https://readme.eikonnex.ai/login/dashboard) which provide OCR Text reader API that can read English and Thai language with outstanding performance. After that, we use some Distance Matrix to prevent error from OCR model and put it in to Dataframe for future usage.

## How to run
1. Clone a repository
```
git clone https://github.com/ScrambledTamako/chula_cv_2022_term_project.git
```
2. Add API KEY\
2.1 Get API KEY from [Readme : Thai Scene Text Reader (eikonnex.ai) API](https://readme.eikonnex.ai/login/api_usage).\
2.2 Edit API KEY in read_label.py line 11.
3. Install require module and run the website in local.
```
cd read-label
pip install -r requirement.txt
streamlit run read_label.py 
```

## How to use
1. Click at Browse Files Button.

![Screen Shot 2565-04-30 at 13 18 10](https://user-images.githubusercontent.com/54425991/166094887-5b59159a-5e9e-4c9f-9439-20884cf53480.png)

2. The website will process image and dataframe then show the result as below.

![Screen Shot 2565-04-30 at 13 18 49](https://user-images.githubusercontent.com/54425991/166094899-c5ffbb3a-0141-4d7a-9e7f-6789abd25c07.png)
![Screen Shot 2565-04-30 at 13 18 53](https://user-images.githubusercontent.com/54425991/166094911-d0584a43-eb55-4fc0-bc23-ce739d222e02.png)

## Result
![Screen Shot 2565-04-30 at 13 22 59](https://user-images.githubusercontent.com/54425991/166095725-1dbecefb-dfe0-456f-8ed8-ba47fe9a1829.png)
![Screen Shot 2565-04-30 at 13 23 36](https://user-images.githubusercontent.com/54425991/166095730-44de1478-fc3a-45d3-a393-4fe55098a8b5.png)
![Screen Shot 2565-04-30 at 13 24 05](https://user-images.githubusercontent.com/54425991/166095736-f0b944d2-3f0e-41d0-b1f8-9270cb171456.png)
![Screen Shot 2565-04-30 at 13 25 26](https://user-images.githubusercontent.com/54425991/166095740-b27cc24f-9a95-48ce-b40b-188fd686841b.png)


## Limitation
Since food labels have several different formats, the values in dataframe result are not precise in some cases.

## Future work
Add more conditions to handle different formats of food labels.


