# Open Closed Principle

- Software entities (classes, modules, functions, etc.) should be open for extension, but closed for modification.
  - In other words, you should strive to write code that doesn't have to be modified every time the requirements change.

## Example

```ts
import {
  HiOutlineArrowNarrowRight,
  HiOutlineArrowNarrowLeft,
} from "react-icons/hi";

interface IButtonProps extends React.ButtonHTMLAttributes<HTMLButtonElement> {
  text: string;
  role?: "back" | "forward" | "main" | "not-found";
  icon?: React.ReactNode;
}

export function Button(props: IButtonProps) {
  const { text, role, icon } = props;

  return (
    <button
      className="flex items-center font-bold outline-none pt-4 pb-4 pl-8 pr-8 rounded-xl bg-gray-200 text-black"
      {...props}
    >
      {text}
      <div className="m-2">
        {/* {role === "forward" && <HiOutlineArrowNarrowRight />}
        {role === "back" && <HiOutlineArrowNarrowLeft />} */}
        {icon}
      </div>
    </button>
  );
}
```

- In this button example we have a button that has a role prop that can be either "back" or "forward" and based on that role we render a different icon.
  - To extend this role adding a new one, to add a new role we would have to modify the Button component and add a new condition to the if statement.
    - This is not a good practice as we are modifying the component instead of extending it.
- To solve this we can extend this and use an icon prop that will receive a ReactNode and we can pass any icon we want to it.
  - This way we are extending the component instead of modifying it.
