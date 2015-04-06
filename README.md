# [DynamicApis](http://www.DynamicApis.com) - SimpleRest Open Standard (SOS)
An open standard format for providing consistent easy to use and undersatnd REST service documentation.

#### Version History

Version | Date | Release Notes
--- | --- | ---
1.0 | 05/02/2015 | Initial release of version 1.0

##### Version 1.0
- Built with strongly typed languages in mind to allow for easy binding on modern user interfaces and to make serialization as simple as it should be.
- Designed in a resource oriented fashion to help encourage resource based REST service design.
- Designed to logically group endpoints by their aggregate root (or root resource).
- Allows creator to indicate version.
- Allows creator to provide general text description of overall servie as well as each resource endpoint provided.
- Allows creator to specify list of supported media types.
- Allows creator to add hyperlinks and associate them globally or on individual endpoints.
- Allows creator to very specifically define input parameters.
- Allows creator to indicate status codes that can be expected globally or on individual endpoints.
- Allows creator to associate error codes and descriptions to status codes that can be expected.
- Allows creator to define custom sample data for any or all input parameters.

## Introduction

On a mission to provide easy to read and easy to understand REST service documentation format.

The goal of SOS is much more than simply creating a json document to power a single user interface designed by the SOS creators. It is the belief of the founders of [DynamicApis](http://www.DynamicApis.com) that service documentation format should be simple and powerful. 
Documentation should be very easy for a developer to read and quickly make sense of in its raw format. It should also be flexible and simple enough to be easily leveraged by ANY modern user interface.

## References
[Http Status Codes](http://en.wikipedia.org/wiki/List_of_HTTP_status_codes) - A list of http status codes from wikipedia.

[Http Media Types](http://en.wikipedia.org/wiki/Internet_media_type) - A little bit about media types and what they are from wikipedia.

[Http Verbs](http://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol#Request_methods) - A list of http verbs (methods) and what they are used for from wikipedia.

## Specification
### Sample
```js
{
   "Description":"Use this service to interact with product information.",
   "Version":"v1",
   "MediaTypeFormatters":[
      {
         "Description":"JSON media type formatter.",
         "SupportedMediaTypes":[
            "application/json",
            "text/json"
         ]
      },
      {
         "Description":"XML media type formatter.",
         "SupportedMediaTypes":[
            "application/xml",
            "text/xml"
         ]
      },
      {
         "Description":"Media type formatter.",
         "SupportedMediaTypes":[
            "application/x-www-form-urlencoded"
         ]
      }
   ],
   "Resources":[
      {
         "BaseUri":"/products/{id}",
         "HttpMethods":[
            {
               "Verb":"GET",
               "Description":"Return a product for a given product id.",
               "FullUri":"/products/{id}",
               "Links":null,
               "Parameters":[
                  {
                     "Name":"id",
                     "Type":"string",
                     "Description":"The unique identifier of the product that is to be returned.",
                     "Usage":"Required",
                     "Location":"BaseUri",
                     "AcceptedValues":null
                  },
                  {
                     "Name":"authorization",
                     "Type":"String",
                     "Description":"Bearer token to authorize the request.",
                     "Usage":"Required",
                     "Location":"Header",
                     "AcceptedValues":null
                  }
               ],
               "HttpStatusCodes":[
                  {
                     "ErrorCode":null,
                     "StatusCode":404,
                     "Description":"Returned when product for respective id could not be found."
                  },
                  {
                     "ErrorCode":"1883.1x332",
                     "StatusCode":500,
                     "Description":"Returned when an unknown error occurs during retrieval of product."
                  }
               ],
               "ReturnType":"Product",
               "Samples":[
                  {
                     "Source":"Body",
                     "Format":"Xsd",
                     "Type":"CallbackUri",
                     "Direction":"Response",
                     "Value":"/xsds/Products?fullUri=%2fproducts%2f%7bid%7d&sampleType=ForResponse&verb=GET",
                     "Name":null
                  },
                  {
                     "Source":"Body",
                     "Format":"Xsd",
                     "Type":"PlainText",
                     "Direction":"Response",
                     "Value":"<xs:schema elementFormDefault=\"qualified\" xmlns:xs=\"http://www.w3.org/2001/XMLSchema\"><xs:complexType name=\"ArrayOfCost\"><xs:sequence><xs:element minOccurs=\"0\" maxOccurs=\"unbounded\" name=\"Cost\" type=\"Cost\" /></xs:sequence></xs:complexType><xs:element name=\"Cost\" nillable=\"true\" type=\"Cost\" /><xs:complexType name=\"Cost\"><xs:sequence><xs:element minOccurs=\"0\" maxOccurs=\"1\" name=\"Amount\" nillable=\"true\" type=\"xs:decimal\" /></xs:sequence></xs:complexType><xs:element name=\"Product\" nillable=\"true\" type=\"Product\" /><xs:complexType name=\"Product\"><xs:sequence><xs:element minOccurs=\"0\" maxOccurs=\"1\" name=\"Id\" nillable=\"true\" type=\"xs:string\" /><xs:element minOccurs=\"0\" maxOccurs=\"1\" name=\"Name\" nillable=\"true\" type=\"xs:string\" /><xs:element minOccurs=\"0\" maxOccurs=\"1\" name=\"Price\" nillable=\"true\" type=\"xs:decimal\" /><xs:element minOccurs=\"0\" maxOccurs=\"1\" name=\"Description\" nillable=\"true\" type=\"xs:string\" /><xs:element minOccurs=\"0\" maxOccurs=\"1\" name=\"DateCreated\" nillable=\"true\" type=\"xs:dateTime\" /><xs:element minOccurs=\"0\" maxOccurs=\"1\" name=\"Costs\" nillable=\"true\" type=\"ArrayOfCost\" /></xs:sequence></xs:complexType></xs:schema>",
                     "Name":null
                  },
                  {
                     "Source":"Body",
                     "Format":"Json",
                     "Type":"CallbackUri",
                     "Direction":"Response",
                     "Value":"/samples/Products?fullUri=%2fproducts%2f%7bid%7d&sampleType=ForResponse&verb=GET",
                     "Name":null
                  },
                  {
                     "Source":"Header",
                     "Format":"String",
                     "Type":"PlainText",
                     "Direction":"Request",
                     "Value":"bearer <TokenGoesHere>",
                     "Name":"authorization"
                  },
                  {
                     "Source":"Body",
                     "Format":"Json",
                     "Type":"PlainText",
                     "Direction":"Response",
                     "Value":"{\"Id\":\"36405fde093c46d78da7cfbae216c4a8\",\"Name\":\"2014 Dodge Viper GTS\",\"Price\":104000.99,\"Description\":\"Brand new 2014 Dodge Viper GTS for sale. Red and black color combo with leather seats. 640hp! Come see it today!\",\"DateCreated\":\"2015-01-01T00:00:00\",\"Costs\":[{\"Amount\":104000.99}]}",
                     "Name":null
                  }
               ]
            }
         ]
      }
   ],
   "HttpStatusCodes":[
      {
         "ErrorCode":null,
         "StatusCode":401,
         "Description":"Returned if oAuth 2 bearer token provided was not valid or does not contain proper scope."
      }
   ],
   "Links":[
      {
         "Uri":"http://www.DynamicApis.com/dapi",
         "Description":"Help documentation for APIs"
      }
   ]
}
```

### Fields
#### Required
- Version
- MediaTypeFormatters
- MediaTypeFormatters.SupportedMediaTypes
- Resources
- Resoures.BaseUri
- Resources.HttpMethods
- Resources.HttpMethods.FullUri
- Resources.HttpMethods.Verb
- Resources.HttpMethods.ReturnType
- Resources.HttpMethods.Parameters.Name
- Resources.HttpMethods.Parameters.Type
- Resources.HttpMethods.Parameters.Usage
- Resources.HttpMethods.Parameters.Location

- If a Link is specified then a valid absolute URL should exist for Link.Uri.
- If an HttpStatusCode is specified then a valid status code should exist for HttpStatusCode.Code
- If a Resources.HttpMethods.Sample is specified then the following are required for that object: Source, Format, Type, Direction, Value 

#### Optional (but recommended)
- Description
- Links
- HttpStatusCodes
- MediaTypeFormatters.Description
- Resources.HttpMethods.Description
- Resources.HttpMethods.HttpStatusCodes
- Resources.HttpMethods.Links
- Resources.HttpMethods.Samples
- Resources.HttpMethods.Samples.Name
- Resources.HttpMethods.Parameters
- Resources.HttpMethods.Parameters.Description
- Resources.HttpMethods.Parameters.AcceptedValues

#### Field Descriptions

##### Version : string
A string representation of the version for the services represented in the SOS document.

##### MediaTypeFormatters : MediaTypeFormatter[]
An array of media type formatters that are supported by the services represented in the SOS document.

##### MediaTypeFormatters.Description : string
A description explaining what media type is being supported.

##### MediaTypeFormatters.SupportedMediaTypes : string[]
An array of strings whos value are the media types (MIME types) that are supported by the services represented in the SOS document.

##### Description : string
A desription explaining, in a global way, what the function of the services do for services represnted in the SOS document.

##### Links : Link[]
A list of links that a developer can use to gain more context or more information outside the scope of what is discussed in the SOS document.

##### Links.Description : string
A description for the link explaining what the link is for.

##### Links.Uri : string
The actual uri for which the link will resolve.

##### HttpStatusCodes : HttpStatusCode[]
An array of status code objects that represent status code return types, a description of why a developer might recieve that type, and an error code (if one exists) for said response.

##### HttpStatusCode.StatusCode : integer
The actual http status code that a developer may expect as a result of making a request to a service represented in the SOS document.

##### HttpStatusCode.Description : string
A description explaining why a developer may get a specific status code returned.

##### HttpStatusCode.ErrorCode : string
An error code that may help provide specific context around a status code response received by a developer.

##### Resources : Resource[]
A logical group of endpoints that represent or speak to the same aggregate root or root resource.

##### Resoures.BaseUri : string
The base uri for which all endpoints will start with.  This is the uri for the aggregate root or root resource. This may be relative or absolute.

##### Resources.HttpMethods : HttpMethod[]
An array of HttpMethod objects that represent all of the endpoints for said resource.

##### Resources.HttpMethods.FullUri : string
The uri for the HttpMethod with all query string values included. This may be absolute or relative. If this is relative then it should be relative to Resources.BaseUri.

##### Resources.HttpMethods.Verb : string
The http verb (or http method) that is associated to the endpoint uri for which this HttpMethod should be invoked.

##### Resources.HttpMethods.ReturnType : string
The return type that a developer can expect as a result of successfully executing a request against said HttpMethod.

##### Resources.HttpMethods.Description : string
A description of what the respective endpoint does upon being invoked.

##### Resources.HttpMethods.HttpStatusCodes : HttpStatusCode[]
An array of status code objects that represent status code return types, a description of why a developer might recieve that type, and an error code (if one exists) for said response.

##### Resources.HttpMethods.Links
A list of links that a developer can use to gain more context or more information outside the scope of what is discussed in the SOS document.

##### Resources.HttpMethods.Samples : Sample[]
An array of sample objects that give the developer example or sample data about input parameters for the respective HttpMethod. This can contain anythng from a JSON object to something like a callback uri for more data.

##### Resources.HttpMethods.Samples.Source : string
The soure for which the sample is attempting to provide context to. Supported types include:
- Body: Tell the developer that the sample they are looking at is in the post body.
- Header: Tell the developer that the sample they are looking at is in a header.
- Cookie: Tell the developer that the sample they are looking at is in a cookie.
- Uri: Tell the developer that the sample they are looking at is in the url.

This value can be extended to include other source types if you wish.

##### Resources.HttpMethods.Samples.Format : string
The format for which the sample is attempting to provide context to. Supported types include:
- String: Tell the developer that the sample they are looking at is a string value with no known format.
- Json: Tell the developer that the sample they are looking at is a valid json object string.
- Xml: Tell the developer that the sample they are looking at is a valid xml object string.
- Xsd: Tell the developer that the sample they are looking at is a valid xsd string.

This value can be extended to include other format types if you wish.

##### Resources.HttpMethods.Samples.Type : string
The actual type of sample that you are providing the developer. Supported types include:
- CallbackUri: Tell the developer that the sample they are looking at is going to be a callback uri which has to be executed to get sample value.
- PlainText: Tell the developer that the sample they are looking at is an actual sample in plain text.

This value can be extended to include other types if you wish.

##### Resources.HttpMethods.Samples.Direction : string
The direction for which the sample is attempting to represent. Supported types include:
- Request: Tell the developer that the sample they are looking at is with respect to the request.
- Response: Tell the developer that the sample they are looking at is with respect to the response.

##### Resources.HttpMethods.Samples.Value : string
The actual value for the sample. This can vary based on the type of sample attempting to provide information for.

##### Resources.HttpMethods.Samples.Name : string
The name, if applicable, for the parameter that the sample is attempting to provide information for.

##### Resources.HttpMethods.Parameters : Parameter[]
Input paramters for the respective HttpMethod that the developer can expect. 

##### Resources.HttpMethods.Parameters.Name : string
The name of the parameter to help give context to the input parameter being described.

##### Resources.HttpMethods.Parameters.Type : string
The type of the parameter being described.

##### Resources.HttpMethods.Parameters.Usage : string
A type that tells the developer if the parameter is required, optional, conditional, or outboundonly. Supported types include:
- Optional: Tell the developer that the target parameter is optional.
- Required: Tell the developer that the target parameter is required.
- Conditional: Tell the developer that the target parameter is required under certain conditions.
- OutboundOnly: Tell the developer that the target parameter is always on a response and never accepted on the request.

This value can be extended to include other types if you wish.

##### Resources.HttpMethods.Parameters.Location : string
A type that tells the developer where they can expect to insert the parameter. Supported types include:
- Header: Tell the developer that the target parameter is located in the header.
- BaseUri: Tell the developer that the target parameter is located in the base uri (not the query string).
- Querystring Tell the developer that the target parameter is located in the query string (not the base uri).
- Cookie: Tell the developer that the target parameter is located in a cookie. This type is to provide a more specific location even though a cookie is technially contained within a header.
- Body: Tell the developer that the target parameter is located in the post body.

This value can be extended to include other types if you wish.

##### Resources.HttpMethods.Parameters.Description : string
A description to provide the developer with more context as to what the parameter represents and what its function is.

##### Resources.HttpMethods.Parameters.AcceptedValues : string[]
An array of strings indicating to the developer that there is a finite number of acceptable inputs for the target parameter. This is very useful for enum types.
