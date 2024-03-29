# 💎 Prisma Class Validator

Automatically generator `class-validator` schema from Prisma client projects.

<!-- prettier-ignore-start -->
|   | Status |
| - | - |
| Build | [![Node CI](https://github.com/koj-co/prisma-class-validator/workflows/Node%20CI/badge.svg)](https://github.com/koj-co/prisma-class-validator/actions?query=workflow%3A%22Node+CI%22) [![Dependencies](https://img.shields.io/librariesio/github/koj-co/prisma-class-validator)](https://libraries.io/github/koj-co/prisma-class-validator) [![GitHub release (latest by date)](https://img.shields.io/github/v/release/koj-co/prisma-class-validator)](https://github.com/koj-co/prisma-class-validator/releases) [![Snyk Vulnerabilities for GitHub Repo](https://img.shields.io/snyk/vulnerabilities/github/koj-co/prisma-class-validator)](https://snyk.io/test/github/koj-co/prisma-class-validator) |
| Health | [![License CI](https://github.com/koj-co/prisma-class-validator/workflows/License%20CI/badge.svg)](https://github.com/koj-co/prisma-class-validator/actions?query=workflow%3A%22License+CI%22) [![CLA Assistant](https://github.com/koj-co/prisma-class-validator/workflows/CLA%20Assistant/badge.svg)](https://github.com/koj-co/prisma-class-validator/actions?query=workflow%3A%22CLA+Assistant%22) [![Pull Request Labeler](https://github.com/koj-co/prisma-class-validator/workflows/Pull%20Request%20Labeler/badge.svg)](https://github.com/koj-co/prisma-class-validator/actions?query=workflow%3A%22Pull+Request+Labeler%22) |
| PRs | [![PR Generator CI](https://github.com/koj-co/prisma-class-validator/workflows/PR%20Generator%20CI/badge.svg)](https://github.com/koj-co/prisma-class-validator/actions?query=workflow%3A%22PR+Generator+CI%22) [![Merge PRs](https://github.com/koj-co/prisma-class-validator/workflows/Merge%20PRs/badge.svg)](https://github.com/koj-co/prisma-class-validator/actions?query=workflow%3A%22Merge+PRs%22) |
<!-- prettier-ignore-end -->

At Koj, we use this package to automatically generate [`@koj/types`](https://www.npmjs.com/package/@koj/types) from our Prisma schema.

## ⭐️ Features

The `readAndGenerateClassValidator` method reads your generated Prisma client (after running `npx prisma generate`) and automatically generates a class-validator schema.

First, install from npm:

```bash
npm install --save-dev prisma-class-validator
```

Usage with TypeScript/Node.js:

```ts
import { readAndGenerateClassValidator } from "prisma-class-validator";
import { writeFile } from "fs/promises";

(async () => {
  const schema = await readAndGenerateClassValidator();
  await writeFile("validator.ts", schema);
})();
```

Usage with JavaScript/Node.js:

```js
const { readAndGenerateClassValidator } = require("prisma-class-validator");
const { writeFile } = require("fs/promises");

(async () => {
  const schema = await readAndGenerateClassValidator();
  await writeFile("validator.ts", schema);
})();
```

## 💻 Example

The `generateClassValidatorFromPrismaClient` method is used to take a string consisting of generated Prisma schema and converting it to class-validator. In this case, you are expected to read the generated Prisma schema `index.d.ts` file and supply that as the input.

<details>
  <summary>Example input</summary>

```ts
generateClassValidatorFromPrismaClient(`
  /**
   * Client
  **/
  
  import * as runtime from '@prisma/client/runtime';
  
  
  /**
   * Model Lead
   */
  
  export type Lead = {
    browser: string | null
    city: string | null
    countryCode: string | null
    createdAt: Date
    email: string
    id: number
    name: string
    operatingSystem: string | null
    region: string | null
    responses: Prisma.JsonValue | null
    timezone: string | null
    updatedAt: Date
  }
  
  /**
   * Model User
   */
  
  export type User = {
    active: boolean
    attributes: Prisma.JsonValue | null
    checkLocationOnLogin: boolean
    countryCode: string
    createdAt: Date
    gender: Gender
  }

  /**
   * Enums
   */

  // Based on
  // https://github.com/microsoft/TypeScript/issues/3192#issuecomment-261720275

  export const Gender: {
    FEMALE: 'FEMALE',
    MALE: 'MALE',
    NONBINARY: 'NONBINARY',
    UNKNOWN: 'UNKNOWN'
  };

  export type Gender = (typeof Gender)[keyof typeof Gender]
`);
```

</details>

<details>
  <summary>Resulting output</summary>

```ts
`/**
 * DO NOT EDIT THIS FILE MANUALLY
 * ==============================
 *
 * This file is automatically generated by Prisma Class Validator using @prisma/client
 * Source: https://github.com/koj-co/prisma-class-validator/blob/HEAD/scripts/generate-types.ts
 */

import {
  IsOptional,
  IsString,
  IsNumber,
  IsNotEmpty,
  IsBoolean,
  IsObject,
  IsDateString,
  IsIn,
} from "class-validator";

/**
 * Model Lead
 */

export class Lead {
  @IsString()
  @IsOptional()
  browser?: string | null;

  @IsString()
  @IsOptional()
  city?: string | null;

  @IsString()
  @IsOptional()
  countryCode?: string | null;

  @IsDateString()
  @IsNotEmpty()
  createdAt!: Date;

  @IsString()
  @IsNotEmpty()
  email!: string;

  @IsNumber()
  @IsNotEmpty()
  id!: number;

  @IsString()
  @IsNotEmpty()
  name!: string;

  @IsString()
  @IsOptional()
  operatingSystem?: string | null;

  @IsString()
  @IsOptional()
  region?: string | null;

  @IsObject()
  @IsOptional()
  responses?: any | null;

  @IsString()
  @IsOptional()
  timezone?: string | null;

  @IsDateString()
  @IsNotEmpty()
  updatedAt!: Date;
}

/**
 * Model User
 */

export class User {
  @IsBoolean()
  @IsNotEmpty()
  active!: boolean;

  @IsObject()
  @IsOptional()
  attributes?: any | null;

  @IsBoolean()
  @IsNotEmpty()
  checkLocationOnLogin!: boolean;

  @IsString()
  @IsNotEmpty()
  countryCode!: string;

  @IsDateString()
  @IsNotEmpty()
  createdAt!: Date;
  
  @IsString()
  @IsIn(["FEMALE", "MALE", "NONBINARY", "UNKNOWN"])
  @IsNotEmpty()
  gender!: Gender;
}

/**
 * Enums
 */

// Based on
// https://github.com/microsoft/TypeScript/issues/3192#issuecomment-261720275

export let Gender: {
  FEMALE: "FEMALE";
  MALE: "MALE";
  NONBINARY: "NONBINARY";
  UNKNOWN: "UNKNOWN";
};

export type Gender = typeof Gender[keyof typeof Gender];`;
```

</details>

## 📄 License

[MIT](./LICENSE) © [Koj](https://koj.co)

<p align="center">
  <a href="https://koj.co">
    <img width="44" alt="Koj" src="https://kojcdn.com/v1598284251/website-v2/koj-github-footer_m089ze.svg">
  </a>
</p>
<p align="center">
  <sub>An open source project by <a href="https://koj.co">Koj</a>. <br> <a href="https://koj.co">Furnish your home in style, for as low as CHF175/month →</a></sub>
</p>
