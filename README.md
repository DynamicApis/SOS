# DynamicApis - SimpleRest Open Standard (SOS)
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

The goal of SOS is much more than simply creating a json document to power a single user interface designed by the SOS creators. It is the belief of the founders of DynamicApis.com that service documentation format should be simple and powerful. 
Documentation should be very easy for a developer to read and quickly make sense of in its raw format and should certainly be flexible and simple enough to be easily leveraged by ANY modern user interface.

## References
[Http Status Codes](http://en.wikipedia.org/wiki/List_of_HTTP_status_codes)

[Http Media Types](http://en.wikipedia.org/wiki/Internet_media_type)

[Http Verbs](http://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol#Request_methods)

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

#### Optional (but recommended)
- Description
- Links
- HttpStatusCodes
- MediaTypeFormatters.Description
- Resources.HttpMethods.Description
- Resources.HttpMethods.HttpStatusCodes
- Resources.HttpMethods.Links
- Resources.HttpMethods.ReturnType
- Resources.HttpMethods.Samples
- Resources.HttpMethods.Parameters
- Resources.HttpMethods.Parameters.Description
- Resources.HttpMethods.Parameters.AcceptedValues

#### Description
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
##### HttpStatusCodes
##### Resources
##### Resoures.BaseUri
##### Resources.HttpMethods
##### Resources.HttpMethods.FullUri
##### Resources.HttpMethods.Verb
##### Resources.HttpMethods.ReturnType
##### Resources.HttpMethods.Description
##### Resources.HttpMethods.HttpStatusCodes
##### Resources.HttpMethods.Links
##### Resources.HttpMethods.ReturnType
##### Resources.HttpMethods.Samples
##### Resources.HttpMethods.Parameters
##### Resources.HttpMethods.Parameters.Name
##### Resources.HttpMethods.Parameters.Type
##### Resources.HttpMethods.Parameters.Usage
##### Resources.HttpMethods.Parameters.Location
##### Resources.HttpMethods.Parameters.Description
##### Resources.HttpMethods.Parameters.AcceptedValues
