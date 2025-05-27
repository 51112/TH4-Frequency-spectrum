# TH5-Frequency-spectrum
# Phân tích Tần số Tiêu thụ Điện năng Hộ gia đình theo Chu kỳ Ngày/Tuần

## 📋 Thông tin dự án

- **Tên dự án:** Phân tích tần số tiêu thụ điện năng hộ gia đình theo chu kỳ ngày/tuần
- **Sinh viên:** Nguyễn Đức Anh
- **Mã số sinh viên:** 2151264640
- **Đề bài:** 1 - Phân tích tần số tiêu thụ điện năng hộ gia đình theo chu kỳ ngày/tuần

## 🎯 Mục tiêu

Sử dụng biến đổi Fourier nhanh (FFT) để phân tích các mẫu chu kỳ trong tiêu thụ điện năng của hộ gia đình, bao gồm:
- Xác định chu kỳ tiêu thụ điện chính (24 giờ, 168 giờ)
- Phân tích phổ tần số để hiểu hành vi tiêu thụ
- Tìm giờ cao điểm tiêu thụ điện trong ngày
- Đánh giá mức độ ảnh hưởng của các chu kỳ khác nhau

## 📊 Dữ liệu

### Nguồn dữ liệu
- **File:** `household_power_consumption.csv`
- **Nguồn:** Individual household electric power consumption Data Set
- **Thời gian:** Dữ liệu thu thập liên tục trong nhiều năm

### Cấu trúc dữ liệu

| Cột | Mô tả | Đơn vị |
|-----|-------|--------|
| `Date` | Ngày quan sát | dd/mm/yyyy |
| `Time` | Thời gian quan sát | hh:mm:ss |
| `Global_active_power` | Tổng công suất hoạt động | kilowatts |
| `Global_reactive_power` | Tổng công suất phản kháng | kilowatts |
| `Voltage` | Điện áp | volts |
| `Global_intensity` | Cường độ dòng điện | ampere |
| `Sub_metering_1` | Công suất nhà bếp | kilowatts |
| `Sub_metering_2` | Công suất phòng giặt | kilowatts |
| `Sub_metering_3` | Công suất điều hòa & nước nóng | kilowatts |

## 🛠️ Cài đặt và Chạy

### Yêu cầu hệ thống
```
Python 3.7+
```

### Thư viện cần thiết
```bash
pip install pandas numpy matplotlib scipy
```

### Chạy phân tích
```bash
python analysis.py
```




## 🔬 Phương pháp phân tích

### 1. Tiền xử lý dữ liệu
- Kết hợp cột Date và Time thành datetime index
- Xử lý giá trị thiếu (thay thế bằng 0)
- Resampling dữ liệu theo giờ

### 2. Biến đổi Fourier nhanh (FFT)
```python
# Áp dụng FFT cho chuỗi thời gian công suất
yf = fft(x)
xf = fftfreq(N, T)[:N // 2]
amps = 2.0 / N * np.abs(yf[0:N // 2])
amps[0] = 0  # Loại bỏ thành phần DC
```

### 3. Phân tích chu kỳ
- **Chu kỳ ngày:** Tần số 1/24 Hz (24 giờ)
- **Chu kỳ tuần:** Tần số 1/168 Hz (168 giờ)
- **Chu kỳ dominance:** Tần số có biên độ cao nhất

## 📈 Kết quả chính

### Phát hiện chu kỳ
- ✅ Chu kỳ 24 giờ: Phản ánh hoạt động sinh hoạt hàng ngày
- ✅ Chu kỳ 168 giờ: Thể hiện sự khác biệt ngày thường/cuối tuần
- ✅ Chu kỳ dominance: Xác định mẫu tiêu thụ quan trọng nhất

### Phân tích theo giờ
- **Giờ thấp điểm:** 2:00-6:00 (đêm khuya, sáng sớm)
- **Giờ cao điểm:** 19:00-21:00 (buổi tối, về nhà)
- **Xu hướng:** Tăng dần từ 6:00, giảm dần từ 22:00

## 📊 Visualization

### 1. Phổ tần số - Chu kỳ ngày
```python
plt.axvline(x=1/24, color='r', linestyle='--', label='Chu kỳ ngày (24h)')
```

### 2. Phổ tần số - Chu kỳ tuần
```python
plt.axvline(x=1/168, color='g', linestyle='--', label='Chu kỳ tuần (168h)')
```

### 3. Tiêu thụ trung bình theo giờ
```python
avg_power_by_hour.plot(kind='bar', color='orange')
```

## 🎯 Ứng dụng thực tiễn

### Quản lý lưới điện
- Dự báo tải điện theo chu kỳ
- Lập kế hoạch bảo trì thiết bị
- Tối ưu hóa phân phối điện năng

### Chính sách năng lượng
- Thiết kế biểu giá điện theo giờ
- Khuyến khích tiết kiệm điện giờ cao điểm
- Phát triển chương trình quản lý nhu cầu

## 🔍 Kết quả mẫu

```
Biên độ tại chu kỳ ngày (24h): 0.3456
Biên độ tại chu kỳ tuần (168h): 0.1234
Chu kỳ chiếm ưu thế trong dữ liệu: 24.00 giờ
Giờ tiêu thụ điện cao nhất trung bình: 19:00
```

## 🚀 Hướng phát triển

### Cải tiến phân tích
- [ ] Tích hợp yếu tố thời tiết
- [ ] Phân tích theo mùa
- [ ] Mở rộng chu kỳ phân tích (tháng, năm)

### Mô hình dự báo
- [ ] Sử dụng kết quả FFT cho dự báo
- [ ] Kết hợp với machine learning
- [ ] Phát triển ứng dụng real-time

### Mở rộng quy mô
- [ ] Phân tích nhiều hộ gia đình
- [ ] So sánh các khu vực địa lý
- [ ] Tích hợp với IoT và smart grid

## 📝 License

Dự án này được phát triển cho mục đích học tập và nghiên cứu.

## 🙏 Acknowledgments

- Cảm ơn bộ dữ liệu Individual household electric power consumption
- Sử dụng các thư viện mã nguồn mở: pandas, numpy, matplotlib, scipy
- Tham khảo phương pháp phân tích tín hiệu số

---

*Cập nhật lần cuối: [Ngày hiện tại]*
