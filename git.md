# Gitflow

Cơ bản về kỹ thuật Gitflow, giúp quản lý code của team, review code và triển khai build automatic

Tham khảo:
- `https://www.conventionalcommits.org/en/v1.0.0/`
- `https://github.com/semantic-release/semantic-release`
- `https://iamchuka.com/gitflow-workflow-continuous-integration-continu/`

## Định nghĩa các loại branch

### Master

Nơi chứa các version cho môi trường production, đã qua được bước kiểm tra

Các version sẽ được gắn tag cụ thể

Chỉ được merge từ các nhánh release, hotfix

Các developer không sử dụng nhánh này

### Develop

Nơi tất cả các nhánh feature đã được merge vào

Trước khi merge vào nhánh này, các feature cần được đảm bảo đã pull bản mới nhất của nhánh cần merge, được test kỹ lưỡng

Sau khi build thành công nhánh này sẽ được deploy đến môi trường test

### Release

Tại nhánh develop, ta sẽ tạo ra nhánh release để sẵn sàng đưa vào production

Một số công việc sẽ thực hiện ở nhánh này: version, cleanup,...

Nhánh này được gắn tag (có k nhỉ?) và sau đó merge đến cả master và develop

### Feature

Cú pháp feature/ten_chuc_nang

Khi có một task, developer sẽ tạo một nhánh feature mới

Sau khi hoàn thành task cần gửi một Pull request đến nhánh develop, lúc này sẽ có người xử lý review code,... và merge vào nhánh develop

Trước khi gửi Pull request vào develop:

- Cần lấy bản mới nhất của develop vào feature này
- Test lại bằng unit test
- Push nhánh feature này
- Gửi pull request đến nhánh develop và chờ được review code

## Commit message

Cú pháp:

```text

<type>(scope tùy chọn): <description>
<body tùy chọn>
<footer(s) tùy chọn>

```

```text
Ví dụ: 
feat(language): add language

```

```text
Ví dụ: 
fix: correct minor typos in code

see the issue for details

on typos fixed.

Reviewed-by: Z
Refs #133

```

### type

- fix: pull request này thực hiện fix bug của dự án
- feature: pull request này thực hiện một chức năng mới của dự án
- refactor: pull request này thực hiện refactor lại code hiện tại của dự án (refactor hiểu đơn giản là việc "làm sạch" code, loại bỏ code smells, mà không làm thay đổi chức năng hiện có)
- docs: pull request này thực hiện thêm/sửa đổi document của dự án
- style: pull request này thực hiện thay đổi UI của dự án mà không ảnh hưởng đến logic.
- performance: pull request này thực hiện cải thiện hiệu năng của dự án (VD: loại bỏ duplicate query, ...)
- vendor: pull request này thực hiện cập nhật phiên bản cho các packages, dependencies mà dự án đang sử dụng.
- chore: từ này dịch ra tiếng Việt là việc lặt vặt nên mình đoán là nó để chỉ những thay đổi không đáng kể trong code (ví dụ như thay đổi text chẳng hạn), vì mình cũng ít khi sử dụng type này

### scope

Phạm vi ảnh hưởng đến đâu

### description

Mô tả khá quát, ngắn gọn về những thay đổi được thực hiện trong pull request

### body

Mô tả chi tiết bổ sung cho phần description

Cách description bởi 1 dòng trắng

Không giới hạn về số dòng

### footer

Chứa các thông tin mở rộng của pull request ví dụ như là danh sách người review, link/id của các pull request có liên quan

Nếu có nhiều footer thì mỗi footer phải chứa một word token là `:<space>` hoặc `<space>#`

### BREAKING CHANGE

Nếu sự thay đổi code trong pull request làm thay đổi lớn khiến cho nó không còn tương thích với phiên bản trước nữa thì sẽ phải đánh dấu pull request này là BREAKING CHANGE

