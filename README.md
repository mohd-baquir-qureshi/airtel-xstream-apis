# Airtel Xstream Unofficial API

This is a free unofficial API to login and fetch HLS Links from Airtel Xstream, this is created just to learn different encryption techniques used in backend, use it for educational purpose only.

---
###### **NOTE:** The mobile number must be a Airtel Number and must have a Active Plan.
 ---
 
## API Reference

#### Send OTP

```
  GET https://axstream.vercel.app/sendOtp
```

| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `mobNo` | `string` | **Required**. 10 Digit Mobile No. |

#### Send OTP Example

```
  GET https://axstream.vercel.app/sendOtp?mobNo=1234567890
```

```json
{
    "did": "06e087c7-6c41-4f61-bb36-0f67jie8c390",
    "message": "SMS sent",
    "token": "CbWknul7IC3u35fJGNDd023IS4s=",
    "uid": "7ABN_j__DAAkqsU5A3mqo2bRLhI2"
}
```

#### Verify OTP and Login

```
  POST https://axstream.vercel.app/verifyOtp
```

| Parameter | Type     | Description                       |
| :-------- | :------- | :-------------------------------- |
| `mobNo`      | `string` | **Required**. The same mobile number used while sending the OTP. |
| `otp`      | `string` | **Required**. OTP Received on Mobile Number. |
| `did`      | `string` | **Required**. "did" value which we got from sendOtp response. |
| `token`      | `string` | **Required**. "token" value which we got from sendOtp response. |
| `uid`      | `string` | **Required**. "uid" value which we got from sendOtp response. |


#### Verify OTP and Login Code Sample in Javascript using Fetch

```
const formdata = new FormData();
formdata.append("mobNo", "1234567890");
formdata.append("otp", "0101");
formdata.append("did", "06e087c7-6c41-4f61-bb36-0f67jie8c390");
formdata.append("token", "CbWknul7IC3u35fJGNDd023IS4s=");
formdata.append("uid", "7ABN_j__DAAkqsU5A3mqo2bRLhI2");
const requestOptions = {
  method: "POST",
  body: formdata
};
fetch("https://axstream.vercel.app/verifyOtp", requestOptions)
  .then((response) => response.text())
  .then((result) => console.log(result))
  .catch((error) => console.error(error));
```

```json
{
    "authToken": "gK/qwuFRTkXqqduoSkw4iN+mv13/hU9kkNBusJPkDjnX4b34TxuMICZSSyvccnXz",
    "did": "06e087c7-6c41-4f61-bb36-0f67jie8c390",
    "mobNo": "1234567890",
    "token": "/tmUqB08ffDHmHIuSfeVv9gUsN8=",
    "uid": "mVUzsG_pUijCS66hL0"
}
```

---
###### **NOTE:** The token and uid parameters will be different from request, so the response from verifyOtp on your system or server to fetch the HLS Streams.
 ---

#### Fetch HLS Stream

```
  POST https://axstream.vercel.app/getStream
```

| Parameter | Type     | Description                       |
| :-------- | :------- | :-------------------------------- |
| `id`      | `string` | **Required**. Content ID which you will get from URL - https://www.airtelxstream.in/movies/welcome/SHEMAROOME_MOVIE_5f20071fa609d206c800aa88 => Here "SHEMAROOME_MOVIE_5f20071fa609d206c800aa88" is the id. |
| `uid`      | `string` | **Required**. "uid" value which we got from verifyOtp response. |
| `token`      | `string` | **Required**. "token" value which we got from verifyOtp response. |
| `authToken`      | `string` | **Required**. "authToken" value which we got from verifyOtp response. |
| `did`      | `string` | **Required**. "did" value which we got from verifyOtp response. |


#### Fetch HLS Stream Code Sample in Javascript using Fetch

```
const formdata = new FormData();
formdata.append("id", "SHEMAROOME_MOVIE_5f20071fa609d206c800aa88");
formdata.append("uid", "mVUzsG_pUijCS66hL0");
formdata.append("token", "/tmUqB08ffDHmHIuSfeVv9gUsN8=");
formdata.append("authToken", "gK/qwuFRTkXqqduoSkw4iN+mv13/hU9kkNBusJPkDjnX4b34TxuMICZSSyvccnXz");
formdata.append("did", "06e087c7-6c41-4f61-bb36-0f67jie8c390");

const requestOptions = {
  method: "POST",
  body: formdata
};

fetch("https://axstream.vercel.app/getStream", requestOptions)
  .then((response) => response.text())
  .then((result) => console.log(result))
  .catch((error) => console.error(error));
```

```json
{
    "abr": {
        "default": "auto"
    },
    "contentId": "SHEMAROOME_MOVIE_5f20071fa609d206c800aa88",
    "contentType": "MOVIE",
    "cp": "SHEMAROOME",
    "deviceLimitExceeded": false,
    "playback": {
        "imaEnabled": false,
        "method": "GET",
        "playUrl": "https://d1kareb10k4vf4.cloudfront.net/shemaroo-vod/altplatform/63edc06a8530b80ace7ab621/main_playlist.m3u8",
        "sendQueryParams": false,
        "supportsDVR": false
    },
    "playbackType": "VOD",
    "plg": "hi",
    "requestId": "0.64987321-1725826083778",
    "subs": {
        "en": "https://d1hisuiegdphro.cloudfront.net/shemaroo-vod/altplatform/63edc06a8530b80ace7ab621/Welcome.srt"
    },
    "success": true
}
```


Made with ❤️ in India.
