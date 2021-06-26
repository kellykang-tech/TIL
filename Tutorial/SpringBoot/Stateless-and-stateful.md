# Stateless와 Stateful

## 1. Stateful?
자바에서 소켓 통신을 할 때 A와 B포트가 연결 돼 있는 상황이다.

```   
 포트                           포트
┌────┐                        ┌────┐
│ A  │ ────────write────────> │  B │
└────┘ <────────read───────── └────┘
                               ^  ^
┌────┐                         │  │
│ C  │ <───────────────────────┘  │
└────┘                            │
                                  │
┌────┐                            │
│ D  │ <──────────────────────────┘
└────┘
```

- **`stateful`** 방식이란 연결이 지속돼있다는 의미이다.

- B가 인증을 통해 A를 확인하고나면 세션이 만들어진다. 세션이 만들어진다는 것은 데이터를 응답해줄 준비가 됐다는 의미이다.

- B 포트의 입장에서는 연결해야 하는 포트가 많아지므로 굉장히 바빠진다. 그러므로 http통신은 stateful 방식을 사용하지 않는다.

- 계속 연결해서 데이터를 주고 받는 채팅은 stateful 방식을 사용한다.
<br>

## 2. Stateless?

```   
클라이언트                      서버
┌────┐ ────────write────────> ┌────┐
│ A  │                        │  B │
└────┘ <────────read───────── └────┘
```
- 요청과 응답이 일어나면 통신을 바로 끊어버린다.  
  요청시마다 스트림을 연결해서 data를 주고 받는 방식을 **`stateless`** 라고 한다.

- stateless방식은 서버 입장에서 부하가 적다.   
  필요할 때마다 `요청 -> 응답 -> 선 끊기`가 이루어진다.

- 한 번 인증을 했을 때, 선이 바로 끊어지는데 새로운 요청이 들어왔을 때 이 클라이언트가 이전의 동일한 클라이언트가 맞는지 보장이 안된다.  
 (= 세션을 유지할 수 있는 방법이 없다.)
<br>

## 3. 알아야할 것

- http는 문서 전달의 목적으로 만들어졌다.  
  하지만 요즘 http는 웹서비스도 만들고 회원가입도 하고 데이터도 주고 받고 인증도 받고 여러가지를 하는데 선이 끊겨버리면 그 사람이 다음에 요청했을 때 동일한 사람인지 어떻게 알 수 있을까?   
  어떻게 인증을 해서 세션을 만들 수 있을까?

- 스프링에서는 시큐리티를 사용해서 어떻게 세션을 유지할 것인지에 대해 배울 수 있다.
  
- 서버가 늘어나고 사용자가 많아짐에따라 세션 생성, 유지, 증명, 데이터 보장, 관리, 암호화를 어떻게 할 것인지를 배우는 것이 관건이다.


 