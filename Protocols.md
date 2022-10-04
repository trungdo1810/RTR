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

- tốc độ truyền: 32MHz; dây cable: 10(trong thực tế thì sử dụng < 1m vì khi truyền xung ck đi 1 quãng đường xa thì sẽ bị delay) 

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
- Clock Polarity(CPOL): dùng để chỉ trạng thái của chân SCK ở trạng thái nghỉ. Chân SCK giữ ở mức cao khi CPOL=1 hoặc mức thấp khi CPOL=0. 

- Clock Phase(CPHA): dùng để chỉ các mà dữ liệu được lấy mẫu theo xung. Dữ liệu sẽ được lấy ở cạnh lên của SCK khi CPHA=0 hoặc cạnh xuống khi CPHA=1.

<div align="center">
    <img src="https://kysungheo.com/wp-content/uploads/2021/11/SPI_5-300x163.png" width="80%">

</div> 

### **1.2. Cách hoạt động của giao tiếp SPI**  


### **1.3. Ưu và nhược điểm**
- **Pros** (ưu điểm)
    - Không có Start bit và Stop bit như I2C và UART. Vì vậy dữ liệu có thể được truyền liên tục mà không bị gián đoạn
    - Không có hệ thống định địa chỉ slave phức tạp như I2C
    - Tốc độ truyền dữ liệu cao hơn I2C (nhanh gần gấp đôi)
    - Các dây MISO và MOSI riêng biệt, vì vậy dữ liệu có thể được gửi và nhận cùng một lúc

- **Cons** (nhược điểm)
    - Sử dụng bốn dây (I2C và UART sử dụng hai dây).
    - Không xác nhận rằng dữ liệu đã được nhận thành công.
    - Không có hình thức kiểm tra lỗi như bit chẵn lẻ (Parity bit) như trong UART.
    - Chỉ cho phép một master duy nhất.

</detail>

## **1. I2C**<a name = "I2C"></a>
### **1.1. Lý thuyết chung**  
- Inter – Integrated Circuit,  là 1 giao thức giao tiếp nối tiếp đồng bộ được phát triển bởi Philips Semiconductors, inter-IC nghĩa là sử dụng để **truyền nhận dữ liệu giữa các IC với nhau**  sử dụng **2** dây.  
- tốc độ truyền: Có các chế độ
    - Standard: 100kHz
    - Fast: 400kHz
    - Fast++: 1MHz (ít thấy vì thường dùng trong các mạch pcb)
- Độ dài cab: 2.5m (thực tế dùng < 20cm)

<div align="center">
    <img src="https://deviot.vn/storage/deviot/Giao%20ti%E1%BA%BFp%20I2C%202.png" width="80%">
</div> 

***Cấu tạo:***
- I2C sử dụng 2 dây truyền tín hiệu:
    - SCL -  Serial Clock Line : Tạo xung nhịp đồng hồ do Master phát đi

    - SDA - Serial Data Line : Đường truyền nhận dữ liệu.

### **1.2. Cách hoạt động của giao tiếp I2C**  
- Hai đường bus SCL và SDA đều hoạt động ở chế độ Open Drain, nghĩa là bất cứ thiết bị nào kết nối với mạng I2C này cũng chỉ có thể kéo 2 đường bus này xuống mức 0 (LOW) - ban đầu 2 dây ở mức 1(HIGH).Lý do làm vậy: Vì để tránh trường hợp bus vừa bị 1 thiết bị kéo lên mức cao vừa bị 1 thiết bị khác kéo xuống mức thấp gây hiện tượng ngắn mạch.

<div align="center">
    <img src="https://camo.githubusercontent.com/99406d56dcc5bd6596d26a2382b508ba594b3f0d742f87d9b28078a66621e791/68747470733a2f2f692e737461636b2e696d6775722e636f6d2f42324f36332e706e67" width="80%">
</div> 

***Khung truyền I2C*** 

<div align="center">
    <img src="https://deviot.vn/storage/deviot/Giao%20ti%E1%BA%BFp%20I2C%203.png" width="80%">
</div> 

-  Khối bit địa chỉ: Thông thường quá trình truyền nhận sẽ diễn ra với rất nhiều thiết bị, IC với nhau. Do đó để phân biệt các thiết bị này, chúng sẽ được gắn 1 địa chỉ  7 bit hoặc 9 bit

<div align="center">
    <img src="https://deviot.vn/storage/deviot/Giao%20ti%E1%BA%BFp%20I2C%204.png" width="80%">
</div> 

- Bit Read/Write: Bit này dùng để xác định quá trình là truyền hay nhận dữ liệu từ thiết bị Master. Nếu Master gửi dữ liệu đi thì ứng với bit này bằng ‘0’, và ngược lại, nhận dữ liệu khi bit này bằng ‘1’.

- Bit ACK/NACK: Viết tắt của Acknowledged / Not Acknowledged. Dùng để so sánh bit địa chỉ vật lý của thiết bị so với địa chỉ được gửi tới. Nếu trùng thì Slave sẽ được đặt bằng ‘0’ và ngược lại, nếu không thì mặc định bằng ‘1’.

- Khối bit dữ liệu: Gồm 8 bit và được thiết lập bởi thiết bị gửi truyền đến thiết bị nhận. Sau khi các bit này được gửi đi, lập tức 1 bit ACK/NACK được gửi ngay theo sau để xác nhận rằng thiết bị nhận đã nhận được dữ liệu thành công hay chưa. Nếu nhận thành công thì bit ACK/NACK được set bằng ‘0’ và ngược lại.

***Quá trình truyền nhận dữ liệu:*** 
- Bắt đầu: Thiết bị Master sẽ gửi đi 1 xung Start bằng cách kéo lần lượt các đường SDA, SCL từ mức 1 xuống 0 để thông báo với các thiết bị khác là sắp có tín hiệu truyền đi.
- Tiếp theo đó, Master gửi đi 7 bit địa chỉ tới Slave muốn giao tiếp cùng với bit Read/Write.
- Slave sẽ so sánh địa chỉ vật lý với địa chỉ vừa được gửi tới. Nếu trùng khớp, Slave sẽ xác nhận bằng cách kéo đường SDA xuống 0 và set bit ACK/NACK bằng ‘0’. Nếu không trùng khớp thì SDA và bit ACK/NACK đều mặc định bằng ‘1’.
- Thiết bị Master sẽ gửi hoặc nhận khung bit dữ liệu. Nếu Master gửi đến Slave thì bit Read/Write ở mức 0. Ngược lại nếu nhận thì bit này ở mức 1.
- Nếu như khung dữ liệu đã được truyền đi thành công, bit ACK/NACK được set thành mức 0 để báo hiệu cho Master tiếp tục.
- Sau khi tất cả dữ liệu đã được gửi đến Slave thành công, Master sẽ phát 1 tín hiệu Stop để báo cho các Slave biết quá trình truyền đã kết thúc bằng các chuyển lần lượt SCL, SDA từ mức 0 lên mức 1.

### **1.3. Ưu và nhược điểm**
- **Pros** (ưu điểm)
    -  Kết nối được nhiều thiết bị mà chỉ sử dụng 2 đường dây

- **Cons** (nhược điểm)
    - Tốc độ truyền thấp hơn SPI
    - Độ dài dây cab < SPI
    - Vì chỉ sử dụng 1 dây SDA để truyền nhận data nên khi 1 thiết bị đang gửi data thì không đồng thời nhận data như có 2 dây truyền nhận giống SPI

## **1. UART**<a name = "UART"></a>
### **1.1. Lý thuyết chung**  

- Universal asynchronous receiver transmitter, là bộ truyền nhận nối tiếp bất đồng bộ

### **1.2. Cách hoạt động của giao tiếp UART**  
- UART không phân biệt Master-Slave mà là 1 giao tiếp ngang hàng.
- Có 2 dây TX(transmit) vs RX(receive)
- Không có dây xung clock CK như SPI, I2C. Trên thiết bị A và B có bộ tạo xung riêng. Nguyên nhân: mục đích của UART khác với SPI và I2C, là để có thể kết nối trên cự li dài.
- Vì A, B có nguồn xung clock khác nhau nên có vấn đề là tốc độ đọc và thời điểm đọc.
    - Tốc độ đọc: có thể lập trình cấu hình được (baudrate: 4800, 9600, 19200, ...)
    


    <div align="center">
        <img src="https://deviot.vn/storage/deviot/UART-Communication.jpg" width="80%">
    </div> 

    - 1 gói data trong UART có 8 bit. Tín hiệu truyền từ A sang B có 1 vấn đề là A chỉ gửi đi và không xác nhận xem là B đã nhận hay chưa và data đã tới B chưa.
    => UART có thể truyền đi xa, tính linh động cao vì không cần tín hiệu hồi tiếp

<div align="center">
    <img src="https://camo.githubusercontent.com/9e986948a29f0eae378d0cd9ee382e60fbf5f58eacda264d92976f6498b2b655/68747470733a2f2f7777772e636972637569746261736963732e636f6d2f77702d636f6e74656e742f75706c6f6164732f323031362f30312f496e74726f64756374696f6e2d746f2d554152542d42617369632d436f6e6e656374696f6e2d4469616772616d2e706e67" width="80%">
</div> 




### **1.3. Ví dụ trong trường hợp cụ thể**
Khi giao tiếp sensor với Pi, 
- Nếu sensor đó là loại định kì gửi thông tin về thì có thể dung SPI, UART, I2C.
- Nếu sensor là loại gửi tín hiệu cảnh báo mà không biết trước thời diểm gửi về => chọn giao tiếp mà phía sensor có thể chủ động gửi data, là UART, không chọn SPI vì SPI **phải** có xung của Master thì Slave mới gửi trả tín hiệu về được
- I2C chỉ phù hợp với các thiết bị nối trong cự li gần.

## **1. CANBus**<a name = "CANBus"></a>
### **1.1. Lý thuyết chung**  
### **1.2. Cách hoạt động của giao tiếp CANBus**  
### **1.3. Ưu và nhược điểm**