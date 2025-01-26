**WSDL (Web Services Definition Language)** - [[XML]]-язык, используемый для описания веб-сервисов и их интерфейсов. Он определяет какие операции сервис предоставляет, какие параметры и типы данных используют, а также какие взаимосвязаны сервисы (местоположения и протоколы).

**Характеристики WSDL:**
1) **Основан на XML.** Полностью соответствует спецификации XML, что делает его платоформо-независимым
2) **Контрактная ориентация.** WSDL определяет чёткий интерфейс сервиса, который может быть использован разработчиками
3) **Поддержка нескольких протколов.** WSDL поддерживает другие протоколы кроме SOAP (например, [[HTTP]] и [[MIMIE]])
4) **Автоматизация разработки.** SoapUI или wsimport могут автоматизировать генерируемый клиентский код на основе WSDL

**Плюсы WSDL:**
1) **Чёткость и стандартизация.** WSDL обеспечивает чёткую спецификацию интерфейса сервиса, что минимизирует ошибки
2) **Интеграция с инструментами разработки.** Инструменты могут автоматизировать генерацию кода клиента или сервиса на основе WSDL
3) **Поддержка сложных операций.** Легко добавлять новые операции или модифицировать существующие без изменения архитектуры

**Минусы WSDL:**
1) **Cложность.** Формат XML может быть громоздким и сложным для понимания без инструментов
2) **Избыточность.** Для простых сервисов WSDL может быть избыточным
3) **Чувствительность к пространствам имён.** Неправильная работа с пространствами имён может вызвать проблемы

**Структура документа WSDL:**
1) **Definitions (определения).** Корневой элемент документа, где определены пространства имён и общие настройки. Пример:  
``` wsdl
<definitions xmlns="http://schemas.xmlsoap.org/wsdl/" 

             xmlns:soap="http://schemas.xmlsoap.org/wsdl/soap/" 

             xmlns:xs="http://www.w3.org/2001/XMLSchema" 

             targetNamespace="http://example.com/wsdl/sample" 

             xmlns:tns="http://example.com/wsdl/sample" 

             name="SampleService">

</definitions>
```
2) **Types (типы).** Определяет структуру данных используемых в сообщениях (обычно, с помощью [[XSD]]). Пример:
``` wsdl
<types>
    <xs:schema targetNamespace="http://example.com/wsdl/sample">
        <xs:element name="RequestData">
            <xs:complexType>
                <xs:sequence>
                    <xs:element name="ID" type="xs:int" />
                    <xs:element name="Name" type="xs:string" />
                </xs:sequence>
            </xs:complexType>
        </xs:element>
        <xs:element name="ResponseData">
            <xs:complexType>
                <xs:sequence>
                    <xs:element name="Status" type="xs:string" />
                    <xs:element name="Message" type="xs:string" />
                </xs:sequence>
            </xs:complexType>
        </xs:element>
    </xs:schema>
</types>
```
3) **Message (сообщения).** Определяет структуры входных и выходных данных для операций. Пример:
``` wsdl
<message name="RequestMessage">
    <part name="parameters" element="tns:RequestData" />
</message>
<message name="ResponseMessage">
    <part name="parameters" element="tns:ResponseData" />
</message>
```
4) **PortType (интерфейсы).** Определяют набор операций, которые предоставляет веб-сервис и соответствующие им сообщения. Пример:
``` wsdl
<portType name="SamplePortType">
    <operation name="GetInfo">
        <documentation>Получение информации по ID.</documentation>
        <input message="tns:RequestMessage" />
        <output message="tns:ResponseMessage" />
    </operation>
</portType>
```
5) **Binding (связывание).** Определяет какие протоколы и транспортные механизмы используются. Пример:
``` wsdl
<binding name="SampleSoapBinding" type="tns:SamplePortType">
    <soap:binding style="document" transport="http://schemas.xmlsoap.org/soap/http" />
    <operation name="GetInfo">
        <soap:operation soapAction="http://example.com/GetInfo" style="document" />
        <input>
            <soap:body use="literal" />
        </input>
        <output>
            <soap:body use="literal" />
        </output>
    </operation>
</binding>
```
6) **Service (сервис).** Определяет конкретное местоположение сервиса. Пример:
``` wsdl
<service name="SampleService">
    <documentation>Пример веб-сервиса</documentation>
    <port name="SamplePort" binding="tns:SampleSoapBinding">
        <soap:address location="http://example.com/sample" />
    </port>
</service>
```

**Пример итогового документа WSDL:**
``` wsdl
<?xml version="1.0" encoding="UTF-8"?>
<definitions xmlns="http://schemas.xmlsoap.org/wsdl/" 
             xmlns:soap="http://schemas.xmlsoap.org/wsdl/soap/" 
             xmlns:xs="http://www.w3.org/2001/XMLSchema" 
             targetNamespace="http://example.com/wsdl/sample" 
             xmlns:tns="http://example.com/wsdl/sample" 
             name="SampleService">

    <!-- Определение типов данных -->
    <types>
        <xs:schema targetNamespace="http://example.com/wsdl/sample">
            <xs:element name="RequestData">
                <xs:complexType>
                    <xs:sequence>
                        <xs:element name="ID" type="xs:int" />
                        <xs:element name="Name" type="xs:string" />
                    </xs:sequence>
                </xs:complexType>
            </xs:element>
            <xs:element name="ResponseData">
                <xs:complexType>
                    <xs:sequence>
                        <xs:element name="Status" type="xs:string" />
                        <xs:element name="Message" type="xs:string" />
                    </xs:sequence>
                </xs:complexType>
            </xs:element>
        </xs:schema>
    </types>

    <!-- Определение сообщений -->
    <message name="RequestMessage">
        <part name="parameters" element="tns:RequestData" />
    </message>
    <message name="ResponseMessage">
        <part name="parameters" element="tns:ResponseData" />
    </message>

    <!-- Определение интерфейса -->
    <portType name="SamplePortType">
        <operation name="GetInfo">
            <documentation>Получение информации по ID.</documentation>
            <input message="tns:RequestMessage" />
            <output message="tns:ResponseMessage" />
        </operation>
    </portType>

    <!-- Привязка интерфейса -->
    <binding name="SampleSoapBinding" type="tns:SamplePortType">
        <soap:binding style="document" transport="http://schemas.xmlsoap.org/soap/http" />
        <operation name="GetInfo">
            <soap:operation soapAction="http://example.com/GetInfo" style="document" />
            <input>
                <soap:body use="literal" />
            </input>
            <output>
                <soap:body use="literal" />
            </output>
        </operation>
    </binding>

    <!-- Определение веб-сервиса -->
    <service name="SampleService">
        <documentation>Пример веб-сервиса</documentation>
        <port name="SamplePort" binding="tns:SampleSoapBinding">
            <soap:address location="http://example.com/sample" />
        </port>
    </service>
</definitions>
```