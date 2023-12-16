import cv2
import numpy as np

img = cv2.imread('cube.png')
img = img.reshape(-1,img.shape[-1])

img1 = cv2.imread('cube1.png')
img1 = img1.reshape(-1,img1.shape[-1])

q = cv2.imread('cube.png')
q = q.reshape(300, 300, 3)

zones = np.unique(img1.reshape(-1,img1.shape[-1]), axis = 0)

def chi(x, zone):
    if np.array_equal(x, zones[zone]):
        return 1
    else:
        return 0
  
pvq = np.zeros((300, 300, 3))

for zone in range(len(zones)):
    part = np.zeros((len(img), 3))
    a = [[0, 0, 0]]
    b = 0
    for i in range(len(img)):
        a += img[i] * chi(img1[i], zone)
        b += chi(img1[i], zone)
    cur_col = a // b
    for i in range(len(img)):
        part[i] = cur_col * chi(img1[i], zone)
    part = part.reshape(300, 300, 3)
    pvq += part

res = q - pvq
cv2.imwrite('pvq.png', pvq)
cv2.imwrite('result.png', res)
