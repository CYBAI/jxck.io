# [web][blog] Blog を移転しました

## Intro

長いこと


### サンプルコード


```js
if ('ServiceWorkerGlobalScope' in self && self instanceof ServiceWorkerGlobalScope) {
  ['install', 'activate', 'beforeevicted', 'evicted', 'fetch', 'message', 'push'].forEach((e) => {
    self.addEventListener(e, (ev) => {
      console.log(e, ev);
    });
  });

  self.addEventListener('install', (ev) => {
    ev.waitUntil(self.skipWaiting());
  });

  self.addEventListener('activate', (ev) => {
    ev.waitUntil(self.clients.claim());
    console.log('claimed');
  });
}
```
