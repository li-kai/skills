---
name: typescript-tests
description:
    TypeScript testing with test.each patterns, and async handling. Use when
    writing or reviewing TypeScript tests.
---

# TypeScript Tests

See [common testing practices](../write-tests/SKILL.md) for general
philosophy.

Run tests with `pnpm test`.

## test.each

```typescript
test.each([
    ["user@gmail.com", true],
    ["invalid.com", false],
])("isValidEmail(%s) returns %s", (email, expected) => {
    expect(isValidEmail(email)).toBe(expected)
})
```

```typescript
test.each([
    { name: "empty array", input: [], expected: { sum: 0, avg: 0 } },
    { name: "single number", input: [5], expected: { sum: 5, avg: 5 } },
])("calculateStats($name)", ({ input, expected }) => {
    expect(calculateStats(input)).toEqual(expected)
})
```

### Typing with index signatures or unions

When cases use types with index signatures (e.g., `Record<string, T>`) or unions
like `boolean | SchemaObject`, TypeScript infers a union across array elements
that adds `prop?: undefined`, breaking `Record` assignability.

Fix with `test.each<T>([...] as const satisfies T[])`:

```typescript
type Case = { name: string; schema: JsonSchema; expected: JsonSchema }

test.each<Case>([
    {
        name: "string",
        schema: { type: "string" },
        expected: { type: "string" },
    },
    {
        name: "ref",
        schema: { $ref: "#/$defs/Foo" },
        expected: { type: "number" },
    },
] as const satisfies Case[])("expand($name)", ({ schema, expected }) => {
    expect(expandSchema(schema)).toEqual(expected)
})
```

- **`test.each<T>`** types the callback parameter, preventing union widening
- **`as const satisfies T[]`** narrows literals, catching typos like
  `type: "strig"` against a string literal union

Without strict types, plain `test.each([...])` is fine.

### test.for

Use `test.for` instead of `test.each` when you need `TestContext` (e.g.,
concurrent snapshot tests). Otherwise the two are equivalent.

## Structure

Keep tests flat. Use descriptive test names instead of nested describe blocks.
Only use `describe()` when you need shared `beforeEach`/`afterEach`, one level
max.

## Async and Errors

```typescript
test.each([{ url: "/users/1", expected: { id: 1 } }])(
    "fetchUser($url) returns user",
    async ({ url, expected }) => {
        expect(await fetchUser(url)).toEqual(expected)
    },
)

test.each([
    { input: null, error: "Cannot be null" },
    { input: -1, error: "Must be positive" },
])("validate($input) throws $error", ({ input, error }) => {
    expect(() => validate(input)).toThrow(error)
})
```
