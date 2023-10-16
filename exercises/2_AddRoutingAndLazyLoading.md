# Add Routing with Lazy loading to you Angular Application with Standalone API
1. Rename the `app-routing.module.ts` to `routes.ts` and remove the `NgModule`-Decorator. 
2. Use the `provideRouter`-Function inside the `providers`-Array in the `app.config.ts` File and add the `routes` as a Parameter. Remove the `importProvdersFrom`-Function
3. Convert the `BookComponent` to Standalone and remove the `BookModule` completely.
4. Rename the `book-routing.module.ts` to `routes.ts` and remove the `NgModule`-Decorator.
5. Instead of Lazy-loading the `BookModule`: Change the Lazy Loading Path to lazy load the `books/routes.ts`
 
## Hints

```typescript
// app/routes.ts
export const routes: Routes = [
    {
        path: '',
        pathMatch: 'full',
        redirectTo: '/books'
    },
    {
        path: 'books',
        loadChildren: () => import('./book/routes').then(m => m.routes)
    }
];
```

[Solution](https://github.com/martinakraus/angular-standalone-intro/commit/fe334197fff6b0691ecd6baeb9d042f4569eb8be)
