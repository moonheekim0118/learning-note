# π μ μ‘ κ³μΈ΅ (Transport Layer)

[μ μ‘κ³μΈ΅](https://velog.io/@moonheekim0118/%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC-OSI-7%EA%B3%84%EC%B8%B5#4-%EC%A0%84%EC%86%A1-%EA%B3%84%EC%B8%B5-transport-layer)μ μλν¬μΈνΈκ° **μ λ’°μ±** μλ λ°μ΄ν° **μ μ‘**μ λ΄λΉνλ κ³μΈ΅μ΄λ€.

- μ λ’°μ± : λ°μ΄ν°λ₯Ό μμ°¨μ  , μμ μ μΌλ‘ μ λ¬νλ€.
- μ μ‘ : *ν¬νΈ λ²νΈ*μ ν΄λΉνλ νλ‘μΈμ€μ λ°μ΄ν°λ₯Ό μ λ¬νλ€.

## μ μ‘κ³μΈ΅μ΄ μλ€λ©΄ ?

- λ°μ΄ν°μ μμ°¨ μ μ‘μ΄ μννμ§ μλ€.
- **νλ¦ λ¬Έμ  (Flow)** : μ‘μμ μ κ° λ°μ΄ν° μ²λ¦¬ μλ μ°¨μ΄κ° μ‘΄μ¬ ν  μ μμΌλ©°, μμ μκ° λ°μ΄ν° νκ³λμ μ΄κ³Όνλλ° μ‘μ μ μΈ‘μμ λ°μ΄ν°λ₯Ό μ μ‘νλ €κ³  ν  κ²½μ° λ°μ΄ν°κ° λλ½λλ λ¬Έμ κ° λ°μνλ€.
- **νΌμ‘ λ¬Έμ  (Congestion)** : λ€νΈμν¬ λ°μ΄ν° μ²λ¦¬ μλμ μν΄μ λ°μ΄ν°κ° μ λλ‘ μ μ‘λμ§ μμ μ μλ€.

**λ°μ΄ν°μ μμ€μ΄ λ°μνλ€. **
_μ΄λ° λ¬Έμ λ₯Ό ν΄κ²°νκΈ° μν΄μ TCPκ° λ±μ₯νλ€. _

<br/>
<br/>

# π TCP (Transmission Control Protocol)

- μ λ’°μ± μλ λ°μ΄ν° ν΅μ μ κ°λ₯νκ² ν΄μ£Όλ νλ‘ν μ½
- μλ°©ν₯ ν΅μ μ ν΅ν΄ Connection μ μ°κ²°νλ€ (3-way handshake)
- λ°μ΄ν° μμ°¨ μ μ‘μ λ³΄μ₯νλ€.
- Flow Control, νλ¦μ μ μ΄ νλ€.
- Congestion Control, νΌμ‘μ μ μ΄νλ€.
- Error Detection , μ€λ₯λ₯Ό κ°μ§νλ€.

## μΈκ·Έλ¨ΌνΈ (Segment)

![](https://images.velog.io/images/moonheekim0118/post/b9944aab-adb4-4402-b433-df339706338d/%E1%84%83%E1%85%A1%E1%84%8B%E1%85%AE%E1%86%AB%E1%84%85%E1%85%A9%E1%84%83%E1%85%B3.jpeg)

- TCP νλ‘ν μ½ λ΄λΆ λ°μ΄ν° λ¨μ
- μμ λ μ΄μ΄μμ μ μ‘λ λ°μ΄ν°λ₯Ό TCP λ΄λΆμμ μλ₯΄κ³  **TCP ν€λ**λ₯Ό μΆκ°ν κ²

## TCP ν€λ

![](<https://images.velog.io/images/moonheekim0118/post/8e0009e3-d4d2-464d-bc51-2204fae812e2/%E1%84%83%E1%85%A1%E1%84%8B%E1%85%AE%E1%86%AB%E1%84%85%E1%85%A9%E1%84%83%E1%85%B3%20(1).jpeg>)

- `SYN` : μ»€λ₯μ μ°κ²°
- `FIN` : μ»€λ₯μ μ°κ²° μ’λ£
- `ACK` : λ°μ΄ν° μμ μμ μλ΅ μ μ΄

## TCP 3-way handshake (Connection μ°κ²°)

![](<https://images.velog.io/images/moonheekim0118/post/71958a89-52aa-453d-9158-1374231f644b/%E1%84%83%E1%85%A1%E1%84%8B%E1%85%AE%E1%86%AB%E1%84%85%E1%85%A9%E1%84%83%E1%85%B3%20(2).jpeg>)

1. ν΄λΌμ΄μΈνΈ μΈ‘μμ SYN λΉνΈλ₯Ό 1λ‘ μ€μ νμ¬ ν¨ν·μ μ μ‘νλ€.
2. μλ² μΈ‘μμ μλ΅μ μλ¦¬κΈ° μν΄ SYN, ACK λΉνΈλ₯Ό 1λ‘ μ€μ νμ¬ ν¨ν·μ μ μ‘νλ€.
3. ν΄λΌμ΄μΈνΈμΈ‘μμ λ€μ ACK λΉνΈλ₯Ό 1λ‘ μ€μ νμ¬ ν¨ν·μ μ μ‘νλ€.

μ΄λ κ² ν΄μ μλ°©ν₯ μ»€λ₯μμ΄ μ°κ²°λλ©΄ μλμ κ°μ΄ λ°μ΄ν° μ μ‘μ νλ€.

## λ°μ΄ν° μ μ‘ κ³Όμ 

![](<https://images.velog.io/images/moonheekim0118/post/c3404afe-b044-48bd-bf97-3acfa9fc0b54/%E1%84%83%E1%85%A1%E1%84%8B%E1%85%AE%E1%86%AB%E1%84%85%E1%85%A9%E1%84%83%E1%85%B3%20(3).jpeg>)

1. ν΄λΌμ΄μΈνΈ μΈ‘μμ ν¨ν·μ μ‘μ νλ€.
2. μλ² μΈ‘μμ μλ΅μ μλ¦¬κΈ° μν΄ ACKλ₯Ό μ‘μ νλ€.
   _3. ACK λ₯Ό μμ νμ§ λͺ»νμ κ²½μ° , ν΄λΌμ΄μΈνΈ μΈ‘μμ ν¨ν·μ μ¬μ μ‘νλ€._

## 4 way-handshake (Connection close)

![](<https://images.velog.io/images/moonheekim0118/post/008370b8-ac19-44d9-a03a-b3c9d90c5f7f/%E1%84%83%E1%85%A1%E1%84%8B%E1%85%AE%E1%86%AB%E1%84%85%E1%85%A9%E1%84%83%E1%85%B3%20(4).jpeg>)

1. ν΄λΌμ΄μΈνΈ μΈ‘μμ FIN λΉνΈλ₯Ό 1λ‘ μ€μ νκ³  μλ²μΈ‘μ μ μ‘νλ€.
2. μλ²μΈ‘μμ μλ΅μ μλ¦¬κΈ° μν΄ ACK λ₯Ό μ μ‘νλ€.
   **_(TIME_WAIT) μλ²μΈ‘μμ λ¨μ ν¨ν·μ ν΄λΌμ΄μΈνΈ μΈ‘μ μ μ‘νλ€._**
3. μλ²μΈ‘μμ λ¨μ ν¨ν·μ λͺ¨λ μ μ‘ν ν, ν΄λΌμ΄μΈνΈ μΈ‘μ FINμ μ μ‘νλ€.
4. ν΄λΌμ΄μΈνΈ μΈ‘μμ μλ΅μ μλ¦¬κΈ° μν΄ ACKλ₯Ό μ μ‘νλ€.

## TCP μ λ¬Έμ μ 

- λ§€λ² μ»€λ₯μμ μ°κ²°ν΄μ μκ° μμ€ λ°μ
- ν¨ν·μ μ‘°κΈλ§ μμ€ν΄λ μ¬μ μ‘νλ λ¬Έμ μ 

_μ΄λ¬ν TCPμ λ¨μ μ λ³΄μνκΈ°μν΄ λμ¨ κ²μ΄ UDP_

<br/>
<br/>

# π UDP (User Datagram Protocol)

- TCPλ³΄λ€ μ λ’°μ±μ΄ λ¨μ΄μ§μ§λ§ μ μ‘ μλκ° μΌλ°μ μΌλ‘ λΉ λ₯Έ νλ‘ν μ½ ( μμ°¨μ μ‘ X, νλ¦μ μ΄ X, νΌμ‘ μ μ΄ X)
- λ¬΄μ°κ²°μ±
- Error Detection
- λΉκ΅μ  λ°μ΄ν°μ μ λ’°μ±μ΄ μ€μνμ§ μμ λ μ¬μ©νλ€. (ex) μμ μ€νΈλ¦¬λ°)

## User Datagram

![](<https://images.velog.io/images/moonheekim0118/post/e9d5d87d-24a7-45ef-a4d8-d01203971205/%E1%84%83%E1%85%A1%E1%84%8B%E1%85%AE%E1%86%AB%E1%84%85%E1%85%A9%E1%84%83%E1%85%B3%20(5).jpeg>)

- UDP νλ‘ν μ½ λ΄λΆ λ°μ΄ν° λ¨μ
- TCPμ λ¬λ¦¬, λ°μ΄ν°λ₯Ό μλ₯΄μ§ μκ³  λ°μ΄ν°μ UDP ν€λλ₯Ό μΆκ°νλ€. (λ°λΌμ λ°μ΄ν°λ₯Ό μͺΌκ°μΌ ν  κ²½μ° μμ© κ³μΈ΅μμ λ°μ΄ν°λ₯Ό μ§μ  μλΌμΌ νλ€.)

## UDP ν€λ

![](data:image/png;base64,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)

## UDP λ°μ΄ν° μ μ‘ κ³Όμ 

![](<https://images.velog.io/images/moonheekim0118/post/e730a3bf-3057-48ad-818b-798aafc1ea5a/%E1%84%83%E1%85%A1%E1%84%8B%E1%85%AE%E1%86%AB%E1%84%85%E1%85%A9%E1%84%83%E1%85%B3%20(6).jpeg>)

<br/>
<br/>

# μ°Έκ³  / μ΄λ―Έμ§ μΆμ²

- [gatevidyalay - TCP header](https://www.gatevidyalay.com/wp-content/uploads/2018/09/TCP-Header-Format.png)
