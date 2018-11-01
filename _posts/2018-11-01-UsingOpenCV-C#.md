---
layout: post
title: Sử dụng Open CV với C#
tags: [.Net]
---
Nếu bạn đã từng làm một số project có liên quan đến xử lý ảnh thì chắc hẳn sẽ biết thư viện OpenCV. Hiện tại đã có phiên bản OpenCV cho .Net là EmgCV, tuy nhiên với ứng dụng thương mại bạn sẽ phải trả tiền. Để tăng tốc độ xử lý cũng như dễ dàng hơn thì theo mình bạn nên sử dụng OpenCV trước sau đó mới đến EmguCV.

Với những ai chưa nghe đến OpenCV hoặc EmguCV bao giờ thì bạn có thể tham khảo ở link sau:
Open CV https://opencv.org (https://opencv.org)
EMGU CV http://www.emgu.com/wiki/index.php/Main_Page (http://www.emgu.com/wiki/index.php/Main_Page)

OpenCV được viết bằng C++, nên sẽ có chút khó khăn khi bạn muốn sử dụng các function của OpenCV trên C#.Net.

Tình huống mình gặp phải đó là trên app của mình có hiển thị ảnh ,với Winform app thì việc hiển thị ảnh hay dùng đối tượng Bitmap. Nhưng OpenCV xử lý ảnh dưới dạng ma trận là kiểu Cv::Mat. Mình mất thời gian để tìm hiểu convert giữa 2 kiểu dữ liệu này và cách làm như sau:

Để dùng OpenCV trên project.Net bạn cần phải xây dựng một class warpper, class này sẽ làm nhiệm vụ giao tiếp giữa C++ và C# như trong project của mình. Việc viết một class wrapper như thế nào mình sẽ viết chi tiết vào một topic khác ^^.

Nguyên lý hoạt động của lớp wrap như sau:

![Wrap-opencv](/img/wrap-opencv.jpg "Wrap-opencv")


Khi có lớp wrapper này rồi thì công việc còn lại chỉ là convert kiểu dữ liệu để xử dụng. Các bạn sử dụng các method sau:
Convert Bitpmap to Mat trong Open CV

~~~~
Mat BitmapToMat(System::Drawing::Bitmap^ bitmap)`
{
IplImage* tmp;

System::Drawing::Imaging::BitmapData^ bmData = bitmap->LockBits(System::Drawing::Rectangle(0, 0, bitmap->Width, bitmap-`>Height), System::Drawing::Imaging::ImageLockMode::ReadWrite, bitmap->PixelFormat);`
if (bitmap->PixelFormat == System::Drawing::Imaging::PixelFormat::Format8bppIndexed)
{
    tmp = cvCreateImage(cvSize(bitmap->Width, bitmap->Height), IPL_DEPTH_8U, 1);
    tmp->imageData = (char*)bmData->Scan0.ToPointer();
}

else if (bitmap->PixelFormat == System::Drawing::Imaging::PixelFormat::Format24bppRgb)
{
    tmp = cvCreateImage(cvSize(bitmap->Width, bitmap->Height), IPL_DEPTH_8U, 3);
    tmp->imageData = (char*)bmData->Scan0.ToPointer();
}

bitmap->UnlockBits(bmData);

return Mat(tmp);
}
~~~~

Convert from Mat to BitMap

~~~~
System::Drawing::Bitmap^ MatToBitmap(Mat srcImg){
int stride = srcImg.size().width * srcImg.channels();//calc the srtide
int hDataCount = srcImg.size().height;

System::Drawing::Bitmap^ retImg;

System::IntPtr ptr(srcImg.data);
//create a pointer with Stride
if (stride % 4 != 0){//is not stride a multiple of 4?
    //make it a multiple of 4 by fiiling an offset to the end of each row
		
//to hold processed data
    uchar *dataPro = new uchar[((srcImg.size().width * srcImg.channels() + 3) & -4) * hDataCount];

    uchar *data = srcImg.ptr();

    //current position on the data array
    int curPosition = 0;
    //current offset
    int curOffset = 0;

    int offsetCounter = 0;
		//itterate through all the bytes on the structure
    for (int r = 0; r < hDataCount; r++){
        //fill the data
        for (int c = 0; c < stride; c++){
            curPosition = (r * stride) + c;

            dataPro[curPosition + curOffset] = data[curPosition];
        }

        //reset offset counter
        offsetCounter = stride;

        //fill the offset
        do{
            curOffset += 1;
            dataPro[curPosition + curOffset] = 0;

            offsetCounter += 1;
        } while (offsetCounter % 4 != 0);
    }
		
		 ptr = (System::IntPtr)dataPro;//set the data pointer to new/modified data array

    //calc the stride to nearest number which is a multiply of 4
    stride = (srcImg.size().width * srcImg.channels() + 3) & -4;

    retImg = gcnew System::Drawing::Bitmap(srcImg.size().width, srcImg.size().height,
        stride,
        System::Drawing::Imaging::PixelFormat::Format24bppRgb,
        ptr);
}
else{

    //no need to add a padding or recalculate the stride
    retImg = gcnew System::Drawing::Bitmap(srcImg.size().width, srcImg.size().height,
        stride,
        System::Drawing::Imaging::PixelFormat::Format24bppRgb,
        ptr);
}

array^ imageData;
System::Drawing::Bitmap^ output;

// Create the byte array.
{
    System::IO::MemoryStream^ ms = gcnew System::IO::MemoryStream();
    retImg->Save(ms, System::Drawing::Imaging::ImageFormat::Png);
    imageData = ms->ToArray();
    delete ms;
}

// Convert back to bitmap
{
    System::IO::MemoryStream^ ms = gcnew System::IO::MemoryStream(imageData);
    output = (System::Drawing::Bitmap^)System::Drawing::Bitmap::FromStream(ms);
}

return output;
}
~~~~

OK! với 2 function như trên chúng ta đã convert được dữ liệu cvMat <-> Bitmap một cách dễ dàng. Việc xử lý ảnh ra sao thì openCV đã có rất nhiều
method để làm rồi. 
