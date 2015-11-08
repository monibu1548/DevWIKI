## WiringPi 를 이용한 software PWM Control

- Raspberry Pi 의 wiringPi 라이브러리를 사용하여 pwm을 software로 처리

### PWM 이란
- PWM ( Pulse Width Modulation )
- " 디지털 출력으로 아날로그 회로를 제어하는 강력한 기법 "
- 전체 주기에서 HIGH ( 1 ) 이 차지하는 비율 ( Duty Ratio ) 로 결정된다.

### Hardware PWM  vs  Software PWM

- Arduino 의 경우 5개, Raspberry 의 경우 1개의 하드웨어 PWM 을 제공한다.
- 역시 해당 핀의 레지스터에 값을 넣음으로써 제어.

|하드웨어 PWM|소프트웨어 PWM|
|---|---|
| 해당 레지스터에 값을 넣으면 그에 해당하는 듀티 비의 PWM 이 일정하게 생성된다 | 커널에서 제공하는 각종 delay 함수를 사용하여 해당 핀을 HIGH, LOW로 수정함으로써 강제적으로 PWM 을 흉내낸다.
|정확한 주기, 정확한 듀비티를 구현 가능하다, 일반적으로 전체 주기는 결정할 수 없으나 일부 라이브러리 형태로 제공|장점은 전체 주기, 듀티비를 사용자 임의로 지정 가능하다. 치명적인 단점은 PWM 하나가 하나의 쓰레드를 차지하므로 현재 CPU 상태에 의해 부정확한 값이 출력될 수 있다.|

### WiringPi - softPWM.c 분석

#### 쓰레드를 생성하는 부분

range ( 전체 주기 ) = [ mark ( HIGH 시간 ) + space ( LOW 시간 ) ] * 임의상수 으로 식이 정해져 있다.

시간 지연함수로는 MicrosecondsDelay() 함수를 사용하여 파형을 유지한다

임의 상수의 기본값은 100 으로 지정되어있다.

따라서 softPwmCreate() 의 range 전달인자로 100을 줄 경우

> 100 * 100 = 100000 us 의 지연시간을 갖는다. 즉 주기는 100Hz 가 된다

즉 range 와 임의상수 값을 조작하여 사용자가 원하는 주기를 만들어 낼 수 있다.

 - 왜 사용자가 주기를 만들 필요가 있을까?!

> 드론 or 정밀 제어가 필요한 장치는 높은 주파수를 요구한다.

> 드론과 같은 RC 계 장치에서는 50Hz 가 표준 주파수이며 드론에서는 보통 400Hz 를 사용해야 안정적인 제어를 할 수 있다고 한다.
> 따라서 나는 Range 2500 에 임의 상수는 1로 2500us, 즉 2.5ms = 400Hz 를 만들어 드론 제어에 사용하였다.