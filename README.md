# Prisma DMMF Extended

An extension library for Prisma's DMMF (Data Model Meta Format) that provides bidirectional conversion between Prisma schema and DMMF.

## Features

- Convert Prisma schema to DMMF (`schemaToDmmf`)
- Convert DMMF back to Prisma schema (`dmmfToSchema`)
- Handle ZenStack syntax and extensions
- Error handling utilities

## Installation

```bash
npm install @mohammed-bahumaish/prisma-dmmf-extended
# or
yarn add @mohammed-bahumaish/prisma-dmmf-extended
# or
pnpm add @mohammed-bahumaish/prisma-dmmf-extended
```

## Usage

```typescript
import { schemaToDmmf, dmmfToSchema } from '@mohammed-bahumaish/prisma-dmmf-extended';

// Convert Prisma schema to DMMF
const prismaSchema = `
  datasource db {
    provider = "postgresql"
    url      = env("DATABASE_URL")
  }
  
  model User {
    id    Int     @id @default(autoincrement())
    email String  @unique
    name  String?
  }
`;

async function example() {
  // Schema to DMMF
  const { datamodel, config } = await schemaToDmmf(prismaSchema);
  console.log('DMMF:', datamodel);
  
  // DMMF back to schema
  const formattedSchema = await dmmfToSchema({
    dmmf: datamodel,
    config: config
  });
  console.log('Schema:', formattedSchema);
}

example();
```

## Project Structure

- `/src` - Source code
  - `index.ts` - Main exports
  - `dmmfToSchema.ts` - Converts DMMF to Prisma schema
  - `schemaToDmmf.ts` - Converts Prisma schema to DMMF
  - `processLine.ts` - Processes schema lines during conversion
  - `handleError.ts` - Error handling utilities
  - `/util` - Utility functions
    - `parser.ts` - Schema parsing utilities

## Development

```bash
# Install dependencies
npm install

# Build the project
npm run build

# Run tests
npm test

# Development with watch mode
npm run dev
```

## License

MIT # prisma-dmmf-extended
