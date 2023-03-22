# JSON files

The JSON loader use [JSON pointer](https://github.com/janl/node-jsonpointer) to target keys in your JSON files you want to target.

### No JSON pointer example

The most simple way of using it, is to specify no JSON pointer.
The loader will load all strings it finds in the JSON object.

Example JSON file:

```json
{
  "texts": ["This is a sentence.", "This is another sentence."]
}
```

Example code:

```typescript
import { JSONLoader } from "langchain/document_loaders";

const loader = new JSONLoader("src/document_loaders/example_data/example.json");
const docs = await loader.load();
console.log({ docs });
```

### Using JSON pointer example

You can do a more advanced scenario by choosing which keys in your JSON object you want to extract string from.

In this example, we want to only extract information from "from" and "surname" entries.

```json
{
  "1": {
    "body": "BD 2023 SUMMER",
    "from": "LinkedIn Job",
    "labels": ["IMPORTANT", "CATEGORY_UPDATES", "INBOX"]
  },
  "2": {
    "body": "Intern, Treasury and other roles are available",
    "from": "LinkedIn Job2",
    "labels": ["IMPORTANT"],
    "other": {
      "name": "plop",
      "surname": "bob"
    }
  }
}
```

Example code:

```typescript
import { JSONLoader } from "langchain/document_loaders";

const loader = new JSONLoader(
  "src/document_loaders/example_data/example.json",
  ["/from", "/surname"]
);
const docs = await loader.load();
console.log({ docs });
```