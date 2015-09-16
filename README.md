<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [node-p360](#node-p360)
  - [SIF documentation](#sif-documentation)
  - [Usage](#usage)
  - [Examples](#examples)
    - [Search private persons](#search-private-persons)
    - [Search contact persons](#search-contact-persons)
    - [Create contact person](#create-contact-person)
    - [Create case](#create-case)
    - [Update case](#update-case)
    - [Create document](#create-document)
    - [UpdateDocument](#updatedocument)
    - [GetDocuments](#getdocuments)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

[![Build Status](https://travis-ci.org/telemark/node-p360.svg?branch=master)](https://travis-ci.org/telemark/node-p360)
[![js-standard-style](https://img.shields.io/badge/code%20style-standard-brightgreen.svg?style=flat)](https://github.com/feross/standard)

# node-p360
Node module for Public 360

## SIF documentation

SI Integration Framework (SIF) is public 360s SOAP-webservice.

For a full list of calls and callbacks see the documentation  [here](https://github.com/telemark/skoleskyss-arbeid/blob/master/biztalk/GenericWebServiceLayer.pdf)

## Usage

```javascript
var p360 = require('node-p360')
var config = require('./config')
var args = { 'parameter': { 'Name': 'Geir' } }
var clientMethod = 'GetContactPersons'

var options = {
  'p360': config.p360,
  'clientMethod': clientMethod,
  'args': args
}

p360(options, function (error, data) {
  if (error) {
    console.error(JSON.stringify(error))
  } else {
    console.log(JSON.stringify(data))
  }
})
```

## Examples

### Search private persons
```javascript
var clientMethod = 'GetPrivatePersons'
var args = {
  'parameter': {
    'Name': 'Geir',
    'PersonalIdNumber': '',
    'Recno': ''
  }
}
```

**Result:**
```javascript
{
    "GetPrivatePersonsResult": {
        "Successful": true,
        "PrivatePersons": {
            "PrivatePersonBase": [
                {
                    "Email": "hallgeir.hall@t-fk.no",
                    "FirstName": "Hallgeir",
                    "LastName": "Hall",
                    "MobilePhone": "+47 90 00 00 00",
                    "PersonalIdNumber": "",
                    "PrivateAddress": {
                        "Area": "TELEMARK",
                        "Country": "NOR",
                        "County": "SELJORD",
                        "State": "",
                        "StreetAddress": "Hygdedalen 42",
                        "ZipCode": "3840",
                        "ZipPlace": "SELJORD"
                      }
                }
            ]
        }
    }
}
```

### Search contact persons
```javascript
var clientMethod = 'GetContactPersons'
var args = {
  'parameter': {
    'Name': 'Geir',
    'PersonalIdNumber': '',
    'Recno': ''
  }
}
```

**Result:**
```javascript
{
    "GetContactPersonsResult": {
        "Successful": true,
        "ContactPersons": {
            "ContactPersonBase": [
                {
                    "Email": "Geir.Gasodden@t-fk.no",
                    "ExternalId": "",
                    "FirstName": "Geir",
                    "LastName": "Gåsodden",
                    "MobilePhone": "+47 95 55 27 59",
                    "PrivateAddress": {
                        "Area": "",
                        "Country": "NOR",
                        "County": "",
                        "State": "",
                        "StreetAddress": "",
                        "ZipCode": "",
                        "ZipPlace": ""
                    }
                },
                {
                    "Email": "geir.grastein@t-fk.no",
                    "ExternalId": "",
                    "FirstName": "Geir",
                    "LastName": "Gråstein",
                    "MobilePhone": "+47 93 00 00 00",
                    "PrivateAddress": {
                        "Area": "",
                        "Country": "NOR",
                        "County": "",
                        "State": "",
                        "StreetAddress": "",
                        "ZipCode": "",
                        "ZipPlace": ""
                    }
                }
            ]
        }
    }
}
```

### Create contact person
```javascript
var clientMethod = 'SynchronizeContactPerson'
var args = {
  'parameter': {
    'FirstName': 'Halvard',
    'MiddleName': 'Ivar',
    'LastName': 'Fotfjes',
    'PersonalIdNumber': '14059733381',
    'Email': 'halvard.fotfjes@t-fk.no',
    'PrivateAddress': {
      'Country': 'NOR',
      'StreetAddress': 'Lovestreet 42',
      'ZipCode': '1337',
      'ZipPlace': 'Telemark'
    }
  }
}
```

**Result:**

### Create case
```javascript
var clientMethod = 'CreateCase'
var args = {
  'parameter': {
    'Title': 'Sakstittel',
    'UnofficialTitle': 'Uoffisiell sakstittel',
    'Status': 'B', // Under behandling
    'SubArchive': '200052', // Codetable: Noark subarchive
    'AccessCode': '13', // Codetable: Accesscode
    'AccessGroup': 'Gruppenavn', // Tilgangsgruppe navn
    'Paragraph': 'Offl §13 jfr Fvl §13', // Codetable: Paragraph
    'ArchiveCodes': {
      0: {
        'Sort': '1',
        'ArchiveType': 'FAGKODE PRINSIPP', // Codetable: Noark classification
        'ArchiveCode': 'N06' // Codetable: Noark classification code
      },
      1: {
        'Sort': '2',
        'ArchiveType': 'Fnr', // Codetable: Noark classification
        'ArchiveCode': '14059733381',
        'IsManualText': 'False'
      }
    },
    'Keywords': 'Stikkord',
    'Contacts': {
      0: {
        'ReferenceNumber': '14059733381',
        'Role': '9', // Codetable: Contact - Case Role
      }
    },
    'ResponsiblePersonIdNumber': '',
    'ResponsibleEnterpriseRecno': '213419' // Recnr ansvarlig virksomhet
  }
}
```

**Result:**

### Update case
```javascript
var clientMethod = 'UpdateCase'
var args = {
  'parameter': {
    'CaseNumber': '15/13742',
    'Title': 'Ny sakstittel'
  }
}
```

**Result:**

### Create document
```javascript
var clientMethod = 'CreateDocument'
var args = {
  'parameter': {
    'Title': 'Dokument tittel',
    'Archive': '2', // Codetable: Document archive
    'Status': '6', // Codetable: Document status
    'Category': '110', // Codetable: Document category
    'ResponsiblePersonRecno': '', // Recnr ansvarlig person
    'ResponsibleEnterpriseRecno': '213419', // Recnr ansvarlig virksomhet
    'Contacts': {
      0: {
        'ReferenceNumber': '14059733381', // Personnummer
        'Role': '5' // Mottaker
      }
    },
    'SendersReference': '',
    'AccessCode': '13', // Codetable: Accesscode
    'Paragraph': 'Offl §13 jfr Fvl §13', // Codetable: Paragraph
    'AccessGroup': 'Gruppenavn', // Codetable: Tilgangsgruppe navn
    'Files': {
      0: {
        'Title': 'Fil tittel',
        'Format': 'PDF', // Codetable: File format
        'Base64Data': data, // Must be base64 encoded
        'VersionFormat': 'A', // Codetable: File status
        'Category': '1' // Codetable: File category
      }
    }
  }
}
```
**Result:**

### UpdateDocument

**Result:**

### GetDocuments

**Result:**
