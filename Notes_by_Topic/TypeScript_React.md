# TypeScript + React

## Interfaces

- Create `Interfaces.ts` file to include interfaces and export to use in components

## Type for Event Handlers

### Type for onChange Event

```ts
import { ChangeEvent } from 'react';
const handleChange = (e: ChangeEvent<HTMLInputElement>) => {};
```

### Type for onSubmit Event

```ts
import { FormEvent } from 'react';
const onSubmit = (e: FormEvent<HTMLFormElement>) => {
  e.preventDefault();
};
```
