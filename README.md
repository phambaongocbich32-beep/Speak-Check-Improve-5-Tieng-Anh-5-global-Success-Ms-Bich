# Speak, Check & Improve 5

**Say it. Check it. Improve it!** – English 5 | Global Success, Unit 1–20

Ms Pham Thi Ngoc Bich - Do Thuc Tinh Primary School

## Tab 🙋 Hỏi đáp (chat cho cả lớp)

Học sinh vào tab **Hỏi đáp**, ghi biệt danh, chọn Unit (không bắt buộc) và gửi câu hỏi. Cô và các bạn cùng thấy, tin mới tự hiện sau vài giây.

### Bật chat chung cho cả lớp (Firebase, miễn phí, làm một lần)

1. Vào https://console.firebase.google.com → **Add project** → đặt tên, tắt Google Analytics.
2. **Build → Realtime Database → Create database** (chọn khu vực Singapore, chế độ *locked mode*).
3. Mở tab **Rules**, dán đoạn dưới đây rồi **Publish**:

```json
{
  "rules": {
    "chat": {
      ".read": true,
      "$id": {
        ".write": "!data.exists()",
        ".validate": "newData.hasChildren(['n','m','t']) && newData.child('n').isString() && newData.child('n').val().length <= 20 && newData.child('m').isString() && newData.child('m').val().length <= 300 && newData.child('t').val() <= now"
      }
    }
  }
}
```

4. Sao chép địa chỉ database (dạng `https://ten-du-an-default-rtdb.asia-southeast1.firebasedatabase.app`) và dán vào dòng `const CHAT_DB=""` trong `index.html` (tìm chữ `CẤU HÌNH`, gần cuối file).
5. Đổi `TEACHER_CODE` thành mã riêng của cô. Khi cô nhập mã, tin nhắn của cô có huy hiệu **Cô giáo**.

Nếu để `CHAT_DB=""`, tab chạy ở chế độ thử: tin nhắn chỉ lưu trên máy đang dùng.

### Lưu ý an toàn
- Trang có chặn số điện thoại, đường link, email và một số từ không lịch sự, nhưng bộ lọc không hoàn hảo. Cô nên đọc chat định kỳ.
- Luật trên cho phép gửi tin mới nhưng không cho sửa/xóa. Muốn xóa tin không phù hợp, cô mở **Realtime Database → Data → chat** trên Firebase và xóa tin đó.
- Mã giáo viên chỉ để hiện huy hiệu, không phải bảo mật chặt chẽ.
