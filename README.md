# Styling

---

## 1. Internal CSS

- Với cách này bạn chỉ cần viết CSS ngay trong thẻ `<style>` và chèn thẻ này ngay trong file html của bạn là được. Bạn có thể đặt thẻ này ở trong cặp thẻ `<head>`, trong `<body>` trước các thẻ cần style, … Và bạn nên đặt nó trước hoặc trong body.

```html
<head>
  <!-- ... -->
  <style type="text/css">
    /* Viết CSS bạn ở đây */
    div {
      color: pink;
    }
  </style>
</head>
<body>
  <!-- ... -->
</body>
```

- **Ưu điểm**:

  - Dễ tiếp cận, test nhanh css của bạn.
  - Vì nó nằm trong 1 file nên dễ dàng gửi nó để preview và không ảnh hưởng các file html khác.

- **Nhược điểm**:
  - Khó quản lý code css khi file quá lớn, thường thì các file css rất dài.
  - Không thể tái sử dụng cho các file html khác.

---

## 2. External CSS

- Đây là các truyền thống thường được sử dụng nhất. Để sử dụng thì bạn cần tách css của mình ra các file khác nhau có đuôi `.css`. Sau đó bạn chỉ cần liên kết nó qua thẻ `<link rel=”stylesheet”>`

```html
<head>
  <!-- ... -->
  <link rel="stylesheet" href="your-path-css-file" />
</head>
<body>
  <!-- ... -->
</body>
```

```jsx
// Trong ReactJS bạn có thể dùng import để nhúng file css vào component
import "your-file.css";
function App() {
  // ...
}
```

- **Ưu điểm**:

  - Dễ dàng tái sử dụng các css của bạn cho nhiều component, file html khác nhau.
  - File html được load nhanh hơn.
  - Code dễ đọc, dễ bảo trì hơn.

- **Nhược điểm**:
  - Bạn phải load tất cả css trong file css nhưng đôi khi không cần dùng tất cả.
  - Phải quản lý nhiều file css hơn và có khả năng bị trùng css ở các file khác nhau.
  - Nếu file css lớn sẽ ảnh hưởng đến tốc độ load trang của bạn.

---

## 3. Inline CSS

- Là việc bạn viết thẳng các css vào trong các thẻ html.

```html
<body>
  <body>
    <div style="color:pink;font-size:15px;">Hello, world!</div>
  </body>
</body>
```

```jsx
const divStyle = {
    coilor: 'pink',
    fontSize: '18px'
};

function App() (
    <div style={divStyle}>
        <p style={{color:'blue'}}>Hello, world!</p>
    </div>
);
```

- **Ưu điểm**:

  - Độ ưu tiên cao hơn so với 2 phương pháp trên.
  - Áp dụng riêng biệt cho 1 thẻ mà không ảnh hương thẻ khác.
  - Dễ dàng test nhanh.
  - Hữu ích khi dùng Javascript để inject vào.

- **Nhược điểm**:
  - Code khó quản lý, quá nhiều thuộc tính trong một thẻ.
  - Không thể tái sử dụng.

**LƯU Ý**: Những cách còn lại dưới đây bản chất nó chỉ giúp chúng ta compile ra CSS và style cho component theo 1 trong 3 cách trên. Vì cuối cùng thì trình duyệt vẫn chỉ hiểu được CSS, chỉ là thay vì viết CSS thuần thì các cách dưới này sẽ dùng cách thức khác để viết nhằm linh động và hiệu quả hơn

---

## 4. CSS Preprocessors như Sass, Less

- Tiền xử lý CSS (CSS Preprocessors) sẽ giúp chúng ta viết css một cách linh hoạt hơn như có thể dùng biến, hàm, mixin, css lồng nhau, vv…

- Một số CSS Preprocessors thường dùng như Sass (Scss), Less, Stylus.

- **Ưu điểm**:

  - Code nhanh và linh hoạt hơn nhiều, tiết kiệm nhiều thời gian.
  - Tái sử dụng các đoạn code thông qua mixin, import, …
  - Kết hợp với BEM là một sự tuyệt vời nhờ vào khả năng viết nested

- **Nhược điểm**:
  - Dễ bị hiểu nhầm về kích thước thật (vì cái thật sự được load là file css đã build ra chứ không phải là file scss lúc dev).
  - Khó dò lỗi và debug hơn css thuần.

---

## 5. Atomic CSS

- **Atomic CSS** là một kiến trúc hay cách thức với CSS, nó không phải thư viện hay gì cả.

- Atomic là nguyên tử, nghĩa là bạn sẽ viết những css cho các class một cách tối giản nhất. Và những class này sẽ là những viên gạch nhỏ để xây dựng lên một ngôi nhà to.

- Atomic CSS phải đảm bảo được tính nguyên tử của nó, nghĩa là một class chỉ làm đúng với ngữ nghĩa và tên của nó. Ví dụ:

```jsx
<-- Cách viết thông thường -->
<style>
  .box{
    display: flex;
    align-items: center;
    justify-content: center;
  }
</style>
<div class="box"></div>
```

```css
/* Dùng Atomic CSS */
.d-flex {
  display: flex;
}
.align-i-center {
  align-items: center;
}
jus-content-center {
  justify-content: center;
}

/* <div class="d-flex align-i-center jus-content-center"></div> */
```

- **Ưu điểm**:

  - File css của bạn sẽ rất gọn nhẹ vì khả năng tái sử dụng rất cao.
  - Viết một lần dùng mãi mãi, nếu bạn làm cá nhân thì có thể tái sử dụng các file atomic đã xây dựng cho mọi project. Từ đó tốc độ code của bạn sẽ tăng đáng kể.
  - Thống nhất với cả team. Vì các class của atomic có ngữ nghĩa cố định nên sẽ không gặp trường hợp người này code kiểu này, người kia hiểu kiểu khác.
  - Tránh trùng lặp code ở nhiều nơi.
  - Các thư viện Atomic xây dựng sẵn xịn xò như [Tailwind](https://tailwindcss.com/), [Tachyons](https://tachyons.io/), [ACSS](https://acss.io/)

- **Nhược điểm**:
  - Nếu tự xây dựng từ đầu, thì bạn phải tốn thời gian để viết từng class (Khổ trước sướng sau)
  - Tốn thời gian cho người mới vào team (phải đọc hết cái đống atomic này)
  - Và class trong thẻ dài ngoằng, đây có vẻ là điểm đáng sợ nhất của nó.

---

## 6. CSS-in-JS

- Css-in-JS là một kỹ thuật dùng Javascript để tạo ra các css và class tương ứng, sau đó gắn vào DOM.

- Chúng ta có thể làm việc này thông qua các thư viện bên ngoài, phổ biến như [Styled-component](https://styled-components.com/), [JSS](https://cssinjs.org/?v=v10.9.1-alpha.2), Radium, …

```jsx
import styled from "styled-components";

const Button = styled.a`
  display: inline-block;
  border-radius: 3px;
  padding: 0.5rem 0;
  margin: 0.5rem 1rem;
  width: 11rem;
  background: transparent;
  color: white;
  border: 2px solid white;
  ${(props) =>
    props.primary &&
    css`
      background: white;
      color: black;
    `}
`;

function App() {
  return (
    <div>
      <Button
        href="https://github.com/styled-components/styled-components"
        target="_blank"
        rel="noopener"
        primary
      >
        GitHub
      </Button>
      <Button as={Link} href="/docs">
        Documentation
      </Button>
    </div>
  );
}
```

- **Ưu điểm**:

  - Tận dụng được sức mạnh của JavaScript để viết css một cách linh động hơn.
  - Có thể truyền props vào để viết dynamic css.
  - Dễ dàng tái sử dụng cho các component khác nhau.
  - Tự động tạo class không trùng lặp nên không lo trùng lặp CSS.
  - Tự động thêm prefix, không lo các trình duyệt khác không hỗ trợ.
  - Code ít hơn, nhanh hơn.
  - Đặc biệt, là đỡ tốn công suy nghĩ tên class như BEM

- **Nhược điểm**:
  - Thay đổi thoái quen viết CSS vì thế cần tốn thời gian tìm hiểu.
  - Khó Debug CSS với cách cũ là dùng tên class.

---

## 7. CSS Modules

- Với CSS modules chúng ta sẽ viết các stylesheet thành từng file nhỏ, phục vụ cho từng modules cụ thể. Cũng sử dụng cách thức import để nhúng file css vào component của chúng ta, nhưng điểm khác của nó là nó sẽ tạo ra một biến chứa các class tự tạo, gần như không trùng lắp. Việc này rất hữu ích.

```css
/* file style.module.css */
.button {
  color: red;
}
.box {
  background-color: red;
}
```

```jsx
import styles from "./style.module.css";

console.log(styles);

function App() {
  return (
    <div className={styles.box}>
      <button className={styles.button}></button>
    </div>
  );
}
/*
  sytles = {
    button: 'style_button_2Lja',
    box: 'style_box_3Klq'
  }
*/
```

- **Ưu điểm**:

  - Có thể dùng lại file css đó mà không lo trùng tên class.
  - Tách biệt module rõ ràng hơn vì thường chỉ dùng cho riêng component đó.
  - Khắc phục được phạm vi global của cách import css như bình thường.

- **Nhược điểm**:

  - Quản lý nhiều file css module hơn.
  - Chỉnh sửa file có thể ảnh hưởng đến các component khác dùng chung css module này.

---

## 8. PostCSS

- [PostCSS](https://postcss.org/) là một Javascript tool cung cấp các API để chúng ta xử lý, biến đổi CSS (A tool for transforming CSS with JavaScript).

- Điểm nổi bật của PostCSS là nó mang tính modular với lượng plugin khủng. Tuỳ vào mỗi project của bạn mà chỉ cần cài các plugin cần thiết.

- Nếu bạn từng dùng Tailwind thì Tailwind khuyên bạn cài đặt nó như một plugin của PostCSS thay vì dùng CDN. Đều này giúp bạn có thể config được nhiều thứ hay ho hơn.

- **Ưu điểm**:

  - Nhiều Plugin hỗ trợ mạnh mẽ, đầy đủ tính năng.
  - Tự động xoá CSS thừa không dùng đến.
  - Sử dụng nhiều tiện ích như Sass.
  - Tự minify, gộp media query, tối ưu code CSS khi ở production mode.
  - Không lo vấn đề trình duyệt không hỗ trợ CSS mới.
  - Tự tạo ra được Plugin theo nhu cầu cụ thể.

- **Nhược điểm**:
  - Cấu hình hơi phức tạp, cần tốn thời gian tìm hiểu.
  - Phụ thuộc vào nhiều plugin.

---

# Hết.
