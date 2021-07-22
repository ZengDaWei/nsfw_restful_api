# nsfw_restful_api
图片鉴黄API，支持自建和Docker

## 快速使用 - Docker版

我将其搭建过程，制作成了一个`Docker`镜像，上传到了`Docker Hub`，提供给大家快速使用。

```bash
$ docker pull zengdawei/nsfw_restful_api
# 镜像映射端口：`3307`
$ docker run -p 3307:3307 -d zengdawei/nsfw_restful_api
```

容器启动完成后，`Docker`会将本机的 `3307` 端口，绑定到容器的 `3307`端口。

### 测试

```bash
$ curl --location --request GET 'http://127.0.0.1:3307/api/nsfw/classify?url=https://image.zdw1.cn/img20210720174923.png'
```

返回结果：

```json
[
    {
        "className": "Drawing",
        "probability": 0.824431836605072
    },
    {
        "className": "Hentai",
        "probability": 0.16360442340373993
    },
    {
        "className": "Neutral",
        "probability": 0.007620695047080517
    },
    {
        "className": "Porn",
        "probability": 0.004154415801167488
    },
    {
        "className": "Sexy",
        "probability": 0.00018858206749428064
    }
]
```

- `probability`，概率
- `className`，类型

上传图片后，总共会返回 5 个维度的数值来鉴别该图片的尺度:

- 绘画（Drawing）—— 无害的艺术，或艺术绘画；
- 变态（Hentai）—— 色情艺术，不适合大多数工作环境；
- 中立（Neutral）—— 一般，无害的内容；
- 色情（Porn）—— 不雅的内容和行为，通常涉及生殖器；
- 性感（Sexy）—— 不合时宜的挑衅内容。

当`porn`评分超过`>=0.6`左右,就几乎是一张带有`色情性质`的图片了。
