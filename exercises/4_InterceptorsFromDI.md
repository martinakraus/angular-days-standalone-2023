# Create an Interceptor for Book-Feature
1. Create a `TokenInterceptor` inside the books-Folder: `ng g interceptor book/token`.
2. Add the Interceptor inside the `providers`-Array in the `AppConfig`
3. You need to call the `withInterceptorsFromDi()`-Function in order to still use the Interceptor
4. Implement the `TokenInterceptor`:
- Clone the old request and set an `Authorization`-Header with the Value `Bearer 118`


## Hints

```typescript
// app.config.ts
export const appConfig: ApplicationConfig = {
    providers: [
        {
            provide: HTTP_INTERCEPTORS,
            useClass: TokenInterceptor,
            multi: true,
        },
        ...
        provideHttpClient(
            withInterceptorsFromDi()
        ),
    ]
};
```


```typescript
// book/token.interceptor.ts
@Injectable()
export class TokenInterceptor implements HttpInterceptor {
    intercept(request: HttpRequest<unknown>, next: HttpHandler): Observable<HttpEvent<unknown>> {
        const modifiedReq = request.clone({
            headers: request.headers.set('Authorization', 'Bearer 118'),
        });
        return next.handle(modifiedReq);
    }
}
```

[Solution](https://github.com/martinakraus/angular-standalone-intro/commit/5b2ef344ad88f5e7556be38222ebe91f68581dcb)
