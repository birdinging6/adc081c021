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
![](https://github.com/birdinging6/adc081c021/blob/main/images/1.png)
