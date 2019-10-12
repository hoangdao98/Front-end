# Angular Framework
Angular là một nền tảng mã nguồn mở dựa trên Typescript, giúp dễ dàng xây dựng các ứng dụng web/mobile/desktop.
# AngularJS và Angular
Một số khác biệt chính

| AngularJS        | Angular    |
| ------------- |-------------|
| AngularJS dựa trên kiến trúc MVC  | Angular dựa trên Service/Controller |
| Sử dụng Javascript để build application      | Sử dụng Typescript để build application      |
| Dựa trên controller | Dựa trên các thành phần tách biệt  |
# Các thành phần chính trong Angular
Angular bao gồm những thành phần sau:
*   **Component:** Đây là thành phần cơ bản của Angular dùng để quản lý HTML views.
*   **Modules:** Module là nơi để khai báo các thành phần mà ta sẽ sử dụng như components, directives, services... Mỗi phần trong module sẽ thực hiện một nhiệm vụ.
*   **Templates:** Nó đại diện cho phần views của một Angular application.
*   **Service:** Nó là nơi giúp ta tái sự dụng code vì nó có thể chia sẻ trên toàn bộ ứng dụng với cơ chế là dependence injection. 
*   **Metadata:** Có thể sử dụng để thêm nhiều dữ liệu vào một Angular class. vd như @NgModule, @Directive, etc.
# Component trong Agular
Component trong angular là một thành phần cơ bản, dùng để quản lý phần views của một application. Mỗi component luôn có 1 template (không có cái thứ 2).

```typescript
import { Component } from '@angular/core';

@Component ({
   selector: 'my-app',
   template: ` <div>
      <h1>{{title}}</h1>
      <div>Learn Angular 8 with examples</div>
   </div> `,
})

export class AppComponent {
   title: string = 'Welcome to Angular world';
}
```
# Directive trong Angular
Directives thêm hành vi vào một DOM element đã tồn tại hoặc một component đã được khởi tạo.
```typescript
import { Directive, ElementRef, Input } from '@angular/core';

@Directive({ selector: '[myHighlight]' })
export class HighlightDirective {
    constructor(el: ElementRef) {
       el.nativeElement.style.backgroundColor = 'yellow';
    }
}
```
Khi thêm directive vào DOM, Đoạn code directive trên sẽ giúp ta chuyển background của DOM sang màu vàng.
```typescript
import { Component } from '@angular/core';
// Import derective here.
@Component ({
   selector: 'my-app',
   // Thêm directive vào DOM
   template: `<div myHighlight>
      <h1>{{title}}</h1>
   </div>`,
})

export class AppComponent {
   title: string = 'Welcome to Angular world';
}
```
# Template trong Angular
Một template là một HTML view mà chúng ta có thể binding dữ liệu và quản lý các thuộc tính của một component. Ta có thể tạo template bằng một trong 2 cách. 

Cách 1: Định nghĩa các thuộc tính ngay bên trong template
```typescript
import { Component } from '@angular/core';

@Component ({
   selector: 'my-app',
   template: '
      <div>
         <h1>{{title}}</h1>
         <div>Learn Angular</div>
      </div>
   '
});

export class AppComponent {
   title: string = 'Hello World';
}
```

Cách 2: Định nghĩa bằng 1 file html
```typescript
import { Component } from '@angular/core';

@Component ({
   selector: 'my-app',
   templateUrl: 'app/app.component.html'
})

export class AppComponent {
   title: string = 'Hello World';
}
```
# Module trong Angular
Module là nơi để khai báo các thành mà ta sẽ sử dụng như components, directives, services... Mỗi phần trong module sẽ thực hiện một nhiệm vụ. Lấy ví dụ file app.module.ts
```typescript
import { NgModule }      from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { AppComponent }  from './app.component';

@NgModule ({
   imports:      [ BrowserModule ],
   declarations: [ AppComponent ],
   bootstrap:    [ AppComponent ]
})
export class AppModule { }
```
Sử dụng `Metadata` là `@NgModule` và sẽ có 3 options như sau
*   imports: 
*   declarations:
*   bootstrap: 

Ngoài ra không chỉ có 3 options trên mà ta còn có các options như providers, entryComponent được sử dụng trong dynamic component.
# Metadata
Metadata sử dụng để cấu hình hành vi của các các lớp. Muốn Angular hiểu được nó thì ta phải cần phải khai báo.

**Class decarators: @NgModule, @Component**
```typescript
import { NgModule, Component } from '@angular/core';

// Khai báo metadata @Component để Angular hiểu đây là component
@Component({
    selector: 'my-component';
    template: 'my-component.component.html'
});

// Khai báo metadata @NgModule để Angular hiểu đây là module
@NgModule({
    imports: [],
    declarations: []
});

export class MyModule {
}
```
**Property decarators: Được sử dụng cho thuộc tính bên trong class như @Input, @Output ...**
```typescript
import { Component, Input } from '@angular/core';

@Component({
    selector: 'my-component',
    template: '<div>Property decorator</div>'
})

export class MyComponent {
    @Input()
    @Output()
    title: string;
}
```
**Method decorators: Được sử dụng cho các method bên trong class @HostListener**
```typescript
import { Component, HostListener } from '@angular/core';

@Component({
    selector: 'my-component',
    template: '<div>Method decorator</div>'
})
export class MyComponent {
    @HostListener('click', ['$event'])
    onHostClick(event: Event) {
        // clicked, `event` available
    }
}
```
**Parameter decorators: Được sử dụng cho các prameter bên trong contructor như @Inject**
```typescript
import { Component, Inject } from '@angular/core';
import { MyService } from './my-service';

@Component({
    selector: 'my-component',
    template: '<div>Parameter decorator</div>'
})
export class MyComponent {
    constructor(@Inject(MyService) myService) {
        console.log(myService); // MyService
    }
}
```
# Lifecycle hook trong Angular.
Angular application sẽ phải trải qua 1 lifecycle xuyên suốt từ đầu đến khi kết thúc ứng dụng.
![lifecycle](https://github.com/sudheerj/angular-interview-questions/raw/master/images/lifecycle.png)

**Chức năng chính của từng method**
*   ngOnChanges: Khi giá trị thuộc tính ràng buộc dữ liệu thay đổi, thì method này sẽ được gọi.
*   ngOnInit: Chỉ chạy lần đầu tiên ngay khi component được khởi tạo. Được gọi sau ngOnChanges.
*   ngDoCheck: Method này sử dụng để phát hiện và xử lý các thay đổi mà Angular không thể hoặc không phát hiện ra. Quá trình này còn được gọi là change dectection. Change detection là cơ chế của Angular để kiểm tra sự thay đổi của bất kỳ các thuộc tính, event ...  Được gọi ngay sau ngOnChanges và ngOnInit
*   ngAfterContentInit: Được gọi khi Angular bind dữ liệu xong. Chỉ được gọi duy nhất 1 lần sau lần gọi đầu tiên của ngDoCheck
*   ngAfterContentChecked: Được gọi ngay sau khi change detector default đã kiểm tra content (Mình chưa hiểu rõ phần này)
*   ngAfterViewInit: Được gọi khi toàn bộ component view được khởi tạo thành công.
*   ngAfterViewChecked: Được chạy mỗi lần view trong component được kiểm tra bởi Change Detection trong Angular.
*   ngOnDestroy: Được gọi ngay sau khi destroy 1 component.

# Dependency Injection trong Angular
Dependency injection (DI), là một desgin parttern quan trọng trong một ứng dụng, nó giúp ta `inject` các đối tượng dependency bên ngoài thay vì mình phải tự tạo ra chúng. Angular đã xây dựng một framework dependency riêng, và ta không thể dựng một ứng dụng Angular mà không có nó.

Trong Angular CLI, DI có 3 phần cơ bản: 
![DI](https://viblo.asia/uploads/d9b69c02-9869-4ac4-a1e4-ee5081dad62c.png)
*   Injector: Một đối tượng chứa các API để chúng ta tạo các instance của dependecies.
*   Provider: Nơi khai báo cho Injector biết để tạo ra dependency.
*   Object: Là một object của kiểu dữ liệu cần khởi tạo

## DI token là cái gì?
Đăng ký 1 provider
```typescript
import { NgModule } from '@angular/core';
import { AuthService } from './auth.service';

@NgModule({
  providers: [AuthService],
})
class ExampleModule {}
```
Ví dụ trên là cách viết tắt, chi tiết thì nó sẽ là như này.
```typescript
import { NgModule } from '@angular/core';
import { AuthService } from './auth.service';

@NgModule({
  providers: [
     { 
        provide: AuthService,
        useClass: AuthService
     }
  ],
})
class ExampleModule {}
```
Ta sẽ inject dependencies vào component

```typescript
import { Component } from '@angular/core';
import { AuthSerivce } from '...'

@Component({
   selector: 'auth-login',
   template: 'auth-login.component.html'
});

export class AuthLoginComponent {
   // Khởi tạo dependency 
   constructor(private authSerivce: AuthService);
}
```
Dependency được đăng ký trong 1 tập Providers sử dụng một tập token-provider. Component inject các các depencenies vào trong hàm khởi tạo sử dụng `token` (token chính là provide trong object). Injector sẽ tìm kiếm một provider trong tập providers sử dụng token. Nếu như được tìm thấy nó sẽ khởi tạo và inject vào trong component. Còn nếu không tìm thấy thì nó sẽ tiếp tục request tới injector của component cha, và cứ tiếp tục như vậy cho đến khi thấy provider. Nếu không tìm thấy provider cho dependency, sẽ có một lỗi xảy ra `"EXCEPTION: Error in Component class – inline template caused by No provider for Service!".`
