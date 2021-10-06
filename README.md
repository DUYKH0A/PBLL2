# PBLL2
Đề tài:CÂY ATM (Mở rộng ra là chức năng của 1 cái app banking)
-Chức năng:Thực hiện các chức năng đầy đủ như 1 cây ATM bình thường
Cách thức hoạt động:
-Khi chương trình chạy, đọc được từ file Account.txt danh sách các tài khoản và số dư đã có sẵn trong ngân hàng=>DSLK
-Các tài khoản gồm các tài khoản thông thường và 1 tài khoản quyền admin.Chức năng của tài khoản quyền admin
    +Có thể kiểm tra tất cả các lịch sử giao dịch của ATM:
      Sẽ hỏi admin muốn xem của 1 người hay của nhiều người
    +Có thể khóa và mở khóa các tài khoản khác
    +Tạo hoặc xóa tài khoản(thường thì sẽ là tạo thôi, chớ tiền của khách hàng ai dám xóa mà xóa)
-Hiển thị ra giao diện,yêu cầu người dùng nhập số tài khoản và mật khẩu, đúng trong danh sách đã tồn tại mới được đăng nhập vào
-Đăng nhập vào xong thì màn hỉnh hiển thị các chức năng của người dùng:Khi đăng nhập sai quá 5 lần thì máy sẽ tự động khóa tài khoản đó
-Khi đăng nhập vào thì cho phép người dùng thao tác với tài khoản của mình y như ngoài đời thật:
  +Rút tiền
  +Truy vấn số dư
  +Chuyển tiền
  +Lịch sử giao dịch: Lịch sử nộp tiền + Lịch sử gửi tiền
  +Chức năng vay tiền nhanh: chỉ giới hạn trong một mức tiền xác định
  +Đổi mật khẩu (Mã PIN)
  +Đăng xuất khỏi tài khoản
 ......
 -Thiết kế có màu mè hoa lá cành các kiểu
 NOTE:CÁC QUÁ TRÌNH THAO TÁC VỚI MK ĐỀU PHẢI CHE MK => COI LẠI HÀM NHẬP MK CHỚ NHƯ KÌ VỪA RỒI NÁT QUÁ
 Tất cả các thông tin đều phải được lưu và lấy ra từ file txt, hoặc sử dụng SQL Sever(tạm thời mới chỉ biết dùng file txt)
======================================================
-Tạo class khách hàng và quản lí khách hàng (tương tự như cái bài quản lí sinh viên của thầy)
1/Class KH:
**private:**
string ID: số tài khoản ngân hàng
string MK:mật khẩu của tài khoản
int SoDu: số dư hiện có trong tài khoản
int NoNganHang:số tiền đang nợ ngân hàng(dùng cho vay tiền nhanh)=>Chỉ cho phép nợ trong 1 số tiền nhất định
**publc:**
**void setMK(string MK):hàm thay đổi MK**
**string getMK():hàm lấy Mk để so sánh khi khách hàng nhập mk**
**void ChuyenKhoan(KH,int tien): chuyển khoản một số tiền đến tài khoản KH**
Note: Mỗi lần thực hiện giao dịch sẽ yêu cầu xác nhận mã PIN
      Các lần giao dịch sẽ được lưu lại thời gian ngày giờ để có thể kiểm tra được lịch sử
      Sau khi rút thì cập nhật số dư mới cho khách và báo là đã chuyển tiền thành công
**void RutTien(int tien):rút một số tiền t từ số dư**
Note:Sau khi rút thì cập nhật số dư mới và thông báo đã rút tiền thành công
      Trường hợp phải có tiền giữ thẻ và số tiền định rút lớn hơn số dư thì thông báo cho khách
**int SoDu():Truy vấn số dư**
Note:Hiển thị cả số dư và số tiền đang nợ ngân hàng
**void LichSuGiaoDich():Hiển thị ra toàn bộ lịch sử giao dịch của tài khoản**
Note:Lưu ý là toàn bộ lịch sử giao dịch này được gom từ nhiều lần đăng nhập khác nhau=>Phải ghi nhớ từ đầu tới cuối
**void VayTienNhanh(int tien):Vay nhanh một số tiền nhỏ từ ngân hàng, số tiền sẽ được chuyển vào số dư, báo nợ tại NoNganHang**
Note: Sau khi vay xong cũng sẽ thông báo qua màn hình
**void DoiMaPIN(string s): đổi mã PIN thành s và thông báo đã đổi thành công**
Note: Nhập mã PIN cũ và xác nhận y xì như ngoài đời
void Dangxuat():thoát khỏi tài khoản và quay về màn hình chính
NOTE:ƯU TIEN LÀM CLASS NÀY TRƯỚC, THẰNG PHÍA SAU KO CÓ CŨNG DC
2/Class Quản lí khách hàng 
private:
int n: số tài khoản hiện có
 p: Một danh sách liên kết các khách hàng//Cái này thì phải định nghĩa lại DSLK
public:
void DOCFILE():Dọc file từ file.txt
void createAcc(string ID,string MK,int sodu,int NoNganHang):tạo một acc mới và gán vào dslk
Note:Sau khi gán xong thì lưu vào file txt để bảo toàn dữ liệu
    Đảm bảo rằng các ID không được giống nhau
void deleteAcc(string ID):Xóa tài khoản có ID đã cho=>cập nhật lại file txt
void lichSuGiaoDich(): cho phép chọn và đọc từ file txt các lịch sư giao dịch
void LockAcc(string ID):chức năng khóa Acc
void UnLockAcc(string ID):chức năng mở khóa acc


