---
title: "Tìm Hiểu Về Chữ S Trong Https"
date: 2019-05-04
draft: false
tags: ["https", "secure"]
categories: ["rails notes"]
mytag: "Secure/HTTPS"
---

# Đặt vấn đề

Đi luôn vào chủ đề, khi mới bắt đầu với môn mạng máy tính ở trường đại học, sự mập mờ khi còn ngồi trên ghế nhà trường khiến chúng ta đôi khi đã nhầm lẫn về `http` và `https`, nhớ ngày đó tôi đã từng nghĩ chúng là 2 giao thức khác nhau, à mà ngày đó tôi có hiểu giao thức là gì không nhỉ :fearful: thôi dẹp qua một bên, bản chất của `https` cũng là giao thức `http` nhưng thêm được chữ `s` ứng với `secure`. Nghe thôi đã thấy bảo mật rồi, `https` ra đời nhằm mục đích làm cho giao thức `http` trở nên an toàn hơn, vậy nó làm cho `http` trở nên an toàn hơn như thế nào?

# Luận bàn

# 1. Http hiểu đơn giản thì hoạt động thế nào?

![hoa](/images/ssl1.png)

Mục đích cuối cùng của mớ hỗn độn rối rắm này cũng là truyền nhận thông tin, tôi có một website tôi muốn gửi nó lên mạng internet để bạn, một ai đó mà tôi không quen có thể vô tình lướt qua đọc được.
Http là một giao thức, hiểu đơn giản là một bộ quy tắc để chung để người sử dụng dùng trình duyệt có thể truy cập tới 1 trang web, và trang web đó hiểu được yêu cầu đó rồi trả về nội dung mà trình duyệt có thể hiểu được, ví như có nhiều ngôn ngữ trên thế giới, vậy giữa 2 người có 2 tiếng nói khác nhau để giao tiếp được họ phải cùng nhau sử dụng một bộ ngôn ngữ chung mà cả hai cùng hiểu được.

Một đặc điểm cơ bản của `http` là nó truyền nhận thông tin dưới dạng **text** thông thường, không hề mã hoã, điều này dẫn tới vấn đề đó là thông tin được truyền nhận nhanh chóng, nhẹ nhàng, nội dung rất thân thiện với người dùng (vì nó là text mà).

Mọi thứ có vẻ good? không hẳn như vậy, việc dữ liệu truyền gửi được lưu dưới dạng text khiến nó quá thân thiện với người dùng, mà người dùng thì không phải ai cũng tốt :smirk: . Có những người dùng mà mục đích họ tới với website của bạn là để phá hoại, họ sẽ dễ dàng tấn công bằng cách nào đó lấy được request của bạn rồi đọc được nội dung trong request đó 1 cách dễ dàng.

Bài học: Không phải lúc nào cũng nên quá thân thiện với người dùng cuối :worried:

# 2. Https khắc phục vấn đề của http như thế nào?

Chúng ta đã nắm được khái quát vấn đề bảo mật gặp phải khi sử dụng `http`. Với những website giải trí thuần tuý với nội dung chủ yếu là hình ảnh âm thanh và không có thông tin cần bảo mật khi không thành vấn đề khi dùng http. Nhưng nếu bạn sử dụng internet banking với http, khi bạn đăng nhập vào tài khoản của mình, gửi một gói tin lên server với username/id và mật khẩu được gửi dưới dạng text trần trụi, bạn thì lại đang truy cập 1 điểm wifi ở 1 cafe house nào đó, nếu có kẻ gian đã có tính toán bủa vây quanh bạn nơi đó, thì còn gì ngăn cản chúng có thể lấy được thông tin đăng nhập của bạn ngay sau khi chúng bắt được gói tin bạn request gửi đi? :disappointed:

Https giải bài toán trên bằng cách, dùng một cách nào đó mã hoá giữ liệu cần `gửi đi/trả về`. Và như vậy là xong, tên hacker xấu xa bỉ bổi vô sỉ (có thể tên là Nhật Duy) trong quán cafe kia sẽ lặng lẽ buồn rầu bỏ cuộc vì dù hắn có bắt được gói tin của bạn thì nó cũng được mã hoá, hắn gãi đầu, gãi tai làm sao để giải mã, làm sao để lấy được thông tin đăng nhập của bạn, cứ thế hắn cứ gãi cứ gãi, còn bạn thì vẫn an toàn (tạm thời).

# 3. Https và vấn đề mã hoá dữ liệu

Trước tiên phải làm rõ là:

| https = http + ssl

Trong đó:

1. http là giao thức tryền tải.

2. ssl là cơ chế bảo mật thông tin.

Note: Sẽ là một bài vietsub rất dài nếu liệt kê mọi điều liên quan về 2 khái niệm này, thay vào đó tôi muốn một cái nhìn khái quát nhanh chóng và dễ tiếp cận. Nếu bạn cần những hiểu biết sâu sắc hơn hãy tìm đến các tài liệu chính thông được những nhà phát triển công bố.

Hãy bắt đầu với một câu chuyện thủa học trò: Tôi là A, tôi thích B, hiện giờ đang trong giờ học môn XYZ nào đó, chúng tôi không có điện thoại, tôi sẽ lựa chọn cách thức khá sơ khai để gửi gắm tình yêu trong sáng của tôi đến B đó là viết ra giấy rồi ném cho B đọc :kissing_heart:

Với http, tôi sẽ viết ra giấy "i love diu" rồi ném cho B, mọi việc đều êm xuôi trừ phi cô giáo (ở đây đóng vai trò là hacker) bắt được mẩu giấy đó và đọc được nội dung, ok fine, tôi sẽ xuống đứng góc lớp mà chả thế biện bạch gì thêm :tired_face:

Với **tư tưởng** https, tôi sẽ viết ra giấy nội dung "i love diu" dưới dạng mã hoá, cô giáo nếu bắt được cũng chỉ nhìn đoạn chữ giun dế mà không hiểu gì, có lẽ tôi vẫn sẽ phải đứng góc lớp nhưng chắc chắn sẽ nhẹ nhàng hơn trường hợp trên :smiley:

Tuy nhiên bên trên chỉ là tư tưởng của https mà thôi, thực tế thì sẽ phức tạp hơn thế.

Các bước tối thiểu cần có như sau:

1. `client hello`, người dùng sử dụng browser sẽ request tới server, đây là tín hiệu để khởi tạo kết nối ssl.

2. `server hello`, khi mà request ở bước một đã tới nơi, server sẽ gửi trả client 2 thông tin quan trọng đó là `ssl certificate` và `public key`.

3. Sau khi kết thúc 2 bước đầu mang tính xã giao để khởi tạo kết nối. Client lúc này đã nhận được dữ liệu từ server ở bước 2, browser sẽ xác minh `ssl certificate`.

4. Browser sau khi xác minh thành công ở bước 3, sẽ sinh ra một `khoá`, khoá này sau đó sẽ được mã hoá tiếp bằng `public key` đã nhận được từ bước 2 (khi gửi lên server thì khoá này đang tồn tại dưới dạng được mã hoá bởi `public key`).

5. Toàn bộ nội dung của request đều sẽ được mã hoá bằng `khoá` ở bước 4, kẻ gian nếu đánh cắp được gói tin này thì sẽ cần có giá trị `khoá` để giải mã, tuy nhiên đáng buồn thay là lúc này khi được gửi đi thì `khoá` đã được mã hoá bằng `public key` vì vậy không thể giải mã được nếu thiếu `private key` được lưu ở server.

6. Request tới server, giá trị `khoá` sẽ được giải mã ra nhanh chóng vì server đang có `private key`. từ giá trị `khoá` này, server sẽ giải mã ra nội dung của request.

Note: Trong nội dung trên có đề cập đến vấn đề mã hoá rất nhiều, nhưng không hề đề cập đến việc sử dụng thuật toán nào để mã hoá, tôi nghĩ rằng chúng ta nên đọc những tài liệu chính thông để có thông tin xác thực nhất, cá nhân tôi, tôi cũng chưa tìm hiểu :kissing_heart:

# 4. Áp dụng https trong dự án như thế nào?

Như đã trình bày ở mục số 3, https là http có thêm cơ chế ssl, cơ chế ssl bạn có thể sử dụng bởi 1 nhà cung cấp bên thứ 3 (Certificate Authority) ví dụ như GoDaddy, Comodo hay 1 dịch vụ miễn phí như Let’s Encrypt.

Nói chung là vì sử dụng dịch vụ bên thứ 3 nên không thể miêu tả phần này được, mỗi dịch vụ sẽ có những tuỳ biến riêng, âu thì mình cứ follow theo trang chủ cho an tâm nhỉ.

# Kết luận

Nói mới nhớ thì thấy mấy anh công ty cũ từng bảo `ranking` google giờ có ảnh hưởng bởi việc bạn sử dụng https hay không, nghe đâu thì việc sử dụng https sẽ giúp bạn có cơ hội bay cao hơn trong bảng rank website của google, có lẽ tôi cũng phải trích rút thời gian sao mà update cái blog nhỏ này lên https, với hi vọng bớt cảnh vắng tanh như chùa bà đanh :pensive:
