# Kafka + ELK Stack trên MacBook (Apple Silicon - M1/M2/M3)

##  Giới thiệu

Dự án này cung cấp môi trường **Kafka + ELK Stack (Elasticsearch, Logstash, Kibana)** được cấu hình sẵn bằng **Docker Compose**, tối ưu cho **MacBook sử dụng Apple Silicon (M1/M2/M3)**.

Mục tiêu:

* Xây dựng pipeline xử lý log & event real-time
* Streaming dữ liệu qua Kafka
* Phân tích và visualize dữ liệu bằng Kibana
* Phù hợp cho học tập, demo và phát triển hệ thống microservices

---

##  Kiến trúc hệ thống

```text
Producer → Kafka → Logstash → Elasticsearch → Kibana
```

* **Producer**: gửi log/event vào Kafka
* **Kafka**: message broker xử lý streaming
* **Logstash**: consume từ Kafka, transform dữ liệu
* **Elasticsearch**: lưu trữ & index dữ liệu
* **Kibana**: visualize & dashboard

---

##  Công nghệ sử dụng

* Kafka + Zookeeper
* Elasticsearch
* Logstash
* Kibana
* Docker & Docker Compose

---

##  Tương thích Apple Silicon

Dự án được cấu hình để chạy ổn định trên:

* MacBook M1 / M2 / M3

Lưu ý:

* Sử dụng image hỗ trợ `arm64`
* Tránh image chỉ hỗ trợ `amd64`

---

##  Yêu cầu hệ thống

* Docker Desktop (>= 4.x)
* RAM khuyến nghị: **8GB+**
* Disk trống: **10GB+**

---

##  Hướng dẫn cài đặt & chạy

### 1️ Clone project

```bash
git clone <your-repo>
cd <project-folder>
```

---

### 2️ Khởi động hệ thống

```bash
docker-compose up -d
```

---

### 3️ Kiểm tra service

* Kafka: `localhost:9092`
* Elasticsearch: http://localhost:9200
* Kibana: http://localhost:5601

---

##  Sử dụng

###  Gửi message vào Kafka

Bạn có thể dùng CLI:

```bash
docker exec -it kafka kafka-console-producer \
--broker-list localhost:9092 \
--topic test-topic
```

---

###  Consume message

```bash
docker exec -it kafka kafka-console-consumer \
--bootstrap-server localhost:9092 \
--topic test-topic \
--from-beginning
```

---

### Logstash Pipeline

Logstash sẽ:

* Consume từ Kafka topic
* Parse dữ liệu
* Đẩy vào Elasticsearch

---

### Kibana Dashboard

Truy cập:
👉 http://localhost:5601

* Tạo index pattern
* Xem log real-time
* Build dashboard

---

## 📁 Cấu trúc project

```text
.
├── docker-compose.yml
├── logstash/
│   └── pipeline.conf
├── kafka/
│   └── config
└── README.md
```

---

##  Lưu ý quan trọng

* Elasticsearch cần nhiều RAM → nếu lỗi, tăng memory Docker
* Nếu Kafka không start:

  * kiểm tra port 9092
  * kiểm tra Zookeeper
* Mac M1 cần image hỗ trợ `arm64`

---

## Test nhanh hệ thống

1. Start docker-compose
2. Gửi message vào Kafka
3. Kiểm tra Logstash log
4. Xem dữ liệu trong Kibana

---

## Hướng phát triển

* Thêm schema registry (Avro)
* Thêm monitoring (Prometheus + Grafana)
* Scale Kafka cluster
* Tích hợp microservices

