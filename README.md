# C51-programming-tips
C51编程小技巧
日常嵌入式控制编程小技巧合计。


## 检查信号 - “低转高检查”
检测输入信号，起始为低电平并在一定时间内变为高电平。

```c
sbit Signal_PORT = P3^7;//这是要检测的信号接口

unsigned int Signal_check(void)
{
    u8 time_temp = 0;

    // 等待DQ为低电平，超时返回1
    while (Signal_PORT && time_temp < 20) 
    {
        time_temp++;
        delay_10us(1);    
    }
    if (time_temp >= 20) return 1;

    // 重置time_temp，等待DQ为高电平，超时返回1
    time_temp = 0;
    while (!Signal_PORT && time_temp < 20) 
    {
        time_temp++;
        delay_10us(1);
    }
    if (time_temp >= 20) return 1;

    return 0;
}
```




























