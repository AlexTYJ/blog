性质：压缩静态图像

编码方式：离散余弦变换(DCT)
> 高低频信息分别处理

压缩策略：根据压缩比，移除高频信息

+ 高频信息占用存储空间大，减少高频信息更容易获得高压缩比
+ 低频信息可以保留物体的基本轮廓和色彩分布，最大限度维持图像质量

优势：适合用于互联网

文件结构：

![image.png|500](https://s2.loli.net/2023/10/12/mfoDZlyGPN8Ebn3.png)
由一系列的segment组成的，每个segment从一个标记（Marker，用以区分和识别图像数据及其相关信息，由2个字节组成，前一个字节是固定值0xFF）开始

![image.png|500](https://s2.loli.net/2023/10/12/u5SmfqXCwjrE7ZH.png)

1. SOI(Start of Image) Marker 
2. APP0 Marker：
```
APP0 Marker:
    Length
    Identifier
    Version
    Density unit of X and Y:   
        units=0-> no unit
        units=1: points/inch
        units=2: points/cm
    X density
    Y density
    Number of thumbnail horizontal pixels
    Number of thumbnail vertical pixels
    Thumbnail RGB bitmap
```
3. APPn (Markers)，n=1~15(optional)
4. One or more DQT（Define Quantization Table）
	+ Quantization table length，Quantization table number，Quantization table 
> 人眼对于一个相对较大范围的区域，辨别色彩细微差异能力比较强（低频），但对于高频区域，却表现一般。受此启发，人们可以对高频部分进行量化，也就是说，把频域上的每个分量，除以针对该分量的常数，然后四舍五入取整。
> 
> 这样一般会把高频分量变为0。
> 
> 但这样操作就要求针对每一个分量设置一个常数值，所以就最终形成了量化表

5. SOF0 (Start of Frame, DCT based)
```
Start of frame length
Precision: color depth (bit-width) of each color channel
Image height
Image width
Number of color components
For each color component
    ID
    vertical sample factor
    horizontal sample factor
    Quantization table # 
```
6. DHT(Define Huffman Table)
```
Huffman table length
Type, AC or DC
Index
bits table
value table
```
7. Start of Scan (SoS) 
```
SoS length
Number of color components
For each color component
	ID
	AC table #
	DC table #
    Compress image data 
```
8. End of Image (EOI)

编码原理：

+ DPCM(differential pulse-code modulation)编码
	+ 对模拟信号幅度抽样的差值进行量化编码的调制方式
		![image.png|400](https://s2.loli.net/2023/10/12/SK5fwdJPECMqAyz.png)
+  JPEG uses DCT：
	+ The DCT transforms an 8×8 block of input values to a linear combination of these 64 patterns. The patterns are referred to as the two-dimensional DCT basis functions, and the output values are referred to as transform coefficients. 

劣势：

+ 不适合用于线条画、文字、图标等
+ 有损压缩会导致这类对象的瑕疵严重
