Python Guru Series 🐍🐍🐍 - Part 4: Concurrency Programming trong Python

Xin chào các bạn, trong bài viết trước, chúng ta đã cùng khám phá về Global Interpreter Lock (GIL). Chúng ta đã tìm hiểu những hạn chế của nó và tác động lớn của nó đến ngôn ngữ Python. Một mặt, GIL giúp quản lý bộ nhớ và lập trình trở nên dễ dàng hơn. Mặt khác, nó cũng ảnh hưởng đến hiệu suất của các chương trình, đặc biệt là trong các tác vụ liên quan đến tính toán dựa trên CPU.

Trong bài viết hôm nay, chúng ta sẽ thảo luận về concurrency programming ( lập trình đồng thời ) trong Python. Chúng ta sẽ xem xét các phương pháp khác nhau để đạt được concurrency programming nhằm khắc phục các hạn chế và ràng buộc của GIL.
Ok, cùng nhau bắt đầu nào.

# 1. Sequential Programming vs. Concurrency Programming
Trước khi đi sâu vào các phương pháp lập trình song song trong Python, hãy cùng điểm qua khái niệm về concurrency programming. Trong lập trình, khái niệm về sequential programming (lập trình tuần tự) và concurrency programming (lập trình đồng thời) khá quen thuộc.
Trong sequential programming, các tác vụ được thực hiện theo thứ tự, từng tác vụ một. Chương trình sẽ không chuyển sang tác vụ tiếp theo cho đến khi tác vụ hiện tại hoàn thành. Như được minh họa đính kèm phía dưới, bạn có thể thấy rõ rằng chương trình thực thi các tác vụ theo thứ tự. Nó chờ task 1 hoàn thành, sau đó mới chuyển sang task 2.
Ngược lại, concurrency programming liên quan đến việc thực hiện các tác vụ đồng thời. Concurrency programming cho phép nhiều tác vụ được thực hiện gần như cùng một lúc. Các tác vụ có thể xen kẽ nhau nhưng không nhất thiết phải chạy chính xác cùng lúc. Chương trình có thể thực hiện nhiều tác vụ, trong đó mỗi tác vụ có thể tạm dừng để chờ dữ liệu hoặc sự kiện để tiếp tục luồng thực thi của mình. Bạn có thể thấy ý tưởng về concurrency programming trong hình minh họa đính kèm phía dưới.

# 2. Concurrency Programming trong Python
Python, với hạn chế của GIL, khiến nó trở thành ngôn ngữ single-threaded base. Tại một thời điểm chỉ phép một luồng thực thi. Vậy những cách nào chúng ta có thể tận dụng sức mạnh của concurrency programming trong Python? Hãy khám phá một số phương pháp phổ biến dưới đây.
## 2.1 Threading
Giống như ngôn ngữ lập trình khác, chúng ta có thể sử dụng threading để tận dụng sức mạnh của lập trình đa luồng (multi-threading) trong Python. Đa luồng là một kỹ thuật sử dụng nhiều luồng chạy trong cùng một process để xử lý các tác vụ khác nhau. Trong Python, chúng ta có thể sử dụng threading trong module threading.
Use Case: Đa luồng phù hợp nhất cho các tác vụ I/O-bound, như đọc/ghi tệp, networking, hoặc tương tác với cơ sở dữ liệu.
**Một số điểm cần lưu ý:**
- Python, dưới ảnh hưởng của GIL, chỉ cho phép một luồng thực thi tại một thời điểm. Điều này có thể ảnh hưởng đến hiệu suất của các chương trình CPU-bound, như bạn có thể đã thấy trong ví dụ từ bài viết trước. Tuy nhiên, GIL ít ảnh hưởng đến các chương trình I/O-bound.
- Các tác vụ I/O-bound là những tác vụ phụ thuộc vào việc chờ đợi tài nguyên bên ngoài, chẳng hạn như đọc/ghi tệp, truy cập cơ sở dữ liệu, hoặc gửi/nhận dữ liệu qua mạng. Trong các tác vụ này, thời gian CPU không phải là yếu tố quyết định hiệu suất mà là thời gian chờ đợi I/O. Khi một tác vụ đang chờ phản hồi từ I/O (chẳng hạn như chờ dữ liệu từ một trang web), luồng có thể tạm thời giải phóng GIL.
- Khi một luồng đang chờ một tác vụ I/O hoàn thành (ví dụ: chờ dữ liệu từ mạng), Python sẽ giải phóng GIL, cho phép các luồng khác thực thi. Do đó, mặc dù chỉ có một luồng có thể giữ GIL tại bất kỳ thời điểm nào, các luồng khác vẫn có thể chạy khi GIL được giải phóng trong thời gian chờ đợi I/O, làm cho việc thực thi hiệu quả hơn.
- Trong ví dụ dưới đây, chúng ta có nhiều luồng thực hiện download_content, trong đó mỗi luồng giữ GIL trong thời gian ngắn để bắt đầu tải xuống, sau đó giải phóng nó trong khi chờ dữ liệu, và cuối cùng nắm lại GIL để xử lý dữ liệu sau khi tải xuống hoàn tất.
## 2.2 Multiprocessing
Phương pháp sử dụng đa luồng vẫn có nhược điểm là bị hạn chế bởi các tác vụ CPU-bound. Chúng ta có thể khắc phục điều này bằng kỹ thuật đa xử lý đa tiến trình (multi-processing) trong Python.

Multi-processing liên quan đến việc chạy nhiều process. Mỗi process sở hữu trình thông dịch Python và không gian bộ nhớ riêng của mình. Điều này có nghĩa là mỗi process sẽ sở hữu GIL của riêng mình. Module multiprocessing cung cấp cách thức để by pass GIL và tận dụng khả năng multi-core của CPU.

Use Case: Multi-processing lý tưởng cho các tác vụ CPU-bound yêu cầu tính toán nặng.

Một ví dụ điển hình về việc áp dụng đa xử lý trong tình huống thực tế là Gunicorn (Web Server Gateway Interface) khi triển khai ứng dụng web Python. Chúng ta thường khởi tạo một số worker process của Gunicorn với cấu hình phù hợp với CPU của server để xử lý nhiều yêu cầu đồng thời hơn.
Tuy nhiên, phương pháp sử dụng multi-processing này cũng bộc lộ hạn chế. Sử dụng multi-processing dẫn đến chi phí cao hơn so với sử dụng multi-threading. Khi các process là riêng biệt, có khả năng chiếm dụng nhiều tài nguyên.

## 2.3. Asyncio
Trong những năm gần đây, Python 3.4 đã giới thiệu Asyncio, cho phép lập trình bất đồng bộ (non-blocking) trong Python.

Asyncio cho phép bạn viết concurrent code sử dụng cú pháp async/await, khá giống với JavaScript và Node.js. Nó phù hợp cho các tác vụ I/O-bound liên quan đến việc chờ đợi, chẳng hạn như các bài toán networking mà không cần phải sử dụng đến luồng hoặc quy trình.

Even loop: asyncio chạy trên một vòng lặp sự kiện xử lý các tác vụ bất đồng bộ. Các tác vụ không bị chặn và có thể tạm dừng và tiếp tục, cho phép các tác vụ khác chạy mà không cần chờ đợi task vụ hiện tại.

Use case: Asyncio rất phù hợp cho các ứng dụng mạng hiệu suất cao, chẳng hạn như các ứng dụng web hoặc các trình thu thập dữ liệu web scrapers.
FastAPI là một framework web Python sử dụng Asyncio để tạo các ứng dụng web Python hiệu suất cao.

Minh họa sử dụng asyncio cho concurrency programming trong Python
# Tóm tắt
Hôm nay, chúng ta đã cùng thảo luận về các phương pháp thực hiện concurrency programming khác nhau trong Python, bao gồm threading, processing, và asyncio. Tùy thuộc vào bài toán, chúng ta có thể kết hợp các phương pháp để giải quyết bài toán của mình. Bản thân mình khá ưa thích lập trình bất đồng bộ sử dụng asyncio trong Python. Vì vậy, bài viết tiếp theo sẽ là về chủ đề này. Mọi người cùng chờ đợi nhé!
Một lần nữa, mình là Phan. Một nhà phát triển tò mò và tận tâm. Hẹn gặp lại các bạn trong các bài viết tiếp theo.