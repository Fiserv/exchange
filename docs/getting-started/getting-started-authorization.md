# Authorization

Exchange uses the Oauth 2.0 Framework for authorizations. To generate token for authoriaation, the `/oauth/token` endpoint may be used, and credentials must be sent as a Basic Auth Header with the request.

## OAuth Token Request

The OAuth endpoint can be used to generate or refresh tokens. Once a token is generated, it can be refreshed before expiration in order to provide a new refreshed token with a new expiry time.

### Generate Token

In order to generate a token, the grant_type `client_credentials` must be used.

<!--
type: tab
titles: Generate Token Request , Generate Token Response
-->
### Generate Token Sample: 

```json
{
  "Content-Type": "application/json",
  "X-API-VERSION": "3",
  "Authorization": "AUTHORIZATION"
}
```


| field | Type | Length | Description |
| -------- | :--: | :------------: | ------------------ |
| `grant_type` | *enum* | N/A |  Grant type of the token. Can be `client_credentials` or `refresh_token` |
| `refresh_token` | *string* | 40 | Used in the request when refreshing the token. Provided in the reponse of the token generation request.  |


<!-- type: tab -->

### Generate Token Response: :

```json
{
  "access_token": "abC0leXAiOiJKV1QiLCJhbGhOeanINQ_pfdt_j97mBqjekKJV4BL-HP6a011p_D7avcSaJ4SeG_tis9D_Gfh66MY7BN73IcAC9Sb_qxaFxSavxvW_d6Nk9hfg8y4OSb7HEB58sxEVfuJ87dsmURWsJz8sxEVfwlk0a2Zbt_BqjekK-Yk-DiJFwiaTtbBqjekKJV4jPhIsxEVfws_wz2MMxkuydcpGl5m-rIpIwT9xAE0avcSaJ4S_4hTU1llskE60vwzv27_URWsJz8sxEVfwlk0a2ZbtXB32u3ERSVyD7TaQjme64Va4ac.rQCcRAu7XObjap3szzy3URWsJzwlk0a2Zbt",
  "token_type": "bearer",
  "expires_in": "28800",
  "scope": [
    "webclient",
    "mobileclient"
  ],
  "jti": "00de-lk8d-01cd-762d-xkuyd6aSaJ4",
  "refresh_token": "RAu7XO69aV4jPhI6c1411b39Jz8sxEVfwv4p"
}

```
| field | Type | Length | Description |
| -------- | :--: | :------------: | ------------------ |
| `access_token` | *enum* | N/A |  Grant type of the token. Can be `client_credentials` or `refresh_token` |
| `token_type` | *string* | 5 | Used in the request when refreshing the token. Provided in the reponse of the token generation request.  |
| `expires_in` | *string* | 5 | Used in the request when refreshing the token. Provided in the reponse of the token generation request.  |
| `scope` | *string* | enum | Used in the request when refreshing the token. Provided in the reponse of the token generation request.  |
| `jti` | *string* | N/A | Used in the request when refreshing the token. Provided in the reponse of the token generation request.  |
| `refresh_token` | *string* | 40 | Used in the request when refreshing the token. Provided in the reponse of the token generation request.  |

---

<!-- type: tab-end -->

### Refresh Token

<!--
type: tab
titles: Refresh Token Request , Refresh Token Response
-->

```json
{
  "grant_type": "refresh_token",
  "refresh_token": "RAu7XO69aV4jPhI6c1411b39Jz8sxEVfwv4p"
}

```

| field | Type | Length | Description |
| -------- | :--: | :------------: | ------------------ |
| `grant_type` | *enum* | N/A |  Grant type of the token. Can be `client_credentials` or `refresh_token` |
| `refresh_token` | *string* | 40 | Used in the request when refreshing the token. Provided in the reponse of the token generation request.  |


<!-- type: tab -->

### Generate Token Response: :


```json
{
  "access_token": "abC0leXAiOiJKV1QiLCxEVfwlk0a2Zbt_BV4BL-HP6a011p_D7avcSaJ4SeIcAC9Sb_qxaFxSavxvW_d6Nlkj02aeB58sxEVfuJ87dsmURWsJz8sxEVfwlk0a2Zbt_BqjekK-Yk-DiJFwiaTtbBqjekKJV4jPhIsxEVfws_wz2MMxkuydcpGl5m-rIpIwT9xAE0avcSaJ4S_4hTU1lskE60vwvwzv27_URWsJz8sxEjme64Va4ac.rQCcRAu7XObxEVfwlk0a2Zbt_BURWsJzwlk0a2Zbt",
  "token_type": "bearer",
  "expires_in": "28800",
  "scope": [
    "webclient",
    "mobileclient"
  ],
  "jti": "l0ae-762d-01cd-01cd-cdxLpaSa32",
  "refresh_token": "llskE60vwzavcPhI6c1411bO69aV4jPxEVfwv4p"
}

```
| field | Type | Length | Description |
| -------- | :--: | :------------: | ------------------ |
| `access_token` | *enum* | N/A |  Grant type of the token. Can be `client_credentials` or `refresh_token` |
| `token_type` | *string* | 5 | Used in the request when refreshing the token. Provided in the reponse of the token generation request.  |
| `expires_in` | *string* | 5 | Used in the request when refreshing the token. Provided in the reponse of the token generation request.  |
| `scope` | *string* | enum | Used in the request when refreshing the token. Provided in the reponse of the token generation request.  |
| `jti` | *string* | N/A | Used in the request when refreshing the token. Provided in the reponse of the token generation request.  |
| `refresh_token` | *string* | 40 | Used in the request when refreshing the token. Provided in the reponse of the token generation request.  |

---

<!-- type: tab-end -->

# Postman

During integration to the API, you may want to use a tool such as Postman to test APIs in the UAT environment.

## Authentication
If testing using postman, the Auth tab can be used to authorise API requests. This can be done by using Auth type Outh 2.0, selecting Grant Type 'Client Credentials', entering the Access Token URL `{{URL}}/oauth/token`, Client ID as as username an Client secret as password and getting new access token. It may be useful to create an environment in postman and use these as variables.

![postman auth](/assets/images/auth_postman.png)

