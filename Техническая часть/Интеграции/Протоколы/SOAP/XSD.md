**XSD** (XML Schema Definition) — язык определения схем для XML-документов.

**Основные особенности XSD:**
1) XSD-документы сами по себе являются XML-файлами
2) Поддерживают типизацию данных (числа, строки, даты и т. д.)
3) Позволяют задавать ограничения, такие как минимальная/максимальная длина строки, диапазон чисел и т. д.

**Структура XSD:**
1) **Корневой элемент.** <xs:schema> — обязательный элемент, указывающий, что документ является схемой XSD
2) **Простые типы данных.** Определяют атрибуты или содержимое элемента (например, xs:string, xs:int)
3) **Сложные типы данных.** Определяют элементы, которые содержат вложенные элементы и/или атрибуты

**Пример XSD:**
``` xsd
<?xml version="1.0" encoding="UTF-8"?>
<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema">
    <xs:element name="library">
        <xs:complexType>
            <xs:sequence>
                <xs:element name="book" maxOccurs="unbounded">
                    <xs:complexType>
                        <xs:sequence>
                            <xs:element name="title" type="xs:string" />
                            <xs:element name="author" type="xs:string" />
                            <xs:element name="price" type="xs:decimal" />
                        </xs:sequence>
                        <xs:attribute name="id" type="xs:int" use="required" />
                    </xs:complexType>
                </xs:element>
            </xs:sequence>
        </xs:complexType>
    </xs:element>
</xs:schema>
```

**Основные элементы и атрибуты XSD:**
1) **<xs:element>.** Определяет элемент:
	1) **Атрибут name.** Имя элемента
	2) **Атрибут type.** Тип данных элемента
	3) **Атрибуты minOccurs/maxOccurs.** Указывают минимальное и максимальное количество повторений элемента
2) **<xs:attribute>.** Определяет атрибут:
	1) **Атрибут name.** Имя атрибута
	2) **Атрибут type.** Тип данных
	3) **Атрибут use.** Указывает, обязателен ли атрибут (required/optional)
3) **<xs:complexType>.** Определяет элементы с вложенной структурой (другие элементы или атрибуты
4) **<xs:simpleType>.** Определяет элемент с простыми данными (например, строки, числа).
5) **<xs:sequence>.** Определяет последовательность вложенных элементов

**Типы данных XSD:**
1) **Простые.** xs:string, xs:integer, xs:boolean, xs:date, xs:decimal
2) **Ограниченные.** Создаются с помощью <xs:restriction>

**Ограничения данных в XSD:**
1) **Длина строки:**
``` xsd
<xs:simpleType name="limitedString">
    <xs:restriction base="xs:string">
        <xs:maxLength value="10"/>
        <xs:minLength value="3"/>
    </xs:restriction>
</xs:simpleType>
```
2) **Диапазон чисел:**
``` xsd
<xs:simpleType name="numberRange">
    <xs:restriction base="xs:int">
        <xs:minInclusive value="1"/>
        <xs:maxInclusive value="100"/>
    </xs:restriction>
</xs:simpleType>
```
3) **Перечисление:**
``` xsd
<xs:simpleType name="colors">
    <xs:restriction base="xs:string">
        <xs:enumeration value="red"/>
        <xs:enumeration value="green"/>
        <xs:enumeration value="blue"/>
    </xs:restriction>
</xs:simpleType>
```
