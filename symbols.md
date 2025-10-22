```note
- Use can use either json or yaml to customize your snippets (but be careful with "" and indent when using yaml
- If any of the field (e.g. description) is set to empty "" or [], then the default value will be used
- Everything in the note section will be saved
- Avoid putting a comma in the end of the json file
```

```json
[
  {
    "name": "\\int",
    "snippet": "\\int_{@1@}^{@2@}",
    "description": "",
    "examples": "",
    "see_also": []
  },
  {
    "name": "\\sum",
    "snippet": "\\sum_{@1@}^{@2@}",
    "description": "",
    "examples": "",
    "see_also": []
  }
]
