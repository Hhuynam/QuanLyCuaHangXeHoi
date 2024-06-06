# QuanLyCuaHangXeHoi
## Tacgia HaHuyNam K215480106063
### Ten De tai: Quan ly showroom O to
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
```

![image](https://github.com/Hhuynam/QuanLyCuaHangXeHoi/assets/130531037/f93088ee-add8-475d-bc32-bfd473c809d9)
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
