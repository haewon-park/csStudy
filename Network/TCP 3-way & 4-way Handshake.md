## TCP 3-way Handshake & 4-way Handshake

### ๐ค **3-way Handshake**

- Why? ์ฅ์น๋ค ์ฌ์ด์ ๋ผ๋ฆฌ์ ์ธ ์ ์์ ์ฑ๋ฆฝ(establish)ํ๊ธฐ ์ํด

![image](https://user-images.githubusercontent.com/44565524/125661341-86cf1929-3293-4730-a092-55496a4aa5cf.png) ![image](https://user-images.githubusercontent.com/44565524/125732101-f11bd194-72f2-410c-a10e-d50f58c2d4b6.png)


1. ํด๋ผ์ด์ธํธ๊ฐ ์๋ฒ์๊ฒ SYN ํจํท์ ๋ณด๋ (sequence : x)
2. ์๋ฒ๊ฐ SYN(x)์ ๋ฐ๊ณ , ํด๋ผ์ด์ธํธ๋ก ๋ฐ์๋ค๋ ์ ํธ์ธ ACK์ SYN ํจํท์ ๋ณด๋ (sequence : y, ACK : x + 1)
3. ํด๋ผ์ด์ธํธ๊ฐ ACK(y+1)๋ฅผ ์๋ฒ๋ก ๋ณด๋ด๊ณ  ์ฐ๊ฒฐ์ด ์ด๋ฃจ์ด์ง

<br>

- SYN: synchronize sequence numbers
- ACK: acknowledgment

<hr>

### ๐ค **4-way Handshake**

- Why? ์ธ์์ ์ข๋ฃํ๊ธฐ ์ํด

![image](https://user-images.githubusercontent.com/44565524/125661616-04417fd9-e2ea-4dfa-8dbf-55f33a4f80af.png)

1. ํด๋ผ์ด์ธํธ๊ฐ ์๋ฒ์๊ฒ ์ฐ๊ฒฐ์ ์ข๋ฃํ๋ค๋ FIN ํ๋๊ทธ๋ฅผ ๋ณด๋
2. ์๋ฒ๋ FIN์ ๋ฐ๊ณ , ํ์ธํ๋ค๋ ACK๋ฅผ ํด๋ผ์ด์ธํธ์๊ฒ ๋ณด๋ (์ด๋ ๋ชจ๋  ๋ฐ์ดํฐ๋ฅผ ๋ณด๋ด๊ธฐ ์ํด CLOSE_WAIT ์ํ๊ฐ ๋๋ค)
3. ๋ฐ์ดํฐ๋ฅผ ๋ชจ๋ ๋ณด๋๋ค๋ฉด, ์ฐ๊ฒฐ์ด ์ข๋ฃ๋์๋ค๋ FIN ํ๋๊ทธ๋ฅผ ํด๋ผ์ด์ธํธ์๊ฒ ๋ณด๋
4. ํด๋ผ์ด์ธํธ๋ FIN์ ๋ฐ๊ณ , ํ์ธํ๋ค๋ ACK๋ฅผ ์๋ฒ์๊ฒ ๋ณด๋ (์์ง ์๋ฒ๋ก๋ถํฐ ๋ฐ์ง ๋ชปํ ๋ฐ์ดํฐ๊ฐ ์์ ์ ์์ผ๋ฏ๋ก TIME_WAIT์ ํตํด ๊ธฐ๋ค๋ฆฐ๋ค)

- ์๋ฒ๋ ACK๋ฅผ ๋ฐ์ ์ดํ ์์ผ์ ๋ซ๋๋ค (Closed)
- TIME_WAIT ์๊ฐ์ด ๋๋๋ฉด ํด๋ผ์ด์ธํธ๋ ๋ซ๋๋ค (Closed)

<br>

**TIME_WAIT**: Client๊ฐ Server๋ก๋ถํฐ FIN์ ์์ ํ๋๋ผ๋ ์ผ์ ์๊ฐ(๋ํดํธ 240์ด)๋์ ์ธ์์ ๋จ๊ฒจ๋๊ณ  ์์ฌ ํจํท์ ๊ธฐ๋ค๋ฆฌ๋ ๊ณผ์ 
