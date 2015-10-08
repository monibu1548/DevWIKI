# 모터의 PID 제어

## PID 란
> P : Proprotinal 비례

> I : Intergral   적분

> D : Differential 미분

을 이용한 자동제어 방식. 실제 목표값에 오차를 적게. 도달할 수 있다.

> 조작량 = ( Kp * 편차 ) + ( Ki * 편차 누적 값 ) + ( Kd * 지난 편차와의 차 )

의 공식을 갖고 조작량을 구한다. 조작량은 모터에 입력해야줘야 하는 값을 의미한다

문제는 이제  Kp, Ki, Kd 를 구하는 것이다.

그리고 모터의 방향에 따라 pid 연산에 의해 나오는 결과를 달리 사용해야 한다.

[ 앞 ]
1   2
 \ /
 / \
4   3
[ 뒤 ]

1,3 번 CW
2,4 번 CCW 일때

1번 제어값 = throttle - PID[roll] + PID[pitch] + PID[yaw]
2번 제어값 = throttle + PID[roll] + PID[pitch] - PID[yaw]
3번 제어값 = throttle - PID[roll] - PID[pitch] - PID[yaw]
4번 제어값 = throttle + PID[roll] - PID[pitch] + PID[yaw]
