# Tổng quan về Python
Python được thiết kể bởi Guido van Rossum, một lập trình viên người Hà Lan, vào năm 1991 với mục tiêu ban đầu là tạo ra một ngôn ngữ lập trình bậc cao tập trung vào sự đơn giản, có khả năng cải thiện năng suất và sự hiệu quả cho lập trình viên. Tính đến quý ba năm 2024, theo số liệu từ Tiobe Index, một trang xếp hạng uy tín về độ phổ biến của các ngôn ngữ lập trình, Python hiện đứng đầu với hơn 16%.

Khi bắt đầu học một ngôn ngữ mới, một điều quan trọng đó là bạn nên hiểu rõ về những điểm mạnh và hạn chế của mỗi ngôn ngữ để có thể linh hoạt áp dụng vào việc giải quyết vấn đề của mình. Một người thầy của mình từng nói: "Lập trình giống như giải quyết các vấn đề trong cuộc sống".

**Dưới đây là những điểm mạnh của Python:**
- Python là một ngôn ngữ linh hoạt, đa năng (nghe giống như tên của nó, dẻo dai như Trăn Anaconda 🐍) với cú pháp đơn giản, dễ học. Nhờ vào lợi thế này, bạn có thể nhanh chóng phát triển một ứng dụng bằng Python.
- Python nổi tiếng trong việc phát triển các ứng dụng liên quan đến Bigdata, AI và Học Máy vì nó có một cộng đồng lớn và nhiều thư viện hỗ trợ.
- Python cũng rất phù hợp để phát triển các ứng dụng web với các framework phổ biến như Django, Flask và FastAPI.
- Ngoài ra, Python có thể được sử dụng để phát triển các ứng dụng Game, các ứng dụng Desktop cho PC, v.v.

**Bên cạnh những điểm mạnh, Python cũng có một số điểm hạn chế:**
- Python được coi là một ngôn ngữ thông dịch. Do đó, nó có thể không phải là lựa chọn tốt nhất ở tốc độ thực thi đối với các tác vụ CPU-bound (cách task vụ tính toán sử dụng CPU) so với các ngôn ngữ biên dịch như C, C++.
- Python là một ngôn ngữ có kiểu dữ liệu động (dynamic type). Điều này có nghĩa là sẽ có nhiều lỗi bạn chỉ có thể phát hiện tại thời điểm runtime. Những ngoại lệ này thường là những ngoại lệ xảy ra ngoài mong muốn.
- Python là một ngôn ngữ đơn luồng (single-threaded language). Do giới hạn của Global Interpreter Lock (GIL), Python chỉ cho phép một luồng chạy các tác vụ tại một thời điểm trong một chương trình Python. Do đó, việc tận dụng sức mạnh của đa luồng (multi-threading) và lập trình song song (parallel programing) trong Python có thể khá thách thức. Nhất là trong bối cảnh các máy tính hiện đại ngày càng có bộ vi xử lý tiên tiến với đa luồng và đa lõi.

Trên đây là một số tóm tắt của mình về ngôn ngữ Python. Đối với mình, mỗi ngôn ngữ đều có vẻ đẹp riêng của nó. Mặc dù có những nhược điểm vốn có, Python vẫn trở nên phổ biến với lịch sử phát triển đã được chứng minh. Đặc biệt trong bối cảnh sự bùng nổ của công nghệ Bigdata và AI, Python vẫn là sự lựa chọn ưu tiên.