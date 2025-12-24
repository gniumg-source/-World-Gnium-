Documentación de GitHub
GraphQL API/Referencia/Escalares
Escalares
Los valores escalares son valores primitivos: Int, Float, String, Boolean o ID.

En este artículo
Acerca de los escalares
Los valores escalares son valores primitivos: Int, Float, String, Boolean o ID.

Cuando llamas a la API de GraphQL, debes especificar subcampos anidados hasta que recuperes únicamente escalares.

Para más información, consulta Introducción a GraphQL.

Base64String
A (potentially binary) string encoded using base64.

BigInt
Represents non-fractional signed whole numeric values. Since the value may exceed the size of a 32-bit integer, it's encoded as a string.

Boolean
Represents true or false values.

CustomPropertyValue
A custom property value can be either a string or an array of strings. All property types support only a single string value, except for the multi-select type, which supports only a string array.

Date
An ISO-8601 encoded date string.

DateTime
An ISO-8601 encoded UTC date string.

Float
Represents signed double-precision fractional values as specified by IEEE 754.

GitObjectID
A Git object ID.

GitRefname
A fully qualified reference name (e.g. refs/heads/master).

GitSSHRemote
Git SSH string.

GitTimestamp
An ISO-8601 encoded date string. Unlike the DateTime type, GitTimestamp is not converted in UTC.

HTML
A string containing HTML code.

ID
Represents a unique identifier that is Base64 obfuscated. It is often used to refetch an object or as key for a cache. The ID type appears in a JSON response as a String; however, it is not intended to be human-readable. When expected as an input type, any string (such as "VXNlci0xMA==") or integer (such as 4) input value will be accepted as an ID.

Int
Represents non-fractional signed whole numeric values. Int can represent values between -(2^31) and 2^31 - 1.

PreciseDateTime
An ISO-8601 encoded UTC date string with millisecond precision.

String
Represents textual data as UTF-8 character sequences. This type is most often used by GraphQL to represent free-form human-readable text.

URI
An RFC 3986, RFC 3987, and RFC 6570 (level 4) compliant URI string.

X509Certificate
A valid x509 certificate string
