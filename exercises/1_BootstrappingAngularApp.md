# Bootstrapping an Angular Application with Standalone API
1. Creat a new Application with `ng new bookmonkey-client --routing false --style scss --skip-tests`.
2. Make the `AppComponent` standalone by adding the attribute `standalone` to the Components Decorator.
3. Use the `bootstrapApplication`-Function to initialize your Angular Application (don't forget to remove the old API `bootstrapModule()`).
4. Now you are save to remove the `AppModule` and deleting the file.
5. Create another standalone Component by running the CLI command `ng generate component home --standalone` and import it inside the `AppComponent`

## Hints

```typescript
// main.ts
import { bootstrapApplication } from '@angular/platform-browser';
import { AppComponent } from './app/app.component';

bootstrapApplication(AppComponent)
  .catch(err => console.error(err));

// app.component.ts
@Component({
  selector: 'app-root',
  standalone: true,
  imports: [HomeComponent]
  // ...
})
export class AppComponent {}
```
