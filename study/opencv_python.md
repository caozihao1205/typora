部分方法使用方法如下 1：imshow（） 显示图像 2：destroyallwindows用于卸载窗口 3：waitkey等待用户按键 其参数是延迟的时间

1：将图像转换成灰度图输出并保存

代码如下：

```python
import cv2
print(cv2.__version__)
img=cv2.imread(图片路径,0)
cv2.imshow("image",img)
k=cv2.waitKey(0)
if k==27:
    cv2.destroyWindow()
elif k==ord('s'):
    cv2.imwrite('result',img)
    cv2.destroyWindow()
```

拆分通道并着色

```python
img=cv2.imread(r"图片路径",0)
cv2.imshow('image',img)
k=cv2.waitKey(0)
if k==27:
    cv2.destroyAllWindows()
elif k==ord('s'):
    b,g,r=cv2.split(img)
    zeros=np.zeros(img.shape[:2],dtype="uint8")
    imgr=cv2.merge([zeros,zeros,r])
    imgg=cv2.merge([zeros,g,zeros])
    imgb=cv2.merge([b,zeros,zeros])
    cv2.imwrite('r.png',imgr)
    cv2.imwrite('g.png',imgg)
    cv2.imwrite('b.png',imgb)
    cv2.destroyAllWindows()
```

捕获摄像头

```python
cap=cv2.VideoCapture(0)
while(True):
    ret,frame=cap.read()
    cv2.imshow(u"Capture",frame)
    key=cv2.waitKey(1)
    if key&0xff==ord('q')or key==27:
        print(frame.shape,ret)
        break
cap.release()
cv2.destroyAllWindows()
```

img.shape[:2]取彩色图片的长、宽
img.shape[:3]取彩色图片的长、宽、通道
img.shape[0]图像的垂直尺寸（高度）
img.shape[1]图像的水平尺寸（宽度）
img.shape[2]图像的通道数
注：矩阵中，[0]表示行数，[1]表示列数