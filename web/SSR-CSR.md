# ๐ ํ์ด์ง ๊ตฌ์ฑ ๋ฐฉ์ - SPA์ MPA

## MPA (Multiple Page Application)

- ์ฌ๋ฌ๊ฐ์ ํ์ด์ง๋ก ๊ตฌ์ฑ๋ ์ดํ๋ฆฌ์ผ์ด์
- ์์ฒญ์ด ์์ ๋ ๋ง๋ค ์๋ฒ๋ก๋ถํฐ ์๋ก์ด ํ์ด์ง๋ฅผ ๋ก๋ํ๋ ๋ฐฉ์์ด๋ค.
- ๋ฐ๋ผ์ ๋ ๋๋ง ๋ฐฉ์์ผ๋ก SSR์ ์ฌ์ฉํ๋ค.

## SPA (Single Page Application)

- ๋จ์ผ ํ์ด์ง ์ดํ๋ฆฌ์ผ์ด์
- ๊ธฐ์กด MPA์ ๋ฌ๋ฆฌ ๋ธ๋ผ์ฐ์ ์ ์ต์ด์ ํ๋ฒ ํ์ด์ง๋ฅผ ๋ก๋ํ๊ณ , ์ด ํ ํน์  ๋ถ๋ถ๋ง Ajax๋ฅผ ํตํด ๋ฐ์ดํฐ๋ฅผ ๋ฐ์ธ๋ฉํ๋ ๋ฐฉ์์ด๋ค.
- ๋ฐ๋ผ์ ๋ ๋๋ง ๋ฐฉ์์ผ๋ก CSR์ ์ฌ์ฉํ๋ค.

<br/>

# ๐ ๋ ๋๋ง ๋ฐฉ์ - CSR๊ณผ SSR ๊ฐ๋

## CSR (Client Side Rendering)

- ํด๋ผ์ด์ธํธ ์ธก์์ HTML์ ๋ ๋๋ง ํ๋ค.

## SSR (Server Side Rendering)

- ์์ฒญ์ด ์ค๋ฉด ์๋ฒ์์ HTML์ ๋ ๋๋ง ํ๋ค.

### SSR๊ณผ SSG (Static Site Generation)

- SSR๊ณผ SSG๋ ์๋ฒ์์ HTML์ ๋ ๋๋งํ์ฌ ๋ณด๋ด์ค๋ค๋ ์ธก๋ฉด์์ ๋น์ทํ์ง๋ง,์ฐจ์ด์ ์ HTML์ ์ธ์  ๋ง๋ค์ด๋๋๋์ด๋ค.
- SSG ๊ฐ์ ๊ฒฝ์ฐ ๋ฏธ๋ฆฌ ๋ง๋ค์ด๋๊ณ , SSR์ ์์ฒญ์ด ์ค๋ฉด ๋ง๋ค์ด๋๋ค.
- ๋ฐ๋ผ์ SSR์ ๋ฐ์ดํฐ๊ฐ ๋ฌ๋ผ์ ธ์ ๋ฏธ๋ฆฌ ๋ง๋ค์ด๋๊ธฐ ์ด๋ ค์ด ํ์ด์ง์ ์ ํฉ
- SSG๋ ๋ฐ๋ ์ผ์ด ๊ฑฐ์ ์๋ ํ์ด์ง์ ์ ํฉ

<br/>

# ๐ CSR๊ณผ SSR์ ๋์ ๊ณผ์ ๊ณผ ํน์ง

## CSR

1. ์ ์ ๊ฐ ์น์ฌ์ดํธ์ ๋ฐฉ๋ฌธํ๋ค.
2. ๋ธ๋ผ์ฐ์ ๊ฐ ์๋ฒ์ ์ฝํ์ธ ๋ฅผ ์์ฒญํ๋ค.
3. ์๋ฒ๋ ๋น ๋ผ๋๋ง ์๋ HTML์ ์๋ตํ๋ค.
4. ๋ธ๋ผ์ฐ์ ๊ฐ HTML์ ํ์ฑํ๋ฉฐ ์ฐ๊ฒฐ๋ JS๋งํฌ๋ฅผ ์ฝ๊ณ , ์๋ฒ๋ก๋ถํฐ JS๋ฅผ ๋ค์ด๋ก๋ ๋ฐ๋๋ค.
5. ๋ธ๋ผ์ฐ์ ๋ JS๋ฅผ ์ด์ฉํด ๋์ ์ผ๋ก DOM์ ์์ฑํ์ฌ ํ์ด์ง๋ฅผ ๋ง๋ค์ด ๋ธ๋ผ์ฐ์ ์ ๋์์ค๋ค.

- CSR์ ๋ธ๋ผ์ฐ์ ๊ฐ JS ํ์ผ์ ๋ค์ด๋ก๋ ๋ฐ๊ณ , ๋์ ์ผ๋ก DOM์ ์์ฑํ๋ ์๊ฐ์ ๊ธฐ๋ค๋ ค์ผ ํ๋ฏ๋ก ์ด๊ธฐ ๋ก๋ฉ ์๋๊ฐ ๋๋ฆฌ๋ค.
- ์๋ฒ๊ฐ ๋น ๋ผ๋๋ง ์๋ HTML์ ๋๊ฒจ์ฃผ๋ฉด ๋๊ธฐ ๋๋ฌธ์ ์๋ฒ์ธก ๋ถํ๊ฐ ์ ๋ค.
- ํด๋ผ์ด์ธํธ ์ธก์์ ๋ผ์ฐํ, ์ฐ์ฐ ๋ฑ์ ๋ชจ๋ ์ง์  ์ฒ๋ฆฌํ์ฌ ๋ฐ์ ์๋๊ฐ ๋น ๋ฅด๊ณ  UX๋ ์ฐ์ํ๋ค.
- ์น ํฌ๋กค๋ฌ ๋ด ์์ฅ์์๋ ์ฒ์ HTML์ด ๋น์ด์๊ธฐ ๋๋ฌธ์ ๊ฒ์ ์์ง ์ต์ ํ์ ๋ถ๋ฆฌํ๋ค. (ํฌ๋กฌ์ ํฌ๋กค๋ฌ์ ๊ฒฝ์ฐ๋ JSํ์ผ์ ์ฝ์ ์ ์๊ธด ํ๋ค.)

## SSR

1. ์ ์ ๊ฐ ์น์ฌ์ดํธ์ ๋ฐฉ๋ฌธํ๋ค.
2. ๋ธ๋ผ์ฐ์ ๋ ์๋ฒ์ ์ฝํ์ธ ๋ฅผ ์์ฒญํ๋ค.
3. ์๋ฒ์์๋ ๋ ๋๋ง ์ค๋น๋ฅผ ๋ง์น HTML, JS์ฝ๋๋ฅผ ์๋ตํ๋ค.
4. ๋ธ๋ผ์ฐ์ ๋ ์ ๋ฌ๋ฐ์ HTML์ ๋ ๋๋งํ๋ค.
5. ๋ธ๋ผ์ฐ์ ๊ฐ JS ์ฝ๋๋ฅผ ๋ค์ด๋ก๋ํ ํ, HTML์ JS๋ก์ง์ ์ฐ๊ฒฐํ๋ค.

- ๋ชจ๋  ๋ฐ์ดํฐ๊ฐ HTML์ ๋ด๊ฒจ์ง ์ฑ๋ก ๋ธ๋ผ์ฐ์ ์ ์ ๋ฌ๋๋ฏ๋ก ๊ฒ์ ์์ง ์ต์ ํ์ ์ ๋ฆฌํ๋ค.
- ์๋ฐ์คํฌ๋ฆฝํธ ์ฝ๋๋ฅผ ์คํํ๊ณ  ๋ค์ด๋ฐ๊ธฐ ์ ์ HTML์ด ๋ ๋๋ง๋๋ฏ๋ก ์ด๊ธฐ ๊ตฌ๋ ์๋๊ฐ ๋น ๋ฅด๋ค. (ํ์ง๋ง JS๋ก์ง์ด ์์ง ์ฐ๊ฒฐ๋์ง ์์ ์ํ์ด๋ฏ๋ก ์ฌ์ฉ์์ ์ด๋ฒคํธ์ ๋ฌด๋ฐ์์ผ ์ ์๋ค. ์ฆ Time to View !== Time to Interect)

<br/>

# ๐ CSR ๋จ์  ๋ณด์ ๋ฐฉ๋ฒ

## ์ด๊ธฐ ๋ก๋ ์๋ ๋ณด์

- Code Splitting
- tree-shaking
- chunk ๋ถ๋ฆฌ

## SEO ๊ฐ์ 

- pre-rendering
- ๋ผ์ด๋ธ๋ฌ๋ฆฌ, ์นํฉ ํ๋ฌ๊ทธ์ธ์ ํตํด ๊ฐ ํ์ด์ง์ ๋ํ HTMLํ์ผ์ ๋ฏธ๋ฆฌ ์์ฑํด๋ ํ, ์๋ฒ์์ ์์ฒญํ๋ ์ฃผ์ฒด๊ฐ ํฌ๋กค๋ฌ๋ผ๋ฉด ์ฌ์ ์ ๋ ๋๋ง ๋ HTML๋ฒ์  ํ์ด์ง๋ฅผ ๋ณด์ฌ์ฃผ๋ ๋ฐฉ๋ฒ์ ์ ์ฉ ํ  ์ ์๋ค.

## CSR + SSR/SSG ๋์ํ๊ธฐ

- ํ๋ ์์ํฌ ์์ด -> ์ง์  ์๋ฒ ์ค์ ํ๊ธฐ
- ํ๋ ์์ํฌ ์ฌ์ฉ -> Next.js / Gatsby

## Isomorphic App || Universal Rendering

- ์ด๊ธฐ ๋ ๋๋ง ๋ฐฉ์์ผ๋ก SSR์ ์ฌ์ฉํ๊ณ ,๊ทธ ํ๋ก๋ CSR์ ์ฌ์ฉํ๋ ๋ฐฉ์
