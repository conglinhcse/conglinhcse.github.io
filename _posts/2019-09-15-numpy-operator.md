---
layout: post
title: Phép toán ma trận trong numpy
subtitle: Giới thiệu phép toán ma trận trong numpy
tags: [numpy]
comments: true
---

### Phép chuyển vị 

{: .box-note}
**Phép chuyển vị** (transpose) là một phép hoán đổi tất cả phần tử đối xứng qua đường chéo chính của ma trận.Nói một các đơn giản là chuyển cột của ma trận thành hàng và ngược lại. Một số tài liệu gọi đây là phép ánh xạ gương qua đường chéo chính của ma trận.  $$A^T_{i,j} = A_{i,j}$$

**numpy** hỗ trợ các hàm `A.T A.transpose()` để tính phép chuyển vị.

### Phép nghịch đảo

{: .box-note}
Trong đại số tuyến tính, ma trận vuông $$ A $$ được gọi là khả nghịch khi tồn tại một ma trận vuông $$ B $$ sao cho tích có hướng của $$ A $$ và $$ B $$ (không quan tâm thứ tự) là một ma trận đơn vị $$ A \times B = B \times A = I $$. Khi đó ta gọi $$ B $$ là ma trận nghịch đảo của $$ A $$, ký hiệu là $$ A^{-1} $$ 

**numpy** hỗ trợ các hàm  numpy.linalg.inv() numpt.linalg..pinv() để tính phép nghịch đảo. 

### Vết ma trận

{: .box-note}
**Vết** (trace) của một ma trận vuông A bậc $$ n \times n $$ được xác định bằng tổng các phần tử trên đường chéo chính của A. $$ tr(A) = a_{11} + a_{22} + a_{33} + ... + a_{nn} $$   

**numpy** hỗ trợ các hàm `numpy.trace()` để vết của ma trận.

### Hạng ma trận

{: .box-note}
**Hạng của ma trận** là số chiều của không gian vector tạo bởi các vector cột của ma trận. Hay dễ hiểu hơn, ta có thể nói hạng của ma trận là số vector cột độc lập tuyến tính tối đa của ma trận. Hoặc đơn giản nhất, hạng của ma trận là số vector hàng khác vector không khi đưa ma trận về dạng bậc thang.

**numpy** hỗ trợ hàm `numpy.linalg.matrix_rank()` để tính hạng của ma trận.

### Định thức

{: .box-note}
**Định thức** là ....

**numpy** hỗ trợ hàm `numpy.det()` để tính định của ma trận.

### Chuẩn ma trận

{: .box-note}
*Chuẩn của ma trận* là một đại lượng cho biết khoảng cách giữa 2 điểm trong không gian n chiều. Chúng được sử dụng thường xuyên trong các bài toán machine learning.

- Trong không gian một chiều, tức đường thẳng, khoảng cách giữa hai điểm là trị tuyệt đối của hiệu giữa hai điểm đó. Ta gọi khoảng cách đấy là norm 1.
- Trong không gian hai chiều, tức mặt phẳng, khoảng cách giữa hai điểm là độ dài của vector tạo bởi hai điểm đó. Ta gọi khoảng cách đấy là norm 2 hay Euclid norm.

**numpy** hỗ trợ hàm `numpy.linalg.norm()` để tính norm của ma trận.

### Vector riêng, trị riêng

Chưa viết

