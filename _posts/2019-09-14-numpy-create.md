---
layout: post
title: Tạo ma trận trong numpy
subtitle: Giới thiệu các các kỹ thuật khởi tạo ma trận trong numpy
tags: [numpy]
comments: true
---

## 1. Tạo ma trận từ các cấu trúc dữ liệu hỗ trợ array interface

Cách đơn giản nhất và cũng thường thấy nhất để khởi tạo ma trận trong numpy là ta sử dụng dụng hàm `numpy.array()` để chuyển các cấu trúc dữ liệu có hỗ trợ array interface (còn gọi là array-like structure) sang kiểu dữ liệu ma trận (`numpy.ndarray`). Cú pháp hàm:

```python
numpy.array(
    object,  # any object exposing the array interface
    dtype=None,  # the desired data-type for the array
    copy=True,  # if true (default), the object is copied
    order='K',  # specify the memory layout of the array
    subok=False,  # if false (default), must be array class
    ndmin=0 # the minimum number of dimensions 
)
```

- **object** là một tham số bắt buộc, truyền vào dữ liệu có hỗ trợ array interface (array-like structure) như : list, tuple....
- **dtype** là một tham số tùy chọn, chỉ định kiểu dữ liệu cho các phần tử của  ma trận. Nếu không được truyền, 'dtype' sẽ chỉ định kiểu dữ liệu ít tốn bộ nhớ nhất mà có thể lưu được tất cả phần tử ma trận. Một vài kiểu dữ liệu thường dùng trong numpy như `int float bool complex`.
- **copy** là một tham số tùy chọn, có giá trị mặc định là `True`. Nếu giá trị là `True` thì dữ liệu của ma trận được cấp phát vùng nhớ mới độc lập với vùng nhớ của `object`, nếu giá trị là `False` thì dữ liệu ma trận dùng chung vùng nhớ với `object`. Tham số này đặc biệt hữu ích để tối ưu hóa sử dụng bộ nhớ. Tuy nhiên một số trường hợp dù `copy=False` nhưng vùng nhớ mới vẫn được cấp phát cho ma trận, ví dụ ta gán `dtype` sang kiểu dữ liệu khác với `object`.
- **order** là một tham số tùy chọn, chỉ định cách lưu trữ ma trận trong bộ nhớ. Nếu các bạn đã học qua C, sẽ biết mảng được lưu thành chuỗi các ô nhớ liền kề nhau. Python lưu trữ ma trận dưới dạng array theo 2 cách  C(hoặc F)-order, nghĩa là nối các hàng(hoặc cột) của ma trận thành 1 chuỗi ô nhớ để lưu trữ.
- **ndmin** : là một tham số tùy chỉnh, chỉ định số chiều tối thiểu của ma trận. Tham số này được dùng khá thường xuyên.

Ngoài ra, nếu bạn đọc một số code cũ sẽ thường xuyên thấy ma trận được khởi tạo từ hàm `numpy.matrix()`. Hàm này có công dụng tương tự `np.array()` tuy nhiên không còn được hỗ trợ ở các phiên bản python trong tương lai.


### 2. Sử dụng hàm tạo ma trận đặc biệt

#### 2.1. Ma trận không

{: .box-note}
**Ma trận không:** Trong đại số tuyến tính, ma trận không (zero matrix) hay còn gọi là ma trận rỗng (null matrix) là một ma trận mà tất cả các phần tử của nó đều bằng 0. Nói một cách toán học, ma trận A được gọi là ma trận không khi và chỉ khi thỏa  $$ A_{i,j} = 0, \forall{i,j} $$

Hàm `numpy.zeros()` trả về ma trận không theo kích thước *shape*.

```python
numpy.zeros(shape, dtype=float, order='C')
```

- **shape** là tham số bắt buộc, chấp nhận kiểu dữ liệu *int* hoặc *tuple of int*, chỉ định kích thước ma trận. 
- **dtype** là một tham số tùy chọn, chỉ định kiểu dữ liệu cho các phần tử của  ma trận. Mặc định là kiểu *float*.
- **order** là một tham số tùy chọn, chỉ định cách lưu trữ ma trận trong bộ nhớ. 

#### 2.2. Ma trận một

{: .box-note}
**Ma trận một:** Trong đại số tuyến tính, ma trận một (matrix of ones, all-ones matrix) là một ma trận mà tất cả các phần tử của nó đều bằng 1. Nói một cách toán học, ma trận A được gọi là ma trận một khi và chỉ khi thỏa  $$ A_{i,j} = 1, \forall{i,j} $$

Hàm `numpy.ones()` trả về ma trận một theo kích thước *shape*.

```python
numpy.ones(shape, dtype=float, order='C')
```

- **shape** là tham số bắt buộc, chấp nhận kiểu dữ liệu *int* hoặc *tuple of int*, chỉ định kích thước ma trận. 
- **dtype** là một tham số tùy chọn, chỉ định kiểu dữ liệu cho các phần tử của  ma trận. Mặc định là kiểu *float*.
- **order** là một tham số tùy chọn, chỉ định cách lưu trữ ma trận trong bộ nhớ. 

#### 2.3. Ma trận đơn vị

{: .box-note}
**Ma trận đơn vị:** Trong đại số tuyến tính, ma trận đơn vị (unit matrix) hay còn gọi là ma trận định danh (identity matrix) là một ma trận vuông có kích $$ n \times n $$ trong đó mọi phần tử trên đường chéo chính bằng $$ 1 $$ và tất cả những phần tử khác đều bằng $$ 0 $$. Ma trận đơn vị thường được ký hiệu là  $$ I_n $$, hoặc đơn là $$ I $$.

$$
\begin{cases}
I_{i,j} = 0, \forall{i \not = j} \\
I_{i,j} = 1, \forall{i = j}
\end{cases}
$$

Hàm `numpy.eye()` trả về ma trận đơn vị, hoặc các biến thể của ma trận đơn vị khi cài đặt các tham số tùy chọn.

```python
numpy.eye(N, M=None, k=0, dtype='float', order='C')
```

- `N` là tham số bắt buộc, chỉ định số hàng của ma trận đơn vị
- `M` là tham số tùy chọn, chỉ định số cột của ma trận đơn vị (mặc định `M=N`)
- `k` là tham số tùy chọn, chỉ định đuờng chéo nhận chuỗi giá trị 1. Mặc định là đường chéo chính (k = 0). Với k > 0 (hoặc k < 0) biểu diễn đường chéo ở (trên hoặc dưới) đường chéo chính k đơn vị.
- `dtype` là một tham số tùy chọn, chỉ định kiểu dữ liệu cho các phần tử của  ma trận. Mặc định là kiểu `float`.

#### 2.4. Ma trận đường chéo

{: .box-note}
**Ma trận đường chéo:** Trong đại số tuyến tính, ma trận đường chéo (diagonal matrix) là một ma trận mà các phần tử bên ngoài đường chéo đều bằng 0. Trong đa số trường hợp ta hiểu đây là ma trận vuông.

Hàm `numpy.diag()` trả về ma trận đường chéo hoặc đường chéo của ma trận.

```python
numpy.diag(v, k=0)
```

- 'v' là ma trận 2 chiều hoặc mảng một chiều.
- `k` là tham số tùy chọn, chỉ định đuờng chéo nhận chuỗi giá trị 1. Mặc định là đường chéo chính (k=0). Với k>0 (hoặc k <0) biểu diễn đường chéo ở trên đường chéo chính k đơn vị.

#### 2.5.  Một số hàm sinh ma trận khác
- `numpy.empty(shape)` trả về mảng với các phẩn tự có giá trị bất ký (giá trị của vùng nhớ được cấp phát). Đây làm hàm thường dùng khi bạn không quan tâm đến giá trị của các phần tử khi khởi tạo ma trận.
- `numpy.arange(start, stop, step)` tương tự hàm `range()` nhưng trả về kiểu dữ liệu `numpy.ndarray`
- `numpy.linspace(start, end, num))` trả về ma trận gồm `num` phần tử có giá trị cách đều nhau nằm trong đoạn [start, end] hoặc khoảng [start, end). 

### 3 Tạo ma trận từ phân phối xác xuất

Chưa viết
