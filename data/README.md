# Dataset access

The original project used a local `trash_images/` directory containing six labeled class folders: `cardboard`, `glass`, `metal`, `paper`, `plastic`, and `trash`. These 2,527 images are not redistributed here because the original dataset files and their distribution permissions have not been provided.

To run the experiments, place the dataset at the repository root as:

```text
trash_images/
  cardboard/
  glass/
  metal/
  paper/
  plastic/
  trash/
```

Original observed class counts: cardboard 403, glass 501, metal 410, paper 594, plastic 482, trash 137. Use the same source/version and check the class counts before comparing published metrics.
