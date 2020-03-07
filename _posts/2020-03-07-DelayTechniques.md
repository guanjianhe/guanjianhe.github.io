---
layout: post
title: 一种延时技巧
tag: 单片机
---

代码如下：

```c
#define bSystem10Msec gTimer.Status.field.bit0
#define bSystem50Msec gTimer.Status.field.bit1
#define bSystem100Msec gTimer.Status.field.bit2
#define bSystem1Sec gTimer.Status.field.bit3

#define bTemp10Msec gTimer.Status.field.bit4
#define bTemp50Msec gTimer.Status.field.bit5
#define bTemp100Msec gTimer.Status.field.bit6
#define bTemp1Sec gTimer.Status.field.bit7

typedef enum
{
    TIMER_RESET = 0,
    TIMER_SET = 1,
} TimerStatus;

typedef struct
{
    unsigned char bit0 : 1;
    unsigned char bit1 : 1;
    unsigned char bit2 : 1;
    unsigned char bit3 : 1;
    unsigned char bit4 : 1;
    unsigned char bit5 : 1;
    unsigned char bit6 : 1;
    unsigned char bit7 : 1;
} Timer_Bit;

typedef union
{
    unsigned char byte;
    Timer_Bit field;
} Char_Field;

typedef struct
{
    unsigned char Tick10Msec;
    Char_Field Status;
} Timer_Struct;

//定义一全局变量
Timer_Struct gTimer;

//10ms中断服务函数，在这里置位的是高四位
void SysTick_Handler(void)
{
    bTemp10Msec = TIMER_SET; //10ms时间到，设置标志位
    ++gTimer.Tick10Msec;     //10ms累计次数

    if (0 == (gTimer.Tick10Msec % 5)) //50ms时间到
    {
        bTemp50Msec = TIMER_SET;
    }

    if (0 == (gTimer.Tick10Msec % 10)) //100ms时间到
    {
        bTemp100Msec = TIMER_SET;
    }

    if (100 == gTimer.Tick10Msec) //1s时间到
    {
        gTimer.Tick10Msec = 0; //这里累计次数要清零
        bTemp1Sec = TIMER_SET;
    }
}

void SysTimer_Process(void)
{
    __disable_irq();            //关中断
    gTimer.Status.byte &= 0xF0; //低四位清零
    gTimer.Status.byte >>= 4;   //“祸水东引”，把高4位给低四位
    gTimer.Status.byte &= 0x0F; //高4位清零，准备在中断中置位
    __enable_irq();             //开中断
}

int main(void)
{
    while (1)
    {
        SysTimer _Process();

        if (TIMER_SET == bSystem10Msec)
        {
            //dosomething
        }

        if (TIMER_SET == bSystem50Msec)
        {
            //dosomething
        }

        if (TIMER_SET == bSystem100Msec)
        {
            //dosomething
        }

        if (TIMER_SET == bSystem1Sec)
        {
            //dosomething
        }
    }
}

```

---

转载请注明：[guanjianhe的博客](https://guanjianhe.github.io/) » [一种延时技巧](https://guanjianhe.github.io/2020/03/DelayTechniques/)
