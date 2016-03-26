# Path Descriptor Spec

Spec that defines how to represent the path of a change on a JavaScript object tree.

## Change triggered

| Change | Descriptor |
| --- | --- |
| value = 'change' | `value` |
| ['value-1'] = 'change' | `'value-1'` |
| [Symbol('sym')] = 'change' | `Symbol(sym)` |
| model.value = 'change' | `model.value` |
| model['value-1'] = 'change' | `model.'value-1'` |
| model[Symbol('sym')] = 'change' | `model.Symbol(sym)` |
| model.list = ['change'] | `model.list` |
| model.list.push('change2') | `model.list[1]` |
| model.list.splice(2, 1) | `model.list[2...]` |
| model.list.splice(1, 2, 'change3', 'change3') | `model.list[1-2]` |
| model.list[0] = {} | `model.list[0]` |
| model.list[0].value = 'change' | `model.list[0].value` |
| model.list[0]['value-1'] = 'change' | `model.list[0].'value-1` |
| model.list[0][Symbol('sym')] = 'change' | `model.list[0].Symbol(test) |

## Multiple changes triggered

## Change listened
| Change | Descriptor |
| --- | --- |
| value1 = 'change1', value2 = 'change2' | `{value1, value2}` |
| value1 = 'change1', ['value-2'] = 'change2' | `{value1, 'value-2'}` |
| value1 = 'change1', [Symbol('sym')] = 'change2' | `{value1, Symbol(sym)}` |
| model.value1 = 'change1', model.value2 = 'change2' | `model{value1, value2}` |

| Descriptor | Changes |
| --- | --- |
