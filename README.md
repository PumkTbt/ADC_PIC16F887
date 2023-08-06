# ADC_PIC16F887

Đo giá trị điện áp lấy từ chân RE1 (0V  5V), chuyển đổi ra giá trị số và hiển thị 8 bit thấp của giá trị số sau khi chuyển đổi trên 8 led. Với fosc = 4MHz. Lập trình PIC16F887,
sử dụng module ADC.

![image](https://github.com/PumkTbt/ADC_PIC16F887/assets/124877073/b4193d12-58b1-4eb1-a5ff-dd0a88d075fc)

Phân tích yêu cầu:
Với yêu cầu chuyển đổi giá trị analog từ chân AN6 (RE1) thành tín hiệu số, và hiển thị lên 8 led nhưng mà chỉ lấy 8 bit thấp của số 10 bit để biểu diễn nên. Ta
có thể sử dụng canh phải, thì khi đó bit ADFM của thanh ghi ADCON1 sẽ bằng 1 (ADFM = 1). Nguồn lấy từ chân của pic, nên hai bit VCFG1 và VCFG0 sẽ có giá trị là 0 (Vss=Vdd=0). Từ đó suy ra thanh ghi ADCON1 có giá trị:
ADCON1 = 0b10000000
- Với nguồn điện áp lấy từ chân RE1 (AN6) thì ta có được 4bit CHS2, CHS2, HS1, CHS0 trong thanh ghi ADCON0 có giá trị là: 0110
- Chọn nguồn xung clock ADC là: Fosc/32. Nên hai bit đầu trong thanh ghi ADCON0 có giá trị là: ADCS1 = 1, ADCS0 = 0. Từ đó ta có thể suy ra được thanh ghi ADCON0 có giá trị:
ADCON0 = 0b10011001

Kết quả hiện thị như sau:
![image](https://github.com/PumkTbt/ADC_PIC16F887/assets/124877073/9abfc2fe-98af-4ff8-8d60-187ea140bc5e)
Ta thấy được là với giá trị vào Vin = 4V, Vref(+) = 5V, Vref(-) = 0V. Biểu diễn là 10 bit nên n = 10 Theo mô phỏng ta thấy bit thấp đến bit cao là từ phải qua trái, led sáng đúng yêu cầu
![image](https://github.com/PumkTbt/ADC_PIC16F887/assets/124877073/1f55d15f-d717-4d94-8f18-a7a990c19f16)
Với kết quả này thì từ công thức tính DV ở trên ta có:
𝐷𝑉 = (2,5. (210 − 1))/(5 − 0) = 511,5
DV2 = 111111111(2) với chỉ lấy 8bit thấp thì ta có 8bit thấp là: 11111111

