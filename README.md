
Phân tích chất lượng danh mục tín dụng KHDN – AIV Bank
AI VIET NAM – eDA Conquer 2026 · Module 2 · Project 2 Thành viên: Thanh Huyền · Chương Lê · Phạm Hải

Dự án phân tích danh mục tín dụng khách hàng doanh nghiệp (KHDN) của AIV Bank tại ngày 30/06/2026, trên ba mặt: quy mô, sinh lời và chất lượng tín dụng. Dữ liệu được mô hình hóa và trực quan hóa bằng Power BI; báo cáo kỹ thuật viết bằng LaTeX.


Câu hỏi phân tích
Quy mô: Dư nợ tăng bao nhiêu và tập trung ở phân khúc, ngành, đơn vị kinh doanh (ĐVKD) nào?
Sinh lời: NII và TOI lũy kế thay đổi ra sao, phân khúc nào có biên lãi ròng (NIM) cao nhất?
Chất lượng tín dụng: Tỷ lệ nợ xấu OD3-5 tăng 0,25 điểm % trong tháng 6 là do nhiều khoản vay cùng xấu đi, hay tập trung ở một số ít khoản lớn?
Phát hiện chính
#
Phát hiện
Bằng chứng
1
Mức tăng nợ xấu tháng 6 gắn với một hợp đồng, không phải xu hướng diện rộng
Loại hợp đồng AIV-LN-0007842 (390 tỷ đồng), OD3-5 chuyển từ +0,25 pp thành −0,15 pp
2
Tỷ lệ OD2 giảm không phải tín hiệu tốt
512,2 tỷ đồng rơi từ OD2 xuống OD3, nhiều hơn 413,7 tỷ đồng trở về nhóm 1
3
Rủi ro chính nằm ở mức độ tập trung
115 hợp đồng vượt 100 tỷ đồng; 10 ĐVKD lớn nhất chiếm 40,1% dư nợ
4
Quy mô tăng nhanh hơn thu nhập lãi
Dư nợ bình quân +13,3% nhưng NII chỉ +2,8%; NIM giảm từ 2,67% (MICRO) xuống 0,97% (BIGCORP 1)

Điểm mới của dự án
Ma trận chuyển nhóm nợ (31/05 → 30/06/2026): theo dõi cùng một tập hợp đồng để thấy nợ di chuyển giữa các nhóm; bấm vào một ô để xem danh sách hợp đồng trong ô đó.
Phép thử loại trừ: loại khoản vay lớn nhất rồi tính lại tỷ lệ nợ xấu, để phân biệt biến động diện rộng với biến động do một khoản vay.
Dashboard (Power BI, 5 trang)
Trang
Nội dung
1. Tổng quan
6 chỉ số chính, xu hướng 18 tháng
2. Dư nợ
Cơ cấu theo phân khúc, kỳ hạn, ngành, sản phẩm, Top 10 ĐVKD
3. NII – TOI
Thu nhập lũy kế theo phân khúc, Top 10 khách hàng và ĐVKD
4. Chất lượng tín dụng
Cơ cấu nhóm nợ theo ngành, tỷ lệ nợ của Top 10 ĐVKD
5. Phân tích sâu
Ma trận chuyển nhóm, phép thử loại trừ, NIM theo phân khúc, phân tán 78 ĐVKD


File Power BI (.pbix): https://drive.google.com/file/d/1JAH1j_-l6JR42FGxo1EMfsuZqnlxg3-g/view?usp=drive_link
Bản PDF của dashboard: https://drive.google.com/file/d/1ZdZ7ZknQEbfMvpdNXDSH93J0ddJcB4uk/view?usp=drive_link
Cấu trúc thư mục
├── README.md                                Trang giới thiệu này
├── AIV_KHDN_Report.pdf                      Báo cáo kỹ thuật kèm Blog (13 trang)
├── AIV_KHDN_MASTER_Dashboard.pdf            Dashboard Power BI xuất ra PDF
├── AIV Bank KHDN – Slide thuyết trình.pdf   Slide thuyết trình
├── AIV_Bank_theme.json                      Theme màu dùng cho dashboard
└── hinh*.png                                Ảnh các biểu đồ dùng trong báo cáo

File Power BI (.pbix, khoảng 40 MB) vượt giới hạn 25 MB của GitHub nên được lưu trên Google Drive, xem đường dẫn ở mục Dashboard phía trên.
Dữ liệu và cách làm
Bộ dữ liệu AIV_Bank_KHDN_Dataset do chương trình cung cấp: 14 bảng (5 fact, 9 dim), 18 tháng từ 01/2025 đến 06/2026. Dữ liệu gốc không đưa lên repo.
Mô hình hình sao với 12 quan hệ trong Power BI; khoảng 80 measure DAX.
Ba quyết định xử lý chính:
Mọi chỉ số số dư được tính tại đúng một ngày báo cáo, không cộng dồn các ngày chụp số dư.
Chỉ dùng 18 tháng có cờ is_reportable = True.
Đối chiếu với bảng QC: 98.367,3 tỷ đồng · 11.073 hợp đồng · 8.778 khách hàng tại 30/06/2026.

Ví dụ measure khóa vào một ngày báo cáo:

Dư nợ =
VAR d = [Ngày BC]
RETURN CALCULATE ( SUM ( fact_loan_balance[balance_vnd] ),
                   REMOVEFILTERS ( dim_date ), dim_date[date] = d )
Công cụ
Power BI Desktop (DAX) · LaTeX (Overleaf) · Jira (quản lý công việc)
