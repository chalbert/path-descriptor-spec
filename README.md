# Path Descriptor Spec

Spec that defines how to represent the path of a change on a JavaScript object tree.

Goals:

- Zero ambiguity
- Represent every change possible
- Represent multiple changes

| Type | Descriptor | (D)ispached / L(istened) |
| --- | --- | --- |
| Property | `value` | D/L |
| String property | `'value-1'` | D/L |
| Symbol property | `Symbol(name)` | D/L |
| Every properties | `{}` | L |
| Multiple properties  | `{value, 'value-1', Symbol(name)}` | D/L |
| Object property | `model.value` | D/L |
| Object string property | `model.'value-1'` | D/L |
| Object symbol property | `model.Symbol(name)` | D/L |
| Every object properties | `model{}` | L | 
| Array item change | `list[2]` | D/L |
| Array item range | `list[2...5]` | D/L |
| Array item range, open start | `list[...2]` | D/L |
| Array item range, open end | `list[2...]` | D/L |
| Array item negative offset | `list[-1]` | D/L |
| Every array items | `list[]` | L |
| Every array items property | `list[].value` | D/L |
| Every array items string property | `list[].'value-1'` | D/L |
| Every array items symbol property | `list[].Symbol(name)` | D/L |
| Array item property | `list[2].value` | D/L |
| Array item range property | `list[2...5].value` | D/L |
| Every array items, every properties  | `list[]{}` | L |
| Multiple properties | `{value1, value2}` | D/L |
| Multiple object properties | `model{value1, value2}` | D/L |
| Multiple array items | `list[3, 6, 8]` | D/L |


## Examples

### Change dispatched

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
| model.list[0][Symbol('sym')] = 'change' | `model.list[0].Symbol(test`) |

### Multiple changes dispatched

| Change | Descriptor |
| --- | --- |
| value1 = 'change1', value2 = 'change2' | `{value1, value2}` |
| value1 = 'change1', ['value-2'] = 'change2' | `{value1, 'value-2'}` |
| value1 = 'change1', [Symbol('sym')] = 'change2' | `{value1, Symbol(sym)}` |
| model.value1 = 'change1', model.value2 = 'change2' | `model{value1, value2}` |
| model.list[0] = 'change1', model.list[3] = 'change2'  | `model.list[0,3]` |
| value = 'change1', model.list[3] = 'change2'  | `{value, model.list[3]}` |

### Change listened

| Descriptor | Changes |
| --- | --- |
