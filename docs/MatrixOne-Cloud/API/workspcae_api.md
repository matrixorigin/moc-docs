# API

## 用户登录

### 获取 token

- 接口

```
POST /auth/login
```

- 输入参数
  
|  参数             | 是否必填 |含义|
|  --------------- | ------- |----  |
| account_name     | 是      | 工作区 ID｜
| username         | 是      | 管理员名称 |
| password         | 是      | 管理员密码 |

- 输出参数
  
|  参数             | 含义 |
|  --------------- | ----  |
| uid              |       |
| Access-Token     | 鉴权码，有效期 15 分钟     |
| Refresh-Token    | 用于 Access-Token 过期后刷新    |

**示例：**

```python
import requests
import json

url = "https://freetier-01.cn-hangzhou.cluster.cn-dev.matrixone.tech/auth/login"
# 设置请求头
headers = {
    "Accept": "application/json, text/plain, */*",
    "Content-Type": "application/json"
}
body = {
    "account_name": "0194dfaa-3eda-7ea5-b47c-b4f4f5940e97",
    "username": "admin:accountadmin",
    "password": "Mo123456!"
}

# 发送请求
response = requests.post(url, headers=headers, json=body)

# 打印响应头和内容（格式化 JSON）
print("Response Headers:", json.dumps(dict(response.headers), indent=4))
print("Response Body:", json.dumps(response.json(), indent=4, ensure_ascii=False))
```

返回示例：

```
Response Headers: {
    "Date": "Wed, 12 Feb 2025 03:38:36 GMT",
    "Content-Type": "application/json; charset=utf-8",
    "Content-Length": "178",
    "Connection": "keep-alive",
    "Access-Token": "eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1aWQiOiJmYTY0NjdhNi1iZmNiLTRkZjAtYWMzNi0wZThkYzU2YTEyNGEtMDE5NGRmYWEtM2VkYS03ZWE1LWI0N2MtYjRmNGY1OTQwZTk3OmFkbWluOmFjY291bnRhZG1pbiIsIm5hbWUiOiIwMTk0ZGZhYS0zZWRhLTdlYTUtYjQ3Yy1iNGY0ZjU5NDBlOTc6YWRtaW46YWNjb3VudGFkbWluIiwiZW1haWwiOiIiLCJsb2dpbl9tZXRob2QiOiIiLCJleHAiOjE3MzkzMzI0MTYsImlhdCI6MTczOTMzMTUxNiwiaXNzIjoibW9pIn0.YVA1ijl1IcdW3W2777oS52M3tyXzn4OSfP3TxHyR7d7h3E_w1AAIVNVkXNZ_G5Rv_4dEobGyaMGtTDUb1GPHjcO5q_5fAJYaQ_kxQ4mDa_ekJbX_F8oZn3v9LUjMUzHdylABcgFtUf7ew4C-0gSUcp8IXYK86ZW8V3kAr_cehKXD6eHj6-5Uw_5g7AdV7weRW7O6kFW2-ULR0MIc6kNfyP0r3_8NZVI6PRrDudhjI09Pc8B8vYV-Ahs5PXcVRDiuMY1_dbJfjxgK2GadF3IC8au9iDcTn1XH985ehck3hLol0_YZUIuYTgTXGGIRE5qWR1Qt2X2dpMQ4vP4F7Nt7zsvvq5GoPCfqC-aueu1vuT29RzuseUuIzHio-9jZwEgkh5Fm0A9nFu4oOAgWwSfLLuhBOJ-EQlDvBGIvqMRoH7039XsaQnjEBlXQRSnMzMDfxpTl93iMQKeN9D-UiOAHpCyBk0DU6MZowKMVWx_jhjpDUwT9lZXoFoio4e0ZSj2dfexPrQuvIQklIRRL-cgbMLCbvqo0ZGufuPNKiSdzY0M0JCDkWRaxK5Tki2VGK_TQyEi8hDk72JW6CavfwUsuaCFGVf9-T8q3GAnV8rmd_XDo_xRkeN5xXRTQZoF24ghS6QeEiqrtNT16vUdPdows2-5rI3NY_dfVpIeSKgYgGX0",
    "Refresh-Token": "eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1aWQiOiJmYTY0NjdhNi1iZmNiLTRkZjAtYWMzNi0wZThkYzU2YTEyNGEtMDE5NGRmYWEtM2VkYS03ZWE1LWI0N2MtYjRmNGY1OTQwZTk3OmFkbWluOmFjY291bnRhZG1pbiIsIm5hbWUiOiIwMTk0ZGZhYS0zZWRhLTdlYTUtYjQ3Yy1iNGY0ZjU5NDBlOTc6YWRtaW46YWNjb3VudGFkbWluIiwiZW1haWwiOiIiLCJsb2dpbl9tZXRob2QiOiIiLCJleHAiOjE3MzkzNTMxMTYsImlhdCI6MTczOTMzMTUxNiwiaXNzIjoibW9pIn0.lZRlH6AvgYTNGHNFCuxfvr-waVb47qCbh2QODo7LkKMA3Xe9zARV6ivYLFuhvRnXubQ8LLeGLKPlTMtx-KhNWx3EAp_wQc_UfJNR1XjXjE1M7X1nggG0hmMvCsqbhAIdcJYiIy27zdgpojUxxhRrjEplUbupGwJYzaRhju6Dg9ieU0S_c03qulpxSOfdoOayv4qgwgRpNiJXifKZASF479lS1XD_lk1RsxrYClib-r1YdXyzxFwZGg80oM39-82U5Zg5ZXO6XfCkJH_wpp1dmstujtWozEevBD3Ca7O8Ku09NRpdmPnyTxo7ShZe_5vk5jEBRvqduRKi-gZaOyH1JvRhjUzNrMcVfhf_KsuRuLs2Am5Q8LCEJqtch8NDYUFXmeJTBY34y8PEG1ZdCo8cvokhIvwrpCLCI9HqxapZqWlYalGMCKt580IHugnW84GO2hLApFF9IxoyJts0sFevv4ZSE1EvQQUnmT2HCZUvIZ5fzKCMNULPu0YpHPK_zjg8jF9w1bERFW770NO_LiPfafXQSbA6n9RP6BxwJ1P93ogzsyyxGgKglrF_sZ9WtVDAprzKrrSuanPhBlQzs8rV_BI0DgSANEouF_4hVOyjW3ouaxm9hMFS3xfI55MhN1mRM9hUnmlsXMZZ-_fY1Cw9apypivX6UmYpjm8UMeJudEI",
    "X-Request-Id": "e7d53eb7-80a2-4dc4-813f-8593aef9d9e1",
    "Set-Cookie": "SERVERID=d576c819bbc92dbf22dc5fdfd690d8a6|1739331516|1739331516;Path=/"
}
Response Body: {
    "code": "OK",
    "msg": "OK",
    "data": {
        "uid": "fa6467a6-bfcb-4df0-ac36-0e8dc56a124a-0194dfaa-3eda-7ea5-b47c-b4f4f5940e97:admin:accountadmin",
        "login_at": "2025-02-12T03:38:36.566638078Z"
    }
}
```

在 Response Header 中获取 access-token 和 refresh-token，从返回结构体中获取 uid。Access-Token 有效期 15min，过期之前，需要调用下面 Refresh 接口，获取新的 Access-Token。后续请求中，Header 中带上 Access-Token 和 uid。

### 刷新 token

在 Access-Token 过期之前，请求中带上 Access-Token，Refresh-Token 和 Uid，新的 Access-Token，Refresh-Token 会在 Response Header 中返回

```
POST auth/refresh
```

**示例：**

其中，accsee-token、refresh-token 和 uid 在**获取 token** 步骤返回。

```python
import requests
import json
# API URL
url = "https://freetier-01.cn-hangzhou.cluster.cn-dev.matrixone.tech/auth/refresh"

# 请求头
headers = {
    "Accept": "application/json, text/plain, */*",
    "Content-Type": "application/json",
    "Access-Token": "eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1aWQiOiJmYTY0NjdhNi1iZmNiLTRkZjAtYWMzNi0wZThkYzU2YTEyNGEtMDE5NGRmYWEtM2VkYS03ZWE1LWI0N2MtYjRmNGY1OTQwZTk3OmFkbWluOmFjY291bnRhZG1pbiIsIm5hbWUiOiIwMTk0ZGZhYS0zZWRhLTdlYTUtYjQ3Yy1iNGY0ZjU5NDBlOTc6YWRtaW46YWNjb3VudGFkbWluIiwiZW1haWwiOiIiLCJsb2dpbl9tZXRob2QiOiIiLCJleHAiOjE3MzkzMzI0MTYsImlhdCI6MTczOTMzMTUxNiwiaXNzIjoibW9pIn0.YVA1ijl1IcdW3W2777oS52M3tyXzn4OSfP3TxHyR7d7h3E_w1AAIVNVkXNZ_G5Rv_4dEobGyaMGtTDUb1GPHjcO5q_5fAJYaQ_kxQ4mDa_ekJbX_F8oZn3v9LUjMUzHdylABcgFtUf7ew4C-0gSUcp8IXYK86ZW8V3kAr_cehKXD6eHj6-5Uw_5g7AdV7weRW7O6kFW2-ULR0MIc6kNfyP0r3_8NZVI6PRrDudhjI09Pc8B8vYV-Ahs5PXcVRDiuMY1_dbJfjxgK2GadF3IC8au9iDcTn1XH985ehck3hLol0_YZUIuYTgTXGGIRE5qWR1Qt2X2dpMQ4vP4F7Nt7zsvvq5GoPCfqC-aueu1vuT29RzuseUuIzHio-9jZwEgkh5Fm0A9nFu4oOAgWwSfLLuhBOJ-EQlDvBGIvqMRoH7039XsaQnjEBlXQRSnMzMDfxpTl93iMQKeN9D-UiOAHpCyBk0DU6MZowKMVWx_jhjpDUwT9lZXoFoio4e0ZSj2dfexPrQuvIQklIRRL-cgbMLCbvqo0ZGufuPNKiSdzY0M0JCDkWRaxK5Tki2VGK_TQyEi8hDk72JW6CavfwUsuaCFGVf9-T8q3GAnV8rmd_XDo_xRkeN5xXRTQZoF24ghS6QeEiqrtNT16vUdPdows2-5rI3NY_dfVpIeSKgYgGX0",
    "Refresh-Token": "eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1aWQiOiJmYTY0NjdhNi1iZmNiLTRkZjAtYWMzNi0wZThkYzU2YTEyNGEtMDE5NGRmYWEtM2VkYS03ZWE1LWI0N2MtYjRmNGY1OTQwZTk3OmFkbWluOmFjY291bnRhZG1pbiIsIm5hbWUiOiIwMTk0ZGZhYS0zZWRhLTdlYTUtYjQ3Yy1iNGY0ZjU5NDBlOTc6YWRtaW46YWNjb3VudGFkbWluIiwiZW1haWwiOiIiLCJsb2dpbl9tZXRob2QiOiIiLCJleHAiOjE3MzkzNTMxMTYsImlhdCI6MTczOTMzMTUxNiwiaXNzIjoibW9pIn0.lZRlH6AvgYTNGHNFCuxfvr-waVb47qCbh2QODo7LkKMA3Xe9zARV6ivYLFuhvRnXubQ8LLeGLKPlTMtx-KhNWx3EAp_wQc_UfJNR1XjXjE1M7X1nggG0hmMvCsqbhAIdcJYiIy27zdgpojUxxhRrjEplUbupGwJYzaRhju6Dg9ieU0S_c03qulpxSOfdoOayv4qgwgRpNiJXifKZASF479lS1XD_lk1RsxrYClib-r1YdXyzxFwZGg80oM39-82U5Zg5ZXO6XfCkJH_wpp1dmstujtWozEevBD3Ca7O8Ku09NRpdmPnyTxo7ShZe_5vk5jEBRvqduRKi-gZaOyH1JvRhjUzNrMcVfhf_KsuRuLs2Am5Q8LCEJqtch8NDYUFXmeJTBY34y8PEG1ZdCo8cvokhIvwrpCLCI9HqxapZqWlYalGMCKt580IHugnW84GO2hLApFF9IxoyJts0sFevv4ZSE1EvQQUnmT2HCZUvIZ5fzKCMNULPu0YpHPK_zjg8jF9w1bERFW770NO_LiPfafXQSbA6n9RP6BxwJ1P93ogzsyyxGgKglrF_sZ9WtVDAprzKrrSuanPhBlQzs8rV_BI0DgSANEouF_4hVOyjW3ouaxm9hMFS3xfI55MhN1mRM9hUnmlsXMZZ-_fY1Cw9apypivX6UmYpjm8UMeJudEI",
    "uid": "fa6467a6-bfcb-4df0-ac36-0e8dc56a124a-0194dfaa-3eda-7ea5-b47c-b4f4f5940e97:admin:accountadmin"
}

# 请求体（Body JSON）
body = {
    "type": "user"
}

# 发送请求
response = requests.post(url, headers=headers, json=body)

# 打印响应头和内容（格式化 JSON）
print("Response Headers:", json.dumps(dict(response.headers), indent=4))
print("Response Body:", json.dumps(response.json(), indent=4, ensure_ascii=False))
```

返回示例：

```
Response Headers: {
    "Date": "Wed, 12 Feb 2025 03:40:45 GMT",
    "Content-Type": "application/json; charset=utf-8",
    "Content-Length": "24",
    "Connection": "keep-alive",
    "Access-Token": "eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1aWQiOiJmYTY0NjdhNi1iZmNiLTRkZjAtYWMzNi0wZThkYzU2YTEyNGEtMDE5NGRmYWEtM2VkYS03ZWE1LWI0N2MtYjRmNGY1OTQwZTk3OmFkbWluOmFjY291bnRhZG1pbiIsIm5hbWUiOiJiZmNiIiwiZW1haWwiOiIiLCJsb2dpbl9tZXRob2QiOiIiLCJleHAiOjE3MzkzMzI1NDQsImlhdCI6MTczOTMzMTY0NCwiaXNzIjoibW9pIn0.DFJLRxEMa9IDXZiMzCGTK634mr8OC7BKzv9n55cLLlAedFygPkuxkNtmViIK1DQn9PUU_76JSkyqszP0OhWWbYtMbv8inLF-lG6VGrsi8DcbX-uQj-zDqi5TqSd35cQQV4AagyXJlePWKyIJsN9rn_ivBbEki9DwgD2zEUx-MEBjRnyXzNxCJNeNAXRmyfHm-OFcuIptcdxmcKXvcP-88W4GNfci2xPChrUV-rkQZyfWosixEaYCbIq8kC2EhpqzeBH1JpP6WuW9wTlMR-20jca4P8UeBf1BfBpdYBJxkmqUmBCojL8BtqWMQMO1EhKpYGoyb7IRoiRQM7c0Ep9ZJjoZ7LxVMdjOLh6v4ZAfW57kQapwD7k49Wf8TQ5V_OhAXcvvbn0q3myMmM4msjtTPs49UwP67p5BpqDJ_YR7z5Y5KiRGZOTYNjDstHDX1alZrQp8V_N5exBTz57YXtDoQaswkqWCw10wr_PiwYL7KubxTUGq46KLTGLG-UOa-DTBl2HFYiMhw3X9Y1k3ZEDohbLycaeVMTdYV0kaFFVMU6AsD68pjB09JL3eFtDeUkE02v6KdWtDEDhSh_I5tpo7tzYKHdxuFKn5Ff99woDEhtR-H1oPBvbwDYOmio-h_nrMIQC5-uRaMFwRzi-P8AIcb_EAhvVDajMwx-AmbBT6pFs",
    "Refresh-Token": "eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1aWQiOiJmYTY0NjdhNi1iZmNiLTRkZjAtYWMzNi0wZThkYzU2YTEyNGEtMDE5NGRmYWEtM2VkYS03ZWE1LWI0N2MtYjRmNGY1OTQwZTk3OmFkbWluOmFjY291bnRhZG1pbiIsIm5hbWUiOiIwMTk0ZGZhYS0zZWRhLTdlYTUtYjQ3Yy1iNGY0ZjU5NDBlOTc6YWRtaW46YWNjb3VudGFkbWluIiwiZW1haWwiOiIiLCJsb2dpbl9tZXRob2QiOiIiLCJleHAiOjE3MzkzNTMxMTYsImlhdCI6MTczOTMzMTUxNiwiaXNzIjoibW9pIn0.lZRlH6AvgYTNGHNFCuxfvr-waVb47qCbh2QODo7LkKMA3Xe9zARV6ivYLFuhvRnXubQ8LLeGLKPlTMtx-KhNWx3EAp_wQc_UfJNR1XjXjE1M7X1nggG0hmMvCsqbhAIdcJYiIy27zdgpojUxxhRrjEplUbupGwJYzaRhju6Dg9ieU0S_c03qulpxSOfdoOayv4qgwgRpNiJXifKZASF479lS1XD_lk1RsxrYClib-r1YdXyzxFwZGg80oM39-82U5Zg5ZXO6XfCkJH_wpp1dmstujtWozEevBD3Ca7O8Ku09NRpdmPnyTxo7ShZe_5vk5jEBRvqduRKi-gZaOyH1JvRhjUzNrMcVfhf_KsuRuLs2Am5Q8LCEJqtch8NDYUFXmeJTBY34y8PEG1ZdCo8cvokhIvwrpCLCI9HqxapZqWlYalGMCKt580IHugnW84GO2hLApFF9IxoyJts0sFevv4ZSE1EvQQUnmT2HCZUvIZ5fzKCMNULPu0YpHPK_zjg8jF9w1bERFW770NO_LiPfafXQSbA6n9RP6BxwJ1P93ogzsyyxGgKglrF_sZ9WtVDAprzKrrSuanPhBlQzs8rV_BI0DgSANEouF_4hVOyjW3ouaxm9hMFS3xfI55MhN1mRM9hUnmlsXMZZ-_fY1Cw9apypivX6UmYpjm8UMeJudEI",
    "X-Request-Id": "82897e92-d37d-48fe-8b05-581705987651",
    "Set-Cookie": "SERVERID=39529de3c161baaf8e06ec55d8dc5e95|1739331644|1739331644;Path=/"
}
Response Body: {
    "code": "OK",
    "msg": "OK"
}
```

## 数据接入

### 连接器

#### 创建连接器

```
POST /conectors
```
  
**输入参数：**
  
|  参数             | 是否必填 |含义|
|  --------------- | ------- |----  |
| name             | 是      | 连接器名称｜
| source_type      | 是      | 连接器类型，4 为 OSS，5 为标准 S3 |
| config           | 是      | 配置 oss 和 s3 的连接信息，如果是 oss 需填写 endpoint、access_key_id、access_key_secret、bucket_name，如果是 s3 除了 oss 中的参数还需填写 region 和信息。 |

**示例：**

```python
import requests

# API URL
url = "https://freetier-01.cn-hangzhou.cluster.cn-dev.matrixone.tech/connectors"  # 请替换为实际 API 地址
# 请求头（如果需要，可以根据需要添加 Authorization 或其他头部）
headers = {
    "user-id":"0194dfaa-3eda-7ea5-b47c-b4f4f5940e97",
    "Access-Token": "eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1aWQiOiI5MWEyMjM0ZS0wYTA2LTRkODQtODE1ZS04NDBlMzc5ZDllMWMtMDE5NGRmYWEtM2VkYS03ZWE1LWI0N2MtYjRmNGY1OTQwZTk3OmFkbWluOmFjY291bnRhZG1pbiIsIm5hbWUiOiIwMTk0ZGZhYS0zZWRhLTdlYTUtYjQ3Yy1iNGY0ZjU5NDBlOTc6YWRtaW46YWNjb3VudGFkbWluIiwiZW1haWwiOiIiLCJsb2dpbl9tZXRob2QiOiIiLCJleHAiOjE3MzkzMjcwNjcsImlhdCI6MTczOTMyNjE2NywiaXNzIjoibW9pIn0.uCRKFQkfQTTWPYi_cKlQk1YbosZUjLNSpeoHGXlW0xqakECyP43A85f1Hop9MQJKTaSZakDofocJCHrtAeOMDxNe_jbK0jUaFUJq4WLCKvwuhE8TalRJ-3bfUCPkUkTWgIu47e_8EFB1-KBzsutbTZOBGGPslK8vY4AK-shEnkbubweRKRJMh1BsuuPRdQrke9h4lXMP7SvV3OM5okBEc7QstJ0oNLzxJ0Y4wdVDmV5LpOtYEwV8dB1F6FQp6mfn8prgK7lVNUWECd2-6ImZ2BJh1LKyRu_4v_MSsRWP_2LrrPJJsEO6lrC5n0L28BCwzVravhjlvmx5M2V3pSbP0DLfqTAv4NmcVg2EIVuBH3eHKYeG-D3-Fh_1SSoNUPm_5B1mgKySna6ldwj2W-0OAv_meBy0tt7J_Yt7V7AyKcCy55C1TIDqgMj9coov61rduRZ4_1c6eaml_PRD_4sv2TDDZ2rJKZnI76ZYbYBNZDpcVm2EjUODWIaCq1dPji9ukUVU9gLL58nmJQ3gJH4MzQaFU5aUrOBL3gT10uF4KnJRapn1cIe0yMmdITS9E6MJhIo73i5qhI1v1CXeqKuRsZmjXhal60irOi-Vz61MvEQ4Fx6c9NGhPXwn-OvygMhyKASc4eyhEOKxs7TMOOqFaXWuLPE3u0Uq4myLUHIxt8o",
    "uid": "91a2234e-0a06-4d84-815e-840e379d9e1c-0194dfaa-3eda-7ea5-b47c-b4f4f5940e97:admin:accountadmin"
}

# 请求体（Body）
body = {
    "name": "oss-test2",  # 连接器名称
    "source_type": 4,  # 4 为 OSS 源，5 为 S3 源
    "config": {
        "oss": {  # 如果 source_type 为 4，填此字段
            "endpoint": "oss-cn-beijing.aliyuncs.com",
            "access_key_id": "xxxx",
            "access_key_secret": "xxxx",
            "bucket_name": "yj-bucket1"
        }
    }
}

# 发送 POST 请求
response = requests.post(url, json=body, headers=headers)

# 检查响应状态
if response.status_code == 200:
    print(response.json())  # 打印返回的 JSON 数据
else:
    print(f"请求失败，状态码：{response.status_code}, 错误信息：{response.text}")
```

返回示例：

```
{'code': 'OK', 'msg': 'OK'}
```

#### 验证连接器

```
POST /connectors/validate
```

**输入参数：**
  
|  参数             | 是否必填 |含义|
|  --------------- | ------- |----  |
| source_type      | 是      | 连接器类型，4 为 OSS，5 为标准 S3 ｜
| connector_id     | 否      | 填写 connector_id 则无需填写 config 信息。|
| config           | 否      | 填写 config 则无需填写 connector_id 信息配置 oss 和 s3 的连接信息，如果是 oss 需填写 endpoint、access_key_id、access_key_secret、bucket_name，如果是 s3 除了 oss 中的参数还需填写 region 信息。 |

**示例：**

```python
import requests

# API URL
url = "https://freetier-01.cn-hangzhou.cluster.cn-dev.matrixone.tech/connectors/validate"  # 请替换为实际 API 地址
# 请求头（如果需要，可以根据需要添加 Authorization 或其他头部）
headers = {
    "user-id":"0194dfaa-3eda-7ea5-b47c-b4f4f5940e97",
    "Access-Token": "eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1aWQiOiIyYzVhN2RjNC0wMzJhLTQyYWMtYjVhZC00ZGI0N2YxMTc3MmItMDE5NGRmYWEtM2VkYS03ZWE1LWI0N2MtYjRmNGY1OTQwZTk3OmFkbWluOmFjY291bnRhZG1pbiIsIm5hbWUiOiIwMTk0ZGZhYS0zZWRhLTdlYTUtYjQ3Yy1iNGY0ZjU5NDBlOTc6YWRtaW46YWNjb3VudGFkbWluIiwiZW1haWwiOiIiLCJsb2dpbl9tZXRob2QiOiIiLCJleHAiOjE3MzkzMzAwNDIsImlhdCI6MTczOTMyOTE0MiwiaXNzIjoibW9pIn0.A33GT6nykw4378PvaSSKYTfYiKWUY34gx6MIMIElKRHy-nvMssX4zTQcny0HneS06984WnoAytAjVlBDOY-BC_x0OzcwmAfgzM2zbhrb9LEfTvBM07rD2ZSRpmmgGBp2y7eR-wGCzVs7UzwlSNY8ZXqzejbdnbRj6cUZbQafcXtOlAPC6cUjITf0Wkgv0K30L3O5wxQR2ONQQpApgodmaYIdQZ4EZq_fgDObNonazQgim7tO_Lhb4bmYlGYc1Isnb7sdbhMos9UmwFlwE6pwAi8IXqkgOYP7R8w6OhrA8CmNZva0J-uW-X-dR2BILTCAArkhEV8yHMBuOJxHNnSkpDcOFHXMBEjzY3VNh2RTrX-bC9aGr24dFDjTICO_z6g-MfFcAceybwlFTjDEeS6T14JyQt1WbAmM4L9GZKcXvUR59sgFsnbRK0V658JUxTbqU0QVzHMFX-WOGL2BKro76nbM4N5NMWw_Q-4TXAXV-NMKBeMohz6XwgN4FilYE2MJws-3tXDn6rzIDUATr35h_eNX-oGlIOlEVh6g_AhaLeTDa0w0_VMcitngPxrrP06y9u1EGE5jYKuqdbVGP8KMfc_ahOxi46-IYMFSxzCNi4R3sOogpFqiWNRjpyojvTlAx4n8pbqoaFZw_aUyyvgbcxamkKwu_345Y9XfHmDFmgs",
    "uid": "2c5a7dc4-032a-42ac-b5ad-4db47f11772b-0194dfaa-3eda-7ea5-b47c-b4f4f5940e97:admin:accountadmin"
}

# 请求体（Body）
body = {
    "source_type": 4,
    "config": {
        "oss": {
            "endpoint": "oss-cn-beijing.aliyuncs.com",
            "access_key_id": "xxxx",
            "access_key_secret": "xxxx",
            "bucket_name": "yj-bucket1"
        }
    }
}

# 发送 POST 请求
response = requests.post(url, json=body, headers=headers)

# 检查响应状态
if response.status_code == 200:
    print(response.json())  # 打印返回的 JSON 数据
else:
    print(f"请求失败，状态码：{response.status_code}, 错误信息：{response.text}")
```

返回示例：

```
{'code': 'OK', 'msg': 'OK', 'data': {'valid': True}}
```

#### 查询连接器

```
GET /connectors/list
```

**输出参数：**
  
|  参数             | 含义 |
|  --------------- | ----  |
| id               |connector-id       |
| source_type      | 连接器类型，4 为 OSS，5 为标准 S3     |
| name             | 连接器名称    |
| status           | 连接状态    |
| created_at       | 创建时间    |
| updated_at       | 更新时间    |
| username         | 创建人    |
| updated_at       | 更新时间    |
| username         | 创建人    |
| related_task_ids | 关联的 TaskID   |
| config           | 连接器配置信息    |
| total            | 返回数目    |

**示例：**

```python
import requests
import json
# API URL
url = "https://freetier-01.cn-hangzhou.cluster.cn-dev.matrixone.tech/connectors/list"  # 请替换为实际 API 地址
# 请求头（如果需要，可以根据需要添加 Authorization 或其他头部）
headers = {
    "user-id":"0194dfaa-3eda-7ea5-b47c-b4f4f5940e97",
    "Access-Token": "eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1aWQiOiJmNDJkMTAwNi1iNDhmLTRiMWQtYmQ0NC0zYTE4ZGQ3YmI4ZWMtMDE5NGRmYWEtM2VkYS03ZWE1LWI0N2MtYjRmNGY1OTQwZTk3OmFkbWluOmFjY291bnRhZG1pbiIsIm5hbWUiOiIwMTk0ZGZhYS0zZWRhLTdlYTUtYjQ3Yy1iNGY0ZjU5NDBlOTc6YWRtaW46YWNjb3VudGFkbWluIiwiZW1haWwiOiIiLCJsb2dpbl9tZXRob2QiOiIiLCJleHAiOjE3MzkzMzI1OTksImlhdCI6MTczOTMzMTY5OSwiaXNzIjoibW9pIn0.fqI9Cmrx4xSBWmSIuzCIDkFjGmBZ2_G32LXn62stm_i5Rw838Ij0PP4iewglP7s-vmeKdzQrgPOz4k6nCaR2sgDRktalggJWdn8C6DRW43MCe-UN8K2CfD6XjT-PuT2VNHu0gzblyTURPtBNuxSHV6JmfDYWHCl5zAtthXgLOSJPPMnC7swCuYeaHtqdDaPljUClnTmmb553Ot1uIgpxdE67rhFHBDJ1RsDNd61WD-y4DLvumWOc8Kxql1tnopNl2oH2hs4g3Xb_C3tubjpDElK2-biMaswO2LvX8yu8ItqXovFQIeve7QWqXLa0tGmBStkDJ7i1psK2MNkf29ZRQS61OL2il9fum3Vbw2YXjZcET6TQVciqkgAaJUTBivY0zMAAbFwgbHTJyRbNIBlZ0Ze29hZUtbTWkOY8cD7UJHGxtGnoiuMhs9ow9krBUzrVHIliipr7CBMORh7i2dpQTNqAwgselcExcXqewgbiKSgnUIWpdhiylXEJbJ8s19WTXWWwQBYhaNe-2w2ZX34twi_utxAAfkALNZBWRTIZdJu65Jffjqv6pLN-JoriTmbNCyIAGQ6V95YxAb09QRSNtRZameBYWacf-4DMplsjHKueSoa4QYCNCU9pf_0Wpjoe1gIbaDp-b_ZOox_mzUXDofH7Yg2hja6P7wAIhSjj17c",
    "uid": "f42d1006-b48f-4b1d-bd44-3a18dd7bb8ec-0194dfaa-3eda-7ea5-b47c-b4f4f5940e97:admin:accountadmin"
}


response = requests.get(url, headers=headers)

print("Response Body:", json.dumps(response.json(), indent=4, ensure_ascii=False))
```

返回示例：

```bash
Response Body: {
    "code": "OK",
    "msg": "OK",
    "data": {
        "connectors": [
            {
                "id": 100004,
                "source_type": 4,
                "name": "oss-test1",
                "status": "active",
                "created_at": 1738919558,
                "updated_at": 1738919558,
                "username": "admin",
                "related_task_ids": [
                    1889223922712281088
                ],
                "config": {
                    "oss": {
                        "endpoint": "oss-cn-beijing.aliyuncs.com",
                        "access_key_id": "xxxx",
                        "access_key_secret": "xxxx",
                        "bucket_name": "yj-bucket1"
                    }
                }
            },
            {
                "id": 100005,
                "source_type": 5,
                "name": "s3-test",
                "status": "active",
                "created_at": 1738919761,
                "updated_at": 1738919761,
                "username": "admin",
                "related_task_ids": null,
                "config": {
                    "s3": {
                        "endpoint": "http://s3.us-west-2.amazonaws.com",
                        "access_key_id": "xxxx",
                        "access_key_secret": "xxxx",
                        "bucket_name": "test-bucket0121",
                        "region": "us-west-2"
                    }
                }
            }
        ],
        "total": 2
    }
}
```

#### 更新连接器

```
PUT /connectors/{id}
```

**输入参数：**
  
|  参数             | 是否必填 |含义|
|  --------------- | ------- |----  |
| name             | 是      | 连接器名称 ｜
| config           | 是      | 连接器配置信息 |

```
{
    "name": "new_connector_name",
    "config": {
        "oss": {
            "endpoint": "new_oss_endpoint",
            "access_key_id": "new_access_key_id",
            "access_key_secret": "new_access_key_secret",
            "bucket_name": "new_bucket_name"
        },
        "s3": {
            "endpoint": "new_s3_endpoint",
            "access_key_id": "new_access_key_id",
            "access_key_secret": "new_access_key_secret",
            "bucket_name": "new_bucket_name",
            "region": "new_region",
            "session_token": "new_session_token"
        }
    }
}
```

**示例：**

```python
import requests
import json
# API URL
url = "https://freetier-01.cn-hangzhou.cluster.cn-dev.matrixone.tech/connectors/100005"  # 请替换为实际 API 地址
# 请求头（如果需要，可以根据需要添加 Authorization 或其他头部）
headers = {
    "user-id":"0194dfaa-3eda-7ea5-b47c-b4f4f5940e97",
    "Access-Token": "eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1aWQiOiJmNDJkMTAwNi1iNDhmLTRiMWQtYmQ0NC0zYTE4ZGQ3YmI4ZWMtMDE5NGRmYWEtM2VkYS03ZWE1LWI0N2MtYjRmNGY1OTQwZTk3OmFkbWluOmFjY291bnRhZG1pbiIsIm5hbWUiOiIwMTk0ZGZhYS0zZWRhLTdlYTUtYjQ3Yy1iNGY0ZjU5NDBlOTc6YWRtaW46YWNjb3VudGFkbWluIiwiZW1haWwiOiIiLCJsb2dpbl9tZXRob2QiOiIiLCJleHAiOjE3MzkzMzI1OTksImlhdCI6MTczOTMzMTY5OSwiaXNzIjoibW9pIn0.fqI9Cmrx4xSBWmSIuzCIDkFjGmBZ2_G32LXn62stm_i5Rw838Ij0PP4iewglP7s-vmeKdzQrgPOz4k6nCaR2sgDRktalggJWdn8C6DRW43MCe-UN8K2CfD6XjT-PuT2VNHu0gzblyTURPtBNuxSHV6JmfDYWHCl5zAtthXgLOSJPPMnC7swCuYeaHtqdDaPljUClnTmmb553Ot1uIgpxdE67rhFHBDJ1RsDNd61WD-y4DLvumWOc8Kxql1tnopNl2oH2hs4g3Xb_C3tubjpDElK2-biMaswO2LvX8yu8ItqXovFQIeve7QWqXLa0tGmBStkDJ7i1psK2MNkf29ZRQS61OL2il9fum3Vbw2YXjZcET6TQVciqkgAaJUTBivY0zMAAbFwgbHTJyRbNIBlZ0Ze29hZUtbTWkOY8cD7UJHGxtGnoiuMhs9ow9krBUzrVHIliipr7CBMORh7i2dpQTNqAwgselcExcXqewgbiKSgnUIWpdhiylXEJbJ8s19WTXWWwQBYhaNe-2w2ZX34twi_utxAAfkALNZBWRTIZdJu65Jffjqv6pLN-JoriTmbNCyIAGQ6V95YxAb09QRSNtRZameBYWacf-4DMplsjHKueSoa4QYCNCU9pf_0Wpjoe1gIbaDp-b_ZOox_mzUXDofH7Yg2hja6P7wAIhSjj17c",
    "uid": "f42d1006-b48f-4b1d-bd44-3a18dd7bb8ec-0194dfaa-3eda-7ea5-b47c-b4f4f5940e97:admin:accountadmin"
}

# 请求体（Body）
body = {
    "name": "s3-test1",  # 连接器名称
    "config": {
                    "s3": {
                        "endpoint": "http://s3.us-west-2.amazonaws.com",
                        "access_key_id": "xxxx",
                        "access_key_secret": "<YOUR_access_key_secret>",
                        "bucket_name": "test-bucket0121",
                        "region": "us-west-2"
                    }

}
}

# 发送 POST 请求
response = requests.put(url, json=body, headers=headers)

if response.status_code == 200:
    print(response.json())  # 打印返回的 JSON 数据
else:
    print(f"请求失败，状态码：{response.status_code}, 错误信息：{response.text}")
```

- 根据实际连接器决定使用哪个配置

#### 查询连接器源文件

```
GET /connectors/files/list
```

```
{
    "connector_id": 123456,
    "cursor": "",
    "limit": 10,
    "file_types": [
        1,
        2,
        3
    ]
}
```

- file_types 表示文件类型，枚举如下：

|  对应枚举值   | 含义 |
|  ----------- | ----  |
| 0            | 空文件类型（可能作为默认或无效值）|
| 1            | TXT 文本文件类型|
| 2            | PDF 文档文件类型|
| 3            | 图片文件类型|
| 4            | PPT 演示文稿文件类型|
| 5            | Word 文档文件类型|
| 6            | Markdown 标记语言文件类型|
| 7            | CSV 逗号分隔值文件类型|
| 8            | Parquet 列式存储文件类型|
| 9            | SQL 文件类型|
| 10           | 目录类型|

- 通过 cursor 和 has_more 的方式进行分页 (has_more 在返回中)，默认第一次传 cursor 为空串，后续根据返回的 cursor 在请求中带上来即可。当 has_more 为 true 时代表还有新数据，false 为没有。
  
### 数据载入

#### 创建载入任务

```
POST /task
```

**请求：**

```
{
  "source_connector_id": 160002,
  "volume_id": "1888787475678015488",
  "source_config": {
    "common_file_task_config": {
      "load_mode_config": {
        "load_interval_type": 2,
        "interval": 60
      },
      "uris": [
        "data_parse/"
      ]
    }
  },
  "config_type": 1
}
```

- volume_id 为目标卷 ID，load_mode_config 为载入模式配置，interval 为载入周期，load_interval_type 表示载入周期单位和类型，如下：

|  对应枚举值   | 含义 |
|  ----------- | ----  |
| 0            | 未知的加载间隔类型，可作为默认的无效值）|
| 1            | 按天进行加载，可能表示每天固定时间加载|
| 2            | 按小时进行加载，可能表示每小时的某个固定时间加载|
| 3            | 按分钟进行加载，可能表示每分钟的某个固定时刻加载|
| 4            | 默认类型，仅加载一次|

- config_type 默认传 1
- source_config 为载入任务源配置，common_file_task_config 为通用文件配置
- source_connector_id：源连接器
- uris 表示需要载入的文件或文件夹 URI 列表

#### 载入任务列表

```
GET /task/list
```

```
/task/list?is_desc=false&load_interval_types=4&load_interval_types=3&load_interval_types=2&load_interval_types=1&order_by=end_at&page=1&page_size=10&status=1&status=2&status=3&status=4
```

- is_desc 和 order_by 用于排序，order_by 取值为 end_at、created_at 和 updated_at
- status 为载入任务状态过滤，取值如下：

|  对应枚举值   | 含义 |
|  ----------- | ----  |
| 0            | 未知状态|
| 1            | 正常执行中或可执行状态|
| 2            | 正在暂停状态|
| 3            | 已暂停状态|
| 4            | 已完成状态|

- load_interval_types 为载入间隔类型，取值如下：
  
|  对应枚举值   | 含义 |
|  ----------- | ----  |
| 0            | 未知间隔类型|
| 1            | 按天间隔|
| 2            | 按小时间隔|
| 3            | 按分钟间隔|
| 4            | 仅执行一次（默认）|

#### 载入任务更新

```
POST /task/update
```

**请求：**

```
{
  "task_id": "1234567890",
  "load_mode_config": {
    "load_interval_type": 1,
    "interval": 24
  },
  "uris": [
    "/DataParse/OBJ"
  ]
}
```

- task_id：载入任务 ID
- load_mode_config：同上。
- uris：同上

#### 载入任务删除

```
POST /task/delete
```

**请求：**

```
{
  "task_id": "1234567890"
}
```

#### 载入任务暂停

```
POST /task/pause
```

**请求：**

```
{
  "task_id": "1234567890"
}
```

#### 载入任务恢复

```
POST /task/resume
```

**请求：**

```
{
  "task_id": "1234567890"
}
```

#### 载入任务重试

```
POST /task/retry
```

**请求：**

```
{
  "task_id": "1234567890",
  "ids": ["id1", "id2", "id3"]
}
```

#### 载入任务获取

```
GET /task/get
```

**请求：**

```
/task/get?task_id=1888896244014280704
```

#### 获取载入任务下的文件

```
GET /task/files
```

**请求：**

```
/task/files?task_id=1888896244014280704&status=1&status=2&page=1&page_size=10
```

- status 取值如下：

|  对应枚举值   | 含义 |
|  ----------- | ----  |
| 0            | 状态未知或未定义|
| 1            | 等待中|
| 2            | 正在上传|
| 3            | 已暂停|
| 4            | 失败|
| 5            | 成功|
| 6            | 正在重试|

## 数据处理

### 工作流

#### 创建工作流

```
POST /byoa/api/v1/index_workflow
```

#### 查看工作流详情

```
/byoa/docs#/index_workflow/get_workflow_detail_byoa_api_v1_index_workflow__workflow_id__get
```

#### 查看工作流列表

```
/byoa/docs#/index_workflow/list_jobs_byoa_api_v1_index_workflow_get
```

#### 修改工作流

```
/byoa/docs#/index_workflow/update_workflow_byoa_api_v1_index_workflow__workflow_id__put
```

#### 删除工作流

```
/byoa/docs#/index_workflow/update_workflow_byoa_api_v1_index_workflow__workflow_id__put
```

### 作业

#### 查看作业详情

```
/byoa/docs#/index_workflow_job/get_job_detail_byoa_api_v1_index_workflow_job__job_id__get
```

#### 查看作业列表

```
/byoa/docs#/index_workflow_job/list_jobs_byoa_api_v1_index_workflow_job_get
```

#### 查看作业文件列表

```
/byoa/docs#/index_workflow_job/get_job_files_byoa_api_v1_index_workflow_job__job_id__files_get
```

#### 重新处理失败文件

```
/byoa/docs#/index_workflow_job/retry_job_files_byoa_api_v1_index_workflow_job__job_id__files_post
```

### 数据探索

#### 查看原始数据卷列表

#### 创建原始数据卷

#### 查看某个原始数据卷（文件列表）

#### 下载某个原始数据卷中的文件

#### 删除某个原始数据卷中的某个文件

#### 查看处理数据卷列表

#### 创建处理数据卷

#### 查看某个处理数据卷（文件列表）

#### 下载某个处理数据卷中的某个文件

#### 查看某个处理数据卷中的某个文件（解析内容）

#### 删除某个处理数据卷中的某个文件的分段

### 指标查看

<http://ob-service.mo-ob/ob/metrics>

示例：

```bash
curl --location --request POST 'http://xxxxxx/ob/metrics' \
--header 'Content-Type: application/json' \
--data-raw '{
  "account": "account_name",
  "start": "2025-02-10T03:08:24+08:00",
  "end": "2025-02-10T11:40:24+08:00",
  "interval": 60,
  "metrics": [
    {
      "name": "PipelineProcessFinishJobCount"
    }
  ]
}'
```

- 用户 id：account name
- 指标名 (可以填写多个)：metrics[x]. name
- 统计开始时间 (RFC3339)：start
- 统计结束时间 (RFC3339)：end
- 时间间隔 (int，秒数)：interval

#### 数据载入

|  指标名称     | 指标名参数                     | 含义               |
| ------------ | ---------------------------- |------------------- |
| 文件完成数量   | PipelineLoadFileCount        |一段时间内成功载入的文件数 |
| 文件载入大小   | PipelineLoadFileSize         |一段时间内成功载入的文件总大小|
| 文件载入延迟   | PipelineLoadFileLatency      |一段时间内每个文件从开始载入到载入成功的平均时间 |
| 文件载入吞吐量 | PipelineLoadFileThroughput   |单位时间内成功载入的数据量（字节/s） |
| 每秒载入文件数 | PipelineLoadFilePerSecond    |单位时间内成功处理的文件数（文件数/s）|
| 文件成功率    | PipelineLoadFileSuccessRate   |一段时间内文件载入的成功率|

### 数据处理

|  指标名称     | 指标名参数                             | 含义               |
| ------------ | -----------------------------------  |------------------- |
| 作业完成数量   | PipelineProcessFinishJobCount        |一段时间内执行处理作业数量|
| 作业处理延迟   | PipelineProcessFinishJobLatency      |一段时间内执行处理作业平均耗时 |
| 工作流成功率   | PipelineProcessWorkflowSuccessRate   |一段时间内工作流执行处理作业的成功率 |
| 工作流超时率   |PipelineProcessWorkflowTimeoutRate    |一段时间内工作流执行处理作业的超时率|