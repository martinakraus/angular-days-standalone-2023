# Convert Some Book Components to Standalone and use it in a Module
1. Convert the Components `BookDetailComponent, BookListComponent, BookNewComponent, BookCardComponent` to standalone by adding the attribute `standalone` to the Components Decorator.
2. Import all dependencies of the components inside the `imports`-Array of their Components Decorator
3. Remove these Components from the `declarations`-Array inside the `BookModule` and add them to the `imports` Array.
4. The Application should compile properly: `nom start`

Note that you also can remove many Modules and Dependencies from the `BookModule` itself

## Hints

```typescript
// book.module.ts
@NgModule({
    imports: [
        ...
        // standalone components needs to be imported
        BookDetailComponent,
        BookListComponent,
        BookNewComponent
    ],
    declarations: [
        BookComponent
    ]
})
export class BookModule {
}
```


```typescript
// book-list.component.ts
@Component({
    selector: 'ws-book-card',
    templateUrl: './book-card.component.html',
    standalone: true,
    imports: [
        MatCardModule,
        NgOptimizedImage,
        MatButtonModule,
        RouterLink
    ],
    styleUrls: [ './book-card.component.scss' ]
})
export class BookCardComponent {
    @Input() content: Book = bookNa();
}
```

[Solution](https://github.com/martinakraus/angular-standalone-intro/commit/84da9ae3d6a554e25881923fd027f99a985956e8)
