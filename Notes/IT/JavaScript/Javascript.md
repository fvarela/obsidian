### let & const
	let. Variable
	const. Constant

Arrow Functions
	function myFnc(){}
	const myFnc = () =>{}


Exports & Imports (Modules)

![[Pasted image 20230417093856.png]]
	
![[Pasted image 20230417094134.png]]


Spread & Rest Operators
	Spread
		const newArray = [...oldArray, 1, 2]
		const newObject = {...oldObject, newProp:5}
	Rest:
		function sortArgs(...args){
		return args.sort()
		}


Destructuring
	Array destructuring:
		[a,b] = ['Hello', 'Max']
		console.log(a) // Hello
		console.log(b) // Max
	Object destructuring
		{name} = {name:'Max', age:28}
		console.log(name) // Max
		console.log(age) // undefined

Array Methods
```const numbers = [1,2,3]
	dons doubleNumArray = numbers.map((num) => {return num*2; });
	console.log(doubleNumArray); // [2,4,6]```