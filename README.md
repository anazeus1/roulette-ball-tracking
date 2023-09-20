
# Roulette-ball-tracking

Track the moving ball in roulette using ![Androidstudio](https://img.shields.io/badge/-OpenCV-000?&logo=opencv)


# Result

https://github.com/anazeus1/roulette-ball-tracking/assets/57845371/ae70fdaf-4bfc-4bfc-9fc3-3b5111ffb2e2

## Usage

### Get coordinates

![Screenshot 2023-09-07 142243](https://github.com/anazeus1/roulette-ball-tracking/assets/57845371/21a9e26f-517f-4024-8054-4ebd1bf37c6c)

## How the Program works

### get scrreenshot
![Screenshot 2023-09-07 143849](https://github.com/anazeus1/roulette-ball-tracking/assets/57845371/dcb6966a-0ba2-4662-8fa2-8d8d94da1a76)

### add eclipse to screenshot
we put the elipse to hide the moving rotator and only detect the ball

![Screenshot 2023-0907 143456](https://github.com/anazeus1/roulette-ball-tracking/assets/57845371/49f7c8c2-3721-42ce-af2b-2102a27b4986)

### crop screenshot
![cropped_image](https://github.com/anazeus1/roulette-ball-tracking/assets/57845371/93a4149a-cf99-4439-9218-587b39e53cb3)

### convert image to gray

![gray_image](https://github.com/anazeus1/roulette-ball-tracking/assets/57845371/f696ea6f-a8db-4f44-9c7d-c0c888c87b83)

### blur the image  
We should specify the width and height of the kernel which should be positive and odd.

![blurred_image](https://github.com/anazeus1/roulette-ball-tracking/assets/57845371/bc94ccb5-cd6e-4229-96a1-eaa4f529bf22)

### track ball
```python

def track_ball(base_line_image_for_ball, screenshot):
    # return the contour of the moving ball

    gray_image_for_ball = transform_screenshot(screenshot)

    # Calculating the absolute difference between baseline image and incoming images and image thresholding
    delta = cv2.absdiff(base_line_image_for_ball, gray_image_for_ball)
    threshold = cv2.threshold(delta, 25, 255, cv2.THRESH_BINARY)[1]

    # dilate the thresholded image to fill in holes, then find contours
    # on thresholded image
    thresh = cv2.dilate(threshold, None, iterations=2)
    contours = cv2.findContours(thresh.copy(), cv2.RETR_EXTERNAL,
                                cv2.CHAIN_APPROX_SIMPLE)
    contours = imutils.grab_contours(contours)
    return contours
```

