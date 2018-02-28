# 🇫🇷 French Social Security Number Parser

[![tested with jest](https://img.shields.io/badge/tested_with-jest-99424f.svg)](https://github.com/facebook/jest) [![npm version](https://badge.fury.io/js/french-ssn.svg)](http://badge.fury.io/js/french-ssn) [![CircleCI Build Status](https://circleci.com/gh/aymericbouzy/french-ssn.svg?style=shield)](https://circleci.com/gh/aymericbouzy/french-ssn) [![codecov](https://codecov.io/gh/aymericbouzy/french-ssn/branch/master/graph/badge.svg)](https://codecov.io/gh/aymericbouzy/french-ssn)

"A la carte" parsing, validation and creation of French Social Security Numbers.

## Installation

```sh
yarn add french-ssn
```

or

```sh
npm i --save french-ssn
```

## Usage

```js
import { parse, isValid, getControlKey } from "french-ssn"

parse("2 55 08 14 168 025 38")
/*
{
  gender: {
    name: 'female',
    title: 'Mme',
  },
  approximateAge: 62,
  birth: {
    month: {
      name: 'août',
      index: 8
    },
    year: 1955,
    approximateDate: 1955-08-17T00:00:00.000Z,
    country: {
      insee: '100',
      name: 'France'
    },
    county: {
      insee: '14',
      name: 'Calvados'
    },
    city: {
      postalCode: '14710',
      name: 'COLOMBIERES',
      insee: '14168'
    }
  }
}
*/

isValid("2 55 08 14 168 025 12") // false
isValid("2 55 08 14 168 025 38") // true
getControlKey("2 55 08 14 168 025") // 38
```

## Api

| Method | arguments | returned value | throws |
| ------ | --------- | -------------- | ------ |
| `parse` | `ssn: string \| number` : You may provide your ssn in various formats : a number with 15 digits, a string, with or without spaces, or any other delimiting character | an object containing information about the ssn owner | will throw if ssn is not correctly formated or if control key does not match. Will not throw if information provided does not make sense, information will simply be marked as "unknown". Eg: `parse("0 ...").gender = { unknown: true }` |
| `isValid` | `ssn: string \| number` | `boolean` (this is only a convenience function, it calls `parse` under the hood in a try catch block) | never |
| `getControlKey` | `partialSSN: string \| number` : The first 13 characters of the ssn | `string` : the control key (2 digits between "01" and "97") | will throw if ssn is not correctly formated |

## Features

* Corsica (2A, 2B)
* DOM-TOM
* Birth in Foreign countries
* Birth in Algeria before 1962
* Birth in Morocco or Tunisia before 1964
* No dependencies (only dev dependencies)

## Limitations

This package loads in memory the name and postal code of 39k+ French towns. You should probably not try to send this package client side.

## Contributing

Please fork this package, and run

```sh
yarn install
yarn test
```

## Issues

Something is not working as expected? Some data is wrong? Documentation is missing? You need a different feature / API? Please file an [issue](https://github.com/aymericbouzy/french-ssn/issues/new), we'll be in touch.

## References

(in French)

* [http://xml.insee.fr/schema/nir.html](http://xml.insee.fr/schema/nir.html)
* [https://www.service-public.fr/particuliers/vosdroits/F33078](https://www.service-public.fr/particuliers/vosdroits/F33078)
* [https://www.wikiberal.org/w/images/1/1a/Num%C3%A9ro_de_S%C3%A9curit%C3%A9_sociale.pdf](https://www.wikiberal.org/w/images/1/1a/Num%C3%A9ro_de_S%C3%A9curit%C3%A9_sociale.pdf)
* [https://public.opendatasoft.com/explore/dataset/correspondance-code-insee-code-postal/](https://public.opendatasoft.com/explore/dataset/correspondance-code-insee-code-postal/)

## Financial Support

Gofer 🤝 (the human-centric work-on-demand solution) is the main support of this package.
