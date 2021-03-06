# π μ΄μ§ νμ (binary search)

> _μ΄μ§ νμμμ 'μ΄μ§'μ 0κ³Ό 1μ μλ―Ένλ κ²μ΄ μλ, νλλ₯Ό λλ‘ λλλ κ²μ μλ―Ένλ€._

<p> μ΄μ§ νμ(binary search)μ μ ν νμ (linear search) κ³Ό ν¨κ» νμ μκ³ λ¦¬μ¦ (search algorithm)μ μνλ€.</p>

<p> μ ν νμμ λͺ¨λ  λ°°μ΄μμ μ¬μ©μ΄ κ°λ₯νμ§λ§, μ΄μ§ νμμ **Sorted array(μ λ ¬λ λ°°μ΄) μμλ§ μ¬μ©μ΄ κ°λ₯**νλ€.</p>

<p> μ΄μ§ νμμ μκ°λ³΅μ‘λλ **O(log N)** μ΄λ€.  
μ λ ¬λ λ°°μ΄μμμ νμμ μ λ ¬μ΄ μλ λ°°μ΄μμμ νμλ³΄λ€ ν¨μ¬ λΉ λ₯΄λ€.
νμ§λ§ μ λ ¬λ λ°°μ΄μμμ μμμ μΆκ°λ, μ λ ¬μ΄ μλ λ°°μ΄μμ μμλ₯Ό μΆκ°νλ κ²λ³΄λ€ μκ°μ΄ λ μμλλ€.</p>

|         μ ν νμ         |                 μ΄μ§ νμ                 |
| :-----------------------: | :---------------------------------------: |
|  λͺ¨λ  λ°°μ΄μμ μ¬μ© κ°λ₯  | μ λ ¬λ λ°°μ΄(sorted array)μμλ§ μ¬μ© κ°λ₯ |
| λ°μ΄ν°κ° λ§μ λ λΉν¨μ¨μ  |          λ°μ΄ν°κ° λ§μ λ ν¨μ¨μ           |
|           O(N)            |                 O(log N)                  |

<br/>
<!-- μ΄μ§ νμμμ μμμ μ«μ nμ μ λ ¬λ λ°°μ΄μ μΆκ°νλ μν©μ κ°μ ν΄λ³΄μ. -->

## π§ μ΄μ§ νμμ λ©μ»€λμ¦

μλ μ¬μ§μ μ°Έκ³ ν΄μ μ΄μ§ νμμ μκ³ λ¦¬μ¦μ μ΄ν΄ν΄λ³΄μ.

![image description](./binary.png)

μ΄μ§ νμμ μ λ ¬λ λ°°μ΄μ **μ μ€μ(midpoint) λΆν° νμμ μμ**νλ€. (_μΈλ±μ€ 0 λΆν°κ° μλλ€!_)
κ·Έλ¦¬κ³  νμμ λμμ΄ λλ targetκ³Ό μ μ€μμ μλ μ«μ(n) μμ ν¬κΈ°λ₯Ό λΉκ΅νλ€.

- **n > target** μ΄λΌλ©΄, λ°°μ΄μ μΌμͺ½μ νμνλ€. (μ€λ₯Έμͺ½μ νμμμ μ μΈμν¨λ€.)

- **n < target** μ΄λΌλ©΄, λ°°μ΄μ μ€λ₯Έμͺ½μ νμνλ€. (μΌμͺ½μ νμμμ μ μΈμν¨λ€.)

μ΄λ κ² λ°°μ΄μ λ°μΌλ‘ μͺΌκ°μ΄ λΉκ΅νλ κ³Όμ μ target μ μ°Ύμ λ κΉμ§ κ³μ λ°λ³΅νλ€.  
μ΄μ§ νμμ λ°°μ΄μ λ°μΌλ‘ μͺΌκ°λ μ€νμ κ±°μΉ  λλ§λ€ μ λ°μ μμλ₯Ό μμ κΈ° λλ¬Έμ νμμ μννλ μλκ° λΉ λ₯΄λ€.

> νμμ ν΄μΌ νλ λ°μ΄ν°μ μμ΄ 2λ°°κ° λμ΄λ, μμμ μννλλ° νμν μ€νμ 1λ²λ§ λ μΆκ°λλ€.

<p>κ·Έλμ μ΄μ§ νμμ μμ²­λ μμ λ°μ΄ν°κ° μλ λ°°μ΄μ λ€λ£°λ κ΅μ₯ν ν¨μ¨μ μ΄λ€. </p>
<br/>

## π©π»βπ» μ΄ μκ³ λ¦¬μ¦μ κ·Έλλ‘ μ½λλ‘ μ?κΈ°λ©΄?

μ€λ¦μ°¨μμΌλ‘ μ λ ¬λ λ°°μ΄ arrayμ, κ·Έ λ°°μ΄μμ νμν΄μΌ νλ μμ target μ΄ μλ€.
targetμ μΈλ±μ€λ₯Ό λ¦¬ν΄ν΄μΌ νλ€λ©΄ μλμ κ°μ΄ μμ±ν  μ μλ€.

```js
function binarySearch(array, target) {
	let left = 0;
	let right = array.length - 1;

	while (left <= right) {
		let mid = Math.floor((left + right) / 2);

		if (array[mid] === target) {
			return mid;
		} else if (array[mid] > target) {
			right = mid - 1;
		} else if (array[mid] < target) {
			left = mid + 1;
		}
	}
	return -1;
}
```
