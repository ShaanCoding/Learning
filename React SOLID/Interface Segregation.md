# Interface Segregation Principle

- Clients should not be forced to depend upon interfaces that they do not use.
  - In other words, don't add too much to an interface, split it up into separate interfaces.

In react: Components should not be forced to depend upon props that they do not use.

## Example

- Imagine we have a products list that contains cards, each card has a product image, name, price, and rating.
- For the image component we may have the input prop that has the interface of Product and it contains the image url, name, price, and rating.
  - This is not a good practice as we are forcing the image component to depend on props that it does not use.
  - We should instead make the image component depend on the image url only.

```ts
import { IProduct } from "./product";

interface IThumbnailProps {
  // product: IProduct;
  imageUrl: string;
}

export function Thumbnail(props: IThumbnailProps) {
  // const { product } = props;
  const { imageUrl } = props;

  return (
    <img className="p-8 rounded-t-lg h-48" src={imageUrl} alt="product image" />
  );
}
```
