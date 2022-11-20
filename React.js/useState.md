const [state, setState] = useState()

You can't put useState in "if" check

Can provide function into useState(()=>{
	console.log('run only once")
})

if provide function runs every time rerender
useState(doSomething())

if object in the state how to update:

setState(prevState => {
	return { ...prevState, count: prevState + 1 }
})