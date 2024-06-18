# QuanLyCuaHangXeHoi
## Tacgia HaHuyNam K215480106063
### Ten De tai: Quan ly showroom O to
## Mo ta bai toan
## 1. Tao cac bang chua thong tin
### Danh sach thong tin ve nhan vien(Ma nhan vien, ho va ten, chuc vu, so dien thoai, dia chi,...);
### hang hoa (dong xe, mau sac, kieu dang,...); 
### Ngay di lam / cham cong;
### tinh trang lam viec ( dang di lam / nghi viec);
### quan ly hang hoa trong kho: so luong xe trong kho, xe moi/ cu, dong xe ban chay nhat va nguoc lai ;...
### dich vu cham soc xe, khach hang;
### doanh thu: doanh so mua ban xe, dich vu di kem,...
### hoa don: kem theo thong tin khach hang, ngay mua, ...
### quan he doi tac: cac doanh nghiep dang thiet lap doi tac, nha cung cap,...
### cac khoan chi phi duy tri doanh nghiep: nop thue, tien dien, chi phi thue mat bang,...
## 2. tao cac thu tuc de hien thi thong tin theo yeu cau
### Tim cac nhan vien dang di lam/ da nghi viec
### Tong doanh thu tu tat ca cac nguon
### Dong xe ban nhieu nhat trong mot thoi diem xac dinh (vi du trong quy 1 nam 2024)


*File nop gom co file .md va file word (co kem hinh anh minh hoa)*
---------------------------------------------------------------------
![markdown](https://github.com/Hhuynam/QuanLyCuaHangXeHoi/blob/main/diagramBaitaplon.jpg)
# tao cac bang de quan ly
## bang thong tin nhan vien
![image](https://github.com/Hhuynam/QuanLyCuaHangXeHoi/assets/130531037/fa8b475c-0bd9-4967-8434-bc0319492efc)
## tao bang thong tin san pham (danh sach cac dong xe)
![image](https://github.com/Hhuynam/QuanLyCuaHangXeHoi/assets/130531037/f1f241e4-c609-47c6-98c4-250460dfb3d5)
## tao bang thong tin tien luong
![image](https://github.com/Hhuynam/QuanLyCuaHangXeHoi/assets/130531037/76e11f43-8512-4027-84b5-4ef096b3ff10)
## tao bang thong tin ve ngay nhan viec, nghi viec cua nhan vien

## full source code: 
```
-- Tạo bảng TinhTrangDiLam
CREATE TABLE TinhTrangDiLam (
    id INT PRIMARY KEY IDENTITY(1,1),
    TenNhanVien NVARCHAR(50) NOT NULL,
    MaNhanVien NVARCHAR(50) NOT NULL,
    NgayNhanViec DATE,
    NgayNghiViec DATE
);

-- Tạo bảng ThongTinNhanVien
CREATE TABLE ThongTinNhanVien (
    id INT PRIMARY KEY IDENTITY(1,1),
    TenNhanVien NVARCHAR(50) NOT NULL,
    MaNhanVien NVARCHAR(50) NOT NULL,
    ChucVu NVARCHAR(50),
    SoDienThoai NVARCHAR(15),
    GioiTinh NVARCHAR(10)
);

-- Tạo bảng ThongTinSanPham
CREATE TABLE ThongTinSanPham (
    id INT PRIMARY KEY IDENTITY(1,1),
    TenDongXe NVARCHAR(50),
    MaSanPham NVARCHAR(50) NOT NULL,
    NhaSanXuat NVARCHAR(50),
    GiaNiemYet DECIMAL(18, 2),
    SoLuongTrongKho INT,
    MauSac NVARCHAR(50),
	PhienBan NVARCHAR(50)
);

-- Tạo bảng TienLuong
CREATE TABLE TienLuong (
    id INT PRIMARY KEY IDENTITY(1,1),
    TenNhanVien NVARCHAR(50) NOT NULL,
    SoTaiKhoan NVARCHAR(50),
    SoNgayCong INT,
    TruLuong INT,
    TienThuong INT,
    LuongCoBan DECIMAL(18, 2),
    TongLuong DECIMAL(18, 2)
);

-- Tạo bảng Quảng Lý Kho để quản lý kho chứa hàng hóa
CREATE TABLE QuanLyKho (
    id INT PRIMARY KEY IDENTITY(1,1),
    MaSanPham NVARCHAR(50) NOT NULL,
    SoLuong INT,
    FOREIGN KEY (MaSanPham) REFERENCES HangHoa(MaSanPham)
);

-- Tạo bảng dịch vụ để chứa thông tin dịch vụ chăm sóc xe, khách hàng,...
CREATE TABLE DichVu (
    id INT PRIMARY KEY IDENTITY(1,1),
    MaKhachHang NVARCHAR(50),
    LoaiDichVu NVARCHAR(100),
    ChiPhi DECIMAL(18, 2),
    NgaySuDung DATE
);

-- Tạo bảng Doanh thu về thông tin doanh thu
CREATE TABLE DichVu (
    id INT PRIMARY KEY IDENTITY(1,1),
    MaKhachHang NVARCHAR(50),
    LoaiDichVu NVARCHAR(100),
    ChiPhi DECIMAL(18, 2),
    NgaySuDung DATE
);

-- Tạo bảng Hóa đơn để chứa thông tin về hóa đơn các loại
CREATE TABLE DichVu (
    id INT PRIMARY KEY IDENTITY(1,1),
    MaKhachHang NVARCHAR(50),
    LoaiDichVu NVARCHAR(100),
    ChiPhi DECIMAL(18, 2),
    NgaySuDung DATE
);

-- Tạo bảng Đối tác để chứa thông tin về dối tác và các nhà cung cấp,...
CREATE TABLE DichVu (
    id INT PRIMARY KEY IDENTITY(1,1),
    MaKhachHang NVARCHAR(50),
    LoaiDichVu NVARCHAR(100),
    ChiPhi DECIMAL(18, 2),
    NgaySuDung DATE
);

-- Bảng Chi phí gồm các chi phí duy trì doanh nghiệp
CREATE TABLE DichVu (
    id INT PRIMARY KEY IDENTITY(1,1),
    MaKhachHang NVARCHAR(50),
    LoaiDichVu NVARCHAR(100),
    ChiPhi DECIMAL(18, 2),
    NgaySuDung DATE
);

```
![image](https://github.com/Hhuynam/QuanLyCuaHangXeHoi/assets/130531037/f93088ee-add8-475d-bc32-bfd473c809d9)
# Tạo các thủ tục - Procedure để hiển thị thông tin 
## tao procedure tinh tong luong nhan vien: tong luong = ((so ngay cong / 30 ) + tien thuong - tru luong)

USE QLshowroomAUTO;
GO
CREATE PROCEDURE TinhTongLuong
    @TenNhanVien nvarchar(50),
	@SoTaiKhoan int,
    @SoNgayCong int,
    @TruLuong int,
    @TienThuong int
AS
BEGIN
    DECLARE @LuongCoBan nvarchar(50);
    DECLARE @TongLuongNhan nvarchar(50);
    
    -- Lấy lương cơ bản của nhân viên
    SELECT @LuongCoBan = LuongCoBan FROM TienLuong WHERE TenNhanVien = @TenNhanVien;

    -- Tính tổng lương
    SET @TongLuongNhan = (@LuongCoBan / 30 * @SoNgayCong) + @TienThuong - @TruLuong;

    -- Cập nhật tổng lương vào bảng TienLuong
    UPDATE TienLuong
    SET SoNgayCong = @SoNgayCong,
        TruLuong = @TruLuong,
        TienThuong = @TienThuong,
        TongLuongNhan = @TongLuongNhan
    WHERE TenNhanVien = @TenNhanVien;

    -- Trả về tổng lương
    SELECT @TongLuongNhan AS TongLuongNhan;
	END;
	GO

## Su dung thu tuc de tinh tong luong cho nhan vien
### EXEC TinhTongLuong @TenNhanVien = 'Nguyen Van Song',
###                   @SoTaiKhoan = 10000123, 
###                   @SoNgayCong = 26,      
###                   @TruLuong = 1000000,   
###                   @TienThuong = 500000;  

## ket qua 
![image](https://github.com/Hhuynam/QuanLyCuaHangXeHoi/assets/130531037/73436129-b072-462e-b01c-6022e57d1fd8)
## toi se thu tao view de hien thi bang luong cua toan bo nhan vien
```
CREATE VIEW TongLuongNhanVien AS
SELECT TenNhanVien, SUM((LuongCoBan / 30 * SoNgayCong) + TienThuong - TruLuong) AS TongLuong
FROM TienLuong
GROUP BY TenNhanVien;
```
![image](https://github.com/Hhuynam/QuanLyCuaHangXeHoi/assets/130531037/ccf44e7b-83b7-42fc-b6af-71a58d77c716)

## Tổng doanh thu từ các nguồn
```
CREATE PROCEDURE TongDoanhThu
AS
BEGIN
    SELECT SUM(DoanhSo) AS TongDoanhThu
    FROM DoanhThu;
END;
```

## Dòng xe bán nhiều nhất trong một thời điểm xác định (ví dụ: quý 1 năm 2024)
```
CREATE PROCEDURE DongXeBanNhieuNhat
    @StartDate DATE,
    @EndDate DATE
AS
BEGIN
    SELECT TOP 1 hh.TenDongXe, COUNT(dt.MaSanPham) AS SoLuongBan
    FROM DoanhThu dt
    JOIN HangHoa hh ON dt.MaSanPham = hh.MaSanPham
    WHERE dt.NgayBan BETWEEN @StartDate AND @EndDate
    GROUP BY hh.TenDongXe
    ORDER BY SoLuongBan DESC;
END;

```
## Tao procedure de neu du lieu trong cot NgayNghiViec duoc cap nhat (tuc la da nghi viec) thi se xoa thong tin lien quan (so tai khoan, tien cong,...) o bang TienLuong
```
CREATE PROCEDURE XoaDuLieuNhanVien 
    @TenNhanVien nvarchar(50)
AS
BEGIN
    -- Kiểm tra xem cột NgayNghiViec của nhân viên đã được cập nhật chưa
    DECLARE @NgayNghiViec nvarchar(50);
    SELECT @NgayNghiViec = NgayNghiViec FROM TinhTrangDiLam WHERE TenNhanVien = @TenNhanVien;

    IF @NgayNghiViec IS NOT NULL
    BEGIN
        -- Nếu NgayNghiViec không rỗng, xóa dữ liệu của nhân viên
        UPDATE TienLuong
        SET SoTaiKhoan = NULL,
            SoNgayCong = NULL,
            TienThuong = NULL,
            TruLuong = NULL,
            TongLuongNhan = NULL
        WHERE TenNhanVien = @TenNhanVien;

        -- Xóa thông tin nhân viên
        DELETE FROM TinhTrangDiLam WHERE TenNhanVien = @TenNhanVien;
        DELETE FROM ThongTinNhanVien WHERE TenNhanVien = @TenNhanVien;

        PRINT 'Du lieu cua nhan vien ' + @TenNhanVien + ' da xoa vi nghi viec';
    END
    ELSE
    BEGIN
        PRINT 'khong co du lieu nghi viec cua nhan vien ' + @TenNhanVien + '.';
    END
END;

```
## Thu xoa du lieu cua nhan vien
![image](https://github.com/Hhuynam/QuanLyCuaHangXeHoi/assets/130531037/30a182d3-9c61-4433-b4a0-223da8425653)
## thu nhap du lieu ngay nghi viec cho nhan vien Ha Thanh Hai va chay exec procedure xoa thong tin de xem thu
![image](https://github.com/Hhuynam/QuanLyCuaHangXeHoi/assets/130531037/5cb5cf2f-69a5-45b1-ab97-447f27464ede)
![image](https://github.com/Hhuynam/QuanLyCuaHangXeHoi/assets/130531037/583dad94-c7a8-4160-9487-17f6a9ae1240)
# tạo cursor để hiển thị danh sách nhân viên giới tính nam
```
-- Khai báo biến để lưu trữ dữ liệu được truy xuất từ cursor
DECLARE @TenNhanVien NVARCHAR(100);
DECLARE @GioiTinh NVARCHAR(10);

-- Khai báo cursor
DECLARE cursor_NhanVienNam CURSOR FOR
SELECT TenNhanVien, GioiTinh 
FROM dbo.ThongTinNhanVien 
WHERE GioiTinh = 'Nam';

-- Mở cursor
OPEN cursor_NhanVienNam;

-- Truy xuất dữ liệu từng hàng từ cursor
FETCH NEXT FROM cursor_NhanVienNam INTO @TenNhanVien, @GioiTinh;

-- Sử dụng vòng lặp để lặp qua các hàng dữ liệu
WHILE @@FETCH_STATUS = 0
BEGIN
    -- Hiển thị dữ liệu (hoặc bạn có thể thực hiện các xử lý khác)
    PRINT 'Tên Nhân Viên: ' + @TenNhanVien + ', Giới Tính: ' + @GioiTinh;

    -- Truy xuất hàng tiếp theo
    FETCH NEXT FROM cursor_NhanVienNam INTO @TenNhanVien, @GioiTinh;
END

-- Đóng cursor
CLOSE cursor_NhanVienNam;

-- Hủy cursor
DEALLOCATE cursor_NhanVienNam;
```
![image](https://github.com/Hhuynam/QuanLyCuaHangXeHoi/assets/130531037/b333d785-3d80-4c42-962a-e501b9b94017)

##  tạo cursor để hiển thị danh sách nhân viên giới tính nữ
```
-- Khai báo biến để lưu trữ dữ liệu được truy xuất từ cursor
DECLARE @TenNhanVien NVARCHAR(100);
DECLARE @GioiTinh NVARCHAR(10);

-- Khai báo cursor
DECLARE cursor_NhanVienNu CURSOR FOR
SELECT TenNhanVien, GioiTinh 
FROM dbo.ThongTinNhanVien 
WHERE GioiTinh = 'Nu';

-- Mở cursor
OPEN cursor_NhanVienNu;

-- Truy xuất dữ liệu từng hàng từ cursor
FETCH NEXT FROM cursor_NhanVienNu INTO @TenNhanVien, @GioiTinh;

-- Sử dụng vòng lặp để lặp qua các hàng dữ liệu
WHILE @@FETCH_STATUS = 0
BEGIN
    -- Hiển thị dữ liệu (hoặc bạn có thể thực hiện các xử lý khác)
    PRINT 'Tên Nhân Viên: ' + @TenNhanVien + ', Giới Tính: ' + @GioiTinh;

    -- Truy xuất hàng tiếp theo
    FETCH NEXT FROM cursor_NhanVienNu INTO @TenNhanVien, @GioiTinh;
END

-- Đóng cursor
CLOSE cursor_NhanVienNu;

-- Hủy cursor
DEALLOCATE cursor_NhanVienNu;
```
![image](https://github.com/Hhuynam/QuanLyCuaHangXeHoi/assets/130531037/197adebe-715d-47fc-9a6c-61e726b0749c)
# tao trigger de nhap so ngay cong va tinh luong vao tong luong trong bang tien luong
```
CREATE TRIGGER tongLuong
ON dbo.TienLuong
AFTER INSERT, UPDATE
AS
BEGIN
    -- Biến để lưu trữ giá trị từ bảng INSERTED
    DECLARE @id INT;
    DECLARE @SoNgayCong INT;
    DECLARE @TienThuong DECIMAL(18, 2);
    DECLARE @TruLuong DECIMAL(18, 2);
    DECLARE @LuongCoBan DECIMAL(18, 2);
    DECLARE @TongLuong DECIMAL(18, 2);
    
    -- Truy xuất giá trị từ bảng INSERTED
    SELECT @id = i.id, 
           @SoNgayCong = i.SoNgayCong,
           @TienThuong = i.TienThuong,
           @TruLuong = i.TruLuong,
           @LuongCoBan = i.LuongCoBan
    FROM INSERTED i;

    -- Tính toán lương tổng cộng
    SET @TongLuong = (@LuongCoBan * @SoNgayCong) + @TienThuong - @TruLuong;

    -- Cập nhật lương trong bảng TienLuong
    UPDATE dbo.TienLuong
    SET TongLuongNhan = @TongLuong
    WHERE id = @id;
END;
```
![image](https://github.com/Hhuynam/QuanLyCuaHangXeHoi/assets/130531037/27734151-c282-4b54-ba51-7993c11ca8cc)
## kiem tra thay doi du lieu trong bang: da tinh tong luong
![image](https://github.com/Hhuynam/QuanLyCuaHangXeHoi/assets/130531037/5ed2b831-3ec1-47bd-a749-bbb5bbe8a85a)

