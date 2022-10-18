# Add a lazily loaded Component and Injector with Standalone API
1. Create another standalone component `BookNewComponent` inside the `books` folder
2. Now we want to load this component lazily, so we need to add the Component import with `loadComponent` into our `BOOK_ROUTES` definition
3. Add an `a`-Tag with a `routerLink` inside the `BookComponent` for Navigation
4. Let's add a `BookApiService` and implement a `getAll`-Function. This Function should return an Array of Books
5. We want do display the books inside the `BookComponent` so we need to inject it there
6. To be able to inject the Service we need to provide it inside the routing definition of `app.routes.ts`

## Bonus:

If you want you can add the `HttpClient` to your `BookApiService` by fetching books from a backend.
1. You can install the dummy-backend with `npm i --global bookmonkey-api`
2. By running `bookmonkey-api` you should be see an output lik e`JSON Server is running on port 4730`
3. By visiting `http://localhost:4730/` in your Browsder you should be able to see a swagger UI. The books are available at `http://localhost:4730/books`
4. You can provide the `HttpClient` by calling `importProvidersFrom` inside the `bootdtrap Function`

## Hints

```typescript
// books/routes.ts
export const BOOK_ROUTES: Routes = [
  ...
    {
      path: 'new', 
      loadComponent: () => import('./create-book/create-book.component').then(m => m.CreateBookComponent)
    }
];


// example Books
[
      {
        title: 'How to win friends',
        author: 'Dale Carnegie',
        abstract:
          "How to Win Friends and Influence People is a self-help book written by Dale Carnegie, published in 1936. Over 30 million copies have been sold worldwide, making it one of the best-selling books of all time. In 2011, it was number 19 on Time Magazine's list of the 100 most influential books."
      },
      {
        title:
          'The Willpower Instinct: How Self-Control Works, Why It Matters, and What You Can Do to Get More of It',
        author: 'Kelly McGonigal',
        abstract:
          'Based on Stanford University psychologist Kelly McGonigal\'s wildly popular course "The Science of Willpower," The Willpower Instinct is the first book to explain the new science of self-control and how it can be harnessed to improve our health, happiness, and productivity'
      },
      {
        author: 'Simon Sinek',
        title: 'Start with WHY',
        abstract:
          "START WITH WHY shows that the leaders who've had the greatest influence in the world all think, act, and communicate the same way -- and it's the opposite of what everyone else does. Sinek calls this powerful idea The Golden Circle, and it provides a framework upon which organizations can be built, movements can be led, and people can be inspired. And it all starts with WHY."
      }
    ]
```


