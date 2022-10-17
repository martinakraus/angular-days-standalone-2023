# Add Routing with Lazy loading to you Angular Application with Standalone API
1. Add a `books` Folder and create another standalone component `BookComponent` inside it
2. Inside the `books`-Folder also add a `routes.ts` File and just add an Array of Routes `BOOK_ROUTES` (don't forget to export it)
3. Add a route to the `BookComponent` inside the Routes Array of `books/routes.ts` 
4. Let's configure now the `APP_ROUTES` by adding a `app.routes.ts` file and insert a routing configuration for default route and a route to the `HomeComponent`
5. Since we want to lazy load the child routes from the `BOOK_ROUTES` we also add them with the new standalone API syntax for lazy loading routes
6. Now we just need to insert the `APP_ROUTES` to the `bootstrapApplication` with the help of the `provideRouter` function.
7. Inside the `AppComponent` we need to add the `<router-outlet></router-outlet>` and two `<a>`-Tags for Navigation to our `/book` and our `/home` Route
8. Don't forget to import everything we need (`RouterOutlet`, `RouterLinkWithHref`) inside the `AppComponent` (The import of the HomeComponent can be removed now)

## Hints

```typescript
// app.routes.ts
export const APP_ROUTES: Routes = [
  { path: '', redirectTo: '/home', pathMatch: 'full' },
  { path: 'home', component: HomeComponent },
  {
    path: 'book',
    loadChildren: () => import('./books/routes').then(m => m.BOOK_ROUTES)
  }
];


// main.ts
...
import { APP_ROUTES } from './app/app.routes';

bootstrapApplication(AppComponent, {
  providers: [
    provideRouter(APP_ROUTES)
  ]
}).catch(err => console.error(err));

// app.component.ts
@Component({
  selector: 'app-root',
  standalone: true,
  imports: [HomeComponent]
  // ...
})
export class AppComponent {}
```

```html
//app.component.html

<h1>Hello Standalone</h1>

<nav>
  <a routerLink="/home">HOME</a>
  <a routerLink="/book">BOOK</a>
</nav>

<router-outlet></router-outlet>

```