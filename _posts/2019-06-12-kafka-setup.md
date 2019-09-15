---
layout: post
title: Cài đặt Apache Kafka
subtitle: Hướng dẫn cài Kafka trên Ubuntu
tags: [kafka]
comments: true
---

Cài Kafka dễ lắm, mấy bạn nên lên trang chủ Kafka coi trước nha. Coi mà làm không được thì hẳn coi bài mình. Mà coi trang chủ mà làm không được chắc do máy bạn cài Java không đúng phiên bản Kafka yêu cầu thôi. Nếu không cài được thì các bạn comment bên dưới bài viết nha, mình sẽ hỗ trợ hết sức.

# Cài đặt Java Development Kit

Vì kafka cần Java Runtime Enviroment (JRE) để chạy, nên chúng ta sẽ cài đặt **OpenJDK**. Ở bài viết này, mình cài phiên bản **1.8**, để cài đặt ta gõ lệnh sau :

```
sudo apt install openjdk-8-jdk
```

Để kiểm tra việc cài đặt OpenJDK thành công hay chưa ta gõ lệnh `java -version`. Nếu output terminal tương tự như sau thì ta thành công.

```
openjdk version "1.8.0_212"
OpenJDK Runtime Environment (build 1.8.0_212-8u212-b03-0ubuntu1.18.04.1-b03)
OpenJDK 64-Bit Server VM (build 25.212-b03, mixed mode)
```
# Đặt biến môi trường cho JAVA

Đầu tiên ta tìm thư mục chứa OpenJDK ta vừa cài bằng lệnh 

```
$(dirname $(dirname $(readlink -f $(which javac))))
```
 
Ta được đường dẫn  `/usr/lib/jvm/java-8-openjdk-amd64/`

Để gán biến môi trường, ta chỉ đơn giản thêm dòng sau vào cuối file `~/.bashrc` :

```
export JAVA_HOME="/usr/lib/jvm/java-8-openjdk-amd64/"
```

Để kiểm tra việc cài biến môi trường thành công hay chưa ? Ta tải lại(reload) file `.bashrc` bằng lệnh `. ~/.bashrc`. Bây giờ ta in ra biến môi trường bằng lệnh `echo $JAVA_HOME` nếu output terminal tương tự như sau thì ta thành công.

```
/usr/lib/jvm/java-8-openjdk-amd64/
```

# Tải về công cụ Apache Kafka

Ở bài viết này mình sẽ tải **Apache Kafka 2.2.0** sử dựng **Scala 2.1.2**

```
wget http://mirrors.viethosting.com/apache/kafka/2.2.0/kafka_2.12-2.2.0.tgz
```

Ta gia nén file vừa tải về, bạn có thể chuyển thư mục vừa giải nén vào vị trí tùy ý. Mình đặt nó và `~/server/`

```
tar -zxvf kafka_2.12-2.2.0.tgz 
```

# Cài biến môi trường cho Kafka

Tương tự như cài biến môi trường cho JAVA, ta chỉ đơn giản thêm dòng sau vào cuối file `~/.bashrc` 

```
export KAFKA_HOME="/root/server/kafka_2.12-2.2.0/"
```
Địa chỉ thư mục có thể thay đổi tùy theo máy. Để kiểm tra việc cài biến môi trường thành công hay chưa ? Ta tải lại(reload) file `.bashrc` bằng lệnh `. ~/.bashrc`. Bây giờ ta in ra biến môi trường bằng lệnh `echo $KAFKA_HOME` nếu output terminal tương tự như sau thì ta thành công.

```
/root/server/kafka_2.12-2.2.0/
```

# Tài liệu tham khảo
1. [Tutorial Point](https://www.tutorialspoint.com/apache_kafka/apache_kafka_installation_steps.htm)
2. [Apache Kafka](https://kafka.apache.org/quickstart)
