## Vấn đề kế thừa

Giờ muốn tạo ra 1 class con\(subclass\) toyota hay ford từ class cha\(superClass\) Car thì làm sao ?

Thử gọi new trong 1 function class xem sao

```js
var superClass = function () {
    console.log(this);
}

var subClass = function () {
    new superClass()
    console.log(this);
}

var obj = new subClass() // > superClass {}
                         // > subClass {}
subClass()               // > global
```

subClass\(\) được gọi trực tiếp nên this ở đây sẽ là global variable  
new superClass\(\) sẽ tạo ra một this mới\(rỗng nếu không tạo superClass.prototype\)

## apply, call, bind

Giờ superClass có một vài phương thức và một vài  thuộc tính.  
Làm sao để khi thạo 1 obj bằng new subClass ta có thể lấy lại những thuộc tính và phương thức nào ?

```js
var superClass = function () {
    this.property = 'abc'
}

superClass.prototype.methode = function() {}
```

Nhớ lại khi chúng ta dùng new subClass\(\) thì chương trình tạo ra 1 this\(2\)  mới, bind nó với subClass.prototype nên this\(2\) này hoàn thoàn không liên quan gì tới this\(1\) của superClass

Chúng ta cần một cách thứ đế gán tất cả thuộc tính/phương thức đã có của this\(2,superClass\) cho this\(1, subClass\) trước khi trả về cho đối tượng. Đó là các phương thức call, bind, apply

\(... chưa xong...\)

## kế thừa thuộc tính

```
var subClass = function (loc) {
    // tạo ra this => this = Object.create(subClass .prototype)
    // pass this này vào superClass func, bind nó với các thuộc tính và phương thức của của superClass
    // bind nó với các thuộc tính và phương thức của của subClass
    // trả lại this cho obj => return this
}
```

Bước 2 và 3 chính là công việc của call

đọc thêm ở đây 1 tí về cách dùng call rồi xem tiếp nào

```js
var superClass = function () {
    this.abc ='xyz'  // this o day se duoc pass vao khi goi call
}

superClass.prototype.methode = function() {}

var subClass = function () {
    // this = Object.create(Car.prototype)
    superClass.call(this)
    // return this
}

var obj = new subClass()
```

## kế thừa phương thức

```js
subClass.prototype = Object.create(superClass.prototype)
```

## one thing missing here

prototype.constructor

