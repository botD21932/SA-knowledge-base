**WS-Security (Web Services Security)** — это стандарт безопасности для SOAP-сообщений. Он определяет набор расширений для обеспечения аутентификации, конфиденциальности, целостности и защиты сообщений, передаваемых между веб-сервисами.

**Основные цели WS-Security:**
1) **Аутентификация.** Проверка личности отправителя сообщения
2) **Целостность данных.** Обеспечение защиты от изменений данных во время передач
3) **Конфиденциальность.** Шифрование данных для предотвращения несанкционированного доступа
4) **Поддержка различных стандартов безопасности.** Интеграция с X.509, Kerberos, SAML и другими механизмами

**Ключевые компоненты WS-Security:**
1) **WS-Security Header.** Все данные WS-Security размещаются в заголовке SOAP-сообщения. Пример:
``` xsd
<SOAP-ENV:Header>
    <wsse:Security>
        <!-- Данные безопасности -->
    </wsse:Security>
</SOAP-ENV:Header>
```
2) **Токены безопасности.** Используются для аутентификации и передачи данных. Основные типы токенов:
	1) **UsernameToken.** Передача имени пользователя и пароля
	2) **BinarySecurityToken.** Для работы с X.509 сертификатами
	3) **SAML Token.** Для передачи информации о пользователе через SAML
3) **Цифровая подпись (Signature):**
	1) Гарантирует целостность данных и подтверждает личность отправителя
	2) Использует алгоритмы шифрования (например, RSA, SHA-256)
4) **Шифрование (Encryption)**:
	1) Используется для защиты конфиденциальных данных
	2) Данные шифруются с использованием симметричного или асимметричного шифрования

**Основные элементы WS-Security:**
1) **UsernameToken.** Используется для простой аутентификации с передачей имени пользователя и пароля. Пример:
``` xsd
<wsse:Security>
    <wsse:UsernameToken>
        <wsse:Username>JohnDoe</wsse:Username>
        <wsse:Password Type="...#PasswordDigest">password123</wsse:Password>
        <wsse:Nonce>randomString</wsse:Nonce>
        <wsu:Created>2025-01-21T12:00:00Z</wsu:Created>
    </wsse:UsernameToken>
</wsse:Security>
```
2) **BinarySecurityToken.** Используется для передачи сертификатов X.509. Пример:
``` xsd
<wsse:Security>
    <wsse:BinarySecurityToken ValueType="...#X509v3"
                              EncodingType="...#Base64Binary">
        MIIE...
    </wsse:BinarySecurityToken>
</wsse:Security>
```
3) **Цифровая подпись.** Добавляется в сообщение для проверки целостности. Пример:
``` xsd
<wsse:Security>
    <ds:Signature>
        <ds:SignedInfo>
            <ds:CanonicalizationMethod Algorithm="...#Exclusive"/>
            <ds:SignatureMethod Algorithm="...#rsa-sha256"/>
            <ds:Reference URI="#Body">
                <ds:DigestMethod Algorithm="...#sha256"/>
                <ds:DigestValue>...</ds:DigestValue>
            </ds:Reference>
        </ds:SignedInfo>
        <ds:SignatureValue>...</ds:SignatureValue>
        <ds:KeyInfo>
            <wsse:SecurityTokenReference>
                <wsse:Reference URI="#Token"/>
            </wsse:SecurityTokenReference>
        </ds:KeyInfo>
    </ds:Signature>
</wsse:Security>
```

**Архитектура безопасности:**
1) **Транспортный уровень**:
	1) Используется SSL/TLS для защиты связи (например, HTTPS)
	2) Подходит для передачи данных от точки до точки
2) **Сообщенческий уровень (WS-Security)**:
	1) Защищает сами сообщения, включая заголовки и тело
	2) Обеспечивает защиту от точки до точки и сквозную защиту

**Механизмы WS-Security:**
1) **Аутентификация.** Использование токенов (например, UsernameToken, X.509)
2) **Целостность.** Проверка цифровой подписи
3) **Конфиденциальность.** Шифрование частей сообщения
4) **Временные метки (Timestamp).** Гарантирует, что сообщение отправлено в определённое время и не может быть повторно использовано

**Пример полного SOAP-сообщения с WS-Security:**
``` xsd
<SOAP-ENV:Envelope xmlns:SOAP-ENV="http://schemas.xmlsoap.org/soap/envelope/"
                   xmlns:wsse="http://schemas.xmlsoap.org/ws/2002/12/secext">
    <SOAP-ENV:Header>
        <wsse:Security>
            <wsu:Timestamp>
                <wsu:Created>2025-01-21T12:00:00Z</wsu:Created>
                <wsu:Expires>2025-01-21T12:05:00Z</wsu:Expires>
            </wsu:Timestamp>
            <wsse:UsernameToken>
                <wsse:Username>JohnDoe</wsse:Username>
                <wsse:Password Type="...#PasswordDigest">password123</wsse:Password>
                <wsse:Nonce>randomString</wsse:Nonce>
                <wsu:Created>2025-01-21T12:00:00Z</wsu:Created>
            </wsse:UsernameToken>
            <ds:Signature>
                <ds:SignedInfo>
                    <ds:CanonicalizationMethod Algorithm="...#Exclusive"/>
                    <ds:SignatureMethod Algorithm="...#rsa-sha256"/>
                    <ds:Reference URI="#Body">
                        <ds:DigestMethod Algorithm="...#sha256"/>
                        <ds:DigestValue>...</ds:DigestValue>
                    </ds:Reference>
                </ds:SignedInfo>
                <ds:SignatureValue>...</ds:SignatureValue>
                <ds:KeyInfo>
                    <wsse:SecurityTokenReference>
                        <wsse:Reference URI="#Token"/>
                    </wsse:SecurityTokenReference>
                </ds:KeyInfo>
            </ds:Signature>
        </wsse:Security>
    </SOAP-ENV:Header>
    <SOAP-ENV:Body wsu:Id="Body">
        <example:Data xmlns:example="http://example.org">
            <example:Item>Value</example:Item>
        </example:Data>
    </SOAP-ENV:Body>
</SOAP-ENV:Envelope>
```