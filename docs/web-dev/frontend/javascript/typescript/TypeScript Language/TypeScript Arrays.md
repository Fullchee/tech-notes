

## Spot the bug

```typescript
function addTriple(inputs: number[]): number {
  return inputs[0] + inputs[1] + inputs[2];
}
```

>[!Spot the bug]-
>Passing `inputs` with two elements
>TypeScript won't catch that bug

