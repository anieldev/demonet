# Remix

<br>

## Route templates

<br>

### Some route with data

```tsx

// someRoute.tsx

import { json } from "@remix-run/node";
import type { LoaderFunction } from "@remix-run/node";
import { useLoaderData } from "@remix-run/react";


type LoaderData = { name: String };


export const loader: LoaderFunction = async () => {
  const data: LoaderData = {
    name: "Jane Doe"
  };
  // The `json` function converts a serializable object into a JSON response
  // All loaders must return a `Response` object.
  return json(data);
};


export default function SomeRouteComponent() {
  const data = useLoaderData<LoaderData>();
  return (
    <div>
      <h1>Hello {data.name}!</h1>
      <p>This is the component that will render when the route matches.</p>
    </div>
  );
}
```
