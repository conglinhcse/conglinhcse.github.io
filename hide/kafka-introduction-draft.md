---
layout: post
title: Giới thiệu Apache Kafka
subtitle: Apache Kafka là gì ?
tags: [kafka]
comments: true
---

Trong big data, chúng ta phải làm việc với một khối lượng dữ liệu khổng lồ. Thách thức được đặt ra như sau :
1. Làm thế nào để thu thập được khối dữ liệu lớn.
2. Làm thế nào để phân tích dữ liệu thu thập được.

Một cách để vượt qua hai thách thức trên đó là chúng ta cần sử dụng **messaging system**.

# Messaging system là gì ?

Messaging system chịu trách nhiệm truyền dữ liệu từ ứng dụng này sang ứng dụng khác, nhờ đó ứng dụng chỉ cần tập trung vào dữ liệu mà không cần lo lắng về cách chia sẽ dữ liệu. Có 2 loại messaging system là **Point to Point** và **Public - Subscribe**.

Giải thích key word được dùng:
- Message là một mảng dữ liệu(byte array), ta có thể lưu dưới nhiều định dạng.
- Consumer có thể là bất kì ứng dụng nào lấy dữ liệu ra để sử dụng.
- Queue là cấu trúc dữ liệu để chứa các message, tuân theo quy tắc [FIFO](https://en.wikipedia.org/wiki/FIFO_(computing_and_electronics)).

## Point to Point Messaging System

Trong point to point system, message sẽ được đặt bên trong queue. Một hoặc nhiều consumer có thể lấy message trong queue, nhưng một message chỉ có thể lấy bởi tối đa một consumer. Khi consumer lấy message thì nó sẽ bị xóa khỏi queue.

![](/img/kafka/example-point-to-point-system.png)

Ví dụ cho hệ thống này là một hệ thống xử lý đơn hàng. Các đơn hàng(message) sẽ được đặt bên trong queue. Hệ thống có thể có nhiều trình xử lý đơn hàng(consumer), nhưng mỗi đơn hàng(message) chỉ được xử lý bởi tối đa 1 trình xử lý đơn hàng(consumer). Và đơn hàng sẽ bị xóa khi xử lý xong.

## Publish-Subscribe Messaging System

Trong publish-subscribe system, các message được duy trình trong 1 topic. Không giống như point to point system, các consumer có thể subcribe 1 hoặc nhiều topic, và lấy tất cả các message trong topic đó.

![](/img/kafka/example-pub-sub-system.png)

Ví dụ cho hệ thống này là hệ thống phân phối video(như youtube). Người dùng(consumer) có thể subscribe nhiều kênh(topic) khác nhau để theo dõi. Và có thể xem bất cứ video(message) của kênh(topic) đã subscribe.

# Apache Kafka là gì ?

Kafka là một hệ thống truyền dữ liệu phân tán (distributed messaging system) sử dụng mô hình publish-subscribe. Kafka  có khả năng truyền một lượng lớn dữ liệu trong thời gian thực, trong trường hợp bên nhận chưa nhận dữ liệu thì dữ liệu vẫn được sao lưu trên một hàng đợi và cả trên ổ đĩa để bảo đảm an toàn. Kafka được xây dựng dựa trên ZooKeeper nên nó tích hợp rất tốt với Apache Storm và Spark để phân tích dữ liệu liên tục theo thời gian thực.

## Cấu trúc của Apache Kafka

![](/img/kafka/kafka-architechture-detail.png)

Apache Kafka gồm các thành phần cơ bản sau :

- **Consumer** là bất kì ứng dụng nào có chức năng subscribe vào một hoặc nhiều topic và lấy các message ra sử dụng.

- **Producer** là bất kì ứng dụng nào có chức năng publish message vào một hoặc nhiều topic.

- **Message** là byte array và developer có thể sử dụng chúng để lưu bất kì object với bất kì format nào - thông thường là String, JSON và Avro

- **Topic** là các stream data có chung thuộc tính. Một topic được chia thành các partition, lưu trên các broker khác nhau.

- **Partition** là chuỗi tuyến tính các message được lưu theo một thứ tự không đổi, trong đó mỗi message được xác định bởi chỉ mục của chúng(gọi là offset).

- **Broker** là một hệ thống chịu trách nhiệm duy trình các message được publish. Mỗi broker chứa 1 một hoặc nhiều các partition của topic.

- **Zookeeper** là một dịch vụ cấu hình và đồng bộ hóa phân tán, đóng vai trò là giao diện phối hợp giữa các broker và consumer, Kafka server chia sẽ thông tin thông qua kafka cluster. Kafka lưu các metadata trong Zookeeper như các thông tin về topics, brokers, consumer offset(queue reader)...

# Tài liệu tham khảo
1. [Tutorial Point](https://www.tutorialspoint.com/apache_kafka)
2. [Apache Kafka](https://kafka.apache.org/intro)