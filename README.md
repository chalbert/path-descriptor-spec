# Path Descriptor Spec

Spec that defines how to represent the path of a change on a JavaScript object tree.

## Change triggered

| Change | Descriptor |
| --- | --- |
| value = 'change' | `value` |
| ['value-1'] = 'change' | `'value-1'` |
| [Symbol('test')] = 'change' | `Symbol(test)` |
| model.value = 'change' | `model.value` |
| model['value-1'] = 'change' | `model.'value-1'` |
| model[Symbol('test')] = 'change' | `model.Symbol(test)` |
| model.list = ['change'] | `model.list` |
| model.list.push('change2') | `model.list[1]` |
| model.list.splice(2, 1) | `model.list[2...]` |
| model.list.splice(-2, 2) | `model.list[..3]` |

## Change listened

| Descriptor | Changes |
| --- | --- |
