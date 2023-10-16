# Add a lazily loaded Component and Injector with Standalone API
1. Now we want to load the `BookNewComponent`, so we need to add the Component import with `loadComponent` into our `book/routes.ts` definition
2. Additionally we want to lazy inject the `BookApiService`: Open the `book/routes.ts` and add a `providers`-Array to the `BookComponent`
3. Remove the `{provideIn: 'root'}`-Object from the `Injectable`-Decorator inside the `BookApiService` and add the Service to the created `providers`-Array

## Hints

```typescript
export const routes: Routes = [
    {
        path: '',
        component: BookComponent,
        providers: [ BookApiService ],
        children: [
            {
                path: '',
                component: BookListComponent
            },
            {
                path: 'new',
                loadComponent: () => import('./book-new/book-new.component').then(m => m.BookNewComponent)
            },
            {
                path: ':isbn',
                component: BookDetailComponent
            }
        ]
    }
];
```

[Solution](https://github.com/martinakraus/angular-standalone-intro/commit/5cfcee4e689de36d6eef044906e18ada7fd6147c)


