The Angular Dependency Injection system allows you inject, into your components, classes and values for you to use, for instance as services. _Injectable_s can be Angular services (such as the [Http class](https://angular.io/docs/ts/latest/api/http/index/Http-class.html)), third-party services (like [ngx-translate](https://github.com/ngx-translate/core)), your own classes or even object values.

# Declaration

In order to inject an `@Injectable`, you need to make sure it is registered in the Dependency Injection system. Let's find out how to declare and register injectables. If you want to create a class that is used as a singleton throughout your module, a service for instance, you should create your class and add the `@Injectable` decorator to it.

```javascript
@Injectable()
export class TheService {
  public publicFunction () {
    return 'I am a public function';
  }
}
```

Then, you need to register it as a _provider_ for the component(s) you want to use it in. You can do this by using the `providers` property of the `@Component` decorator:

```javascript
import { TheService } from './the-service.ts';

@Component({
  selector: 'compo',
  providers: [TheService],
  ...
})
class Compo {
  ...
}
```

# Injection

Injecting an _Injectable_ is done through the constructor of the class you want to inject it into.

```javascript
constructor(
  public router: Router,
  public theService: TheService,
  private http: Http,
  ) {
  ...
}
```

The type of the parameter is the name of the class you want to inject. Making the injectable `public` will make it accessible by the template.
