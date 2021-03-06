# ibus-table-vietnamese

![](icons/vietnamese.png)

Do cả `ibus-unikey` và `ibus-bogo` đều rất buggy nên mình phát triển hai bảng
gõ này dùng tạm.

## Cài đặt

1. Cài đặt `ibus-table` nếu bạn chưa cài.
2. Dùng `git` clone `ibus-table-vietnamese` hoặc tải tệp ZIP ở **Clone or
   download** rồi giải nén. Sau đấy `cd` vô thư mục đó.
3. Dịch database từ mã nguồn

    ```sh
    ibus-table-createdb --name=tables/vni.db --source=tables/vni.txt
    ibus-table-createdb --name=tables/telex.db --source=tables/telex.txt
    ```

4. Giả định `DATADIR` là `/usr/share`. Sao chép các tệp cần thiết vô
   `${DATADIR}/ibus-table/`:

    ```sh
    sudo cp tables/{telex.db,vni.db} ${DATADIR}/ibus-table/tables
    sudo cp icons/vietnamese.png ${DATADIR}/ibus-table/icons
    ```

5. Khởi động lại `ibus-deamon` bằng lệnh `ibus-daemon -drx`.
6. Chạy `ibus-setup`. Trong tab **Input Method** chọn *Add, Vietnamese, Telex*
   hoặc *VNI* rồi chọn *Add*.

## Phương thức gõ

Để đơn giản hoá vấn đề, các bộ gõ này tuân theo một vài quy luật sau, mà các
bạn có thể gọi là dị, hoặc bất tiện, tuỳ các bạn, cơ mà mình mong nó vẫn hữu
ích ở một mữc độ nhất định:

* Chỉ gõ từng kí tự, dấu chữ cái trước, dấu của tiếng sau, ví dụ như để gõ từ
  *nện* trong VNI, bạn gõ `ne65n` - các cách gõ khác đều không cho kết quả như
  mong muốn.
* Với kiểu gõ Telex, bạn cần gõ ***tất cả*** các chữ cái hoa để có được kí tự
  in hoa. Điều này giúp bảng gõ đơn giản mà vẫn gõ được khi bật *Caps Lock*, ví
  dụ *Ừ* được gõ bằng `UWF`. Đơn giản hơn đến mức độ nào à, ừm, gần 5 lần. Có
  37 kí tự được gõ từ 2, phím, 30 từ 3. Kí tự gõ từ 2 phím có 3 cách khác nhau,
  3 phím có 7 cách. Mà bạn biết là mình xây dựng các bảng gõ này bằng tay nên
  chẳng có lí do gì để làm phức tạp hoá vấn đề lên cả không phải do mình lười,
  mình có lười thật, cơ mà nếu do người làm thì bảng gõ càng dài sẽ càng tiềm
  ẩn lỗi.
* Lại với kiểu gõ Telex, mình cho thêm kí tự thoát `\` của VNI vô, bỏ đi thao
  tác sửa lỗi kiểu `ooo` để gõ `oo` rất nhập nhằng. Ví dụ như để gõ từ *Đoòng*,
  bạn gõ `DDo\ofng`. Cảm ơn mình sau khi phải gõ từ có âm *ôô*. Nhân tiện mình
  cũng bỏ luôn việc dùng `z` để huỷ dấu. Simple Telex (cả v1 và v2, là cái
  `w[]{}` ấy) đều không được hỗ trợ.

## Tính năng lạ :beetle:

Bản thân `ibus-table-vietnamese` chỉ là bảng dữ liệu cho `ibus-table` nên cố
nhiên không thể có bug. Tuy nhiên, do `ibus-table` được thiết kế để với mục
đích ban đầu là để gõ các ngôn ngữ CJK (Trung Quốc, Nhật Bản, Hàn Quốc) vốn
phức tạp hơn chữ viết hệ Latin như chữ Quốc ngữ nhiều lần, bộ gõ này có nhiều
tính năng không cần thiết cho việc gõ tiếng Việt như việc sử dụng các phím di
chuyển (như Page Up, Page Down, các phím mũi tên) để chọn kí tự cần gõ. Xem
thêm ở [README của ibus-table](https://github.com/kaio/ibus-table/). Cơ mà hẳn
là các phím kí tự (số 1 đến 9, `-` và `+`) vẫn gõ được bình thường.

## Lưu ý khi dùng Vim

`ibus-table` không tương thích với Vim, vì vậy mình đã lập 2 keymap tương tự,
[đã được merge vô Vim](https://github.com/vim/vim/tree/master/runtime/keymap)
từ phiên bản 7.4.1942. Để sử dụng keymap này, trong `vimrc` bạn thêm mấy dòng
sau:

    set keymap=vietnamese-telex " hoặc vietnamese-vni
    " Tắt keymap và ibus khi khởi động Vim
    set imdisable iminsert=0 imsearch=-1
