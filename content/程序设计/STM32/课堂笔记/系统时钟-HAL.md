# 硬件原理

系统滴答定时器  systick   ->  M3内核中的定时器  ->  默认能用的  

# 使用原理

(1) 配置计数的时基  ->  多长时间触发一次中断

​	基础时间 -> 默认使用的72MHz -> 1/72us  ->  clkSource = 1

​	配置需要的时间 -> 重装载寄存器  ->

​		循环触发 -> N-1   一次性使用 -> N

(2) 中断处理函数中 编写响应的代码逻辑

# 案例实现

(1) hal系统帮助我们实现了systick的初始化 

​	72MHz  ->   配置1ms的中断周期  -> 设置了对应的优先级  

(2) 编写中断处理函数

​	SysTick_Handler ->  弱定义 HAL_IncTick  -> 实现一下就可以了  ->  

​	被hal库用作延迟  ->  不要修改源代码  可以直接使用累加的值完成

```c
void HAL_IncTick(void)
{
  // 不要删除原先的计数代码
  uwTick += uwTickFreq;
  // count++;
  if (uwTick % 1000 == 0)
  {
    HAL_GPIO_TogglePin(LED1_GPIO_Port, LED1_Pin);
  }
}
```

