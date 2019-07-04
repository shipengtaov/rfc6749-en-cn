# OAuth 2.0 协议中英文对照翻译

[rfc6749](https://tools.ietf.org/html/rfc6749)


## Docs

- Abstract Protocol Flow

        +--------+                               +---------------+
        |        |--(A)- Authorization Request ->|   Resource    |
        |        |                               |     Owner     |
        |        |<-(B)-- Authorization Grant ---|               |
        |        |                               +---------------+
        |        |
        |        |                               +---------------+
        |        |--(C)-- Authorization Grant -->| Authorization |
        | Client |                               |     Server    |
        |        |<-(D)----- Access Token -------|               |
        |        |                               +---------------+
        |        |
        |        |                               +---------------+
        |        |--(E)----- Access Token ------>|    Resource   |
        |        |                               |     Server    |
        |        |<-(F)--- Protected Resource ---|               |
        +--------+                               +---------------+


### Grant Types

对比各个 Grant 的图以更直观地了解不同 grant 的区别。

- Authorization Code Grant

        +----------+
        | Resource |
        |   Owner  |
        |          |
        +----------+
             ^
             |
            (B)
        +----|-----+          Client Identifier      +---------------+
        |         -+----(A)-- & Redirection URI ---->|               |
        |  User-   |                                 | Authorization |
        |  Agent  -+----(B)-- User authenticates --->|     Server    |
        |          |                                 |               |
        |         -+----(C)-- Authorization Code ---<|               |
        +-|----|---+                                 +---------------+
          |    |                                         ^      v
         (A)  (C)                                        |      |
          |    |                                         |      |
          ^    v                                         |      |
        +---------+                                      |      |
        |         |>---(D)-- Authorization Code ---------'      |
        |  Client |          & Redirection URI                  |
        |         |                                             |
        |         |<---(E)----- Access Token -------------------'
        +---------+       (w/ Optional Refresh Token)

- Implicit Grant

        +----------+
        | Resource |
        |  Owner   |
        |          |
        +----------+
             ^
             |
            (B)
        +----|-----+          Client Identifier     +---------------+
        |         -+----(A)-- & Redirection URI --->|               |
        |  User-   |                                | Authorization |
        |  Agent  -|----(B)-- User authenticates -->|     Server    |
        |          |                                |               |
        |          |<---(C)--- Redirection URI ----<|               |
        |          |          with Access Token     +---------------+
        |          |            in Fragment
        |          |                                +---------------+
        |          |----(D)--- Redirection URI ---->|   Web-Hosted  |
        |          |          without Fragment      |     Client    |
        |          |                                |    Resource   |
        |     (F)  |<---(E)------- Script ---------<|               |
        |          |                                +---------------+
        +-|--------+
          |    |
         (A)  (G) Access Token
          |    |
          ^    v
        +---------+
        |         |
        |  Client |
        |         |
        +---------+

- Resource Owner Password Credentials Grant

        +----------+
        | Resource |
        |  Owner   |
        |          |
        +----------+
             v
             |    Resource Owner
            (A) Password Credentials
             |
             v
        +---------+                                  +---------------+
        |         |>--(B)---- Resource Owner ------->|               |
        |         |         Password Credentials     | Authorization |
        | Client  |                                  |     Server    |
        |         |<--(C)---- Access Token ---------<|               |
        |         |    (w/ Optional Refresh Token)   |               |
        +---------+                                  +---------------+

- Client Credentials Grant

        +---------+                                  +---------------+
        |         |                                  |               |
        |         |>--(A)- Client Authentication --->| Authorization |
        | Client  |                                  |     Server    |
        |         |<--(B)---- Access Token ---------<|               |
        |         |                                  |               |
        +---------+                                  +---------------+

### Links

- [Difference between Client and User-Agent](https://stackoverflow.com/questions/35637601/difference-between-client-and-user-agent/35638254)

按这里的描述来说 [rfc6749#section-9: Native Applications](https://tools.ietf.org/html/rfc6749#section-9), user-agent 即浏览器

