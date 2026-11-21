# Phiếu QC 1 — Road v1.0

Lô được kiểm (học viên): nguyenxuanlam (04051)        Người kiểm (học viên): Lê Quang Vinh (04059)
Ngày: 2026-11-21                          Phiên bản guideline: Road v1.0  
File được kiểm (tên + `revision` trong manifest): `nguyenxuanlam-manifest.json` (`revision: 1`), gồm `nguyenxuanlam-front.zip` (16 ảnh) và `nguyenxuanlam-fisheye.zip` (12 ảnh)  
Số ảnh kiểm: 6 (+ 22 ảnh thêm rà soát toàn lô XML, ghi riêng)   Số nhãn đã kiểm (shape + tag): 52 (trên 6 ảnh mẫu chính: `A05`, `A07`, `A09`, `A14`, `B03`, `B04`)  

## Tổng hợp theo mã
| Mã | Loại lỗi | Số mục kiểm | Số lỗi | Mức |
| --- | --- | ---: | ---: | --- |
| QC1-01 tag camera | sai thuộc tính / bỏ sót | 6 | 0 | nặng |
| QC1-02 đủ L1, R1 | bỏ sót | 6 | 4 | nặng |
| QC1-03 position | sai thuộc tính / thừa | 4 | 0 | nặng |
| QC1-04 tâm vạch, chiều, điểm dừng | sai phạm vi / bỏ sót | 4 | 0 | chính |
| QC1-05 vạch đứt, che | sai phạm vi / sai thuộc tính | 4 | 0 | chính |
| QC1-06 style, color, kind | sai thuộc tính | 4 | 0 | chính |
| QC1-07 vùng lái | sai phạm vi / bỏ sót / thừa | 6 | 1 | chính |
| QC1-08 đèn, màu | bỏ sót / sai phạm vi / sai thuộc tính | 6 | 0 | nặng / chính |
| QC1-09 facing, type, group, biển phụ | sai thuộc tính | 7 | 0 | chính |
| QC1-10 hình in, đủ biển | bỏ sót / sai phạm vi | 7 | 0 | chính |
| QC1-11 fisheye | sai phạm vi / sai thuộc tính | 10 | 2 | chính |
| QC1-12 file | lỗi file | 2 | 0 | nhẹ / nặng |

## Danh sách lỗi (mỗi lỗi một dòng)
| # | Mã | Ảnh | Nhãn (label, id) | Mức | Mô tả ngắn |
| --- | --- | --- | --- | --- | --- |
| 1 | QC1-02 | A05_b2576c8c-2de20b8a.jpg | lane (L1, R1) | nặng | Thiếu cả 2 vạch giới hạn làn cơ bản L1 và R1 (chỉ có 1 polygon drivable) |
| 2 | QC1-02 | A07_b41ace08-c8468690.jpg | lane (L1) | nặng | Thiếu vạch L1 phía bên trái (chỉ gán R1, R2 và road_curb) |
| 3 | QC1-02 | A09_c7e6d5d1-c8af9fe3.jpg | lane (R1) | nặng | Thiếu vạch R1 phía bên phải (chỉ gán L1 và road_curb) |
| 4 | QC1-02 | A14_ca04d99f-c1282bb7.jpg | lane (R1) | nặng | Thiếu vạch R1 (chỉ có L1 và các vùng crosswalk) |
| 5 | QC1-07 | A14_ca04d99f-c1282bb7.jpg | drivable | chính | Bỏ sót hoàn toàn vùng lái (drivable) trên khung hình |
| 6 | QC1-11 | B03_04267_RV.png | lane (R1) | chính | Polyline trên ảnh fisheye chỉ đặt 2 điểm thẳng `(786.61,361.05;677.53,282.83)`, không bám theo cung cong |
| 7 | QC1-11 | B04_05535_RV.png | traffic_light | chính | Hộp đèn ở tọa độ `(1062.96, 238.96)` nằm sát mép phải ngoài vùng 80% bán kính fisheye nhưng chưa bật `edge_zone=true` |

## Ca mơ hồ
| Ảnh | Câu hỏi cho lead | Lời đáp (nếu có) |
| --- | --- | --- |
| B11_07282_RV.png | Ảnh fisheye_rear chỉ có 4 tag ảnh và không có bất kỳ shape nào; cần xác nhận lại theo bảng kế hoạch ảnh Task 2 xem ảnh này có thuộc diện bỏ qua không gán shape hay học viên bỏ sót toàn bộ. |  |

## Quyết định
Lỗi nặng: 4   Lỗi chính: 3 / 52 nhãn = 5.77 %   Lỗi nhẹ: 0   Ca chờ lead: 1  
Quyết định (Release / Hold / Rework): Rework  
Lý do (theo luật của phiếu): Phát hiện 4 lỗi mức độ **nặng** (`QC1-02` bỏ sót các vạch làn cơ bản `L1`/`R1` trên nhiều ảnh) và 3 lỗi mức độ **chính** (`QC1-07` thiếu vùng lái ở `A14`, `QC1-11` vẽ thiếu điểm theo cung cong và thiếu cờ `edge_zone` trên ảnh fisheye). Theo quy tắc QC 1, chỉ cần có từ 1 lỗi **nặng** trở lên thì lô không đạt chuẩn Release mà bắt buộc chuyển sang **Rework** để học viên sửa lại trên CVAT và xuất lại gói bàn giao kèm manifest `--revision 2`.  

Loại lỗi: bỏ sót = thiếu nhãn phải có; thừa = gán cái không phải đối tượng; sai phạm vi = hình lệch, sai chiều, dừng sai chỗ, tràn vùng. Ba loại này theo cách chia lỗi gán nhãn của ISO/IEC 5259-4 (mục 8.4.2); "sai thuộc tính" và "lỗi file" là khóa học thêm. Cách xếp mức: [thang mức lỗi](../docs/qc_severity_road_v1.0.md).
