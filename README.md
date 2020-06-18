# Error-7-PERMISSION_DENIED-The-caller-does-not-have-permission-at-Object.callErrorFromStatus
Error: 7 PERMISSION_DENIED: The caller does not have permission at Object.callErrorFromStatus


## Error:
```

Error: 7 PERMISSION_DENIED: The caller does not have permission at Object.callErrorFromStatus (/srv/node_modules/@google-cloud/iot/node_modules/@grpc/grpc-js/build/src/call.js:30:26) at Http2CallStream.call.on (/srv/node_modules/@google-cloud/iot/node_modules/@grpc/grpc-js/build/src/client.js:96:33) at emitOne (events.js:121:20) at Http2CallStream.emit (events.js:211:7) at process.nextTick (/srv/node_modules/@google-cloud/iot/node_modules/@grpc/grpc-js/build/src/call-stream.js:100:22) at _combinedTickCallback (internal/process/next_tick.js:132:7) at process._tickDomainCallback (internal/process/next_tick.js:219:9)

```

## solve

Google Firbase Store rule setting

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /{document=**} {
      allow read, write: if true;
    }
  }
}
```

should change
```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /{document=**} {
      allow read, write: if false;
    }
  }
}
```

or

```
service cloud.firestore {
  match /databases/{database}/documents {
    match /{document=**} {
      allow read, write: if request.auth.uid != null;
    }
  }
}
```
## See details

https://firebase.google.com/docs/firestore/security/get-started

如果添加了这些权限那么app中或者网页中就需要导入登录 google.auth不然就会获取数据错误


