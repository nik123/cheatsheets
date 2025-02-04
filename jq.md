# jq

```
# Pretty-printing
cat in.json | jq '.'

# filter a single field:
cat in.json | jq '.fieldname'

# Gat first element of from the field 'array':
cat in.json | jq '.array[0]' 
```
