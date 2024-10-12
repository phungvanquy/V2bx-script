## Mô tả chức năng

- Tự động cài đặt v2bx trên **nhiều** VPS (node) để kết nối với hệ thống v2board.

## Quy trình hoạt động

- Sử dụng một máy **Control Center** (Ansible host) để quản lý và thực thi các lệnh cài đặt v2bx qua SSH trên các node từ xa (VPS).

## Hướng dẫn sử dụng

### 1. Chuẩn bị môi trường

- Tạo một VPS với hệ điều hành **Ubuntu 22.04** hoặc cao hơn.
- Clone repo từ GitHub về VPS.

### 2. Cài đặt Ansible

Chạy lệnh sau để cài đặt Ansible:

```bash
sudo apt update
sudo apt install ansible
```

### 3. Cấu hình thông số chung

- Tạo file `vars.yaml` và cấu hình các thông số cần thiết như sau:

```yaml
cloudflare_api_token: <cloudflare_api_token để tự động tạo DNS>
V2BOARD_PANEL_URL: <URL của panel v2board>
V2BOARD_API_KEY: <API key để v2bx kết nối với v2board>
```

### 4. Khai báo thông tin các node

- Tạo file `inventory.ini` để khai báo thông tin các node cần cài đặt v2bx. Ví dụ:

```ini
[v2bx_hosts]
<node_name_1> ansible_host=<node1_ip> ansible_user=root ansible_password=<node1_password> dns_record=<dns_record> dns_zone=<dns_zone> NODE_ID=<node_id trong v2board> PROTOCOL_TYPE="hysteria"
<node_name_2> ansible_host=<node2_ip> ansible_user=root ansible_password=<node2_password> dns_record=<dns_record> dns_zone=<dns_zone> NODE_ID=<node_id trong v2board> PROTOCOL_TYPE="vless"
```

### 5. Cài đặt v2bx

Chạy lệnh cài đặt v2bx trên các node:

```bash
make install
```

Với các bước trên, bạn có thể tự động triển khai v2bx trên nhiều VPS một cách nhanh chóng và dễ dàng.