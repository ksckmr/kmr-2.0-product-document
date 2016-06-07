## 通用请求

 **[1. 服务信息](#fu_wu_xin_xi)**
 
 **[2. 公共参数](#gong_gong_can_shu)**
 
 **[3. 签名机制](#qian_ming_ji_zhi)**
 
 **[4. 通用错误信息](#tong_yong_cuo_wu_xin_xi)**

<h3 name="fu_wu_xin_xi" id="fu_wu_xin_xi">1.服务信息</h3>


---



* 服务地址
 
　　金山云KMR服务接入地址：
  
 　　•　北京地区：kmr.cn-beijing-6.api.ksyun.com <br/>
 　　•　上海地区：kmr.cn-shanghai-2.ksyun.com

* 通讯协议

　　只支持通过HTTP协议进行通信。

* 请求方法

　　支持HTTP POST方法发送请求。

* 请求参数

　　每个请求都需要指定要执行的操作，即X-Action参数（例如ListClusters），以及每个操作都需要包含的公共请求参数和指定操作所特有的请求参数。

* 编码方式

　　请求及返回结果都使用UTF-8字符集进行编码。

* 返回结果

　　仅支持json格式的返回结果。


<h3 name="gong_gong_can_shu" id="gong_gong_can_shu">2.公共参数</h3>


---



| 名称 | 描述 | 是否必须 |
| -- | -- | -- |
| Host | KMR服务的Host name | 是 |
| Authorization | 授权参数 | 是 |
| Content-Type | 数据结构类型（application/json） | 是 |
| X-Action | 请求的目标操作，例如：ListClusters | 是 |
| X-Version | 请求的目标操作，例如：2016-05-20 | 是 |
| X-Ksc-Content-Sha256 | Sha256哈希值，用于计算签名 | 否 |
| X-Ksc-Date | 请求发出的时间，格式：<br>yyyyMMdd'T'HHmmss'Z'  | 是 |


<h3 name="qian_ming_ji_zhi" id="qian_ming_ji_zhi">3.签名机制</h3>


---



　　发送给KMR服务的HTTP请求中，必须包含授权参数和其他公共参数。KMR服务使用用户的Access Key ID和Secret Access Key进行加密方式来验证请求者的身份。Access Key ID和Secret Access Key由金山云发给用户，Access Key ID作为用户的身份标识，Secret Access Key作为用户和服务器端进行签名计算的密钥。

　　Http请求header中 Authorization字段是服务的授权参数，其格式为：

```
Authorization="[HashMethod][空格]Credential=[access_key]/[scope],SignedHeaders=[signed_headers],Signature=[signature]"
```
　　其中：
  
　　[HashMethod] ="KSC4-HMAC-SHA256"<br>
　　[access_key] =用户Access key ID<br>
　　[scope] = [timestamp]/[region]/[service][req_type]<br>
　　timestamp为yyyyMMdd格式的时间戳，region为请求服务所在区域名，service为访问的服务名，req_type为请求的类型。<br>
　　[signed_headers]：将Headers按照name升序排列<br>
　　[signed_headers] = [header_name_1];[header_name_2]....

　　签名算法：

```
[signature]= sha256(sha256(sha256(sha256(sha256("KSC4"+sign_key,timestamp),region),service),req_type),string_to_sign)
```

　　其中：

　　[sign_key] =用户Secret Access Key<br>
　　[stringToSign] = "KSC4-HMAC-SHA256" + "\n"<br>
　　　 　　+ [X-Ksc-Date] + "\n"<br>
　　　 　　+[scope] + “\n”<br>
　　　　　 + SHA-256([canonical_request])<br>
　　[canonical_request] = [HTTPRequestMethod] + "\n"<br>
　　　　　 + [CanonicalURI] + "\n"<br>
　　　　　 + [CanonicalQueryString] + "\n"<br>
　　　　　 + [CanonicalHeaders] + "\n"<br>
　　　　　 + [signed_headers] + "\n"<br>
　　　　　 + SHA-256([request_body])<br>
　　[HTTPRequestMethod] = POST或GET<br>
　　[CanonicalURI] = 请求URL中除去Endpoint之外的剩余部分。目前URL等于Endpoint，所以CanonicalURI为空<br>
　　[CanonicalQueryString] = 空<br>
　　[CanonicalHeaders]：按照[signed_headers]中的排序方式进行排序<br>
　　[CanonicalHeaders] =<br>
　　　　　　LowerCase (HeaderName1) + ‘:’ + Trim (HeaderValue1) + "\n"<br>
     　　　+LowerCase (HeaderName2) + ‘:’ + Trim (HeaderValue2) + "\n"<br>
　　　　　　+.......<br>
　　[request_body] = Post 请求的body部分<br>
　　

　　Python版签名代码示例：

```
def canonical_request(self, http_request, sign_headers):
        cr = []
        cr.append(http_request.method.upper())
        cr.append(self.canonical_uri(http_request))
        cr.append(self.canonical_query_string(http_request))
        headers_to_sign = self.headers_to_sign(http_request, sign_headers)
        cr.append(self.canonical_headers(headers_to_sign) + '\n')
        cr.append(self.signed_headers(headers_to_sign))
        if self.header_name_content_sha256 in http_request.headers:
            content_hash = self._ensure_bytes(http_request.headers[self.header_name_content_sha256])
            cr.append(content_hash)
        else:
            cr.append(self.payload(http_request))
        return '\n'.join(cr)

def string_to_sign(self, http_request, canonical_request, scope):
        sts = [self.hash_method]
        sts.append(http_request.headers[self.header_name_date])
        sts.append(scope)
        sts.append(sha256(canonical_request.encode('utf-8')).hexdigest())
        return '\n'.join(sts)

def _sign(self, key, msg, hex=False):
        key = self._ensure_bytes(key)
        if hex:
            sig = hmac.new(key, msg.encode('utf-8'), sha256).hexdigest()
        else:
            sig = hmac.new(key, msg.encode('utf-8'), sha256).digest()
        return si

def signature(self, string_to_sign, scope, secret_key):
        parts = scope.split('/')
        ts = parts[0]
        region = parts[1]
        service = parts[2]
        req_type = parts[3]
        k_date= self._sign((self.hash_keyword + secret_key).encode('utf-8'), ts)
        k_region = self._sign(k_date, region)
        k_service = self._sign(k_region, service)
        k_signing = self._sign(k_service, req_type)
        return self._sign(k_signing, string_to_sign, hex=True)
```

<h3 name="tong_yong_cuo_wu_xin_xi" id="tong_yong_cuo_wu_xin_xi">4.通用错误信息</h3>


---


|错误码 | 错误名称 | 错误描述|
| -- | -- | -- |
|400 | APIException<br>UNKNOWN_EXCEPTION |	调用API异常<br>遇到未知的异常|
|403 |	FORBIDDEN|	请求被禁止|
|404 |	NOT_FOUND|	未找到请求的API |
|500 |	INTERNAL_SERVER_ERROR|	服务内部错误 |
|501 |	NOT_IMPLEMENTED_ERROR|	API未实现 |
