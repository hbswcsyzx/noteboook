<style>
    table {
        width: auto;
        margin: 0 auto;
        border: 1px solid #000000;
        border-collapse: collapse;
        font-family: "Consolas";
        font-size: 15px;
    }

    th,
    td {
        border: 1px solid #000000;
        text-align: center;
    }
</style>

# 整理

## 基础类型
<table>
    <tr>
        <th>分类</th>
        <th>声明变量</th>
        <th>类型</th>
        <th>指针步长</th>
        <th>占用内存</th>
    </tr>
    <tr>
        <th rowspan="3">多维数组</th>
        <td>int arr0;</td>
        <td>int</td>
        <td>不是指针</td>
        <td>sizeof(int) = 4</td>
    </tr>
    <tr>
        <td>int arr1[5];</td>
        <td>int *</td>
        <td>sizeof(int) = 4</td>
        <td>sizeof(int *) = 8</td>
    </tr>
    <tr>
        <td>char arr2[3][5];</td>
        <td>char (*)[5]</td>
        <td>5 * sizeof(char) = 5</td>
        <td>sizeof(char (*)[5]) = 8</td>
    </tr>
    <tr>
        <th rowspan="3">多重指针</th>
        <td>int *ptr1;</td>
        <td>int *</td>
        <td>sizeof(int) = 4</td>
        <td>sizeof(int *) = 8</td>
    </tr>
    <tr>
        <td>int **ptr2;</td>
        <td>int **</td>
        <td>sizeof(int *) = 8</td>
        <td>sizeof(int **) = 8</td>
    </tr>
    <tr>
        <td>int ***ptr3;</td>
        <td>int ***</td>
        <td>sizeof(int **) = 8</td>
        <td>sizeof(int ***) = 8</td>
    </tr>
    <tr>
        <th>函数</th>
        <td>int func(unsigned a, char b);</td>
        <td>int (*)(unsigned int, char)</td>
        <td>无效</td>
        <td>sizeof(pointer) = 8</td>
</table>

## 数组与指针
<table>
    <tr>
        <th>分类</th>
        <th>声明变量</th>
        <th>类型</th>
        <th>指针步长</th>
        <th>占用内存</th>
    </tr>
    <tr>
        <th rowspan="4">指针数组</th>
        <td>int *a0;</td>
        <td>int *</td>
        <td>sizeof(int) = 4</td>
        <td>sizeof(int *) = 8</td>
    </tr>
    <tr>
        <td>int *a1[4];</td>
        <td>int **</td>
        <td>sizeof(int *) = 8</td>
        <td>sizeof(int **) = 8</td>
    </tr>
    <tr>
        <td>int *a2[4][7];</td>
        <td>int *(*)[7]</td>
        <td>7 * sizeof(int *) = 56</td>
        <td>sizeof(int *(*)[7]) = 8</td>
    </tr>
    <tr>
        <td>int *a3[4][7][10];</td>
        <td>int *(*)[7][10]</td>
        <td>7 * 10 * sizeof(int *) = 60</td>
        <td>sizeof(int *(*)[7][10]) = 8</td>
    </tr>
    <tr>
        <th rowspan="3">数组指针</th>
        <td>int *pt0;</td>
        <td>int *</td>
        <td>sizeof(int) = 4</td>
        <td>sizeof(int *) = 8</td>
    </tr>
    <tr>
        <td>int(*pt1)[5];</td>
        <td>int (*)[5]</td>
        <td>5 * sizeof(int) =20</td>
        <td>sizeof(int (*)[5]) = 8</td>
    </tr>
    <tr>
        <td>int(*pt2)[3][5];</td>
        <td>int (*)[3][5]</td>
        <td>3 * 5 * sizeof(int) = 60</td>
        <td>sizeof(int (*)[3][5]) = 8</td>
    </tr>
</table>

## 函数与指针
<table>
    <tr>
        <th>分类</th>
        <th>个人理解</th>
        <th>示例</th>
        <th>赋值</th>
        <th>调用</th>
    </tr>
    <tr>
        <th>指针函数</th>
        <td>返回值为指针的函数</td>
        <td>int *func(int x, int y);</td>
        <td rowspan="2">fpt = &amp;func;<br>or fpt = func;</td>
        <td rowspan="2">ptr = (*fpt)();<br>or ptr = fpt();</td>
    </tr>
    <tr>
        <th>函数指针</th>
        <td>指向函数的指针</td>
        <td>int (*fpt)(int x, int y);</td>
    </tr>
    <tr>
        <th>函数型指针</th>
        <td>类比整型指针、字符型指针的一种指针</td>
        <td>typedef void (*func_ptr)(void);</td>
        <td colspan="2">详见混合部分</td>
</table>

<br><br>

# 补充 <span style="font-size: 16">( 关于 <span>*typedef*</span> )</span>

<p style="color: #6a737d">以下仅为个人理解，不一定正确。
    <a
        href="https://www.bilibili.com/video/BV15h4y1M7p2/">
        参考B站
    </a>
</p>

我以前一直认为， *typedef* 跟 #*define* 的作用是一样的，都只是换个名字而已，例如

```c
typedef int INT; // 定义实质 int 的别名为 INT ;
#define INT int; // 定义别名 INT 的实质是 int ;
```
这种理解其实不够全面。
例如

```c
typedef int ARR[20][25];
ARR array; // 这总不能理解为：定义 int 的别名是 ARR[20][25] 吧
// 而以上相当于 int array[20][25];
```
所以，现在我的理解是， *typedef* 不是给已知类型起别名，而是一种新的创建变量的方式。<br>
相当于，设立了一对传送门，在上例中 *ARR* 就是传送门，把 *array* 传送到 *typedef* 的式子中进行定义。<br>
不过， *ARR* 确实已经是一种新的变量类型了。
<br><br>又例如：

```c
typedef void (*func_ptr)(void);
func_ptr func_array[] = {func1, func2};
```
相当于

```c
void (*func_array[])(void) = {func1, func2};
```
可以发现，与上面声明函数相关变量的原始方式相比<br>
用 *typedef* 更符合 *变量类型-变量名-维度* 的直觉。<br>
同时这也说明，这种直觉其实是不全面的。


# 总结
1. 数组变量名 arr 是数组首元素的地址，&amp;arr 才是整个数组的地址。它们在数值上相等但类型不同。
<div>

```c
int f1(int a[], int n);

int main()
{
    int a[10] = {1, 2, 3, 4, 5, 6, 7, 8, 9, 0};
    int(*pt)[10];
    pt = &a; // 通过编译
    pt = a; // 报错 "assignment to 'int (*)[10]' from incompatible pointer type 'int *' "
}
```
</div>

2. 函数名和函数名的地址都是函数在内存中的位置
3. 取址符(&amp;)只能对**左值**或**函数指示符**取地址。(from IntelliSense)
4. 变量名不存储在任何内存区域（栈、堆等），它只是编译器的符号标识。(from Deepseek)
5. 变量名不是地址，而是通过编译器映射到地址的符号。(from Deepseek)
6. 常量变量的值 根据作用域和类型存储在 .rodata 或栈区，但变量名本身仍只是符号。(from Deepseek)
7. 函数标识符就表示了它的地址。(from CSDN)

<br><br>

# 成果检验 *(all from Deepseek)*

## 简单
#### 题目
```c
#include <stdio.h>

void set_value(int *p) { *p = 100; }

int sum_array(int arr[], int size)
{
    int sum = 0;
    for (int i = 0; i < size; i++)
        sum += arr[i];
    return sum;
}

int main()
{
    int a = 10;
    set_value(&a);

    int arr[3] = {1, 2, 3};
    int total = sum_array(arr, 3);

    printf("a = ?\ntotal = ?\n");
}
```
#### 解析
```c
#include <stdio.h>

void set_value(int *p) { *p = 100; }

int sum_array(int arr[], int size)
{
    int sum = 0;
    for (int i = 0; i < size; i++)
        sum += arr[i];
    return sum;
}

int main()
{
    int a = 10;
    set_value(&a); // 通过指针修改 a 的值
    printf("a 的地址：%p，修改后值：%d\n", (void *)&a, a);

    int arr[3] = {1, 2, 3};
    printf("arr 首元素地址：%p\n", (void *)arr);
    int total = sum_array(arr, 3);
    printf("total = %d\n", total);

    printf("答案：\na = 100\ntotal = 6\n");
}
```

## 中等
#### 题目
```c
#include <stdio.h>

typedef int (*MathOp)(int, int); 

int add(int a, int b) { return a + b; }
int sub(int a, int b) { return a - b; }

int main()
{
    MathOp operations[2] = {add, sub}; 

    int matrix[2][3] = {{1, 2, 3}, {4, 5, 6}};
    int(*row_ptr)[3] = matrix;

    int x = operations[0](row_ptr[0][1], row_ptr[1][2]);
    int y = operations[1](x, 3);

    printf("x = ?\ny = ?\n");
}
```
#### 解析
```c
#include <stdio.h>

typedef int (*MathOp)(int, int);

int add(int a, int b) { return a + b; }
int sub(int a, int b) { return a - b; }

int main()
{
    MathOp operations[2] = {add, sub}; // 函数指针数组
    printf("operations[0] 地址：%p（指向 add）\n", (void *)operations[0]);

    int matrix[2][3] = {{1, 2, 3}, {4, 5, 6}};
    int(*row_ptr)[3] = matrix; // 数组指针
    printf("row_ptr 指向的数组：{%d, %d, %d}\n", row_ptr[0][0], row_ptr[0][1], row_ptr[0][2]);

    int a = row_ptr[0][1]; // 2
    int b = row_ptr[1][2]; // 6
    printf("x = add(%d, %d) = %d\n", a, b, add(a, b));
    int x = add(a, b);

    printf("y = sub(%d, 3) = %d\n", x, sub(x, 3));
    int y = sub(x, 3);

    printf("答案：\nx = 8\ny = 5\n");
}
```

## 困难
#### 题目
```c
#include <stdio.h>

int *get_addr(int (*matrix)[3], int row)
{
    return matrix[row];
}

int main()
{
    int arr[2][3] = {{1, 2, 3}, {4, 5, 6}};

    int *(*func_array[2])(int(*)[3], int) = {get_addr, get_addr};

    int *(**func_ptr)(int(*)[3], int) = func_array;

    int *p1 = func_ptr[0](arr, 1);
    int *p2 = (*(func_ptr + 1))(arr, 0);

    printf("p1[2] = ?\np2[1] = ?\n");
}
```
#### 解析
```c
#include <stdio.h>

int *get_addr(int (*matrix)[3], int row)
{
    printf("返回第 %d 行首地址：%p\n", row, (void *)matrix[row]);
    return matrix[row];
}

int main()
{
    int arr[2][3] = {{1, 2, 3}, {4, 5, 6}};
    printf("arr 地址：%p\n", (void *)arr);

    // 定义：由返回指针的函数构成的数组，元素类型为 int *(*)(int (*)[3], int)
    int *(*func_array[2])(int(*)[3], int) = {get_addr, get_addr};
    printf("func_array[0] 地址：%p\n", (void *)func_array[0]);

    // 指向函数指针数组的指针
    int *(**func_ptr)(int(*)[3], int) = func_array;

    // 分步解析
    int *p1 = func_ptr[0](arr, 1); // 获取 arr[1] 的地址
    printf("p1 指向的值：{%d, %d, %d}\n", p1[0], p1[1], p1[2]);

    int *p2 = (*(func_ptr + 1))(arr, 0); // 等效于 func_array[1](arr,0)
    printf("p2 指向的值：{%d, %d, %d}\n", p2[0], p2[1], p2[2]);

    printf("答案：\np1[2] = 6\np2[1] = 2\n");
}
```

## 极限
#### 题目
```c
#include <stdio.h>

int (*sum_row(int (*mat)[3]))[2]
{
    static int res[2][2];
    for (int i = 0; i < 2; i++)
    {
        res[i][0] = *(*mat + i * 3) + *(*mat + i * 3 + 1) + *(*mat + i * 3 + 2);
        res[i][1] = i;
    }
    return res;
}

int (*max_col(int (*mat)[3]))[2]
{
    static int res[3][2];
    for (int j = 0; j < 3; j++)
    {
        int max_val = *(*(mat) + j);
        int max_idx = 0;
        for (int i = 1; i < 2; i++)
        {
            if (*(*(mat + i) + j) > max_val)
            {
                max_val = *(*(mat + i) + j);
                max_idx = i;
            }
        }
        res[j][0] = max_val;
        res[j][1] = max_idx;
    }
    return res;
}

int main()
{
    int arr[2][3] = {{1, 2, 3}, {4, 5, 6}};

    int(*(*fc[2])(int(*)[3]))[2] = {sum_row, max_col};
    int(*(*(*func_ptr)[2])(int(*)[3]))[2] = &fc;

    int(*result1)[2] = (*func_ptr)[0](arr);
    int(*result2)[2] = (*func_ptr)[1](arr);

    printf("result1[0][0] = ?\nresult2[2][1] = ?\n");
}
```
#### 解析
```c
#include <stdio.h>

// 行求和函数，返回静态二维数组指针
int (*sum_row(int (*mat)[3]))[2]
{
    static int res[2][2];
    for (int i = 0; i < 2; i++)
    {
        res[i][0] = *(*mat + i * 3) + *(*mat + i * 3 + 1) + *(*mat + i * 3 + 2);
        res[i][1] = i;
        printf("sum_row计算第%d行和：%d\n", i, res[i][0]);
    }
    printf("sum_row返回地址：%p\n", (void *)res);
    return res;
}

// 列最大值函数，返回静态二维数组指针
int (*max_col(int (*mat)[3]))[2]
{
    static int res[3][2];
    for (int j = 0; j < 3; j++)
    {
        int max_val = *(*(mat) + j);
        int max_idx = 0;
        for (int i = 1; i < 2; i++)
        {
            if (*(*(mat + i) + j) > max_val)
            {
                max_val = *(*(mat + i) + j);
                max_idx = i;
            }
        }
        res[j][0] = max_val;
        res[j][1] = max_idx;
        printf("max_col计算第%d列最大值：%d（行号%d）\n", j, max_val, max_idx);
    }
    printf("max_col返回地址：%p\n", (void *)res);
    return res;
}

int main()
{
    int arr[2][3] = {{1, 2, 3}, {4, 5, 6}};

    // 函数指针数组声明
    int(*(*fc[2])(int(*)[3]))[2] = {sum_row, max_col};
    printf("fc数组地址：%p\n", (void *)&fc);
    printf("fc[0]指向sum_row地址：%p\n", (void *)fc[0]);

    // 三级指针声明
    int(*(*(*func_ptr)[2])(int(*)[3]))[2] = &fc;
    printf("func_ptr指向fc地址：%p\n", (void *)func_ptr);

    // 解引用过程分解
    printf("解引用func_ptr得到fc地址：%p\n", (void *)(*func_ptr));
    printf("获取fc[0]函数指针：%p\n", (void *)(*func_ptr)[0]);

    // 调用sum_row
    int(*result1)[2] = (*func_ptr)[0](arr);
    printf("result1首地址：%p\n", (void *)result1);

    // 调用max_col
    int(*result2)[2] = (*func_ptr)[1](arr);
    printf("result2首地址：%p\n", (void *)result2);

    // 最终输出
    printf("result1[0][0] = %d\n", **result1);             // 6
    printf("result2[2][1] = %d\n", *(*(result2 + 2) + 1)); // 1
}
```
#### 优化
```c
#include <stdio.h>

// 使用typedef简化函数指针类型
typedef int (*RowFunc)(int (*)[3]); // 函数指针类型
typedef int (*ColFunc)(int (*)[3]); // 函数指针类型
typedef int ResultArray[2][2];      // 二维数组类型

// 行求和函数
ResultArray *sum_row(int (*mat)[3])
{
    static ResultArray res;
    for (int i = 0; i < 2; i++)
    {
        res[i][0] = *(*mat + i * 3) + *(*mat + i * 3 + 1) + *(*mat + i * 3 + 2);
        res[i][1] = i;
    }
    return &res;
}

// 列最大值函数
ResultArray *max_col(int (*mat)[3])
{
    static ResultArray res;
    for (int j = 0; j < 3; j++)
    {
        int max_val = *(*(mat) + j);
        int max_idx = 0;
        for (int i = 1; i < 2; i++)
        {
            if (*(*(mat + i) + j) > max_val)
            {
                max_val = *(*(mat + i) + j);
                max_idx = i;
            }
        }
        res[j][0] = max_val;
        res[j][1] = max_idx;
    }
    return &res;
}

int main()
{
    int arr[2][3] = {{1, 2, 3}, {4, 5, 6}};

    // 使用typedef简化声明
    typedef ResultArray *(*FuncArray[2])(int(*)[3]);
    FuncArray fc = {sum_row, max_col};

    // 简化后的指针声明
    FuncArray *func_ptr = &fc;

    // 函数调用
    ResultArray *result1 = (*func_ptr)[0](arr);
    ResultArray *result2 = (*func_ptr)[1](arr);

    // 输出结果
    printf("result1[0][0] = %d\nresult2[2][1] = %d\n",
           (*result1)[0][0], (*result2)[2][1]);
}
```