# RKVM - Ubuntu 22.04 VM Setup

Script tự động tạo và chạy Ubuntu 22.04 Virtual Machine với QEMU/KVM.

## Tính năng

- Tự động tải Ubuntu 22.04 cloud image
- Cấu hình cloud-init với user/password sẵn
- Hỗ trợ cả chế độ Console và GUI
- SSH port forwarding (port 24)

## Yêu cầu

- Linux với KVM support (hoặc QEMU trên Windows/Mac)
- QEMU/KVM
- cloud-localds (cloud-utils)

## Cách sử dụng

### 1. Chế độ Console (mặc định - không có GUI)

```bash
bash vm.sh
```

**Thông tin đăng nhập:**
- Username: `root` hoặc `ubuntu`
- Password: `root` hoặc `ubuntu`

### 2. Chế độ GUI (có giao diện đồ họa)

Có 2 cách:

#### Cách 1: Sửa script (đơn giản)

Mở file `vm.sh`, tìm dòng:
```bash
GUI_MODE=false
```

Đổi thành:
```bash
GUI_MODE=true
```

Sau đó chạy:
```bash
bash vm.sh
```

Sau khi đăng nhập vào VM, cài desktop environment:
```bash
apt update
apt install -y ubuntu-desktop-minimal
# Hoặc nhẹ hơn:
apt install -y xfce4 xfce4-goodies
```

Khởi động lại VM và bạn sẽ thấy giao diện desktop.

#### Cách 2: Dùng script riêng (vm-gui.sh)

```bash
bash vm-gui.sh
```

## Cấu hình

Có thể chỉnh sửa các thông số trong script:

- `MEMORY`: RAM (mặc định: 32768 = 32GB)
- `CPUS`: Số CPU cores (mặc định: 8)
- `SSH_PORT`: Port SSH forwarding (mặc định: 24)
- `DISK_SIZE`: Dung lượng ổ cứng (mặc định: 100G)
- `GUI_MODE`: Bật/tắt GUI (mặc định: false)

## SSH vào VM

Sau khi VM chạy, bạn có thể SSH vào từ máy host:

```bash
ssh -p 24 root@localhost
# hoặc
ssh -p 24 ubuntu@localhost
```

Password: `root` hoặc `ubuntu`

## Lưu ý

- Lần đầu chạy sẽ mất thời gian để tải image (~600MB)
- Đợi 1-2 phút sau khi VM boot để cloud-init hoàn tất
- Để có GUI, cần cài desktop environment sau khi vào VM (mất 10-20 phút)
- VM files được lưu tại `~/vm` (hoặc `~/vm-gui` cho GUI mode)

## Troubleshooting

**Login incorrect?**
- Đợi thêm 1-2 phút để cloud-init hoàn tất
- Đảm bảo nhập đúng: username `root`/`ubuntu`, password `root`/`ubuntu`
- Caps Lock phải tắt

**Không thấy GUI?**
- Đảm bảo đã set `GUI_MODE=true`
- Đã cài desktop environment trong VM chưa?
- Thử khởi động lại VM

