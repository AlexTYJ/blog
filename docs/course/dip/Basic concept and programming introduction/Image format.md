规范：==基于像素==，矩形框形式
> 某些图像格式与操作系统高度相关

表示：

+ 图像：2D array or matrix

+ 像素：
    + 灰度图：1字节 \[0, 255]
    + 彩色图：3字节 R, G, B


编码方式：

+ 压缩：有损 / 无损
+ 不压缩

代表格式：BMP（压缩 / 不压缩）, JPEG（有损压缩）, TIFF（用于GIS）, GIF, PNG（用于网页）, ...

## BMP
简介：Windows标准文件格式，后缀名.bmp / .dib
> BMP通常不压缩（可支持压缩）

文件结构：

![image.png|300](https://s2.loli.net/2023/09/28/byFt9c6lGXdhDpk.png)

```c
BITMAPFILEHEADER bmfh;
BITMAPINFOHEADER bmih;
RGBQUAD aColors[];
BYTE aBitmapBits[];
```

### Image file header

![image.png|350](https://s2.loli.net/2023/09/28/uPGHIhbZo9BMpjm.png)

```c
typedef struct tagBITMAPFILEHEADER {
	WORD bfType;
	DWORD bfSize;
	WORD bfReserved1;
	WORD bfReserved2;
	DWORD bfOffBits;
} BITMAPFILEHEADER, *PBITMAPFILEHEADER;
```

### Image information header
![image.png|550](https://s2.loli.net/2023/09/28/PwFfaOkSL2vH7di.png)

```c
typedef struct tagBITMAPINFOHEADER {
	DWORD bitsize;
	LONG biWidth;
	LONG biHeight;
	WORD biPlanes;
	WORD biBitCount;
	DWORD biCompression;
	DWORD biSizeImage;
	LONG biXPelsPerMeter;
	LONG biYPelsPerMeter;
	DWORD biClrUsed;
	DWORD biClrImportant;
} BITMAPINFOHEADER, *BITMAPINFOHEADER;
```

### Palette
大小：N * 4 bytes

格式：对于每一个颜色，R, G, B各1 byte， 1 byte 恒为0

### Bitmap Data
大小：取决于图像大小和位深

规定：

+ 每一行的字节数必须是 ==4的倍数==，否则需要补齐
+ BMP文件数据从下到上，从左到右（上下颠倒）
