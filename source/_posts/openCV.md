# OpenCV

参考文件：https://docs.opencv.org/4.5.2/d5/d10/tutorial_js_root.html

### 1、常用方法：

```javascript
//读取图片-> mat对象
cv.imread(document.getElementById('imageSrc'))

//输出到canvas
cv.inshow('canvasOutput2',dst)  //element id,mat类型的对象

//设置画布大小
cv.Size(800, 600)
cv.resize(src, src, dsize);  // 输入对象，输出对象，输出对象的大小

//设置画面颜色 (对画面操作前最好将其转换成RGB)
//https://blog.csdn.net/keith_bb/article/details/53470170
cv.cvtColor(src, src, cv.COLOR_RGBA2GRAY, 0);
cv.threshold(src, src, 100, 255, cv.THRESH_OTSU);
//cvtColor+threshold 将图片转为二进制图像

//轮廓检索
//https://blog.csdn.net/dcrmg/article/details/51987348
 cv.findContours(src, contours, hierarchy, cv.RETR_TREE, cv.CHAIN_APPROX_NONE); 
//灰度图片或二进制图像，存储轮廓，存储每个轮廓的相对关系，轮廓检索模式，轮廓近似方法

//绘制轮廓
//https://blog.csdn.net/qq_18343569/article/details/47982167
cv.drawContours(src_clone, contours, i, color, 1);

//图片描线
cv.Canny()
//图片模糊
cv.blur()
cv.filter() 

```

