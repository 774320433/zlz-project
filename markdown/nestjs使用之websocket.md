# nestjs使用之websocket.md


```typescript
import {OnGatewayConnection, OnGatewayDisconnect, OnGatewayInit, SubscribeMessage, WebSocketGateway, WebSocketServer, WsResponse, } from '@nestjs/websockets';
import {Server} from 'ws';
import {UseGuards} from '@nestjs/common';
import {AuthGuard} from '../guard/auth.guard';

@WebSocketGateway({ path: '/followquant2/websocket/connect' })
export class QuantGateway implements OnGatewayConnection, OnGatewayInit, OnGatewayDisconnect {
  @WebSocketServer()
  server: Server;

  // @SubscribeMessage('events')
  // onEvent(client: any, data: any): Observable<WsResponse<number>> {
  //   console.log('client : ', data);
  //   return from([1, 2, 3]).pipe(map(item => ({ event: 'events', data: item })));
  // }

  // @UseFilters(new WebsocketFilter())
  @UseGuards(AuthGuard)
  @SubscribeMessage('test')
  onTest(client: any, data: any): WsResponse<any> {
    console.log('test');
    // throw new WsException('Invalid credentials.');
    const event = 'events';
    return { event, data };
  }

  handleConnection(client: any, ...args: any[]): any {
    // throw new WsException('Invalid credentials.');

    console.log('connection test');

    // setTimeout(() => {
    //   client.send('events');
    //   client.close();
    // },3000);
  }

  afterInit(server: any): any {
    console.log('init');
  }

  handleDisconnect(client: any): any {
    console.log('disconnect');
  }
}
```
