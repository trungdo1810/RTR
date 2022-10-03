# Wired Communication
- Parallel: số dây = số tín hiệu truyền đi, dùng cho các thiết bị yêu cầu tốc độ truyền tải dữ liệu nhanh như tivi. Ưu điểm: tốc độ dữ liệu truyền nhanh; nhược điểm:cần nhiều dây, nhiều chân in/out=> kích thước thiết bị lớn  
- Serial: truyền tín hiệu nối tiếp. Nhược điểm: giao thức giữa 2 thiết bị A và B phức tạp hơn; cụ thể: 
    vd A truyền dữ liệu cho B
    - speed => tốc độ truyền của A và tốc độ nhận của B phải đồng bộ.
    - timing - thời điểm đọc của B   
    => Cần đồng bộ về tốc độ truyền nhận và nhận thời điểm đọc dữ liệu 
## **Serial Communication Protocols**  

- [SPI](#SPI)
- [I2C](#I2C)
- [UART](#UART)
- [CANBus](#CANBus)
<detail>
## **1. SPI**<a name = "SPI"></a>
### **1.1.Lý thuyết chung**  
- SPI - Serial Peripheral Interface(giao diện ngoại vi nối tiếp) được phát triển bởi hãng Motorola.

***Cấu tạo:***
- Sử dụng **4** dây giao tiếp:  

<div align="center">
    <img src="https://deviot.vn/storage/deviot/Giao%20tiep%20SPI%202.png" width="80%">

</div> 
   
    - SCK(Serial Clock): Master tạo xung SCK cung cấp cho Slave. Chức năng: giữ nhịp cho giao tiếp SPI

    - MISO(Master Input Slave Output): Tín hiệu Slave truyền đi và Master nhận

    - MOSI(Master Output Slave Input): Tín hiệu Master truyền đi và Slave nhận.

    - SS(Slave Select)/CS(Chip Select): Chọn thiết bị Slave cụ thể để giao tiếp. Để chọn Slave thì Master chủ động kéo chận SS xuống 0(LOW)  

***Các chế độ hoạt động:***  
Tín hiệu xung clock trong SPI có thể đồng bộ hóa bằng cách sử dụng các thuộc tính của cực(Clock Polarity) và pha(Clock Phase) của xung clock.    
- Clock Polarity: cho phép các bit được xuất ra và lấy mẫu trên cạnh lên hoặc xuống của chu kì clock.

- Clock Phase: có thể được đặt để đầu ra và lấy mẫu xảy ra trên cạnh đầu tiên hoặc cạnh thứ hai của chu kỳ đồng hồ, bất kể nó tăng hay giảm

<div align="center">
    <img src="https://kysungheo.com/wp-content/uploads/2021/11/SPI_5-300x163.png" width="80%">

</div> 

### **1.2. Cách hoạt động của giao tiếp SPI**  


### **1.3. Ưu và nhược điểm**
- **Pros** (ưu điểm)
    - Không có Start bit và Stop bit như I2C và UART. Vì vậy dữ liệu có thể được truyền liên tục mà không bị gián đoạn
    - Không có hệ thống định địa chỉ slave phức tạp như I2C
    - Tốc độ truyền dữ liệu cao hơn I2C (nhanh gần gấp đôi)
    - Các dòng MISO và MOSI riêng biệt, vì vậy dữ liệu có thể được gửi và nhận cùng một lúc

- **Cons** (nhược điểm)
    - Sử dụng bốn dây (I2C và UART sử dụng hai dây).
    - Không xác nhận rằng dữ liệu đã được nhận thành công.
    - Không có hình thức kiểm tra lỗi như bit chẵn lẻ (Parity bit) như trong UART.
    - Chỉ cho phép một master duy nhất.

</detail>

## **1. I2C**<a name = "I2C"></a>
### **1.1. Lý thuyết chung**  
### **1.2. Cách hoạt động của giao tiếp I2C**  
### **1.3. Ưu và nhược điểm**

## **1. UART**<a name = "UART"></a>
### **1.1. Lý thuyết chung**  
### **1.2. Cách hoạt động của giao tiếp UART**  
### **1.3. Ưu và nhược điểm**

## **1. CANBus**<a name = "CANBus"></a>
### **1.1. Lý thuyết chung**  
### **1.2. Cách hoạt động của giao tiếp CANBus**  
### **1.3. Ưu và nhược điểm**