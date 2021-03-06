<div align="center">
  <h1>๐ต์ต์  ์ํฐ์คํธ ํ์คํธ๐ถ</h1>
</div>

![8](https://user-images.githubusercontent.com/87234410/154940264-8de8f832-46c7-4702-b6ad-51a2e963d4d9.jpg)

- Page : https://music-quizz.vercel.app/

## ๊ฐ์

- ์ ํํ ์ํฐ์คํธ์ ์จ๋ฒ๊ณผ ๋ธ๋์ ๊ดํ ํด์ฆ ์๋น์ค
- Spotify API๋ฅผ ํ์ฉํ์ฌ ์๋์ผ๋ก ํด์ฆ๋ฅผ ์์ฑ

## ๋ชฉํ์ ๊ธฐ๋ฅ

### ๋ชฉํ

- ์ ์ ๊ฐ ์ ํํ ์ํฐ์คํธ์ ๋ํ ๊ด์ฌ๋๋ฅผ ์ ์ ์๋๋ก ์ ์ํ
- ์์ API๋ฅผ ๊ธฐ๋ฐ์ผ๋ก ๋ฌธ์ ๊ฐ ์๋์ผ๋ก ์์ฑํ ๋๋๋ก ๊ธฐ๋ฅํ
- ํ์คํธ๋ฅผ ์ฆ๊ธฐ๊ณ  ์ธ์ฆํ๋ MZ ์ธ๋ ํธ๋ ๋์ ๋ถํฉํ๋ ์ฝํ์ธ ํ

### ๊ธฐ๋ฅ

- ์ ํํ ์ํฐ์คํธ์ ์จ๋ฒ๊ณผ ๋ธ๋์ ๊ดํ ํด์ฆ๋ฅผ ์ ๊ณต
- ์ ๊ณต๋๋ ํด์ฆ๋ API๋ฅผ ํ์ฉํ์ฌ ์ด 4๊ฐ๋ก ๊ตฌ์ฑ๋จ
  - ์จ๋ฒ์ ์๋ก๋ ๊ณก ์ ํ
  - ์๋ก๊ณก์ด ํฌํจ๋ ์จ๋ฒ ์ ํ
  - ์จ๋ฒ์ ๋ฐ๋งค ์ฐ์ ์ ํ
  - ๊ณก์ ์ผ๋ถ๋ถ์ ๋ฃ๊ณ  ๊ณก ์ ๋ชฉ ์ ํ
- ๊ฒฐ๊ณผ๋ฅผ SNS์ ๊ณต์ ํ  ์ ์๋๋ก ์ ๊ณต

## ๊ฐ๋ฐ ํ๊ฒฝ

### ๊ธฐ์  ์คํ

- ํ๋ก ํธ์๋ : React / TypeScript / Styled-component
- ๋ฐฑ์๋ : Spotify API ํ์ฉ (https://developer.spotify.com)

### ์ฐธ์ฌ ์ธ์

- ์ค๋๊ท(@OhRaeKyu), ์์์ฒ (@IRONDESK)

### ๊ฐ๋ฐ ์ผ์ 

- 2022๋ 02์ 06์ผ - ํ๋ก์ ํธ ๊ธฐํ
- 2022๋ 02์ 07์ผ ~ 02์ 09์ผ - UI ๊ตฌํ
- 2022๋ 02์ 09์ผ ~ 02์ 11์ผ - ๊ธฐ๋ฅ ๊ตฌํ
- 2022๋ 02์ 12์ผ ~ 03์ 03์ผ - ๋ฆฌํฉํ ๋ง

## ์ฃผ์ ์ฝ๋

### Spotify API ํธ์ถ (src/API/getAlbumID.ts)

```ts
// ๊ฐ์์ ์จ๋ฒ id ๋ถ๋ฌ์ค๊ธฐ
export const getArtistAlbum = async (artistId: string) => {
  const access_token: string = await getAuth();
  const api_url: string = `https://api.spotify.com/v1/artists/${artistId}/albums?include_groups=album&market=KR`;

  try {
    const res = await axios.get(api_url, {
      headers: {
        Authorization: `Bearer ${access_token}`,
      },
    });
    let targetArray: any = [];
    while (targetArray.length < 3) {
      targetArray.push(res.data.items[getRandom(res.data.items.length)].id);
      let set: any = new Set(targetArray);
      targetArray = [...set];
    }
    return await targetArray;
  } catch (err) {
    console.log(err);
  }
};

// ๋๋ค ๊ฐ ๋ฐํ ํจ์
const getRandom = (n: number) => {
  return Math.floor(Math.random() * n);
};
```

- API์์ ์ํฐ์คํธ์ ์จ๋ฒ์ ๋ถ๋ฌ์ ๊ทธ ์ค 3๊ฐ๋ฅผ ๋๋ค์ผ๋ก `targetArray`์ ๋ด์์.
- ๋ฌธ์ ๋ฅผ ์์ฑํ  ๋, ์จ๋ฒ์ด ์ค๋ณต๋ผ์ ๋ถ๋ฌ์์ง๋ ๋ฌธ์ ๊ฐ ์์์.

```ts
// ๊ธฐ์กด ์ฝ๋
return [
  res.data.items[getRandom(res.data.items.length)].id,
  res.data.items[getRandom(res.data.items.length)].id,
  res.data.items[getRandom(res.data.items.length)].id,
];
```

- `targetArray`๋ฅผ `Set`์ ์ฌ์ฉํด ์ค๋ณต๋๋ ์จ๋ฒ์ด ๋ด๊ธฐ๋ ๊ฒ์ ๋ฐฉ์งํจ.

<br/>

### API Data ๋ ๋๋ง (src/components/Quiz/QuizItem.tsx 46-64)

```tsx
if (data && data.length === 3) {
  return (
    <ItemWrap>
      <Correct>{correct ? 'Correct ' + correct : null}</Correct>
      <Progress max={quizLength} value={question} />
      <Question question={question} data={data} randList={randList} />
      <Answer
        question={question}
        setQuestion={setQuestion}
        correct={correct}
        setCorrect={setCorrect}
        data={data}
        randList={randList}
      />
    </ItemWrap>
  );
} else {
  return null;
}
```

- API Data๋ฅผ ๋ ๋๋ง ํ๋ ๊ณผ์ ์์ ์ด๊ธฐ ๊ฐ(null)์ ์ํด undefined type error๊ฐ ๋ฐ์ํ์๋ค.
- if-else ๊ตฌ๋ฌธ์ ํตํด data์ ๊ฐ์ด ์ ๋๋ก ์ ์ฅ ๋์์ ๋ ์กฐ๊ฑด๋ถ ๋ ๋๋ง ๋  ์ ์๋๋ก ํด๊ฒฐํจ.

<br/>

## File Tree

```
๐music-quiz
โโ .gitignore
โโ package-lock.json
โโ package.json
โโ๐ public
โ  โโ favicon.ico
โ  โโ๐ icon
โ  โ  โโ instagram.png
โ  โ  โโ kakao-talk.png
โ  โ  โโ SpotifyLogo.png
โ  โโ index.html
โโ README.md
โโ๐ src
โ  โโ๐ API
โ  โ  โโ getAlbumID.ts
โ  โโ App.css
โ  โโ App.tsx
โ  โโ๐ components
โ  โ  โโ๐ Home
โ  โ  โ  โโ ArtistBox.tsx
โ  โ  โ  โโ HeaderTitle.tsx
โ  โ  โโ๐ Layout
โ  โ  โ  โโ Advertisement.tsx
โ  โ  โ  โโ Footer.tsx
โ  โ  โโ๐ Quiz
โ  โ  โ  โโ Answer.tsx
โ  โ  โ  โโ Question.tsx
โ  โ  โ  โโ QuizItem.tsx
โ  โ  โโ๐ Result
โ  โ     โโ ResultContents.tsx
โ  โ     โโ ShareContents.tsx
โ  โโ constants.ts
โ  โโ index.css
โ  โโ index.tsx
โ  โโ๐ pages
โ     โโ Home.tsx
โ     โโ Quiz.tsx
โ     โโ Result.tsx
โโ tsconfig.json
```
