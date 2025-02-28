# adc081c021使用记录
## 第一个内部寄存器：地址指针寄存器
在IIC协议中选定好adc081c021的器件地址后，第一个BIT即要确定此寄存器值，来指定后续读取和配置的寄存器。
![](https://github.com/birdinging6/adc081c021/blob/main/images/1.png)
8'h00:AD转换结果寄存器（只读）

8'h01:报警状态寄存器

8'h00:设置寄存器

8'h00:报警低限存器

8'h00:AD转换结果寄存器

8'h00:AD转换结果寄存器

8'h00:AD转换结果寄存器
## 第二个内部寄存器：AD转换结果寄存器（只读）
在自动模式下，该寄存器被读一次，就进行并完成一次转换。
![](https://github.com/birdinging6/adc081c021/blob/main/images/2.png)
reg[15]为报警标志位，由报警状态寄存器与报警状态寄存器共同控制，详见下面两个寄存器管脚说明

reg[14:12]预留

reg[11:4]为AD转换结果位，reg[11]为最高位，reg[4]为最低位。

reg[3:0]预留
## 第三个内部寄存器：报警状态寄存器
显示电压超上限还是下限并控制AD转换结果寄存器的reg[15]
![](https://github.com/birdinging6/adc081c021/blob/main/images/3.png)
reg[7:2]预留

reg[1]为上限报警位 1'b1:所输入的电压值超过报警上限阈值,并使得AD转换结果寄存器的reg[15]为1'b1
                  1'b0:(1)iic直接写为1'b0;(2)设置寄存器中reg[4]为1'b0,且恢复到阈值内

reg[0]为下限报警位 1'b1:所输入的电压值低于报警下限阈值,并使得AD转换结果寄存器的reg[15]为1'b1
                  1'b0:(1)iic直接写为1'b0;(2)设置寄存器中reg[4]为1'b0,且恢复到阈值内
## 第四个内部寄存器：报警状态寄存器

![](https://github.com/birdinging6/adc081c021/blob/main/images/4.png)
reg[7:5]为循环间隔

reg[4]为上下限报警自动清除位 1'b0:当电压值恢复到阈值内时,报警状态寄存器中已经变化的报警位恢复                                  到1'd0
                           1'b1:当电压值恢复到阈值内时,报警状态寄存器中已经变化的报警位不会                                  恢复到1'd0.只有手动写入1'b0才会恢复
                           
reg[3]为报警标志使能位 1'b0:使得AD转换结果寄存器中reg[15]不起作用
                      1'b1:使得AD转换结果寄存器中reg[15]起作用

reg[2]为ALERT管脚使能位 1'b0:失能ALERT管脚，使其可输出高阻态
                       1'b1:使能ALERT管脚，使其可输出1'b0 or 1'b1

reg[1]保留,必须被写为1'b0

reg[0]为ALERT管脚输出位 1'b0:ALERT管脚输出1'b0
                       1'b1:ALERT管脚输出1'b1
## 第五个内部寄存器：下限寄存器
设置下限电压
![](https://github.com/birdinging6/adc081c021/blob/main/images/5.png)
reg[15:12]保留,必须被写为1'b0

reg[11:4]为下限电压设置位，reg[11]为高位

reg[3:0]保留,必须被写为1'b0
## 第六个内部寄存器：上限寄存器
设置下限电压
![](https://github.com/birdinging6/adc081c021/blob/main/images/6.png)
reg[15:12]保留,必须被写为1'b0

reg[11:4]为上限电压设置位，reg[11]为高位

reg[3:0]保留,必须被写为1'b0
## 第七个内部寄存器：滞回电压寄存器
设置滞回电压值Va，便于报警后报警位的清除。当电压低于上限值Va的范围或高于下限值Va的范围后能自动清除，注意报警状态寄存器中reg[4]上下限报警自动清除位应为1'b0才可起作用。
![](https://github.com/birdinging6/adc081c021/blob/main/images/7.png)
reg[15:12]保留,必须被写为1'b0

reg[11:4]为滞回电压值Va设置位，reg[11]为高位

reg[3:0]保留,必须被写为1'b0
## 第八个内部寄存器：最低电压值Vmin寄存器
在自动转换模式下，若所得电压V<Vmin,则Vmin<=V,否则不变，在任何情况下都可写入16'h0fff清空Vmin
在正常模式下不起作用
![](https://github.com/birdinging6/adc081c021/blob/main/images/8.png)
reg[15:12]保留,必须被写为1'b0

reg[11:4]为最低电压值Vmin设置位，reg[11]为高位

reg[3:0]保留,必须被写为1'b0
## 第九个内部寄存器：最高电压值Vmax寄存器
在自动转换模式下，若所得电压V>Vmax,则Vmax<=V,否则不变，在任何情况下都可写入16'h0000清空Vmin
在正常模式下不起作用
![](https://github.com/birdinging6/adc081c021/blob/main/images/9.png)
reg[15:12]保留,必须被写为1'b0

reg[11:4]为最高电压值Vmax设置位，reg[11]为高位

reg[3:0]保留,必须被写为1'b0
