# Liskov Substitution Principle

- Listov Substitution Principle states that if you have a parent class and a child class, then the parent class can be substituted by its child class without affecting the functionality of the program.
  - In other words, if you have a class that implements an interface, then you should be able to swap that class with a subclass of it without breaking the code that uses it.

## Example

- Imagine we had a search function that takes a search term and returns a list of results.
  - We can implement this function using an interface that defines the shape of the search function.
    - This way we can implement this function in different ways and we can swap the implementation without breaking the code that uses it.

```ts
import cx from "clsx";

interface ISearchInputProps
  extends React.InputHTMLAttributes<HTMLInputElement> {
  isLarge?: boolean;
}

export function SearchInput(props: ISearchInputProps) {
  const { value, onChange, isLarge, ...restProps } = props;

  return (
    <div className="flex w-10/12">
      <div className="relative w-full">
        <div className="flex absolute inset-y-0 left-0 items-center pl-3 pointer-events-none">
          <svg
            aria-hidden="true"
            className="w-5 h-5 text-gray-500 dark:text-gray-400"
            fill="none"
            stroke="currentColor"
            viewBox="0 0 24 24"
            xmlns="http://www.w3.org/2000/svg"
          >
            <path
              strokeLinecap="round"
              strokeLinejoin="round"
              strokeWidth="2"
              d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z"
            ></path>
          </svg>
        </div>
        <input
          type="search"
          id="default-search"
          className={cx(
            "block p-4 pl-10 w-full text-sm text-gray-900 bg-gray-50 rounded-lg border border-gray-300 focus:ring-blue-500 focus:border-blue-500 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500 outline-none",
            isLarge && "text-3xl"
          )}
          placeholder="Search for the right one..."
          required
          value={value}
          onChange={onChange}
          {...restProps}
        />
      </div>
    </div>
  );
}
```

- Need to make sure that the SearchInput component is not tightly coupled to the implementation of the search function.

  - We can do this by using an interface that defines the shape of the search function.
    - This way we can implement this function in different ways and we can swap the implementation without breaking the code that uses it.

- Liskov feels like a more specific version of the Open Closed Principle.
  - Open Closed Principle states that you should be able to extend a class's behavior without modifying it.
  - Liskov Substitution Principle states that you should be able to replace a class with its subclass without breaking the code that uses it.
    - This is a more specific version of the Open Closed Principle.
