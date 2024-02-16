使用场景：扫描仪，CAD，GIS

特性：

+ 支持从高端到低端的设备
+ 可扩展性强，支持公共和私用的标记结构
+ 支持各种压缩格式
+ 有公共软件库支持
+ 功能强大：
	1. 二值
	2. 灰度图
	3. 调色板
	4. 真彩色
	5. 其他扩展

文件结构：
```c
struct TIFF_img {
     unsigned char **mono;
     unsigned char **cmap;
     unsigned char ***color;
     char          TIFF_type; 
     char          compress_type;
     int           height;
     int           width;
};
```
![image.png|600](https://s2.loli.net/2023/10/12/9aDr5AgcSKh7e26.png)

编码方式：LZW

特点：

1. 一个GIF文件可以存储多幅图像
2. 带有色彩表（全局、局部色彩表）
3. 支持图像定序显示或覆盖
4. 可以错行存放
5. 支持文本覆盖
