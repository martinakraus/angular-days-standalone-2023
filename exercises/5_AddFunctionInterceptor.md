# Add functional Interceptor
1. Create a File `book/api-version.interceptor.ts` (Do not use the Angular CLI for it)
2. Add following Function to it:

```typescript
export const ApiVersionInterceptor = (request: HttpRequest<unknown>, next: HttpHandlerFn): Observable<HttpEvent<unknown>> => {
    const modifiedReq = request.clone({
        headers: request.headers.set('X-Api-Version', '11'),
    });
    return next(modifiedReq);
}
```

3. Open the `book/routes.ts`-File and a  `providers`-Array to the path `new`
4. Add the `BookApiService` to this Array and also `provideHttpClient()`
5. Add the Function `withInterceptors()` inside the `provideHttpClient()` and pass in the `ApiVersionInterceptor` (Note the `withInterceptors` takes an Array)

You should see the `X-Api-Version`-Header on the `POST`-Request but not the `Authorization`-Header

6. In order to also execute the parent-Interceptor as well add the function `withRequestsMadeViaParent()` to the `provideHttpClient`-Function

## Hints

```typescript
// book/routes.ts
...
{
    path: 'new',
    ...
    providers: [
    BookApiService,
    provideHttpClient(
        withRequestsMadeViaParent(),
        withInterceptors(
            [ ApiVersionInterceptor ]
        )
    )
]
},
```


```typescript
// book/api-version.interceptor.ts
export const ApiVersionInterceptor = (request: HttpRequest<unknown>, next: HttpHandlerFn): Observable<HttpEvent<unknown>> => {
    const modifiedReq = request.clone({
        headers: request.headers.set('X-Api-Version', '11'),
    });
    return next(modifiedReq);
}
```

[Solution](https://github.com/martinakraus/angular-standalone-intro/commit/575dec35d7ec77a18d55d562646ed7918aa722ff)
