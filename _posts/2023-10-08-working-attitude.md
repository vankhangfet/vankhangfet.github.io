---
layout: post
title: Thế nào là làm việc nghiêm túc?
tags: [Others]
---
Trong tuần đợt phát hành phiên bản phầm mềm vừa rồi, đội nhóm của chúng tôi đã làm việc không tốt. Lý do không tốt ở đây là chúng tôi
đã có một số bug còn xảy ra khi app đã được public trên store. Điều đó dẫn đến khách hàng có phàn nàn về chất lượng, cho dù chúng tôi
đã rất nỗ lực để đưa sản phẩm được bàn giao đúng ngày, và đến với khách hàng sớm hơn.

Tôi đã nhận được một phàn nàn rằng chúng tôi đã làm việc "chưa đủ nghiêm túc". Tôi đã bất ngờ khi nghe thấy vậy, tuy nhiên điều đó khiến tôi dành thời gian suy nghĩ kỹ càng hơn về đội nhóm, cách thức làm việc. Tại sao khách hàng có cảm nhận như vậy? 

Làm product rất khó, không hề đơn giản. Nó yêu cầu đội phát triển phải thật cẩn thận, chỉn chu, chi tiết nữa. Điều này sẽ khó nhận ra đối
với đội BE, nhưng với team FE thì dễ dàng nhận ra hơn. End-user sẽ nhìn thấy giao diện sản phẩm đầu tiên, và bất cứ điều gì làm cho user 
cảm thấy không thân thiện, có nghĩa ràng chúng ta đã làm sản phẩm chưa đủ tốt.

Nhìn lại quá trình phát triển thì chúng tôi đã mắc một số lỗi cơ bản, khi so sánh giao diện, hiển thị giữa iOS và Android. Có một khác biệt, nhưng dường như chúng tôi đã không nhận ra. Điều đó khiến khách hàng nghĩ rằng chúng tôi đã không nghiêm túc, tuy điều này có hơi bất công, nhưng nó là bài học quý giá để chúng tôi nhận ra rằng, cần phải chỉn chu hơn nữa. Phân tích kỹ hơn một chút, tôi nhận ra rằng
khi phân tích nguyên nhân và cách giải quyết các bạn dev đã không cung cấp đủ tốt thông tin. Và nó gián tiếp dẫn đến một hệ quả đó là người đọc có cảm giác sự cố đã không được phân tích kỹ càng, và nó có thể lặp lại trong tương lai. 

Vậy làm sao để khắc phục điểm này? 

"Lỗi xảy ra" --> "Không nhận ra" --> "Nhận ra lỗi" --> "Lặp lãi lỗi". Nếu như bạn rơi vào vòng lặp như vậy, thì nó sẽ khiến đội phát triển của bạn gặp khó khăn, và khách hàng sẽ có ấn tượng không tốt. 

Điều cần làm là, khi "nhận ra lỗi" hãy phân tích thật kỹ nguyên nhân. Làm thế nào để phân tích kỹ nguyên nhân? Tôi nghĩ phải thực hiện
ít nhất 2Why? Có lẽ không cần 5Why? Nhưng đặt câu hỏi tự vấn 2 lần bao giờ cũng tốt hơn 1 lần, nó sẽ giúp bạn tốt hơn trong lần tiếp theo.

Hãy xem một tình huống mà tôi gặp phải?


