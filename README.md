# Airbnb CSS / Sass Styleguide

*Cách tiếp cận CSS và Sass hợp lý nhất*

## Mục lục

  1. [Thuật ngữ](#terminology)
    - [Khai báo](#khai-báo)
    - [Selector](#selectors)
    - [Thuộc tính](#thuộc-tính)
  2. [CSS](#css)
    - [Quy cách](#quy-cách)
    - [Chú thích](#chú-thích)
    - [OOCSS và BEM](#oocss-và-bem)
    - [ID Selector](#id-selectors)
    - [JavaScript hook](#javascript-hooks)
    - [Đường viền](#đường-viền)
  3. [Sass](#sass)
    - [Cú pháp](#cú-pháp)
    - [Thứ tự](#sắp-xếp-các-khai-báo-thuộc-tính)
    - [Biến](#biến)
    - [Mixins](#mixins)
    - [Mở rộng directive](#extend-directive)
    - [Selector lồng nhau](#selectors-lồng-nhau)
  4. [Translation](#translation)

## Thuật ngữ

### Khai báo

Một “khai báo” là tên gọi của một selector (hoặc một nhóm các selector) với một nhóm các thuộc tính. Dưới đây là ví dụ:

```css
.listing {
  font-size: 18px;
  line-height: 1.2;
}
```

### Selector

Trong một khai báo, “selector” là phần sẽ xác định xem phần tử nào trong DOM sẽ được style bởi các thuộc tính xác định. Selector có thể tương ứng với các phần tử HTML, cũng như class hay ID của phần tử, hoặc bất kì thuộc tính nào của nó. Dưới đây là ví dụ về selector:

```css
.my-element-class {
  /* ... */
}

[aria-hidden] {
  /* ... */
}
```

### Thuộc tính

Thuộc tính là một cặp khóa-giá trị, và một khai báo có thể chứa một hoặc nhiều khai báo của thuộc tính. Cách khai báo của thuộc tính như sau:

```css
/* some selector */ {
  background: #f1f1f1;
  color: #333;
}
```

## CSS

### Quy cách

* Sử dụng soft tab (2 dấu cách) cho khoảng cách thụt vào (indentation)
* Nên sử dụng dấu gạch ngang trong camelCasing của tên class.
  - Dấu gạch dưới và PascalCasing áp dụng được nếu bạn sử dụng BEM (xem [OOCSS and BEM](#oocss-and-bem) bên dưới).
* Không sử dụng ID Selector.
* Khi sử dụng nhiều selector trong một khai báo, viết mỗi selector trên một dòng riêng.
* Trước dấu ngoặc nhọn `{` phải có một dấu cách trong khai báo.
* Trong thuộc tính, đặt một dấu cách đứng sau dấu hai chấm `:` .
* Đặt dấu đóng ngoặc nhọn `}` của một khai báo trên một dòng mới.
* Đặt một dòng trống giữa các khai báo.

**Không nên**

```css
.avatar{
    border-radius:50%;
    border:2px solid white; }
.no, .nope, .not_good {
    // ...
}
#lol-no {
  // ...
}
```

**Nên**

```css
.avatar {
  border-radius: 50%;
  border: 2px solid white;
}

.one,
.selector,
.per-line {
  // ...
}
```

### Chú thích

* Nên dùng hai gạch (`//`) để đặt chú thích.
* Nên đặt chú thích trên một dòng riêng, không đặt ở cuối dòng.
* Viết chú thích chi tiết cho những dòng code mà không thể hiện được ý nghĩa rõ ràng khi đọc, ví dụ:
  - Sử dụng z-index
  - Khả năng tương thích và trình duyệt

### OOCSS và BEM

Chúng tôi khuyến khích một số cách kết hợp giữa OOCSS và BEM cho những lý do sau:

  * Giúp tạo ra mối quan hệ chặt chẽ rõ ràng giữa CSS và HTML
  * Giúp tạo ra những thành phần có thể tái sử dụng.
  * Cho phép ít lồng nhau (nested) và giảm sự riêng biệt 
  * Giúp xây dựng stylesheet có khả năng mở rộng

**OOCSS**, hay “CSS hướng đối tượng”, là một phương pháp để viết CSS mà khuyến khích bạn định hình stylesheet như một sự tập hợp của nhiều “đối tượng” (object): có thể tái sử dụng, có thể lặp lại độc lập xuyên suốt toàn bộ một trang web.

  * [OOCSS wiki](https://github.com/stubbornella/oocss/wiki) của Nicole Sullivan
  * [Giới thiệu về OOCSS](http://www.smashingmagazine.com/2011/12/12/an-introduction-to-object-oriented-css-oocss/) trên Smashing Magazine

**BEM**, hay “Block-Element-Modifier”, là một quy ước đặt tên cho class trong HTML và CSS. Ban đầu nó được phát triển bởi Yandex với codebase lớn, có khả năng mở rộng, và có thể coi như một tập hợp của các hướng dẫn cho việc thực hiện OOCSS.

  * [BEM 101](https://css-tricks.com/bem-101/) trên CSS Tricks
  * [Giới thiệu về BEM](http://csswizardry.com/2013/01/mindbemding-getting-your-head-round-bem-syntax/) của Harry Roberts

Chúng tôi khuyến khích sử dụng một biến thể của BEM với “block” PascalCase, mà nó hoạt động riêng biệt khá hiệu quả với các thành phần (component) (vd: React). Dấu gạch dưới và gạch ngang vẫn được sử dụng cho thành phần Modifier và thành phần con.

**Ví dụ**

```jsx
// ListingCard.jsx
function ListingCard() {
  return (
    <article class="ListingCard ListingCard--featured">

      <h1 class="ListingCard__title">Adorable 2BR in the sunny Mission</h1>

      <div class="ListingCard__content">
        <p>Vestibulum id ligula porta felis euismod semper.</p>
      </div>

    </article>
  );
}
```

```css
/* ListingCard.css */
.ListingCard { }
.ListingCard--featured { }
.ListingCard__title { }
.ListingCard__content { }
```

  * `.ListingCard` là một “block” và đại diện cho thành phần cao hơn
  * `.ListingCard__title` là một “phần tử” và biểu diễn như là một phần tử con của `.ListingCard` để tạo thành “block”.
  * `.ListingCard--featured` là một “modifier” và đại diện cho các trạng thái khác nhau hay các biến thể của block `.ListingCard`.

### ID Selector

Việc chọn những phần tử bằng ID trong CSS vẫn khả thi, nhưng nhìn chung vẫn không nên được áp dụng. ID selector tạo ra nên [tính đặc trưng](https://developer.mozilla.org/en-US/docs/Web/CSS/Specificity) không cần thiết cho các khai báo của bạn và không thể tái sử dụng lại được.

Để biết thêm về chủ đề này, đọc [bài viết của CSS Wizardry](http://csswizardry.com/2014/07/hacks-for-dealing-with-specificity/) về cách để giải quyết vấn tính đặc trưng trong CSS.

### JavaScript hook

Tránh việc gắn kết cùng một class trong CSS và JavaScript. Kết hợp cả hai ít nhất có thể gây lãng phí thời gian trong suốt quá trình tái cấu trúc mã nguồn khi lập trình viên phải kiểm tra chéo mỗi class khi thay đổi, và trong trường hợp xấu nhất, lập trình viên có thể sẽ phải đối mặt với việc phá vỡ một chức năng nào đó.

Chúng tôi khuyến khích tạo ra các class riêng cho JavaScript để gắn kết, tiền tố bắt đầu với `.js-`:

```html
<button class="btn btn-primary js-request-to-book">Request to Book</button>
```

### Đường viền

Sử dụng `0` thay vì `none` để xác định rằng đối tượng này không có đường viền.

**Không nên**

```css
.foo {
  border: none;
}
```

**Nên**

```css
.foo {
  border: 0;
}
```

## Sass

### Cú pháp

* Sử dụng cú pháp `.scss`, không bao giờ sử dụng cú pháp gốc `.sass`
* Sắp xếp CSS và `@include` theo một logic (xem bên dưới)

### Sắp xếp các khai báo thuộc tính

1. Khai báo thuộc tính

    Khai báo toàn bộ thuộc tính cơ bản trước, những gì không phải là `@include` hay selector lồng nhau (nested).

    ```scss
    .btn-green {
      background: green;
      font-weight: bold;
      // ...
    }
    ```

2. Khai báo `@include`

    Nhóm những `@include` ở cuối cùng để làm cho việc đọc toàn bộ selector dễ dàng hơn.

    ```scss
    .btn-green {
      background: green;
      font-weight: bold;
      @include transition(background 0.5s ease);
      // ...
    }
    ```

3. Selector lồng nhau

    Selector lồng nhau, _nếu cần thiết_, đặt ở cuối cùng, và không có gì viết sau nó nữa. Thêm khoảng trắng giữa khai báo và selector lồng nhau, cũng như giữa các phần tử lồng nhau liền kề. Áp dụng tương tự hướng dẫn như trên cho selector lồng nhau.

    ```scss
    .btn {
      background: green;
      font-weight: bold;
      @include transition(background 0.5s ease);

      .icon {
        margin-right: 10px;
      }
    }
    ```

### Biến

Nên dùng gạch ngang giữa tên biến (e.g. `$my-variable`) thay vì camelCase or snake_case. Nó cũng được chấp nhận để đặt tiền tố cho tên biến nếu có ý định sử dụng trong cùng một tập tin với dấu gạch dưới (vd: `$_my-variable`).

### Mixin

Mixin nên được sử dụng để không lặp lại các đoạn code giống nhau với phương châm (DRY - Don't-Repeat-Yourself) trong code của bạn, thêm sự rõ ràng, hoặc tách sự phức tạp--theo cách tương tự mà chức năng được đặt tên. Mixin không có đối số có thể hữu ích cho việc này, nhưng chú ý rằng nếu bạn không nén lại (vd: gzip), nó có thể tạo ra sự trùng lặp mã nguồn không cần thiết.

### Mở rộng directive

Nên tránh sử dụng `@extend` vì nó có một hành vi nguy hiểm tiềm tàng, đặc biệt khi sử dụng các selector lồng nhau. Thậm chí mở rộng placeholder selector cấp cao nhất có thể gây ra vấn đề nếu thứ tự của selector thay đổi sau đó (vd: nếu chúng đang ở một tập tin khác, và thứ tự của các tập tin được tải sẽ thay đổi). Gzip nên được sử dụng để thực hiện việc nén mà bạn có thể làm được với `@extend`, và bạn có thể DRY đoạn code của mình một cách đẹp đẽ với mixin.

### Selector lồng nhau

**ĐỪNG lồng selector hơn 3 cấp!**

```scss
.page-container {
  .content {
    .profile {
      // STOP!
    }
  }
}
```

Khi selector trở nên như vậy, bạn có thể đã viết CSS theo:

* Liên kết chặt với HTML (đặc trưng thấp) *—hoặc—*
* Quá cụ thể (đặc trưng quá cao) *—hoặc—*
* Không tái sử dụng


Lặp lại: **không bao giờ được lồng ID selector!**

Nếu bạn phải sử dụng ID selector ngay từ đầu (và bạn thực sự không nên làm thế), thì chúng không bao giờ nên được lồng nhau. Nếu bạn nhận ra mình đang làm điều này, bạn cần phải xem xét lại mã HTML, hoặc tìm hiểu tại sao lại cần tính đặc trưng cao đến như vậy. Nếu bạn đang viết HTML và CSS tốt, bạn **không bao giờ nên** cần phải làm điều này.

## Bản dịch

  Styleguide này cũng có trong những ngôn ngữ khác:

  - ![tw](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Taiwan.png) **Chinese (Traditional)**: [ArvinH/css-style-guide](https://github.com/ArvinH/css-style-guide)
  - ![cn](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/China.png) **Chinese (Simplified)**: [Zhangjd/css-style-guide](https://github.com/Zhangjd/css-style-guide)
  - ![ja](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Japan.png) **Japanese**: [nao215/css-style-guide](https://github.com/nao215/css-style-guide)
  - ![ko](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/South-Korea.png) **Korean**: [CodeMakeBros/css-style-guide](https://github.com/CodeMakeBros/css-style-guide)
  - ![PT-BR](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Brazil.png) **Portuguese**: [felipevolpatto/css-style-guide](https://github.com/felipevolpatto/css-style-guide)  
  - ![ru](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Russia.png) **Russian**: [Nekorsis/css-style-guide](https://github.com/Nekorsis/css-style-guide)
  - ![es](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Spain.png) **Spanish**: [ismamz/guia-de-estilo-css](https://github.com/ismamz/guia-de-estilo-css)
