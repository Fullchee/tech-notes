## Number input

<iframe width="360" height="360" src="https://www.youtube.com/embed/nnZS761ngXE" title="Number-only inputs aren&#39;t so straight-forward" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

```html
<input
	type="text" <!-- or keep type="number" and hide the arrow with CSS -->
	inputmode="numeric" <!-- shows the 9 digit grid -->
	pattern="[0-9]+" <!-- typing non-digits won't do a/th in Chrome -->
	>
```


## Type validation with TS and zod

<iframe width="550" height="360" src="https://www.youtube.com/embed/9N50YV5NHaE" title="Blazing Fast Tips: Build ANYTHING with Zod + Generics" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

## FormData API
[Bytes #174 - Putting the "p" in npm](https://bytes.dev/archives/174)

```html
<form>
  <input type="text" name="name" />
  <input type="number" name="number" />
  <input type="date" name="date" />
  <button type="submit">Submit</button>
</form>
```

```ts
  const form = $('form')
  form.addEventListener('submit', (e) => {
    e.preventDefault()
    const formData = new FormData(form)
    const date: string = formData.get('date')
    const number = formData.get('number')
    // ...
  })
```

## Getting right type from the input value
```typescript
const num: number = $('input[type="number"]').valueAsNumber

const date: Date = $('input[type="date"]').valueAsDate
```