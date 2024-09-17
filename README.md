# Kubernetes-Nvidia
![image](https://github.com/user-attachments/assets/210fbf5c-721b-43b2-93e9-4889f16d3de3)
Kubernetes Device Plugin dùng cho GPU
Hiện tại Kubernetes đang hỗ trợ việc quản lý các GPU (không chỉ Nvidia mà còn con cả AMD và Intel) thông qua các Device Plugin tuy vậy chúng sẽ không được cài đặt sẵn mà cần ta tự thực hiện thông qua việc cài đặt GPU driver và cấu hình device plugin tương ứng dựa trên hướng dẫn của bên sản xuất GPU. Khi đã cài đặt plugin thành công, cụm của ta sẽ hiển thị tài nguyên có thể lập lịch tùy chỉnh, chẳng hạn như amd.com/gpu hoặc nvidia.com/gpu. Sẽ có một chút lưu ý khi sử dụng chúng như sau:

Ta có thể chỉ định GPU limits mà không cần chỉ định requests vì Kubernetes sẽ sử dụng limits làm giá trị yêu cầu theo mặc định.
Ta có thể chỉ định GPU trong cả hai limits và requests nhưng hai giá trị này phải bằng nhau.
Ta không thể chỉ định GPU requests mà không chỉ định limits.
Khi đó một manifest mẫu được dùng để sử dụng GPU với một pod sẽ như sau:
apiVersion: v1
kind: Pod
metadata:
  name: example-vector-add
spec:
  restartPolicy: OnFailure
  containers:
    - name: example-vector-add
      image: "registry.example/example-vector-add:v42"
      resources:
        limits:
          gpu-vendor.example/example-gpu: 1 # requesting 1 GPU

