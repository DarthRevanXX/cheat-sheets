
Add `@Exclude()` decorator to the entity
In `controller` to route add decorator 
`@UseInterceptors(ClassSerializerInterceptor)`

Downside
depends on permission if we have admin but anyway there will not excluded field

## Build interceptors

class CustomInterceptor

intercept(context: ExecutionContext, next: CallHandler) - need to be implemented

To run before handler
```
export class SerializeInterceptor implements NestInterceptor {

  constructor(private dto: any) {}

  intercept(context: ExecutionContext, handler: CallHandler): Observable<any> {

    // Run something before a request is handled by the request handler

    console.log('I am running before the handler', context);

  

    return handler.handle().pipe(

      map((data: any) => {

        // Run something before the response is sent out

        console.log('I am running after the handler', data);

        return plainToInstance(this.dto, data, {

          excludeExtraneousValues: true,

        });

      }),

    );

  }

}
```


