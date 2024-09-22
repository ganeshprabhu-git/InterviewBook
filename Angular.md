
Here are detailed answers for the questions:

1. **What is Angular?**
   Angular is a platform and framework for building single-page client applications using HTML and TypeScript. It is maintained by Google and offers a comprehensive suite of tools and features for building robust and scalable web applications. Angular combines declarative templates, dependency injection, end-to-end tooling, and integrated best practices to solve development challenges.

2. **What is a Component?**
   In Angular, a component is a fundamental building block of the application. It consists of three parts:
   - **Template**: Defines the HTML view for the component.
   - **Class**: Contains the component's logic, properties, and methods.
   - **Metadata**: Provided by decorators such as `@Component`, which define the component's configuration, including its selector, template URL, and style URLs.

   Example:
   ```typescript
   import { Component } from '@angular/core';

   @Component({
     selector: 'app-hello-world',
     template: `<h1>Hello World</h1>`,
     styles: [`h1 { color: red; }`]
   })
   export class HelloWorldComponent {}
   ```

3. **What is a Directive?**
   Directives are classes in Angular that add behavior to elements in the DOM. There are three types:
   - **Structural Directives**: Change the DOM layout by adding or removing elements. Example: `*ngIf`, `*ngFor`.
   - **Attribute Directives**: Change the appearance or behavior of an element. Example: `ngClass`, `ngStyle`.
   - **Component Directives**: Directives with a template (essentially components). Example: Custom components like `HelloWorldComponent`.

   Example of an Attribute Directive:
   ```typescript
   import { Directive, ElementRef, Renderer2, HostListener } from '@angular/core';

   @Directive({
     selector: '[appHighlight]'
   })
   export class HighlightDirective {
     constructor(private el: ElementRef, private renderer: Renderer2) {}

     @HostListener('mouseenter') onMouseEnter() {
       this.renderer.setStyle(this.el.nativeElement, 'backgroundColor', 'yellow');
     }

     @HostListener('mouseleave') onMouseLeave() {
       this.renderer.setStyle(this.el.nativeElement, 'backgroundColor', 'transparent');
     }
   }
   ```

4. **What is session management in Angular?**
   Angular itself does not provide session management, but it can be handled using various methods:
   - **Cookies**: Use Angular services to manage cookies.
   - **Local Storage/Session Storage**: Use the Web Storage API to store session data.
   - **Tokens**: Use authentication tokens stored in local or session storage and attach them to HTTP requests.

   Example using Local Storage:
   ```typescript
   localStorage.setItem('userSession', JSON.stringify(userData));
   const userSession = JSON.parse(localStorage.getItem('userSession'));
   ```

5. **What is the difference between AOT (Ahead-of-Time) and JIT (Just-in-Time) compiler?**
   - **AOT Compiler**: Compiles Angular HTML and TypeScript code into JavaScript code during the build phase. This results in faster application load times since the browser loads pre-compiled code. It also helps in detecting template errors at compile time.
     ```bash
     ng build --prod
     ```
   - **JIT Compiler**: Compiles code in the browser at runtime. Useful during development because it allows for faster build and serve times, but it can lead to slower application load times in production due to compilation happening in the browser.
     ```bash
     ng serve
     ```

6. **What is Dependency Injection?**
   Dependency Injection (DI) is a design pattern used to implement IoC (Inversion of Control) where Angular provides dependencies to a component or service instead of the component or service creating the dependencies itself. This helps in managing services and making the code more modular and testable.

   Example:
   ```typescript
   import { Injectable } from '@angular/core';

   @Injectable({
     providedIn: 'root'
   })
   export class DataService {
     constructor() {}
   }

   @Component({
     selector: 'app-data',
     template: `Data Component`
   })
   export class DataComponent {
     constructor(private dataService: DataService) {}
   }
   ```

7. **How do you run an Angular application, and what is the default port? How can you change the default port?**
   - To run an Angular application, use the Angular CLI command:
     ```bash
     ng serve
     ```
     By default, the application runs on port 4200.
   - To change the default port, use the `--port` flag:
     ```bash
     ng serve --port 4300
     ```

8. **What are the lifecycle methods in Angular? Explain the different lifecycle hooks like ngOnInit, ngOnChanges, ngDoCheck, etc. Why does the constructor get triggered first? What is the purpose of ngOnInit?**
   Angular components have a series of lifecycle hooks that allow developers to tap into different phases of a component's lifecycle. Key lifecycle hooks include:
   - **`ngOnChanges`**: Called when an input property value changes.
   - **`ngOnInit`**: Called once after the first `ngOnChanges`. It’s used to initialize component data.
   - **`ngDoCheck`**: Called with every change detection cycle.
   - **`ngAfterContentInit`**: Called after content (ng-content) has been projected into the component.
   - **`ngAfterContentChecked`**: Called after the projected content has been checked.
   - **`ngAfterViewInit`**: Called after the component's view and child views have been initialized.
   - **`ngAfterViewChecked`**: Called after the component's view and child views have been checked.
   - **`ngOnDestroy`**: Called just before the component is destroyed.

   **Constructor**: Called when the component is instantiated. It’s used to inject dependencies and initialize simple properties. It does not have access to the component’s template or inputs.

   **Purpose of `ngOnInit`**: It’s used to perform complex initialization logic that requires access to the component's inputs or to perform data-fetching operations. It ensures that the component is fully initialized before any other operations are performed.

9. **What is a single-page application (SPA) and how does Angular implement routing? Explain how navigation works in Angular. Describe the steps to create routing in an Angular application.**

   **Single-Page Application (SPA)**: A web application that interacts with the user by dynamically rewriting the current page, rather than loading entire new pages from the server. This approach provides a more fluid and responsive user experience.

   **Angular Routing**: Angular's routing mechanism allows navigation between different views or components. It is implemented using the Angular Router, which manages the application’s navigation.

   **Steps to Create Routing**:
   1. **Define Routes**: Create a routing module where you define routes. Each route maps a URL path to a component.
      ```typescript
      import { NgModule } from '@angular/core';
      import { RouterModule, Routes } from '@angular/router';
      import { HomeComponent } from './home/home.component';
      import { AboutComponent } from './about/about.component';

      const routes: Routes = [
        { path: '', component: HomeComponent },
        { path: 'about', component: AboutComponent }
      ];

      @NgModule({
        imports: [RouterModule.forRoot(routes)],
        exports: [RouterModule]
      })
      export class AppRoutingModule { }
      ```
   2. **Configure the Router Outlet**: Add `<router-outlet>` to your application’s main template where you want routed content to be displayed.
      ```html
      <!-- app.component.html -->
      <router-outlet></router-outlet>
      ```
   3. **Navigate Programmatically**: Use Angular’s `Router` service to navigate between routes.
      ```typescript
      import { Router } from '@angular/router';

      @Component({
        selector: 'app-nav',
        template: `<button (click)="goToAbout()">Go to About</button>`
      })
      export class NavComponent {
        constructor(private router: Router) {}

        goToAbout() {
          this.router.navigate(['/about']);
        }
      }
      ```
   4. **Route Guards**: Optionally, use route guards to protect routes or perform pre-navigation logic. 

   With these steps, you can set up and manage routing in an Angular application efficiently.
