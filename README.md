


# Банкнуудын API
```diff
+ Хаан банк 
- Худалдаа хөгжлийн банк 
- Голомт
```
Ер нь заваараа дээрх хэдэн банкуудын л API-г гарганаа.
## Features
- Мөнгө татах, шилжүүлэх үйлдлийг автоматжуулах

### Хаан банк 
 **Нэвтрэх хэсэг curl command**
 curl комманд ажиллуулахад нууц үг нь эхлээд base64 тэгээд urlencode хийгдсэн байх шаардлагатайг анхаарна уу
```curl
curl -i -s -k -X $'POST' \
    -H $'Host: api.khanbank.com:9003' -H $'Accept: application/json, text/plain, */*' -H $'Authorization: Basic ********************************************' -H $'Device-Id: AAAAAAAA-BBBB-CCCC-DDDD-AAAAAAAAAAAA' -H $'User-Agent: Mozilla/5.0 (Linux; Android 9; SM-N950N Build/PPR1.180610.011; wv) AppleWebKit/537.36 (KHTML, like Gecko) Version/4.0 Chrome/93.0.4577.82 Mobile Safari/537.36' -H $'Accept-Language: mn-MN' -H $'Secure: yes' -H $'Content-Type: application/x-www-form-urlencoded' -H $'Content-Length: 2' -H $'Accept-Encoding: gzip, deflate' -H $'Connection: close' \
    --data-binary $'{}' \
    $'https://api.khanbank.com:9003/v1/auth/token?grant_type=password&username=USERNAME&password=urlencode(b64(PASSWD))&channelId=G'
```
 **Нэвтрэх хэсэг жишээ код (python)**
```python
def login
    """1. headers дээр байгаа  Authorization дээр байх баахан однуудад таны нэр, болон нууц үгнээс гаргаж авсан string байх ёстой энийг, хаанбанкны апп автоматаар хийчихэж байгаа болохоор яг яаж generate хийж байгааг нь задлаж үзээгүй. Нэвтрэх хүсэлтэнд хамт үүсч байгаа. Бүр олж чадахгүй бол нэг видео заавар оруулъя даа. 
    2. Device-id нь мөн automatically үүсч байгаа. Гэхдээ ямарч утга байсан болно доорх форматын дагуу.
    3. USERNAME гэсэн талбар дээр нэвтрэх нэр
    4. base64encodedPASSWD гэсэн утга дээр нууц үгээ base64 болгоод оруулна. 
    5. User-agent аа солиж болно, солихгүй ч байсан болно. 
    Өөр өөрчлөх талбар байхгүй.
    """
    import requests

    headers = {
        'Host': 'api.khanbank.com:9003',
        'Accept': 'application/json, text/plain, */*',
        'Authorization': 'Basic ********************************************', 
        'Device-Id': 'AAAAAAAA-BBBB-CCCC-DDDD-AAAAAAAAAAAA', # Device ID-г бол өмнө орж байсанаараа л оруулахад хангалттай. 
        'User-Agent': 'Mozilla/5.0 (Linux; Android 9; SM-N950N Build/PPR1.180610.011; wv) AppleWebKit/537.36 (KHTML, like Gecko) Version/4.0 Chrome/93.0.4577.82 Mobile Safari/537.36',
        'Accept-Language': 'mn-MN',
        'Secure': 'yes',
        'Content-Type': 'application/x-www-form-urlencoded',
        'Content-Length': '2',
        'Accept-Encoding': 'gzip, deflate',
        'Connection': 'close',
    }

    params = (
        ('grant_type', 'password'),
        ('username', 'USERNAME'), # Нэвтрэх нэрээ энд бичнээ
        ('password', 'base64encodedPASSWD'), # Энэ дээр зүгээр password-оо base64-оор энкод хийгээд тавихад хангалттай
        ('channelId', 'G'),
    )

    data = '{}'

    response = requests.post('https://api.khanbank.com:9003/v1/auth/token', headers=headers, params=params, data=data, verify=False)
    return response.text
```
**Нэвтрэх хэсэгээс ирэх response** 
Энэ response дээрээс ерөөсөө access_token оо л авахад, гүйлгээ хийх хуулга харах гэх мэт үйлдлийг хийх боломжтой. Refresh токеноороо 300 секунд тутам ажиллуулснаар session-оо 900 секунд барих боломжтойг харж байна.

<details>
	 <summary> Үр дүн харах </summary>
  
```json
            {
                "access_token" : "*************************",
                "access_token_expires_in":299,
                "refresh_token" : "*************************",
                "refresh_token_status": "approved",
                "refresh_token_expires_in": 899,
                "organization_name": "khanprod",
                "token_type": "BearerToken",
                "default_account": "",
                "business": "",
                "business2": "",
                "birthday": "",
                "register_no": "****************",
                "lang": "Mongolian",
                "send_email": "",
                "send_sms": "",
                "last_ip": "AAAAAAAA-BBBB-CCCC-DDDD-AAAAAAAAAAAA",
                "login_count": "",
                "last_date": "*********************",
                "auto_ext": "",
                "address": "8.8.8.8",
                "bill_custid": "",
                "connected_time": "*********************",
                "option_login_name": "",
                "show_access_confirm": "",
                "segment": "Mass",
                "display_name": "*********************",
                "department": "",
                "email": "*********************",
                "show_sec_aq_alert": "",
                "create_sec_aq": "",
                "change_pass": "",
                "mobile": "***********",
                "email": "*********************",
                "last_name_en": "*********************",
                "first_name_en": "*********************",
                "last_name": "*********************",
                "first_name": "*********************",
                "role_id": "*********************",
                "customer_type": "Citizen",
                "email_masked": "*********************",
                "mobile_masked": "*********************",
                "last_name_masked": "*********************",
                "last_name_en_masked": "*********************",
                "cif":"*********************",
                "org_code":"*********************",
                
                "feedback": "0",
                "bank_id":"003",
                "principal_id":"*********************",
                "salutation":"Mr. / Ms.",
                "division_access_indicator":"Public",
                "login_date":"*********************",
                "logoff_date":"*********************",
                "multi_currency_txn_allowed":"Yes",
                "category_code":"SOFTWARE",
                "limit_scheme":"Retail - 20,000,000.00 with USSD 3m",
                "range_limit_scheme":"",
                "login_allowed":"Yes",
                "transaction_allowedaccount_format":"",
                "account_format":"NickName(Currency)-AccountId",
                "access_scheme":"Retail-Mass Access Scheme",
                "login_channel":"G",
                "last_unsuccessfull_login_channel":"App Mobile",
                "date_format":"yyyy/MM/dd",
                "transaction_authorization_scheme":"Retail Default",
                "calendar_type":"Gregorian",
                "unified_login_user":"No",
                "confidential_transaction_access":"No Access",
                "amount_format":"Million Format",
                "out_of_office_preference":"No",
                "account_masking_required":"No",
                "prospect_indicator":"No",
                "last_unsuccessfull_login_time":"*********************",
                "phone_number":"",
                
                "connection_id":"*********************",
                "device_confirmtype":"",
                "sec_qa_confirmed":"",
                "device_confirm_try_count":"",
                "login_option_show_access_confirm":"",
                "device_confirm_blocked":"",
                "device_is_permanent":"",
                "location_is_permanent":"",
                "device_confirm_option":"",
                "location_confirm_option":"",
                "system_settings":"",
                "primary_account_id":"*********************",
                "unique_id":"*********************",
                "bucketid":"",
                "force_signon_password_change_flag":"N",
                "force_txn_password_change_flag":"N",
                "force_security_question_change_flag":"N",
                "force_ussd_pin_change_flag":"N",
                "force_mode_change_flag":"N",
                "primary_authentication_mode":"",
                "authorization_mode":"",
                "total_login_count":"***",
                "actual_login_count":"**",
                "maximum_skip_count":"*",
                "segment_code":"5",
                "secondary_authentication_mode":"",
                "user_applicable_secondary_auth_modes":"",
                "security_question":[],
                "user_type":"1",
                "email_address":"",
                "mobile_number":""
            }     
```
</details>

**Refresh token ашиглаж холболтоо уртасгах хүсэлт**

```curl
curl -i -s -k -X $'POST' \
    -H $'Host: api.khanbank.com:9003' -H $'Accept: application/json, text/plain, */*' -H $'Authorization: Basic *****************************************' -H $'Accept-Language: mn-MN' -H $'User-Agent: Mozilla/5.0 (Linux; Android 9; SM-N950N Build/PPR1.180610.011; wv) AppleWebKit/537.36 (KHTML, like Gecko) Version/4.0 Chrome/93.0.4577.82 Mobile Safari/537.36' -H $'Secure: yes' -H $'Content-Type: application/x-www-form-urlencoded' -H $'Content-Length: 2' -H $'Accept-Encoding: gzip, deflate' -H $'Connection: close' \
    --data-binary $'{}' \
    $'https://api.khanbank.com:9003/v1/auth/refresh?grant_type=refresh_token&refresh_token=******************************'
```

```python
def refresh():
	import requests

	headers = {
	    'Host': 'api.khanbank.com:9003',
	    'Accept': 'application/json, text/plain, */*',
	    'Authorization': 'Basic *****************************************',
	    'Accept-Language': 'mn-MN',
	    'User-Agent': 'Mozilla/5.0 (Linux; Android 9; SM-N950N Build/PPR1.180610.011; wv) AppleWebKit/537.36 (KHTML, like Gecko) Version/4.0 Chrome/93.0.4577.82 Mobile Safari/537.36',
	    'Secure': 'yes',
	    'Content-Type': 'application/x-www-form-urlencoded',
	    'Content-Length': '2',
	    'Accept-Encoding': 'gzip, deflate',
	    'Connection': 'close',
	}

	params = (
	    ('grant_type', 'refresh_token'),
	    ('refresh_token', '*****************************************'),
	)

	data = '{}'

	response = requests.post('https://api.khanbank.com:9003/v1/auth/refresh', headers=headers, params=params, data=data, verify=False)
	return response.text
```

**Refresh token хүсэлтээс  ирэх response**

```json
{
                "access_token" : "**************************",
                "access_token_expires_in":299,
                "refresh_token" : "**************************",
                "refresh_token_status": "approved",
                "refresh_token_expires_in": 899
}
```

**Хуулга харах**
За тэр *account=*********** энэ хэсэг дээрх баахан однууд нь таны дансны дугаар байх юм шүү. 
```curl
curl -i -s -k -X $'GET' \
    -H $'Host: api.khanbank.com:9003' -H $'Accept: application/json, text/plain, */*' -H $'Authorization: Bearer ************************' -H $'Device-Id: AAAAAAAA-BBBB-CCCC-DDDD-AAAAAAAAAAAA' -H $'Accept-Language: mn-MN' -H $'User-Agent: Mozilla/5.0 (Linux; Android 9; SM-N950N Build/PPR1.180610.011; wv) AppleWebKit/537.36 (KHTML, like Gecko) Version/4.0 Chrome/93.0.4577.82 Mobile Safari/537.36' -H $'Secure: yes' -H $'Accept-Encoding: gzip, deflate' -H $'Connection: close' \
    $'https://api.khanbank.com:9003/v1/omni/user/custom/recentTransactions?account=**********'
```
```python
def  recent_transaction():
	import requests
	headers = {
	'Host': 'api.khanbank.com:9003',
	'Accept': 'application/json, text/plain, */*',
	'Authorization': 'Bearer ********************',
	'Device-Id': 'AAAAAAAA-BBBB-CCCC-DDDD-AAAAAAAAAAAA',
	'Accept-Language': 'mn-MN',
	'User-Agent': 'Mozilla/5.0 (Linux; Android 9; SM-N950N Build/PPR1.180610.011; wv) AppleWebKit/537.36 (KHTML, like Gecko) Version/4.0 Chrome/93.0.4577.82 Mobile Safari/537.36',
	'Secure': 'yes',
	'Accept-Encoding': 'gzip, deflate',
	'Connection': 'close',
	}
	params = (
	('account', '************'),
	)
	response = requests.get('https://api.khanbank.com:9003/v1/omni/user/custom/recentTransactions', headers=headers, params=params, verify=False)
	return response.text
```

**Хуулга харах response**
Гэх мэт орж ирнээ. 
<details>
	 <summary> Үр дүн харах </summary>
  
```json
[
    {
        "tranDate": "************",
        "time": "00:00",
        "amount": -200.0,
        "description": "************",
        "relatedAccount": "",
        "currency": "MNT",
        "code": "****",
        "refId": "************",
        "balance": 123456789
    },
    {
        "tranDate": "************",
        "time": "00:34",
        "amount": -500.0,
        "description": "*********",
        "relatedAccount": "************",
        "currency": "MNT",
        "code": "****",
        "refId": "************",
        "balance": 123456789
    }
]
```
</details>

**Хаанбанкны дансруу шилжүүлэг хийх**

> 1. "primaryAccessCode":"b64(passwd_transfer)"      Энд гүйлгээний нууц үг b64 encode хийгдэж орноо.
> 2. "initiatorAccount":"***********         Энд бол таны дансны дугаар байх юмаа.
> 3. "amount":"***"  Энд шилжүүлэх дүн
> 4. "counterpartyAccount": "*****************" Энд шилжүүлэх данс байнаа.
> 5. "payeeName": "***************", Нэр нь байхымаа
> 6. "accountNumber": "************", Энд шилжүүлэх данс байнаа.

```curl
curl -i -s -k -X $'POST' \
    -H $'Host: api.khanbank.com:9003' -H $'Accept: application/json, text/plain, */*' -H $'Channelcontext: {\"authorizationDetails\":{\"primaryAccessCode\":\"b64(passwd_transfer)\",\"userId\":\"*****\"}}' -H $'Authorization: Bearer ***********************' -H $'Device-Id: AAAAAAAA-BBBB-CCCC-DDDD-AAAAAAAAAAAA' -H $'Accept-Language: mn-MN' -H $'User-Agent: Mozilla/5.0 (Linux; Android 9; SM-N950N Build/PPR1.180610.011; wv) AppleWebKit/537.36 (KHTML, like Gecko) Version/4.0 Chrome/93.0.4577.82 Mobile Safari/537.36' -H $'Secure: yes' -H $'Content-Type: application/json' -H $'Content-Length: 1183' -H $'Accept-Encoding: gzip, deflate' -H $'Connection: close' \
    --data-binary $'{\"transactionReferenceName\":\"\",\"transactionType\":\"TPA\",\"transactionDate\":\"2021-10-10T16:00:00\",\"frequencyType\":\"O\",\"templateId\":0,\"transactionCurrency\":\"MNT\",\"recurringDetails\":{\"validityIndicator\":\"N\",\"recurringFrequency\":\"0\",\"numberOfInstallments\":\"\",\"lastPaymentDate\":\"\",\"firstPaymentAmount\":0,\"lastPaymentAmount\":0,\"isFrequentTransaction\":false},\"entryDetails\":[{\"entryID\":0,\"initiatorAccount\":\"***********\",\"amount\":\"***\",\"accountCurrency\":\"MNT\",\"counterpartyType\":\"H\",\"network\":\"WIB\",\"remarks\":\"description bh ymaa end\",\"transactionPurpose\":\"\",\"markAsDelete\":\"N\",\"payeeReference\":\"\",\"payeeAccountDetails\":{\"counterpartyAccount\":\"*************\",\"adhocPayeeDetails\":{\"payeeName\":\"******************************",\"payeeNickName\":\"\",\"accountNumber\":\"**************\",\"accountIdentifier\":\"A\",\"payeeAccountType\":\"\",\"accountCurrency\":\"MNT\",\"payeeBank\":\"HBK\",\"payeeNetwork\":\"WIB\",\"payeeBankIdentifier\":\"003\",\"isInternationalBankAccountNumber\":\"No\",\"saveToPersonalPayee\":\"N\",\"counterpartyAddressVO\":{\"addressLine1\":\"\",\"addressLine2\":\"\",\"addressLine3\":\"\",\"city\":\"\",\"zipCode\":\"\",\"state\":\"\",\"country\":\"\"}}},\"additionalCounterpartyDetails\":{\"phoneNumber\":\"\",\"referencePartyName\":\"\",\"transferInformation\":\"\"}}]}' \
    $'https://api.khanbank.com:9003/v1/omni/user/v2/multientrytransactionsrequests'
```
**python жишээ код**
```python

def send_to_khanbank():
"""
Энд яаг curl дээр тайлбарласан шиг утгууд нь солигдноо.
"""
    import requests

    headers = {
        'Host': 'api.khanbank.com:9003',
        'Accept': 'application/json, text/plain, */*',
        'Channelcontext': '{"authorizationDetails":{"primaryAccessCode":"********","userId":"******"}}',
        'Authorization': 'Bearer ****************',
        'Device-Id': 'AAAAAAAA-BBBB-CCCC-DDDD-AAAAAAAAAAAA',
        'Accept-Language': 'mn-MN',
        'User-Agent': 'Mozilla/5.0 (Linux; Android 9; SM-N950N Build/PPR1.180610.011; wv) AppleWebKit/537.36 (KHTML, like Gecko) Version/4.0 Chrome/93.0.4577.82 Mobile Safari/537.36',
        'Secure': 'yes',
        'Content-Type': 'application/json',
        'Content-Length': '1183',
        'Accept-Encoding': 'gzip, deflate',
        'Connection': 'close',
    }

    data = '{"transactionReferenceName":"","transactionType":"TPA","transactionDate":"2021-10-10T16:00:00","frequencyType":"O","templateId":0,"transactionCurrency":"MNT","recurringDetails":{"validityIndicator":"N","recurringFrequency":"0","numberOfInstallments":"","lastPaymentDate":"","firstPaymentAmount":0,"lastPaymentAmount":0,"isFrequentTransaction":false},"entryDetails":[{"entryID":0,"initiatorAccount":"***********","amount":"***","accountCurrency":"MNT","counterpartyType":"H","network":"WIB","remarks":"********","transactionPurpose":"","markAsDelete":"N","payeeReference":"","payeeAccountDetails":{"counterpartyAccount":"**********","adhocPayeeDetails":{"payeeName":"****************************","payeeNickName":"","accountNumber":"**********","accountIdentifier":"A","payeeAccountType":"","accountCurrency":"MNT","payeeBank":"HBK","payeeNetwork":"WIB","payeeBankIdentifier":"003","isInternationalBankAccountNumber":"No","saveToPersonalPayee":"N","counterpartyAddressVO":{"addressLine1":"","addressLine2":"","addressLine3":"","city":"","zipCode":"","state":"","country":""}}},"additionalCounterpartyDetails":{"phoneNumber":"","referencePartyName":"","transferInformation":""}}]}'

    response = requests.post('https://api.khanbank.com:9003/v1/omni/user/v2/multientrytransactionsrequests', headers=headers, data=data, verify=False)
    return response.text
```
**Бусад банкны дансруу шилжүүлэг хийх**


```curl
curl -i -s -k -X $'POST' \
    -H $'Host: api.khanbank.com:9003' -H $'Accept: application/json, text/plain, */*' -H $'Channelcontext: {\"authorizationDetails\":{\"primaryAccessCode\":\"*********\",\"userId\":\"*****\"}}' -H $'Authorization: Bearer *********************' -H $'Device-Id: AAAAAAAA-BBBB-CCCC-DDDD-AAAAAAAAAAAA' -H $'Accept-Language: mn-MN' -H $'User-Agent: Mozilla/5.0 (Linux; Android 9; SM-N950N Build/PPR1.180610.011; wv) AppleWebKit/537.36 (KHTML, like Gecko) Version/4.0 Chrome/93.0.4577.82 Mobile Safari/537.36' -H $'Secure: yes' -H $'Content-Type: application/json' -H $'Content-Length: 1159' -H $'Accept-Encoding: gzip, deflate' -H $'Connection: close' \
    --data-binary $'{\"transactionReferenceName\":\"\",\"transactionType\":\"XFR\",\"transactionDate\":\"2021-10-10T16:00:00\",\"frequencyType\":\"O\",\"templateId\":0,\"transactionCurrency\":\"MNT\",\"recurringDetails\":{\"validityIndicator\":\"N\",\"recurringFrequency\":\"0\",\"numberOfInstallments\":\"\",\"lastPaymentDate\":\"\",\"firstPaymentAmount\":0,\"lastPaymentAmount\":0,\"isFrequentTransaction\":false},\"entryDetails\":[{\"entryID\":0,\"initiatorAccount\":\"**********\",\"amount\":\"***\",\"accountCurrency\":\"MNT\",\"counterpartyType\":\"H\",\"network\":\"ACH\",\"remarks\":\"description bhimaa end\",\"transactionPurpose\":\"\",\"markAsDelete\":\"N\",\"payeeReference\":\"\",\"payeeAccountDetails\":{\"counterpartyAccount\":\"**********\",\"adhocPayeeDetails\":{\"payeeName\":\"*********\",\"payeeNickName\":\"\",\"accountNumber\":\"*****************\",\"accountIdentifier\":\"A\",\"payeeAccountType\":\"\",\"accountCurrency\":\"MNT\",\"payeeBank\":\"OBK\",\"payeeNetwork\":\"ACH\",\"payeeBankIdentifier\":\"150000\",\"isInternationalBankAccountNumber\":\"No\",\"saveToPersonalPayee\":\"N\",\"counterpartyAddressVO\":{\"addressLine1\":\"\",\"addressLine2\":\"\",\"addressLine3\":\"\",\"city\":\"\",\"zipCode\":\"\",\"state\":\"\",\"country\":\"\"}}},\"additionalCounterpartyDetails\":{\"phoneNumber\":\"\",\"referencePartyName\":\"\",\"transferInformation\":\"\"}}]}' \
    $'https://api.khanbank.com:9003/v1/omni/user/v2/multientrytransactionsrequests'
```

Үргэлжлэлийг дараа 7 хоногт :( 
Энэ 7 хоногт кофе сайн уувал хурдан оруулна. Кофены мөнгө шилжүүлэх бол миний данс доор байгаа шүү xD.  

*1235115077 Голомт банк Энхболд шүү*