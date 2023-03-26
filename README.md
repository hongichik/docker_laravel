# Tài liệu build Docker cho Laravel và ReactJS

## Cấu trúc thư mục

- `backend`: chứa mã nguồn Laravel
- `frontend`: chứa mã nguồn ReactJS
- `docker`: chứa thông tin cấu hình Docker
    - `BE_nginx`, `FE_nginx`: thư mục chứa khóa cho HTTP và HTTPS
        - `cert.pem`, `key.pem`: khóa cho HTTP, HTTPS
        - `env.conf`: chứa mật khẩu cấu hình
    - `nginx`: chứa cấu hình Nginx chung
        - `log`: thư mục chứa log
        - `nginx.conf`: chứa cấu hình cho `backend` và `frontend`
    - `mysql`: chứa cấu hình MySQL và cơ sở dữ liệu MySQL
        - `db`: thư mục chứa cơ sở dữ liệu MySQL
        - `mysql.cnf`: chứa cấu hình MySQL
    - `redis`: chứa cơ sở dữ liệu Redis
    - `php`: chứa cấu hình PHP cho Laravel
        - `Dockerfile`: chứa cấu hình hình ảnh PHP
        - `php.ini`: chứa cấu hình PHP
    - `.env`: chứa cấu hình cơ sở dữ liệu MySQL và tên dự án
## truy cập vào thư mục wsl
- cho `\\wsl$` vào đường dẫn thư mục
>\\wsl$
## Cấu hình cơ bản

### Cấp quyền cho PHP truy cập vào thư mục `storage` trong PHP

- Đầu tiên, chạy lệnh `docker-compose up` từ thư mục `docker`
- Cấp quyền `777` cho thư mục `storage`. Nếu không cấp quyền, sẽ báo lỗi không thể lưu log
- Truy cập vào container của `php`

  > docker exec -it BE_php_(tên được cấu hình trong `.env`) /bin/bash

- Cấp quyền cho thư mục

  > chmod -R 777 storage

### Các lệnh sử dụng Docker cơ bản

- Chạy Docker

  > docker-compose up

- Xóa tất cả container

  > docker rm -f $(docker ps -aq)

- Xóa hết image không sử dụng

  > docker image prune -a

- Liệt kê container đang chạy

  > docker ps

- Liệt kê tất cả container, bao gồm cả đang chạy và không

  > docker ps -a

- Xóa 1 container. Thêm `-f` để xóa kể cả khi container đang chạy

  > docker rm my_container

  > docker rm 1234567890ab

  > docker rm -f my_container

  > docker rm -f 1234567890ab

- Dừng container

  > docker stop my-container

- Chạy 1 container

  > docker start <container-id>

- Liệt kê các image
    >docker images
- Xóa 1 image
    >docker rmi <image-id>
- Vô 1 container để thao tác
    >docker exec -it (id container) /bin/bash
- Chạy cmd và giải phóng cmd (dùng để chạy ngầm)
    >docker exec -itd (name container) (lệnh cmd)


### Lệnh chạy laravel artisan 
>php artisan serve --host=0.0.0.0 --port=8000

### ubuntu xóa thư mục
>rm -r (đường dẫn file)
