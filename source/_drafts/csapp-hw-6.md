
 曹真 2015302580272 

# 旋转

像素的核心数据结构形式：

``` c
typedef struct {
unsigned short red; /* R value */
unsigned short green; /* G value */
unsigned short blue; /* B value */
} pixel;

```
这里是`RIDX`的定义

```
#define RIDX(i,j,n) ((i)*(n)+(j))
```

缓存有2^14byte大小，是直接缓存，有2^14/2^5 = 2^9行，每行32 = 2^5byte。 
每个像素4字节，也就是缓存中一个块可以存8个像素。 

下面这张图直观的展示了如何将一张图片旋转90度：

![](http://orkqx44nq.bkt.clouddn.com/15141245552433.jpg)
<center>Rotate</center>

提供的原始代码扫描源图像矩阵的行，复制到目标图像的列
矩阵。

**项目的整体结构:**

![](http://orkqx44nq.bkt.clouddn.com/15141252012200.jpg)

**cache的结构**

模拟16 KB的直接映射高速缓存，具有32字节的高速缓存行。 

**代码：**

我们修改循环的顺序：对于一个已经划好的矩阵，让src从最下面一行开始，按照行优先的顺序从下向上扫描,这样一来对应的dst矩阵就符合我们的要求了。扫描完这个矩阵之后，只要以矩阵为单位在进行扫描就行了。 

``` c


char *rotate_descr = "Rotate: Change steps";

void rotate(int dim, pixel *src, pixel *dst) {
    int i, j, k, l;

    for (i = 0; i < dim; i += STEP) {
        for (j = 0; j < dim; j += STEP) {
            for (k = 0; k < STEP; k++) {
                if (k + i < dim) {
                    for (l = 0; l < STEP; l++) {
                        if (l + j < dim) {
                            COPY(&dst[PIXEL(dim - 1 - j - l, i + k, dim)], &src[PIXEL(i + k, j + l, dim)]);
                        } else {
                            break;
                        }
                    }
                } else {
                    break;
                }
            }
        }
    }
    return;
}


```




# 平滑

原理图：

![](http://orkqx44nq.bkt.clouddn.com/15141245704135.jpg)


<center>smooth原理图</center>

代码：

``` c
char smooth_descr[] = "SMOOTH: Column-wise Traversal of src";void smooth(int dim, pixel *src, pixel *dst) {	int i, j;	for(i=0; i<dim;i++) {		COPY(&dst[PIXEL(i,0,dim)], &src[PIXEL(i,0,dim)]);		COPY(&dst[PIXEL(i,dim-1,dim)], &src[PIXEL(i,dim-1,dim)]);	}	for(j=1; j<dim-1;j++) {		COPY(&dst[PIXEL(0,j,dim)], &src[PIXEL(0,j,dim)]);		COPY(&dst[PIXEL(dim-1,j,dim)], &src[PIXEL(dim-1,j,dim)]);	}	for(j=1; j<dim-1; j++) {		for(i=1; i<dim-1; i++) {			SMOOTH(&dst[PIXEL(j,i,dim)],					&src[PIXEL(j,i,dim)],					&src[PIXEL(j-1,i,dim)],					&src[PIXEL(j+1,i,dim)],					&src[PIXEL(j,i+1,dim)],					&src[PIXEL(j,i-1,dim)],					&src[PIXEL(j-1,i-1,dim)],					&src[PIXEL(j+1,i+1,dim)],					&src[PIXEL(j-1,i+1,dim)],					&src[PIXEL(j+1,i-1,dim)]);		}	}	return;}
```

# 测试结果

我们在macOS下进行编译测试：

> gcc *.h *.c 
> ./a.out


![](http://orkqx44nq.bkt.clouddn.com/15141244811722.jpg)


