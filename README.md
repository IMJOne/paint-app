![paint](https://user-images.githubusercontent.com/110226567/213916087-48672534-0e63-4b39-a609-471326aea375.png)

# ๐จ Paint app

์๋ฐ์คํฌ๋ฆฝํธ ๋ฏธ๋ ๊ทธ๋ฆผํ ์ดํ ๐ [Demo](https://imjone.github.io/paint-app/)

<br />

## ๐ข ํ๋ก์ ํธ ๊ฐ์

Canvas API๋ฅผ ์ฌ์ฉํ์ฌ ์ ์ํ ๋ฐ๋๋ผ ์๋ฐ์คํฌ๋ฆฝํธ ๋ฏธ๋ ๊ทธ๋ฆผํ์๋๋ค.<br />
๊ทธ๋ฆผํ์ ํต์ฌ ๊ธฐ๋ฅ๋ค(๊ทธ๋ฆฌ๊ธฐ, ์ฑ์ฐ๊ธฐ, ํ์คํธ ๋ฐ ์ด๋ฏธ์ง ์ฝ์ ๋ฑ)์ ๊ตฌํํ์์ผ๋ฉฐ,<br />
์ฌ์ฉ์์ ๋์ ๋ณดํธํ๊ธฐ ์ํ ๋คํฌ ๋ชจ๋ ํ๋ง๋ฅผ ์ง์ํฉ๋๋ค.

<br />

## ๐จ๏ธ ์ฌ์ฉ ๊ธฐ์ 

<p>
 <img src="https://img.shields.io/badge/HTML-e34f26?style=flat-square&logo=HTML5&logoColor=white" />
 <img src="https://img.shields.io/badge/CSS-1572b6?style=flat-square&logo=CSS3&logoColor=white" />
 <img src="https://img.shields.io/badge/JavaScript-f7df1e?style=flat-square&logo=JavaScript&logoColor=white" />
</p>

<br />

## ๐ ์ฃผ์ ๊ธฐ๋ฅ

- ๋ธ๋ฌ์ฌ ์ฌ์ด์ฆ ๋ณ๊ฒฝ
- ์์ ๋๊ตฌ ๋ชจ๋ ๋ณ๊ฒฝ
- ์ปฌ๋ฌ ํผ์ปค ๋ฐ ์ปฌ๋ฌ ํ๋ ํธ
- ์์ ์คํ ์ทจ์ / ๋ค์ ์คํ
- ๋ผ์ดํธ ๋ชจ๋ / ๋คํฌ ๋ชจ๋ ํ ๊ธ๋ง

<br />

## ๐ป ์์ค ์ฝ๋

์ ์ฒด ์ฝ๋ ๋ณด๋ฌ ๊ฐ๊ธฐ ๐ [Notion](https://imjone.notion.site/Paint-app-3b7fa527999141cbbe0b2885a43fed05)

### ๐ ๊ทธ๋ฆฌ๊ธฐ ๋ชจ๋ (์  ๊ทธ๋ฆฌ๊ธฐ / ์ง์ฐ๊ฐ)

์ฌ์ฉ์๊ฐ ๋ง์ฐ์ค๋ฅผ ๋๋ฅด๋ ์๊ฐ๋ถํฐ ๋ฐ๋ก ์ ์ ๊ทธ๋ฆฌ๊ธฐ ์์ํด์ผ ํ๊ธฐ ๋๋ฌธ์,<br />
canvas ์์์ ๋ง์ฐ์ค๊ฐ ์ด๋ ์ค์ด๋ผ๋ฉด `ctx`๊ฐ ์ค์๊ฐ์ผ๋ก ์ฌ์ฉ์์ ๋ง์ฐ์ค ์์น๋ฅผ ๋ฐ๋ผ๊ฐ๋๋ค.<br />
๋ง์ฐ์ค๋ฅผ ๋๋ฅด๊ณ  ์์ ๋(`mousedown`) ๊ทธ๋ฆฌ๊ธฐ ๋ชจ๋๊ฐ ์์๋๋ฉฐ, ๋ง์ฐ์ค๋ฅผ ๋ผ๋ฉด(`mouseup`) ๊ทธ๋ฆฌ๊ธฐ ๋ชจ๋๊ฐ ์ข๋ฃ๋ฉ๋๋ค.

```javascript
function startDrawing() {
  isDrawing = true;
}

function stopDrawing() {
  isDrawing = false;
}

function handleDrawingMode(event) {
  const x = event.offsetX;
  const y = event.offsetY;

  if (isDrawing) {
    ctx.lineTo(x, y);
    ctx.stroke();

    switch (currentMode) {
      case tools.draw:
        ctx.strokeStyle = colorPicker.value;
        break;
      case tools.erase:
        ctx.strokeStyle = '#ffffff';
      default:
        break;
    }
  }
  ctx.beginPath(); // ์ด์ ์ ๊ทธ๋ ค์ง canvas์ path์ ์ฐ๊ฒฐ ๋์ด์ค
  ctx.moveTo(x, y); // ์ฌ์ฉ์์ ๋ง์ฐ์ค ์์น๋ก ctx ์ค์๊ฐ ์ด๋
}

canvas.addEventListener('mousemove', handleDrawingMode);
canvas.addEventListener('mousedown', startDrawing);
canvas.addEventListener('mouseup', stopDrawing);
```

### ๐ ์ฝ์ ๋ชจ๋ (์ ์ฑ์ฐ๊ธฐ / ํ์คํธ / ์ด๋ฏธ์ง)

ํ์ฌ ํ์ฑํ๋ ๋ชจ๋์ ๋ฐ๋ผ ๊ฐ๊ฐ ๋ค๋ฅธ ์ผ์ด์ค๊ฐ ์คํ๋ฉ๋๋ค.<br />
`fill` - ํ์ฌ ์ ํ๋ ์์์ผ๋ก canvas ์ ์ฒด๋ฅผ ๊ฐ๋ ์ฑ์๋๋ค.<br />
`text` - `insertText` ํจ์๋ฅผ ํธ์ถํ์ฌ canvas์ ํ์คํธ๋ฅผ ๊ทธ๋ฆฝ๋๋ค.<br />
`image` - `insertImage` ํจ์๋ฅผ ํตํด ์๋ก๋๋ ์ด๋ฏธ์ง๋ฅผ canvas์ ๊ทธ๋ฆฝ๋๋ค.

```javascript
function handleInsertMode(event) {
  switch (currentMode) {
    case tools.fill:
      ctx.fillRect(0, 0, CANVAS_WIDTH, CANVAS_HEIGHT);
      break;
    case tools.text:
      insertText(event);
      break;
    case tools.image:
      if (uploadImage) ctx.drawImage(uploadImage, event.offsetX, event.offsetY);
      break;
    default:
      return;
  }
}

function insertText(event) {
  const text = textInput.value;
  if (!text) return;
  for (let i = 0; i < fonts.length; i++) {
    if (fontFamily.value === fonts[i].family) {
      ctx.font = `${fontWeight.value} ${fontSize.value}pt ${fonts[i].family}`;
      fonts[i].load().then(() => ctx.fillText(text, event.offsetX, event.offsetY));
    } else {
      ctx.font = `${fontWeight.value} ${fontSize.value}pt ${fontFamily.value}`;
      ctx.fillText(text, event.offsetX, event.offsetY);
    }
  }
}

function insertImage(event) {
  const file = event.target.files[0];
  if (file) {
    const url = URL.createObjectURL(file); // ์ด๋ฏธ์ง์ ๋ธ๋ผ์ฐ์  ๋ฉ๋ชจ๋ฆฌ URL์ ์ ๊ทผ
    uploadImage = document.createElement('img');
    uploadImage.src = url;
  }
}

canvas.addEventListener('click', handleInsertMode);
```

### ๐ ์์ ๋ณ๊ฒฝํ๊ธฐ

์ฌ์ฉ์ ํธ์์ฑ์ ์ํด ์ปฌ๋ฌ ํผ์ปค ๋ฟ๋ง ์๋๋ผ ์ธ๊ธฐ ์์์ ๋ชจ์ ๋์ ์ปฌ๋ฌ ํ๋ ํธ ๋ํ ํจ๊ป ์ ๊ณตํฉ๋๋ค.<br />
์ํ๋ ์์์ ํด๋ฆญํ๋ฉด `ctx`์ ์์์ด `data-color` ์์ฑ์ ์ ์๋ ์์์ผ๋ก ๋ณ๊ฒฝ๋ฉ๋๋ค.

```html
<div class="color-option" style="background: #880015" data-color="#880015"></div>
<div class="color-option" style="background: #ed1c24" data-color="#ED1C24"></div>
<div class="color-option" style="background: #ff7f27" data-color="#FF7F27"></div>
<div class="color-option" style="background: #fff200" data-color="#FFF200"></div>
<div class="color-option" style="background: #22b14c" data-color="#22B14C"></div>
<div class="color-option" style="background: #00a2e8" data-color="#00A2E8"></div>
<div class="color-option" style="background: #3f48cc" data-color="#3F48CC"></div>
<div class="color-option" style="background: #a349a4" data-color="#A349A4"></div>
...
```
```javascript
function clickColorOption(event) {
  const colorOption = event.target.dataset.color;
  if (!colorOption) return;
  ctx.strokeStyle = colorOption;
  ctx.fillStyle = colorOption;
  colorPicker.value = colorOption;
}
```

<br />

## ๐ ๋ฐฐ์ด ์  ๋ฐ ๋๋ ์ 

- Canvas ๋ผ๋ ์๋ก์ด API๋ฅผ ์ฌ์ฉํด๋ณผ ์ ์์ด ์ ๋ง ์ ๊ธฐํ๊ณ  ์ฌ๋ฐ๋ ๊ฒฝํ์ด์์ต๋๋ค.
- ๋ฌธ์ ๊ฐ ๋ฐ์ํ์ ๋ ์ฝ๋์ ํ๋ฆ์ ์ฐจ๊ทผ์ฐจ๊ทผ ๋ฐ๋ผ๊ฐ๋ฉฐ ๋ต์ ์ฐพ์๋๊ฐ๋ ํ์ ๊ธฐ๋ฅผ ์ ์์์ต๋๋ค.
- ์ด๋ฏธ์ง ๋๋๊ทธ ๋ฐ ๋ํ ์ฝ์ ๋ฑ์ ์กฐ๊ธ ๋ ๊ทธ๋ฆผํ์ค๋ฌ์ด(?) ๊ธฐ๋ฅ์ ํจ๊ป ๊ตฌํํ์ง ๋ชปํด ์์ฝ์ต๋๋ค.
