# Bài tập số 5

# Đặc tả yêu cầu

## Yêu cầu kiến thức

- Làm quen với trình quản lý ảo hóa nổi tiếng nhất: Kubernetes
- Hiểu rõ những khái niệm sau của Kubernetes: Cluster, Node, Deployment, Pod, Namespace, Service, Ingress.
- Hiểu về cách phân quyền cho các Service Account.
- Hiểu về các cơ chế vertical autoscale, horizontal autoscale và cluster autoscale.

## Yêu cầu kỹ năng

- Biết cách deploy ứng dụng lên Kubernetes (local).
- Sử dụng nhuần nhuyễn những command kubectl phổ biến: get, top, logs, exec

# Đề bài

## Yêu cầu đề bài

1. Tạo một cluster local, có thể sử dụng Kind (hoặc Minikube)
2. Deploy ứng dụng web đếm số lượng truy cập ở tuần 2 lên Kind bằng cách viết những file config cần thiết như ConfigMap, Secret, Deployment, Service, Ingress
3. Config Nginx vẫn giữ nguyên

## Thời gian làm bài: 14 ngày

## Yêu cầu bài làm

- Đối với project:
    - Sau khi deploy, kết quả cuối cùng không thay đổi
    - Push bài tập lên Gitlab, sử dụng Git Terminal **(không sử dụng Git Desktop)**

## Yêu cầu và hướng dẫn nộp bài

- Sử dụng Gitlab để lưu trữ bài tập
    - Tạo 1 private group trên [Gitlab](https://gitlab.com/) có tên `cs_<your_name>`, chẳng hạn `cs_nguyen_huu_trung`
    - Nếu tên group bị trùng thì thêm một chữ số theo thứ tự Alphabet phía sau, chẳng hạn `cs_nguyen_huu_trung_1`
    - Nếu group đã được tạo trước đó thì không cần tạo lại
    - Thêm member cho group: [@trungngh](https://www.notion.so/trungngh), @dangvu99 với role `Reporter`
    - Tạo 1 private project bên trong private group vừa được tạo, có tên `devops_week5`
    - Download [GIT client](https://git-scm.com/downloads/guis) và sử dụng nó để push kết quả bải tập lên Gitlab
    
- Thông báo hoàn thành bài tập và trao đổi với người hướng dẫn Vũ Hải Đăng theo địa chỉ email `dangvh@cystack.net`, CC cho anh **Nguyễn Hữu Trung** theo địa chỉ `trungnh@cystack.net` với tiêu đề là `HomeworkDevopsX-<Hoten>` (X là số thứ tự của tuần). Phần nội dung thư không để trống, có ghi một số thông tin vắn tắt liên quan. Ví dụ:

```
Chào anh,

Em là xxx, 
    
Bài tập tuần X đã được em push lên gitlab tại địa chỉ https://gitlab.com/cs_nguyen_huu_trung/weekX/
    
Rất mong nhận được sự phản hồi từ anh.
    
Em cảm ơn.
```

## Lưu ý

- Bài bị phát hiện copy từ người khác, không hiểu nội dung thì TTS sẽ chịu hình thức kỷ luật ở mức cao nhất.
- Mọi nguồn tham khảo đều phải được ghi chú rõ ràng trong báo cáo
- Bài nộp không theo chuẩn nêu trên sẽ không được công nhận.

# Tài liệu tham khảo

## Liên quan trực tiếp tới nội dung chính

### Lý thuyết

- [Kubernetes service account](https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/)

### Kỹ năng

- [Kubernetes for beginner with example](https://www.youtube.com/watch?v=s_o8dwzRlu4)
- [Kubernetes HPA](https://www.youtube.com/watch?v=FfDI08sgrYY)
- [Kubernetes VPA](https://www.youtube.com/watch?v=jcHQ5SKKTLM)
- [Kubernetes CA](https://www.youtube.com/watch?v=jM36M39MA3I)