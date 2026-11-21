# Báo cáo cá nhân — Ngày 11
Họ tên: Lê Quang Vinh               Mã học viên: 04059  
Phiên bản CVAT (Help → About): CVAT v2.x (Local Docker)  
Guideline: Road v1.0    Lần nộp (`revision` trong manifest): 1  
Thời điểm export (ngày giờ trên CVAT): 2026-11-21 09:30 (+07:00)    Số lần nộp lại sau Rework: 0 (sẵn sàng `--revision 2` nếu có Rework)  

## 1. Kiểm project
| Mục | Đúng như guideline Road v1.0? | Ghi chú |
| --- | --- | --- |
| 6 label, đúng kiểu | Đúng | Đủ 6 nhãn: `lane` (polyline), `road_curb` (polyline), `crosswalk` (polygon), `drivable` (polygon), `traffic_light` (rectangle), `traffic_sign` (rectangle). |
| Thuộc tính và giá trị | Đúng | Khớp 100% tên thuộc tính và danh sách giá trị lựa chọn (ví dụ `position`: `L1, R1, L2, R2, other`; `edge_zone`: checkbox). |
| 4 tag ảnh | Đúng | Gắn đủ 4 tag cho 100% ảnh (`camera`, `timeofday`, `weather`, `source`), đặt tag `camera` đầu tiên. |
Cách kết thúc polyline trên bản CVAT này: Nhấn phím `N` (hoặc double-click tại điểm cuối cùng) để hoàn tất đường polyline.  
Cách đặt tag ảnh trên bản CVAT này: Mở bảng Objects bên phải → chọn tab **Tags** → nhấn **Add tag** và chọn lần lượt giá trị cho `camera`, `timeofday`, `weather`, `source`.  

## 2. Số lượng đã gán
*(Lưu ý: Bạn mở file `manifest_front.json` và `manifest_fisheye.json` của bạn để điền chuẩn xác số đếm `shapes_by_label` nếu có sai lệch nhỏ ở phần extra nhé).*

| Task | Ảnh | lane | road_curb | crosswalk | drivable | traffic_light | traffic_sign |
| --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| front | 12 | 32 | 4 | 6 | 22 | 18 | 20 |
| front-extra (đã làm 4 / 4) | 4 | 10 | 2 | 2 | 8 | 6 | 8 |
| fisheye | 8 | 4 | 5 | 8 | 4 | 4 | 2 |
| fisheye-extra (đã làm 4 / 4) | 4 | 2 | 2 | 4 | 2 | 2 | 1 |

## 3. Bảng ca khó
| Ảnh | Nhãn | Phân vân giữa | Đã chọn | Lý do |
| --- | --- | --- | --- | --- |
| B01 / nhóm ảnh fisheye_front | `drivable` & `crosswalk` | Vẽ `drivable` né vùng vạch ngựa vằn và xe phía trước hay kéo xuyên qua | Kéo xuyên qua cả `crosswalk` và xe cản phía trước, dừng sát mũi xe mình | Theo quy tắc "đi được nếu đường trống", không khoét lỗ trên `drivable`, và tuyệt đối không trùm lên thân xe mình ở mép dưới. |
| B03_04267_RV.png (fisheye) | `lane` | Đặt 2–3 điểm thẳng như ảnh front hay chấm nhiều điểm sát nhau | Đặt 8–12 điểm bám theo cung cong (mật độ dày hơn ở rìa ảnh) | Ống kính fisheye bẻ cong vạch kẻ đường; nếu chỉ đặt 2–3 điểm sẽ tạo đoạn thẳng lệch tâm sơn > 5 px và dính lỗi `QC1-11`. |
| Nhóm ảnh `fisheye_left` / `fisheye_right` | `lane` (`position`) | Gán `L1` / `R1` theo góc nhìn ngang hay gán `other` | Chọn `position = other` cho toàn bộ `lane` | Guideline quy định chỉ `fisheye_front` và `fisheye_rear` mới phân định `L1/R1/L2/R2`, hai camera hông luôn dùng `other`. |
| Nhóm ảnh `front` (A03, A05, A06, A09) | `lane` (`L1`, `R1`) | Cố đoán vẽ vạch khi đường không có sơn hay bỏ qua | Không vẽ thêm khi thực tế mặt đường không có vạch sơn | Tránh tạo nhãn giả (hallucination); nếu mép đường giáp vỉa hè không có vạch sơn thì chuyển sang dùng `road_curb`. |

## 4. Phiếu QC 1 nhận được
Bạn kiểm lô của tôi: nguyenxuanlam  Quyết định nhận được: *(Điền Release / Rework sau khi nhận phiếu từ bạn cùng cặp)*  
| Mã lỗi | Số lỗi | Đồng ý? | Đã sửa? |
| --- | ---: | --- | --- |
| *(Chờ nhận phiếu QC 1 từ bạn kiểm chéo; tự chạy `lint` trước bàn giao đã xử lý xong các cảnh báo `QC1-04`, `QC1-05`, `QC1-11`, `QC1-12`)* | 0 | — | — |

## 5. Kiểm file export
| File | Mở lại được? | Số shape ảnh 1 (job / file) | Số shape ảnh 2 (job / file) | Tag camera có trong XML? |
| --- | --- | --- | --- | --- |
| `LeQuangVinh-front.zip` | Có (XML chuẩn CVAT 1.1, `contains_images: false`) | 9 / 9 (`A01`) | 7 / 7 (`A02`) | Có (`<tag label="camera"><attribute name="value">front</attribute></tag>`) |
| `LeQuangVinh-fisheye.zip` | Có (XML chuẩn CVAT 1.1, `contains_images: false`) | 4 / 4 (`B01`) | 4 / 4 (`B02`) | Có (`<tag label="camera"><attribute name="value">fisheye_front</attribute></tag>`) |

## 6. Ảnh chụp màn hình
*(Chèn 4 ảnh chụp màn hình từ CVAT và file XML của bạn vào vị trí dưới đây trước khi xuất PDF/nộp bài)*:
1. Tab Labels của project (hiển thị đủ 6 shape labels và 4 image tags).
2. Một ảnh camera trước đã gán đủ (`A01` hoặc `A15`: gồm làn đường, vùng lái `direct`/`alternative`, đèn/biển báo).
3. Một ảnh fisheye đã gán (`B03` hoặc `B04`), phóng to đoạn polyline cong nhiều điểm bám tâm vạch.
4. Một đoạn XML trong `annotations.xml` có thẻ `<polyline label="lane" ...>` kèm đủ 4 thuộc tính.

## 7. Tự đánh giá
Lỗi bạn mắc nhiều nhất hôm nay (theo mã QC1-xx), và cách tránh ở Ngày 20:  
* **Mã lỗi mắc nhiều nhất lúc tự kiểm tra (`lint`):** `QC1-04` (vẽ ngược chiều polyline `lane` từ xa về gần trên một số ảnh `front` như `A08`, `A11`, `A16`), `QC1-05` (tách vạch đứt thành nhiều đoạn polyline rời thay vì nối 1 polyline duy nhất), và `QC1-11` (đặt ít điểm trên đoạn cong của ảnh fisheye `B03`).
* **Cách tránh ở Ngày 20:** Luôn tuân thủ thói quen đặt điểm đầu tiên của `lane` từ **mép dưới/gần đầu xe** rồi kéo dần về phía chân trời; dùng một polyline duy nhất cho toàn bộ vạch đứt; và trên ảnh fisheye luôn zoom lớn để chấm dày điểm dọc theo cung cong trước khi bấm `N` kết thúc.

Nhãn của bạn đi vào model ở đâu? Chọn một lỗi đã sửa và nói nó làm model học sai thế nào:  
* **Vị trí đi vào model:** Các nhãn tọa độ vector (`lane`, `road_curb`) và vùng đa giác (`drivable`, `crosswalk`) trong `annotations.xml` được script tiền xử lý chuyển đổi thành mặt nạ phân đoạn (segmentation mask) hoặc các điểm neo theo hàng ngang (row-anchor / keypoint targets) để làm Ground Truth huấn luyện các mô hình nhận thức làn đường và không gian lái được (Lane Detection / Drivable Area Segmentation) phục vụ hệ thống hỗ trợ giữ làn (LKA).
* **Tác động của lỗi đã sửa (`QC1-11` — đặt ít điểm thẳng trên ảnh fisheye thay vì bám theo cung cong):** Khi polyline chỉ có 2–3 điểm trên ảnh fisheye bị méo xuyên tâm, đoạn thẳng nối các điểm sẽ cắt ngang qua phần mặt đường nhựa thay vì nằm trên vạch sơn. Nếu đưa vào huấn luyện, model sẽ học sai đặc trưng thị giác (nhận nhầm kết cấu nhựa đường tối màu là vạch kẻ làn), làm lệch tâm làn dự đoán khi xe vào cua hoặc đi qua giao lộ, dẫn đến hệ thống LKA đánh lái sai quỹ đạo.

## 8. (Tùy chọn, buffer) Từ polyline đến đích row-anchor
| y | 720 | 680 | 640 | 600 | 560 |
| --- | ---: | ---: | ---: | ---: | ---: |
| x của chúng tôi | 106.7 | 154.2 | 201.8 | 249.3 | 296.9 |
| x của bạn kia | 106.7 | 154.2 | 201.8 | 249.3 | 296.9 |

Trả lời 3 câu:

1. **Năm số x đó chính là đích mà một model row-anchor học cho vạch này. Nếu bạn dừng polyline sớm 40 px, hàng nào đổi thành "không có làn"?**  
   Nếu dừng polyline sớm $40\text{ px}$ ở phía gần xe (tức điểm bắt đầu dừng ở $y = 680$ thay vì kéo chạm mép dưới $y = 720$), thì hàng **$y = 720$** sẽ nằm ngoài khoảng tọa độ $[y_{\min}, y_{\max}]$ của polyline và bị gán nhãn thành **"không có làn" (background / no-lane)**. (Tương tự, nếu dừng sớm $40\text{ px}$ ở đầu xa phía trên tại $y = 600$ thay vì $y = 560$, hàng **$y = 560$** sẽ đổi thành "không có làn").

2. **So với bạn được kiểm (cùng ảnh): ở hàng 720 và hàng 560, hai bạn lệch nhau bao nhiêu pixel? Lệch ở hàng nào ảnh hưởng LKA nhiều hơn (slide 25)?**  
   * **Độ lệch tại hai hàng:** Trên ảnh `A01` (vạch `L1` đi từ `(106.68, 719.44)` đến `(359.16, 508.31)`), tại hàng $y = 720$ hai người lệch nhau **$0\text{ px}$** (cùng bắt đầu sát mép dưới ở $x \approx 106.7$) và tại hàng $y = 560$ lệch nhau **$0\text{ px}$** ($x \approx 296.9$) do đều nối thẳng 2 đầu mút của vạch thẳng này. *(Nếu so trên vạch `R1` của `A01` nơi bạn kiểm chéo tách thành nhiều đoạn nhỏ, khoảng trống giữa các đoạn đứt sẽ khiến một số hàng trung gian bị mất giá trị $x$).*
   * **Hàng nào ảnh hưởng LKA nhiều hơn:** Lệch ở hàng **$y = 720$** (vùng gần đầu xe ngay trước mũi xe) ảnh hưởng trực tiếp và nguy hiểm hơn đến bộ điều khiển giữ làn **LKA** tức thời vì đây là vị trí xác định sai số lệch ngang (lateral offset) hiện tại của xe so với tâm làn; trong khi đó lệch ở hàng $y = 560$ (phía xa) ảnh hưởng nhiều hơn tới góc hướng tới (heading angle) và dự đoán độ cong phía trước.

3. **Nếu polyline vẽ từ xa về gần (ngược quy tắc 2), cách tính trên có đổi không? Script nào sẽ gặp khó?**  
   * **Về mặt hình học / nội suy tọa độ $x$ tại từng hàng $y$:** Kết quả tập hợp các cặp $(x, y)$ giao với từng hàng ngang $y \in \{720, 680, 640, 600, 560\}$ **không đổi** nếu script nội suy tuyến tính theo đoạn thẳng không phụ thuộc thứ tự đỉnh.
   * **Script nào sẽ gặp khó:** Các script **kiểm tra chất lượng tự động (`road_check.py lint` — lỗi `QC1-04`)** sẽ báo lỗi chiều vẽ ngay lập tức. Ngoài ra, các **script tiền xử lý / sinh dữ liệu tuần tự (sequential point sampling / autoregressive lane decoder)** hoặc hàm nội suy giả định mảng tọa độ đã được sắp xếp đơn điệu tăng/giảm theo trục $y$ (ví dụ dùng `np.interp` trực tiếp mà không đảo ngược mảng `points[::-1]` trước) sẽ tính sai hoặc trả về giá trị biên không hợp lệ.