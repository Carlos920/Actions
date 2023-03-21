# Actions
### `aliyun_signin.yml`
> 参考  
> https://github.com/ImYrS/aliyun-auto-signin  
> https://www.52pojie.cn/thread-1757911-1-1.html


<details> 
    <summary>获取chat_id</summary>


> bot_token `xxx:yyyyyyyyyy`  
    
> chat_id 

#### query api

```
https://api.telegram.org/bot<bot_token>/getUpdates
```

- user chat_id

```js
"from": {
          "id": xxxxxxx,
          "is_bot": false,
          "first_name": "xxx",
          "language_code": "zh-hans"
        }
```

- group/channel chat_id
    
```js
"chat": {
          "id": -xxxxxxx,
          "title": <channel name>,
          "username": "<channel username>",
          "type": "channel"
        }

```

#### Test api
```bash
curl -X POST "https://api.telegram.org/bot<bot_token>/sendMessage" -d "chat_id=<chat_id>&text=<message>"
```

</details>
