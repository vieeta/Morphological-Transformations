import cv2
import numpy as np
from google.colab.patches import cv2_imshow

def dilation(x,kernel):
  new_x= np.array(x)
  for i in range (1,len(x)-1):
    for j in range (1,len(x[i])-1):
      if (x[i-1][j-1] == kernel[0][0] or x[i-1][j] == kernel[0][1] or x[i-1][j+1] == kernel[0][2] or x[i][j-1] == kernel[1][0] or x[i][j] == kernel[1][1] or x[i][j+1] == kernel[1][2] or x[i+1][j-1] == kernel[2][0] or x[i+1][j] == kernel[2][1] or x[i+1][j+1] == kernel[2][2]):
        new_x[i][j] = 1
      else:
        new_x[i][j] = 0
  return new_x

def erosion(x,kernel):
  new_x= np.array(x)
  for i in range (1,len(x)-1):
    for j in range (1,len(x[i])-1):
      if (x[i-1][j-1] == kernel[0][0] & x[i-1][j] == kernel[0][1] & x[i-1][j+1] == kernel[0][2] & x[i][j-1] == kernel[1][0] & x[i][j] == kernel[1][1] & x[i][j+1] == kernel[1][2] & x[i+1][j-1] == kernel[2][0] & x[i+1][j] == kernel[2][1] & x[i+1][j+1] == kernel[2][2]): 
        new_x[i][j] = 1
      else: 
        new_x[i][j] = 0
  return new_x

def opening(x,kernel):
  img_ero = erosion(x,kernel)
  img_dil = dilation(img_ero,kernel)
  return img_dil

def closing(x,kernel):
  img_dil = dilation(x,kernel)
  img_ero = erosion(img_dil,kernel)
  return img_ero

def convert01to0255(img):
  new= np.array(img) 
  for i in range(len(img)):
      for j in range(len(img[i])):
          if img[i][j] == 0:
              new[i][j] = 0
          else:
              new[i][j] = 255
  return new

def convert255to1(img):
  new= np.array(img) 
  for i in range(len(img)):
      for j in range(len(img[i])):
          if img[i][j] == 0:
              new[i][j] = 0
          else:
              new[i][j] = 1
  return new
  
import cv2
import numpy as np
from google.colab.patches import cv2_imshow
from PIL import Image  

img = cv2.imread('/content/drive/My Drive/binary.jpg'); 
kernel = np.ones((3,3), np.uint8)

#convert to grayscale and resize
dim = (200,200)
img1 = cv2.resize(img, dim, interpolation = cv2.INTER_AREA);
grayimg = cv2.cvtColor(img1, cv2.COLOR_BGR2GRAY);

#making 2d array and padding
np_img = np.asarray(grayimg) 
np_img = np.pad(np_img, pad_width=1, mode='constant', constant_values=0)

#convert dari (0,255) ke (0,1)
new_A= convert255to1(np_img)

#morphology image processing
print('Original')
cv2_imshow(np_img)
img_dil = dilation(new_A,kernel)
img_ero = erosion(new_A,kernel)
img_ope = opening(new_A,kernel)
img_clo = closing(new_A,kernel)

#convert dari (0,1) ke (0,255)
new_dil = convert01to0255(img_dil)
new_ero = convert01to0255(img_ero)
new_ope = convert01to0255(img_ope)
new_clo = convert01to0255(img_clo)

print('Dilation')
cv2_imshow(new_dil)
print('Erosion')
cv2_imshow(new_ero)
print('Opening')
cv2_imshow(new_ope)
print('Closing')
cv2_imshow(new_clo)
